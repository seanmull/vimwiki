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

(just the front end) PAS - permitted api set = array of api set ids

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

Optional Create group

https://nightlifemusic.atlassian.net/wiki/spaces/GHQ/pages/1303511147/create+group

Optional assign a user to a group

https://nightlifemusic.atlassian.net/wiki/spaces/GHQ/pages/1302626510/update

If we wanted to limit what numbers you can use?

Optional Set out a policy rule

Be able to call all the macygrey api

API set just a way to group api methods together
create functionality in enterprise X
need to permission to get access to the API
we are doing this before we have client
the alternative would be to create an API set id everytime you need to test something

Auth
Two level
method - trying to use an api
policy attached to the api-set id
if there are no policy rules it means can access all the parameters (whitelist)
as you add rules you blacklist what you can access
parameter - can use the api but what values can use in request and response

once you have a policy and that has to be applied to the group
h-drive you need to be able to login

doors-v1.admin.api_set.create
channel - identifier , hashed the channel and methods to create the api_set_id
Example:
channel: "@nightlife/x-app-system/GetSystemResolver"

    Example method string
    export namespace get {
        export const METHOD: string = "nl-macygrey.list.get";
        export const PATH_IReq: string = "list.get.IReq";

    put in the jwt
    you should get the api_set

    go to enterprise x to create a group policy
    enterprise.nighlifr/create-policy

    give this to users which is done in the group

    nl_doors_v1.api_sets this is the tables

    ui is broken setting the for group creation

    we belong in the devs group

    add the policy to the to group
    group policies
    group_id policy_id

    you need the api_set_id to send request

    refresh permissions are needed at times

    policies rules
    redis one is not currently implemented
    we don't really have policy rules for anything

    you do a curl command to get all the key value stores

    Useful method in Doors
    authorize_in_meta
        the * allows any method
    getCpoString
    validateAgainstCpo

    async authorize_in_meta({ nl_meta, ...params }: nl_doors_v1.nl_meta, meta: FunctionMetadata): Promise<[RequestParams<any>, FunctionMetadata]> {
