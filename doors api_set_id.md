model it after aws

api_set - collection of methods

it only deals with methods not params

to give permission to interaction with the api

just permission to the apps that we wanted

methods in the base files

method based authorization => parameter level authorization

policies - api-set has one policy attached to

policy is intended to provide more detailed permission for specific => most of blank

if its blank you can access all parameters

you can apply conditions to the policies.

send api-set id => methods => value in parameters

nl-crowd => system.list => one set of parameter

the api-set id would have to update anytime we change access.

psedocode api set specify methods , array of strings and channel and the friendly name

channel was like an application 

each part of its application has its own channel

its not unique

identifier of the api-set is a hash of the channel and method

half driven how do we hide and show certain elements based on permission

element on the screen attached to one or more api-set id

(just the front end) PAS - permitted api set  = array of api set ids

if your elements are a subet of the pas then you can see the element



 

Create API set

https://nightlifemusic.atlassian.net/wiki/spaces/GHQ/pages/1303511090/create  

Create policy and Create API set to policy mapping

https://nightlifemusic.atlassian.net/wiki/spaces/GHQ/pages/1302593608/create+policy 

API or the UI

https://enterprise.nightlifr.com/create-policy 

Assign policy to group

https://enterprise.nightlifr.com/update-group-policy 

Currently broken will fix soon

Optional  Create group

https://nightlifemusic.atlassian.net/wiki/spaces/GHQ/pages/1303511147/create+group 

Optional assign a user to a group

https://nightlifemusic.atlassian.net/wiki/spaces/GHQ/pages/1302626510/update 

If we wanted to limit what numbers you can use?

Optional Set out a policy rule
