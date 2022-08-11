[#](#) Tips from sarmed pair programming

## How to get logs
install bunyan
`npm i -g bunyan`

## How to get the final couple lines in a log it will update
`tail -f stdout.log | bunyan`

## How to get secrets 
`kubectl get secrets rmq-apps-user -o json`
`echo <password from secrets> | base64 --decode`

## To get logs in the container
```
[kubectl](kubectl) logs -f deploy/nl-test
```

## Viewing logs from a running container in K8s:
```
kubectl logs -f deploy/nl-test
```

## Launch.json stuff
in env
`NLCONF_LOG__PATH: //path to where logs will be`
`NLCONF_HTTP_SERVER__PORT: //new http server port`
envfile path to env file

## Typical environment variables
`NLCONF_BENCHMARK=`
`NLCONF_REDIS__HOST=redis.dev.nightlifr.com`
`NLCONF_RMQ__HOST=rmq.dev.nightlifr.com`
`NLCONF_RMQ__PASS=x7ADHopKkyo7V`
`NLCONF_RMQ__USER=apps`


## create a definition file
1. rabbit Mq cluster operator
2. operator then uses the rabbitMQ api to provide the definiton
3. add queue to rmq using the yaml file in middleware folder

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

## Test local connection to doors

