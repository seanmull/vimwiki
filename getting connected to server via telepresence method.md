Steps in the process

1. add the following to for helm values:
```
command:
    - ts-node
    - src/main.ts
    - -P tsconfig.run.json
PWD: /app/backend/nl-nessie/src
```
2. Get the environment variable that you need depending on what environment you are in.
3. Hosts usually have the name dev for biggie-smalls
4. May need to connect to database to see if tables are in dev.
5. Ask someone about networking info for connecting to biggie-smalls
6. If not you may need to copy them over from production

