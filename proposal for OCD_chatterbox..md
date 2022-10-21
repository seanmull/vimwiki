# Proposal for OCD chatterbox

## Context:
OCD is a management system for supporting the download of music lists for the HDMS.  Currently it handles the following tasks:

1. Accesses the content server.
2. Finds the systems that need a database update.
3. Creates and schedules jobs across OCD.
4. Exposes an API to update Enterprise X.
5. Manages events for all listeners.
6. Stores status of system if it is online or not.
7. Defines and stores tasks.
8. Tasks are managed via a trickle feed model where each task is run under a set interval.
9. Identify all systems that need updates.
10. Determines which song/lists are valid songs to download.
11. Determines which songs should be culled.
12. And much more..

OCD chatterbox is the first step in separating responsibility from OCD.  This would more closely adhere to a micro-service model, which is more maintainable and scalable. We will start with separating the functionality of job status.

## Requirements
* A new backend will be deployed on the production cluster.
* Any shared libraries will be moved to a more suitable location in mono.
* All shared state data will be stored in a Redis cache
* Metrics will be collected for the following parameters utilizing Prometheus:
```typescript
    // Both events already set up for RMQ, just send the same info to Prometheus
    sendStatusEvent(data: Array<nl_ocd.content.job.Status>) {
        if (this.service.rmqRpc !== undefined) {
            this.service.rmqRpc.emitEvent("job_status", data)
        }
    }
    this.service.rmqRpc.emitEvent("jobs_data", {
        job_count: jobsToSend.length,
        activte_jobs: activeCount,
        total_download_speed: downloadSpeed,
        active_ocd_jobs: ocdJobs,
        total_ocd_jobs: totalOCDJobs
    })
```

## What does the job status controller do?
Monitoring job status is accomplished through the jobStatusController.ts.

In summary, it does the following:  
* Looks for any jobs that are currently not being monitored by OCD.
    - Method:  updateDatabase()
* Updates the jobs that are monitored by OCD.
    - Method:  getAllJobsStatus()
    - Note: Both are accomplished by utilizing:
        - RPC requests to nl-hdms
        - Connecting to biggie-small and performing SQL queries.
- Find jobs that have errors and deletes them after a day or two.
    - Method: deleteEntry(entry: any)
- It runs these tasks in a timed loop but has the ability to add time when the traffic is higher than expected
    - Method: checkIfServerIsUnderLoad() to scale up

## Architectural Diagram

```mermaid
flowchart LR
    C --->|read Jobs Status| A(nl-OCD)
    B(nl-OCD_chatterbox) --->|writes Job status| C[(redis)]
    A ---> |imports|D(shared_libraries)
    B ---> |imports|D(shared_libraries)
```


## Extract Libraries List

Libraries that need to be shared
```typescript
// from jobStatusController
import { Task } from '../tasks/task'
// change this away into regular queries
// this ORM stuff is "change as you go"
export interface OcdModels {
    status_monitor : any
    completed_jobs : any
    scheduled_jobs : any
    server_conf : any
    errors : any
    recently_checked : any
    list_activation_schedule : any
    content_server_access: any
}
// Controllers
ErrorsController
OnlineSystemsController
// We are here
InternalSystemsController
// TaskScheduler each app will have its own scheduler
this.ocdService.taskScheduler.addTask(this.jobsStatusController.checkStatusTask)
this.ocdService.taskScheduler.addTask(this.jobsStatusController.sendStatusTask)
```
## Files that would compose OCD chatterbox

1. Jobstatus.ts - Main file that gathers all the system job status.
2. JobAPI.ts - Only used to expose an endpoint 
3. ActiveJobs.ts - Helper object that defines parameters of an active job.
4. CleanUpErroredUserJobsController.ts - update Errors table

## Stuff that would need to be "repurposed" within OCD

- OcdModels - will move query away from the ORM style. 
- The event handlers called that have to do with load balancing.
```typescript
    this.jobsStatusController.addListener("status", (data) => {
    this.ocdService.loadBalancing
        .updateStatus(data.system_id, data.paused, data.job_type)
    })
    this.jobsStatusController.addListener
                    ("update_job_status", (data) => {
    this.ocdService.loadBalancing.updateJobStatus(data)
    })
```

## What data needs to be stored in Redis?

### All shared state between the applications

- Task - no need to be shared.
- ErrorsController - this just queries the database. No shared state.
- OnlineSystemsController - seems like separate functions. No shared state
- InternalSystemsController - calls one function that needs systems array. This would be shared between both apps. Use redis to store the following:
    ```typecript
        private systems: Array<OnlineSystems> = []
        export interface OnlineSystems { 
            systemID: string
            lastCheck: Date
            status: string
     }
    ```
Note: This will need to be read and written from OCD.
- ActiveJobs - need to store the following:
    ```typescript
        private lastRecordedStatus: Array<nl_ocd.content.job.Status> = []
        export namespace job {

            export interface Status {
                system: string
                job_id: number
                status: string
                percent_completed?: string
                downloaded?: number
                total_files?: number
                download_speed?: string
                job_type?: string
                files_downloading?: Array<FileStatus>
            }
    ```
