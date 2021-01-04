## VSCode `settings.json`
```json
{
  "window.zoomLevel": -1,
  "typescript.updateImportsOnFileMove.enabled": "always",
  "files.eol": "\n",
  "eslint.alwaysShowStatus": true,
  "eslint.validate": [
    "javascript",
    "javascriptreact",
    {
      "language": "typescript",
      "autoFix": true
    },
    {
      "language": "typescriptreact",
      "autoFix": true
    }
  ],
  "eslint.autoFixOnSave": false,
  "editor.formatOnSave": true,
  "editor.tabSize": 2,
  "prettier.endOfLine": "lf",
  "prettier.eslintIntegration": true,
  "prettier.singleQuote": true,
  "prettier.trailingComma": "all",
  "files.insertFinalNewline": true,
  "[typescript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[jsonc]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  }
}
```

## VSCode `launch.json`
```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Current TS Tests File",
      "type": "node",
      "request": "launch",
      "program": "${workspaceRoot}/node_modules/mocha/bin/_mocha",
      "args": [
        "--async-stack-traces",
        "-r",
        "ts-node/register/transpile-only",
        "${relativeFile}"
      ],
      "cwd": "${workspaceRoot}",
      "protocol": "inspector",
      "env": {
        "TS_NODE_PROJECT": "tsconfig.json",
        "TS_NODE_FILES": "true",
        "DEBUG": "error*,warn*,info*"
      }
    }
  ]
}
```