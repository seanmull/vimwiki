Task in confluence:
Need an OCD server that is dedicated to the front end. It is only an API server with all the OCD logic in it.
It doesn't do background top-up content, databases, or software. (API top-up would still happen)

This will require OCD to database or redis things.

List of APIs used by enterprise X:


Q & A with Brad

OCD is going to remain one code base with a configuration switch.

Main OCD - This will be responsible for pushing software and music to the systems.
Lite OCD - This will be responsible for exposing the following endpoints for enterprise (both 2 and X)
1. Server
- nl-ocd.server.configuration.set - just database call
- nl-ocd.server.configuration.get -  just database call
- nl-ocd.server.errors.get -  just database call
- nl-ocd.server.errors.remove - just database call
2. Content
- nl-ocd.content.getSystemListDetails
- nl-ocd.content.updateSystemLists
- nl-ocd.content.getSystemReport
- nl-ocd.content.cleanUpDrive
- nl-ocd.content.delete_files
- nl-ocd.content.download_files
- nl-ocd.content.replaceImages
- nl-ocd.content.job.kill
- nl-ocd.content.job.resume
- nl-ocd.content.job.pause
- nl-ocd.content.job.status
- nl-ocd.content.job.pauseAll
- nl-ocd.content.job.statusAll
- nl-ocd.content.job.resumeAll
- nl-ocd.content.job.systemsAll
- nl-ocd.content.job.missingSystems
- nl-ocd.content.job.cleanUpErrored
- nl-ocd.content.job.find
- nl-ocd.content.server_access
3 .Database
- nl-ocd.database.push
4 .Software
- nl-ocd.software.push (work your way up)
-   software
-   loadbalancing
-   jobManager
-   findsystems

Several tasks are:
1. For OCD light - Turn off timers for:
    1. Database server
    2. Software server - uses an event for system online events
    3. Tricklefeed server - this is for pushing content
2. Look into the missingEvent function that is triggers on a database rebuild

