Steps in the process

1. connect to aws
2. get to the development eks
3. connect to telepresence
4. add the following to for helm values:
```
command:
    - ts-node
    - src/main.ts
    - -P tsconfig.run.json
PWD: /app/backend/nl-nessie/src
```
5. Go to the development helm and copy all the env variables over to the json.
Example of a launch.json:
```
   {
      "name": "Prod NESSIE",
      "type": "node",
      "request": "launch",
      "args": ["${workspaceRoot}/src/main.ts"],
      "runtimeArgs": ["--no-lazy", "-r", "ts-node/register"],
      "cwd": "${workspaceRoot}",
      "protocol": "inspector",
      "env": {
        "PWD": "${workspaceRoot}/src",
        "NLCONF_LOG__LEVEL": "info",
        "NLCONF_LOG__PRETTY": "false",
```
Example of helm file:
```
replicas: 2
disableProbe: true
nme: nl-nessie
version: 1.0.46
image: 174155838907.dkr.ecr.ap-southeast-2.amazonaws.com/nl-nessie:1.0.46
command:
    - ts-node
    - src/main.ts
    - -P tsconfig.run.json
env:
  NLCONF_LOG__LEVEL: info
  NLCONF_LOG__PRETTY: "false"
  PWD: /app/backend/nl-nessie/src
  NLCONF_NESSIE__HOST: biggie-smalls.dev.nightlifr.com
  NLCONF_NESSIE__DATABASE: nl_nessie
  NLCONF_NESSIE__USER: nl_nessie
```
5. Look over the formatting differences. For all secrets enter the following in command line.
6. For secrets:
 ```
kubectl get secret <name> -o jsonpath="{.data.<key>}" | base64 --decode
 ```
7. Once all the config is good look out for the following scenerios
8.    Rmq request is undefined - usually means the queue isn't there.
9.    ECCESS issue on port 80 - just change http port to 3001
10.   Connection with sql - check if tables are there.
