## VSCode
`settings.json`

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

`launch.json`

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

_______

## TSConfig

`tsconfig.json`

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

_______

## VSCode ESLint

`eslint.json`
```json
{
  "parser": "@typescript-eslint/parser",
  "plugins": ["@typescript-eslint", "import"],
  "extends": [
    "airbnb-base",
    "plugin:@typescript-eslint/recommended",
    "plugin:import/typescript",
    "plugin:prettier/recommended",
    "prettier/@typescript-eslint"
  ],
  "env": {
    "node": true,
    "mocha": true
  },
  "rules": {
    "no-useless-constructor": "off",
    "@typescript-eslint/explicit-function-return-type": "off",
    "@typescript-eslint/no-explicit-any": "off",
    "@typescript-eslint/indent": "off",
    "@typescript-eslint/no-non-null-assertion": "off",
    "import/extensions": ["error", "never", { "packages": "always" }],
    "no-underscore-dangle": "off",
    "func-names": "off",
    "max-classes-per-file": "off",
    "max-len": ["error", 140],
    "linebreak-style": ["error"],
    "import/prefer-default-export": "off",
    "prettier/prettier": "error"
  },
  "settings": {
    "import/resolver": {
      "typescript": {}
    }
  }
}
```

`package.json`
```
{
  "lint": "eslint . --ext .ts",
  "lint:fix": "eslint . --ext .ts --fix",
}
```