# Code Convention

## GIT Message

Format of the git message

```
<type>(<scope>): <header-title>

<message-body>

<footer>
```

- `type`
    - `feat`: initial commit, new feature, major to minor ,changes, adding new dependencies
    - `refactor`: changes that does not affect the test
    - `perf`: changes that focus more in performance but does not affect the test 
    - `docs`: changes about documentation
    - `test`: changes happen under the `test/` folder.
    - `build`: when the `package-lock` is updated
    - `chore`: when updating old dependencies
- `scope`: in what area of the code is changed sample:
    - `library`
    - `middleware`
    - `ci`
    - `docker-compose`
    - `command-handlers`
- `header-title`: concise of what you did. It should be in a imperative. It means, you are command. E.g.
    - update library
    - change variable name
- `message-body`: the descriptive format on what you did.
    - Update library to support maxmind.
    - Change design pattern from bridge to strategy to accomodate different payout APIs.

- `footer`: This is mostly used as reference. For example:
    - `[Jira Card](link)`
    - `[Design Docs](link)`
    - `[GraphQL Change Request](link)`

### Examples
With type and header title only.

```git
feat: change new logger format
```

With type, scope and header title.
```
feat(ci): run asynchronous test in circleci
```


With the header, body and footer.
```git
feat(library): add new utility

Add utility function to generate new serial code depending on the supplemented type.

- [Jira](link)
```

## Typescript

Type name should be PascalCased.
```ts
type Vendor = {...};

type VendorType = ...;
```

Type's properties should be camelCased.
```ts
type Vendor = {
  name: string;
  dateTimeCreated: Date;
}
```

Enum name should be PascalCased.
```ts
enum Colors {...};
```

Enum keys should be PascalCased while the values should be CONSTANT_SNAKE_CASE.
```ts
enum Colors {
  YellowGreen = 'YELLOW_GREEN',
  BlueGreen = 'BLUE_GREEN'
};
```

Variable name should be camelCased.
```ts
const naturalized = Boolean(null);

const naturalizedDate = Boolean(new Date());
```

Functions should be camelCased.
```ts
function camelCased() {...}

const camelCased() {...}
```

Class name should be PascalCased.
```ts
class AppError extends Error {}
```

Class#method should camelCased.
```ts
class Aggregate {
  public apply() {}
}
```