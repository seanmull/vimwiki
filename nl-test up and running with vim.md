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
