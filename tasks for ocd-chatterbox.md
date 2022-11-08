# Tasks for OCD chatterbox

-   [ ] Implement Redis cache in OCD-chatterbox.
-   [ ] Figure out why I am not getting back data for this. I suspect this is since I am not connected to nl-hdms. However this wouldn't address why when making request to production I get the same results
-   [ ] Talk with sarmed to get a bit of overview of Prometheus
-   [ ] Add in the Prometheus stuff.
-   [ ] If I have time remove the ocd models ORM stuff and replace it with simple query stuff

# Done
-   [x] Ask if we want all backends to enforce strict typing. This is something that has to be discussed in meeting between developers.
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
-   [X] Make all the RMQ connections between the two apps.
-   [X] Test out the RMQ connections
