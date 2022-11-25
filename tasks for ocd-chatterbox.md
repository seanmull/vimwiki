# Tasks for OCD chatterbox

-   [x] Make a better redis keys, like brad had.
-   [x] Move up cleanupErrors a level
-   [x] The API controller would need to be shared. Yes share this.
-   [x] Remove the update cache part of loadbalancer. Not needed.
-   [x] Move tricklefeed out of loadbalancer the way brad wanted them. This may not be needed
-   [X] Need to initialize internal systems and online systems.
-   [X] Change up the events and emitters the way brad mentioned. 3 down one to go. Still need to test this one. Talk to brad or someone.
-   [X] Also add the get and update wrappers around this. This may not be needed either.
-   [x] Find a way to take services out of the loadbalancer cache. Have it pass through chatterbox.
-   [x] Look into the activeJobs pubsub. I might have already done the events and emitters.
-   [x] Move erroredJobsController back to ocd.
-   [X] Find out how to interact with chatterbox and compare that to OCD. Checked in on the ocd side now need to check it on the chatterbox side.
-   [X] Remove all the jobStatus from OCD and see what breaks
-   [X] Merge master into my branch.
-   [X] Look over the diff and do some typical cleanup
-   [X] Update the readme.
-   [X] Resolve any errors I see in vscode
-   [X] Deploy on dev and try it out.
        %% - [ ] Talk with sarmed to get a bit of overview of Prometheus
        %% - [ ] Add in the Prometheus stuff.
        %% - [ ] If I have time remove the ocd models ORM stuff and replace it with simple query stuff

# Done

-   [x] Ask if we want all backends to enforce strict typing. This is something that has to be discussed in meeting between developers.
-   [x] Identify all config and service related resources needed to chatterbox
-   [x] Getting the loadbalencer to work for things on the chatterbox side.
-   [x] Add more state in the redis call for loadbalancer, need to get everything since its needs to update on the ocd side
-   [x] Resolve issues with circular references when stringifying big objects
-   [x] Move all the redis stuff to the loadbalancer
-   [x] Set up the cache for set up time till
-   [x] Figure out why I am not getting any data back from the rpc calls. Exparament and let some jobs start then call it.
-   [x] Look over errored clean jobs, loadbalancing and seeing of I am not calling out things twice
-   [x] Investigate if I moved the endpoints into chatterbox. If so move them back.
-   [x] Determine where we want to put the shared stuff. Put shared library in backend. Similar file
        and folder structure structure but striped down.
-   [x] Need understand how the workspaces thing to create dependency tree.
-   [x] Check if files are still removed.
-   [x] Move all the shared stuff and test if everything works in OCD.
-   [x] Do a little research with redis just to understand how it works.
-   [x] Look over nessie stuff to get an idea how to use redis for nightlife apps
-   [x] Implement Redis cache in OCD-shared.
-   [x] Build chatterbox using genesis.
-   [x] Add in files.
-   [x] Change names and links
-   [x] Set up queues for nl-ocd chatterbox
-   [x] Need to get It to get me connected to the RMQ host
-   [x] Get connected to RMQ
-   [x] Set up queues in namespace with v-host
-   [x] Add rpc handler for content job status. See ocd does it.
-   [x] Resolved dependency conflict with loadbalencer in shared library
-   [x] Added and tested event handler for database update
-   [x] Make all the RMQ connections between the two apps.
-   [x] Test out the RMQ connections
