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

## Brain-storm

- Adding some api.
- See how its all laid out
- A month or so until you are comfortable with live
- Hard to define a goal
- Visualize where we want we go.
- How would we design it from scratch.
- Identify requires and outcomes we want to acheve

## Goals

- Set up the hdms.  Speak with brendon to set up the hdms.  I could IT.
- Set up the app. In a manner that is connected to production server layer.
- Switch this to talking to the development namespace.

Meeting with Sharan
9:30 - 11:30 M-Th for a month
Document as we go
Create quick point - polish up the documents later

intranet can tell me what is assigned to me
build27
the monitor hdmi is what the customers see

intranet
radio icon will tell you the online status
vnc icon indicated whether you can remote into the systems

## processes for NMS

- hardisks - delphi interfaces, uses txt files to persist data to 
- bill - billboards - manage the advertising, JPEGS, MPEG-4(Video)
- eggBP - audio video playback
- mp  - Applications responsible for media playback
- hsm - application connects to the live-server
      sharing messages with the live server
      - Creates HTTP websocket connections
      - Passes message to and from harddisk.exe(NMS) to the node-live (Live service)
      - Messages are JSON documents with 'actor-verb-object-target' structure
      - Uses SQLlite database along with txt files to persist information to disk
      - To access the application Left ctrl + Left shift + backspace
      - This would allow you to look at logs to see if the connectivity to live service
      - Alt + Tab
- sap - Local websocket server for apps to connect directly to the NMS crowdDJ Kiosk
     - A nodeJS runtime environment
     - Gos around the live server
- All nms software files are located on N:\video_cd     
      
Venue - mulitple systems , multiple people
Client code is a venue
Define what systems each person should access

Monday - we can look at the traffic for all the messages that are being sent back
