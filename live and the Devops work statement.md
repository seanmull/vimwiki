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


