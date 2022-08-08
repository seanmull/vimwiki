# Tips from sarmed pair programming

## How to get logs
install bunyan
`npm i -g bunyan`

## How to get the final couple lines in a log it will update
`tail -f stdout.log | bunyan`

## How to get secrets 
`kubectl get secrets rmq-apps-user -o json`
`echo <password from secrets> | base64 --decode`

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
