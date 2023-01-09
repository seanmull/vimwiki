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
      
Venue - multiple systems , multiple people
Client code is a venue
Define what systems each person should access

Monday - we can look at the traffic for all the messages that are being sent back

Currently Systems are hooked up to production
Namespaces -
    each dev has mulitple namespace
    some contain multi applications some just have one
kube started with default
live wasn't on kube
all app on a namespaces, rmq, live
Prometheus on monitoring
create replicas for each developers
app-sm contains all apps for sm, same for live
rmq is only one name space but we have multiple vhosts
two containers with live pod (node and php)

ws document
ws connection to the live server
application have ability to connect to live server if they same network

cruise ships have only satelite internet. Media player works since they connect to the local 
network

Current home IP
- IP 192.168.1.208
- VPN 172.22.25.110 VCN connection
Note: going from home to office aws and back (alot of hops)

Old way of connect to VCN
use VNC view
VPN client is trying to connect to somewhere office
Disconnect to VPN, IT will need to help with connecting to vpn with vcn
production live service
ws://live.nightlife.com.au/hl/websocket

on vnc
shift and enter to just restart application rather then restart the whole system

Send this to the websocket
```json
{
  "published": {
    "time": "2022-12-28T01:14:29.915Z"
  },
  "actor": {
    "type": "client",
    "auth_user": "sean.mull",
    "auth_pass": "nightlife",
    "api_version": 3.96
  },
  "verb": {
    "event_category": "control",
    "event": "subscribe"
  },
  "object": {
    "systems": [
      {
        "system": "MULL0007B",
        "zone": 1
      }
    ]
  },
  "target": {
    "system": "MULL0007B",
    "zone": 1
  }
}
```

Cannot connect to my local ip for the HDMS with VPN up

Send James a message.  To re-configure my router
Router a sticker how to access it
Type that into a browser user_name and password
Printed on the router itself

How to get logs for individiual containers in a pod
```bash
k logs -n live-sm live-84767888bf-86ndf live-server-node
```

Basic goals
- migrate the code base to javascript
- modify the systems listing 
- php -> node
- release this request
- send this to production get the response
- development
- name the implementation as listing2
- load test the api

How to make an api call with the live server
```json
curl https://live.nightlife.com.au/api -XPOST -H 'Content-Type: application/json' -d '{
  "published": {
    "time": "2022-12-29T01:24:07.984Z"
  },
  "actor": {
    "type": "client",
    "auth_user": "sean.mull",
    "auth_pass": "nightlife",
    "api_version": 3.96
  },
  "verb": {
    "event_category": "request_systems",
    "event": "listing"
  },
  "object": {
    "systems": [
      {
        "system": "XING01",
        "zone": 1
      }
    ]
  },
  "target": {
    "system": "XING01",
    "zone": 1
  }
}'
    // sharans
    "auth_user": "sharan.nambiar",
    "auth_pass": "Nightlife01",
    // jukebox
    "auth_user": "nightlife.jukebox",
    "auth_pass": "jeF4PraH2e4Q",
```

production k8s
  - default namespace - most code in mono get deployed here
  - live namespace - one pod 3 containers
  -     pod name - live
  -     containers - live-server-node, live-server-php, live-server-cleanup
  -     all of the code is in the mono-live repo
development k8s
  - default namespace 
  - live namespace
  - multiple namespace - for each default and live namespace
  -     default namespace name is as follows "app-<initials of person>"
  -     live namespace "live-<initials of person>"

We test the production for the websocket connection 
Document the updates within the live squad.
ab test tool

finding a load testing for websockets
understand the build script
ensure that it is insync with the pipelines
understanding [telepresence io](telepresence.io)

aws makes the pod accessable through a network
kubernetes service sits in front of the pod to make it accessable
    cluster pod - 
    node - fixed port
    loadbalencer - over the internet
aws loadbalencer - services file creates a loadbalancer
look for errors in k9s
aws console will tell where the instance is created

test if live is accesable through the internet
EC2 -> Load balancers ->live-namespace-internal

subnet is only available in the private newtwork
route 53 has the DNS records

funtional test for the API
updating the build the script make the right name spaces
once the application is up change the DNS from the route 53 to make it accessable agains the nightlifr domain

you can create two chrome profiles if you need to look through two different aws accounts
look into live-bt compare to my namespace

anything that is blocking the connection to the live server namespace
apps are possibly
music systems need to connect to the namespaces
sharan wants this to be accessable
live system needs to be accessable to systems and the apps

live deployment on thursday
we had to rollback
some 3rd partie devices (kiosks, app) were not responding

music system - interface with the app.  We often give a tablet.
manage my nightlife - 
- MMNL Android - Customer Supplied device phone(tablet), App installed from the Android Playstore
- MMNL iOS - Customer supplied device (phone/tablet), App installed from the iOS App Store
- MMNL Android - Nightlife supplied tablet (sometimes called the turntablet), App installed from an MDM called Hexnode.  Use one platform to manage all the devices
    MDM - mobile device management
- MMNL WebApp - Web Broswer on customer/nightlife supplied computer
crowdDJ -
- crowdDJ Android - Customer Supplied device (phone/tablet), App installed from the Android Playstore
- crowdDJ iOS - Customer supplied device (phone/tablet), App installed from the iOS App Store
- crowdDJ Kiosk - Nightlife supplied tablet (sometimes called the turntablet), App installed from an MDM called Meld. Device uses ChromeOS and the app is a webApp
- crowdDJ Scan2Play - Web Broswer on customer/nightlife supplied device. Accessible by QR code

Only the mobile devices check location before making song requests

Variables for trouble shooting
1. Which app? MMNL or CDJ
2. Platform. Ois, Android, Web
3. Device. Customer or nightlife supplied?
4. Connect through live or directly
   - Nightlife supplied devices are set to connect directly. [CrowdDj kiosk, MMNL tablet]
5. Which account is used?
   - User account has been generated.
   - Guest account with daily password.
       - For MMNL, the format mmnl.<systemcode> password is accessable from intranet 
       - For CDJ, the format cdj.<systemcode> password is accessable from intranet 
       - Intranet access allows this
   - Nightlife type tablets turntablet and password is nightlife

If the system is set to local access only it can only connect directly to the specific device they have.
Who works in that venue
Create a person record
Create a system for client
Each person connected to each system.

URL to get access to MMNL. example
https://managemynightlife.com/?system=NMVG01B&zone=1&user=mmnl.NMVG01B&password=VPIB&method=web#/main/nowplaying/playlist

QR code is generate from browser tool putting in the url

critical db
hdmslive2 - remaining table that we are not replication 
hdmslive_rep - selection of tables replicating from AWS to local servers
hdmslive_tmp - temporary info.  Gets removed every time it gets restarted

24425
11905

Looking at the request made from the api. 

Test that need to be made
1 Request system listing2 for sean.mull
2 Request system listing2 for nightlife.jukebox
3 Request system mmnl.<systemcode> 
4 Request system cdj.<systemcode>
5 Request system intranet api call from the teams chat

intranet/apps/contact_search/client_response.php

911

916
Makeing a call hdmlslive_api(array reqeests)

intranet/shared/includes/hdmlslive_api.php
send the request via curl
