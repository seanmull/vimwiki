# Tips from sarmed pair programming

## How to get logs
install bunyan
`npm i -g bunyan`

## How to get the final couple lines in a log it will update
`tail -f stdout.log | bunyan`

## How to get secrets 
```
kubectl get secrets rmq-apps-user -o json
echo <password from secrets> | base64 --decode
```

## Viewing logs from a running container in K8s:
```
kubectl logs -f deploy/nl-test
```

## Launch.json stuff
```
in env
`NLCONF_LOG__PATH: //path to where logs will be`
`NLCONF_HTTP_SERVER__PORT: //new http server port`
envfile path to env file
```

## Typical environment variables
```
NLCONF_BENCHMARK=
NLCONF_REDIS__HOST=redis.dev.nightlifr.com
NLCONF_RMQ__HOST=rmq.dev.nightlifr.com
NLCONF_RMQ__PASS=x7ADHopKkyo7V
NLCONF_RMQ__USER=apps
```


## create a definition file
1. rabbit Mq cluster operator
2. operator then uses the rabbitMQ api to provide the definiton
3. add queue to rmq using the yaml file in middleware folder
4. do the same with the bindings look for the nl-exchange folder

The main exchange were all the pods goes to nl-exchange
queues destinations from the exchange
binding routes from the exchange to destination (the backend)
destinations is usually a queue

Two queues one for request and response
And another for events but this might be optional if the config doesn't have it

```
let addTwoNumbers: ReqResFunction<any, any> = (a, b)  => {
      return Promise.resolve().then(() => {return a.num1 + a.num2})
    }
    this.rpc.addRpcHandler(nl_test_gen.schema.addTwoNumbers.METHOD,
                           addTwoNumbers, null, true)
                           
```
a is the object getting returns from the queue

## Set up EACCES
Careful with listening on port 80

## Test out connection with door with postman
1. Go to authenticate.login
2. Do the post request to get the jwt
3. Go to nightlife api - preinstall script and paste the jwt.  This will enable authentication

## Here are two ways to access to environment variables

### Deploy doors with environment variables
```
kubectl exec -it deploy/nl-doors-v1 -- env  > backend/nl-doors-v1/deploy/development/.env
```

### Connect to telepresence
```
telepresence connect
```
Intercept here to get access to environment variables and intercept traffic

## Doors

Setting up the postman post request
```
{
 "params": {
    "num1": 1,
    "num2": 2,
    "nl_meta": {
        "auth": {
>>            "jwt": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjoic2FybWFkLnRhcmFyIiwiaWF0IjoxNjYwMDA4NzQ4LCJleHAiOjE2NjAwOTUxNDh9.amhxym7EGlf4Pxmn0UeM5IksXAmIl-OsFvDwFrfHIXE",
>>            "api_set_id": "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa"
        }
    }
 },
 "id": "368c2df0-0492-11ec-8e7d-8b11a818ed55",
 "method": "nl-test.schema.addTwoNumbers",
 "jsonrpc": "2.0"
}
```
nl_meta get through door
jwt we got through the login api which can be found in postman after making the request
api_set_id we are using admin but this will change

Header set to application json
Look out for syntax error is you json parsing error

## Pipeline setup
1. Go to aws site: https://nightlifesso.awsapps.com/start#/
2. Click nightlife-development, management console
3. Look for elastic container registry
4. Add repository
5. Give it a name
6. Run build and deploy

## Whats in the boilerplate code

```
├── deploy
│   ├── development
│   │   └── helm_values.yaml
│   └── production
│       └── helm_values.yaml
├── package.json
├── package-lock.json
├── README.md
├── src
│   ├── config.ts
│   ├── controllers
│   │   └── sample.ts
│   ├── main.ts
│   ├── nlbackend.ts
│   └── rpc
│       └── interfaces.ts
├── tsconfig.base.json
├── tsconfig.json
├── tsconfig.publish.json
└── tsconfig.run.json
RPC folder
├── gen_keys.json
├── gen.ts
├── interfaces.ts
├── schema.schema.addTwoNumbers.IReq.json
├── schema.schema.addTwoNumbers.IRes.json
├── schema.schema.IReq.json
└── schema.schema.IRes.json
```

Some stuff to consider for the development environment
1. If there are any backends that may having conflicting ports when routing http.
2. Make sure that the queues and bindings are set up for the namespace you are trying to add.
3. Make sure the pod is not running when you are deving.  You need a local instance of the pod running when running the script but you need to make sure its not running afterwords.

The tasks in vs-code. You need to make sure each script has a ";" at the end. 

Two documents will help you understand the process:
This one is useful for setting up a debug env
https://nightlifemusic.atlassian.net/wiki/spaces/GHQ/pages/2092040245/Debugging
This one is useful for understanding the folders in mono and namespaces:
https://nightlifemusic.atlassian.net/wiki/spaces/GHQ/pages/2092990477/Folder+Structures+in+Mono
