## Terminology

Timebomb - this is something to keep track of when someone has not used the system.  This is usuallya case when a customer hasn't payed.  This is usually a grace period of about 3 month.  Afterward the system get shut off

## Requirements

The Greylist is list of rules for systems when they install software and music. It affects whether software and databases can install and how long a software license s valid for. The data for the greylist is currently stored in a text file at the following location:

http://intranet.nightlife.com.au/greyList

The data needs to move to a database and we need a set of CRUD APIs to manage that data, we also need to http link to the data in the same format as above.

Below is an attempt at describing the format of the gray list data:

[TIMEBOMB COUNTER],[SOFTWARE MUSIC INSTALLS],[SYSTEM CODE],[SERIAL NUMBER],[TOTAL TIMEBOMB]

e.g. 99SM,PRID00057,NMS1234,998

TIMEBOMB COUNTER - Set the number of days until the software license expires. A value of 0 de-registers the system, a value of 99 does not change the current counter value

SOFTWARE MUSIC INSTALLS - An S in the first position will allow software installs to occur on a system any other character will block software installs. An M in the second position will allow music installs to occur on a system. any other character will stop music from installing. Need to review for remote database installs.

SYSTEM CODE - The system code of a media player for which the rule apply

SERIAL NUMBER - The serial number of a media player for which the rule apply

TOTAL TIMEBOMB - [Optional] The default time period for the software license is 90 days. The number in this field will set a different time period, generally used to extend the the license period beyond 90 days.

## Endpoints
API’s:

  get - return all the details for a particular system / sytems. Params Array<string> system_codes
  set_timebomb - Set the timeout for the time bomb. Params Array<string> system_codes
  set_allow_software - Sets if the system is allowed to receive software updates or not.

## Methods


## Basic Architecture

    intranet logs
       ^
    nl-macyGray -----> db
       V
      API
      
      
Live server has logs that are in a given format
```
```
  
The backend will store the data into a sql table
A API will be exposed on the cluster allowing users access endpoints
