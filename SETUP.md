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

## VSCode `tsconfig.json`
```json
{
  "compilerOptions": {
    "target": "es2017",
    "module": "commonjs",
    "allowJs": true,
    "moduleResolution": "node",
    "lib": ["esnext", "es2016.array.include", "esnext.asynciterable"],
    "allowSyntheticDefaultImports": true,
    "esModuleInterop": true,
    "outDir": "./build",
    "sourceMap": true,
    "strictNullChecks": true,
    "noUnusedLocals": true,
    "skipLibCheck": true
  },
  "include": ["src/"]
}
```

## VSCode `tslint.json`
```json
{
  "rules": {
    "max-line-length": {
      "options": [120]
    },
    "new-parens": true,
    "no-arg": true,
    "no-shadowed-variable": true,
    "no-bitwise": true,
    "no-conditional-assignment": true,
    "no-consecutive-blank-lines": true,
    "quotemark": [true, "single"],
    "no-irregular-whitespace": true,
    "indent": [true, "spaces", 2],
    "semicolon": [true, "always", "ignore-interfaces"],
    "whitespace": [
      true,
      "check-branch",
      "check-decl",
      "check-operator",
      "check-module",
      "check-separator",
      "check-rest-spread",
      "check-type",
      "check-typecast",
      "check-type-operator",
      "check-preblock"
    ]
  },
  "nodePath": "./node_modules"
}
```