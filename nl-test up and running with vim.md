Step

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

