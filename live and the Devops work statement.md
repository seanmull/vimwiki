# Current tasks

1. Read over what sarmed has done so far.
2. Read over what brad has done so far.
3. Try to schedule some time with Sarmed to discuss that node server and some stuff I need to be aware.  Not really sure what the structure of the meeting is

## Key points for understanding migration plan

### History
1. Data was the location for the old cloud based applications. While production will the be the new location. 
2. We have AWS managed environments that utilized docker images and are orchestrated by kubernetes.
3. Data only holds the databases such as biggie smalls and redshift
4. Live now has the following:
    1. They are all containerized
    2. They are all deployed on a kubernetes pod
    3. Volumes are connected to make live changes
    4. For changes to take affect you would need to restart the pod
    5. This is just for development.
5. RMQ is now highly available in the cluster, thanks to kubernetes operators.  This will allow us to deprecate nl-rmq.
6. Prometheus is part of kubernetes operators as well.

### Steps of the plan
1. Building the production environment.
2. Redirecting all media players to nightlife production
3. Redirecting all enterprise productions to nightlife production
4. Clean up nightlife data


# Done

1. Look over roles and [responsibilities for Devops.](responsibilities for Devops.)

# Live and DevOps workstatement

2 applications

-   node-live
-   php-live

## History

1st version was written in php
LAMP stack
(apache -> nginx) webserver - recieves requests
webserver recieves any http 80 https 443 request for a file or to execute a php script
live.nightlife.com.au:[80,443]/api/ - execute a php script
live.nightlife.com.au:[80,443]/\*/ - return a file that resides which in the /var/www/..
apache set to execute php code with a thread websocket support was not available
node-live was developed since we needed websockets
all systems connect to node-live using websockets
all apps ie manage my nightlife and crowd dj all use ws
node call the php

## Components

1. NMS - nightlife music system
2. HSM - hdms state machine - brad works on this qt c++
3. Harddisk - hard disk is the core media application, customer facing application build by
   tim ds delphi application with c++ dll handles the playback of the audio
4. Open VPN client

## How to connect to an HDMS

1 .Get into remmina

```bash
remmina
```

2. Pick connection option - vnc
3. Enter the host of the machine: ex: 192.168.4.87 (the machine behind you)
4. Enter pw: hdms


## How to connect to the websocket tester

Set server 1 to ws://live.nightlife.com.au/hl/websocket

Actor json

```json
{
    "type": "client",
    "auth_user": "sean.mull",
    "auth_pass": "nightlife",
    "api_version": 3.96
}
```

Object json

```json
{ "systems": [{ "system": "NMVG02B", "zone": 1 }] }
```

Target json

```json
{ "system": "NMVG02B", "zone": 1 }
```


