Step

Current issues:
Nvim-dap doesn't allow ${file} substitutions in the strings for env variables.
Perhaps just hard code the paths for now

1. Make sure the debugger is build (vscode node 2 adapted)
2. with nvim dap launchjs: 
```
dap.adapters.node = {
  type = 'executable',
  command = '/usr/bin/node',
  args = { os.getenv('HOME') .. '/dev/microsoft/vscode-node-debug2/out/src/nodeDebug.js' },
}
require('dap.ext.vscode').load_launchjs(nil, { node = { "javascript", "typescript", "node2" } })

```
Note: The first value is from launch.json in vscode the second is the adapter config
Also make sure the adapter is set up for each file type that bound to each config

Also with typescript you need to put the following shebang above the file:
```
#! /usr/bin/env node
```

The only real issue I have is when you have env parameters in launch.jsons.  dap will not be
able to replace this with the right values:

```
"env": {
  "PWD": "${workspaceRoot}/src",
  "NLCONF_LOG__PATH": "${workspaceRoot}/stdout.log",
  "NLCONF_HTTP_SERVER__PORT": "3001",
  "NLCONF_RMQ__HOST": "rmq.dev.nightlifr.com"
},
```

Example of working config
```
  {
    "type": "node",
    "request": "launch",
    "name": "Launch Program",
    "skipFiles": ["<node_internals>/**"],
    "args": ["${workspaceFolder}/src/main.ts"],
    "runtimeArgs": ["--no-lazy", "-r", "ts-node/register"],
    "cwd": "${workspaceFolder}", <-- change this to workspacefolder
    "protocol": "inspector",
    "envFile": "${workspaceFolder}/.env",
    "env": {
      "PWD": "/home/seanm@NIGHTLIFE.COM.AU/projects/mono/backend/nl-test/src", <-- give abs path
      "NLCONF_LOG__PATH": "${workspaceRoot}/stdout.log", <-- same here
      "NLCONF_HTTP_SERVER__PORT": "3001",
      "NLCONF_RMQ__HOST": "rmq.dev.nightlifr.com"
    },
    "internalConsoleOptions": "openOnSessionStart"
  }
]

```

