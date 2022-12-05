# Tasks

-   [x] Look into task start and see what other jobs don't need to be running in OCD
-   [x] Figure out all the tasks names.
-   [x] Look into dry run and see if I just want to do that for lite.
-   [x] Build a more complete list of API calls in insomnia.
-   [ ] Figure out whats going with rmq error
-   [ ] Try to start spin up two different application with same code base
-   [ ] Try to get everything running in dev.

-   [ ] Run some queries to see if you see any speed difference. Don't think we need this.

Task names

OCD only
Backblaze
this.loginTask = new Task(5, () => { this.login() }, 'B2 Login Task')
this.versionTask = new Task(5, () => { this.downloadReleases() }, 'B2 Version Task')

        Tricklefeed
        this.task = new Task(120, () => { this.startNewDownloads() }, 'New Downloads Task')
        if(!this.ocdConfig.is_ocd_lite){
            this.ocdService.taskScheduler.addTask(this.task)
            this.ocdService.taskScheduler.addTask(this.cleanUpDatabaseController.task)

        cleanUpDatabaseController
        this.task = new Task(this.initialCheck, () => { this.cleanUpCompletedJobsTable() }, 'Cleanup OCD Database Task')

        updateSystemDatabase
        this.task = new Task(this.quickCheckTime, () => { this.updateDatabaseVersions() }, 'Update Database Task')
        this.pushWorkedTask = new Task(60, () => { this.hasDatabaseInstalled() }, 'Pushed Database Task')

        updateSoftware
        this.task = new Task(this.quickCheckTime, () => { this.updateSoftwareVersions() }, 'Update Software Task')

        software server
        this.task = new Task(this.greyListCheckTime, () => { this.getGreyList() }, 'New Downloads Task')

        Internal server access
        this.task = new Task(5, () => { this.cleanupInternalSystems() }, 'New Downloads Task')

Both
Listcache
this.task = new Task(this.cleanupTime, () => { this.clear() }, 'List cache cleanup')
this.memoryTask = new Task(this.quickCheckTime, () => { this.checkMemory() }, 'List cache memory')

        Findsystem
        this.task = new Task(this.taskTime, () => { this.clearCache() }, 'Clear Cache')

        DNSlookup
        this.task = new Task(this.timeTillNextCheck, () => { this.resolveDNS() }, 'Update DNS Task')

        Errorjobs
        this.task = new Task(this.initialCheck, () => { this.reportErrors() }, 'Job Errors Task')

            this.ocdService.taskScheduler.addTask(this.erroredJobsController.task)
        }

        Jobsscheduled
        this.task = new Task(this.timeTillNextCheck, () => { this.checkJobs() }, 'Jobs Scheduled Task')

        job manager
        this.task = new Task(-1, () => { this.startJob() }, 'Job Manager Task')

        ContentserverErrorReport
        this.task = new Task(15, () => { this.sendReport() }, 'CSA Report')

        Check content server access
        this.task = new Task(this.quickCheckTime * 1.5, () => { this.checkContentServerAccess() }, 'Content Access Task')

        Online systems
        this.task = new Task(this.timeTillNextCheck, () => { this.populate() }, 'Online Systems Task')



        Chatterbox
        this.checkStatusTask = new Task(this.timeTillNextCheck, () => { this.getAllJobsStatus() }, 'Job Status Task')
        this.sendStatusTask = new Task(60, () => {
            if (this.activeJobs.hasStoredStatus()) {
                let onlineSystems: Array<string> =  ErrorsController.instance.cleanupSyncingSystems(this.currentIteration)
                this.sendStatistics(this.activeJobs.getLastRecorded(), onlineSystems)
                console.log("Job Status Sent")
            }
        }, 'Job Send Status Task')
