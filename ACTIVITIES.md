# ACTIVTIES
> 💡 **TAKE NOTE**: See [`SETUP.md`](https://github.com/ralphcasipe1/onboarding/blob/main/SETUP.md)

## ACtivity 1 RAMDAJS 
> You can use JavaScript first to familiarize yourself in RamdaJS
> 
> Then you can use TypeScript

- Add a unit test for each function, Please use:
    - `mocha`
    - `chai`
    
This is the shape of the car object

```typescript
type Car {
  name: string;
  horsepower: number;
  dollarValue: number;
  inStock: boolean;
}

const car = {
  name: 'Aston Martin One-77',
  horsepower: 750,
  dollarValue: 1850000,
  inStock: true,
}
```

### Rewrite this function using `.compose`

```typescript
type IsLastInStock = (cars: Car[]): boolean;

const isLastInStock: IsLastInStock = (cars) => {
  const lastCar = R.last(cars);

  return R.prop('inStock', lastCar);
};
```

### Create a function using `.compose`

Create a helper function that receive car objects and calculate the average.

```typescript
type averageDollarValue = (cars: Car[]) => number
```

### Use `.compose`

```typescript
const fastestCar = (cars) => {
  const sorted = R.sortBy(car => car.horsepower, cars);

  const fastest = R.last(sorted);

  return R.concat(fastest.name, ' is the fastest');
};
```

### Write a function that get each respective accounts' total payout

Given this object:

``` typescript
const data = [
  { acc_1: 1 },
  { acc_1: 2 },
  { acc_2: 3 },
];
```

> 💡 **TAKE NOTE**: The properties here are dynamic it means you could have a property like this, `acc_cefacd298d2e5d08b43001aeb169eea4`

The result would be like this:

```typescript
[{ acc_1: 3 }, { acc_2: 3 }]
```

_____

## Activity 2 Part 1 KOA CRUD VENDOR
- KoaJS
- Typescript
- Mongoose

Write a function that can **CRUD** a `vendor` in **RESTful API**.

The vendor object shape

```typescript
enum VendorType {
  Seamless = 'SEAMLESS'
  Transfer = 'TRANSFER'
};

type Vendor = {
  _id: string;
  name: string;
  type: VendorType;
  dateTimeCreated: Date;
  dateTimeUpdated: Date; 
}
```

### Tech stack
- [KoaJS](https://github.com/koajs/koa)
  - `npm i -S koa`
  - `npm i -D @types/koa`

- [TypeScript](https://www.typescriptlang.org/)
  - `npm i -D typescript`

- [Mongoose](https://github.com/Automattic/mongoose)
  - `npm i -S mongoose`
  - `npm i -D @types/mongoose`

## Adopting GraphQL
- `npm i -S apollo-server graphql`

These are the Query and Mutation for vendor:
```gql
type Query {
  vendor(id: ID): Vendor
  vendors: [Vendor]
}

type Mutation {
  createVendor(input: CreateVendorInput!): Boolean!
  updateVendor(id: ID!, input: UpdateVendorInput!): Boolean!
  deleteVendor(id: ID!): Boolean!
}
```

____________

## Activity 2 Part 2 Member
> **NOTE:** Use the _koa-crud, the activity #2_

- Can create, list, select, update and delete member.
- member have a `username`, `password`, and `realName`
    - `username` should be required and unique
    - `password` should not be visible in member's details and members' list
    - `realName` is optional.

## Activity 2 Part 3 Authentication
**Member should go through authentication to have access to `vendors` and `promos`**

For authentication you can use a RESTful api like for example the endpoint is:

```bash
POST authenticate
```

and the return value would be:

```json
{
  "token": "<token>"
}
```

You can use this in Apollo GraphQL Playground by adding a `Authorization` in http headers:
```json
{
  "Authorization": "Bearer <token>"
}
```
## Activity 2 Part 4 Promo

Add your implementation given these `Queries` and `Mutations`.
```gql
type Query {
  promo: Promo
  promos: [Promo]!
}

type Mutation {
  createPromo(input: CreatePromoInput!): Boolean!
  updatePromo(input: UpdatePromoInput!): Boolean!
  deletePromo(id: ID!): Boolean!
}
```

As an admin/operator you can create a promo

- A promo should these core fields `name`, `template`, `title`, `description`, `submitted`, `enabled`, and `status`.
    - `name` is required
    - `template` only accepts `DEPOSIT` and `SIGN_UP`
    - `title` is require
    - `description` is required
    - `status` only accepts `DRAFT`, `ACTIVE` and `INACTIVE`
        - the default value of `status` is `DRAFT`
- An admin could only delete promos that are `DRAFT` and `INACTIVE`.

- If the promo is a `DEPOSIT` then it should have a field of `minimumBalance`.

- If the promo is a `SIGN_UP` then it should have a field of `requireMemberFields`.
    - `requireMemberFields` is an array that accepts these values:
        - **REAL_NAME**
        - **EMAIL**
        - **BANK_ACCOUNT**

## Activity 2 Part 5 Promo Enrollment Request
Add logic to these following `Mutation`:

```gql
type Query {
  promoEnrollmentRequest: PromoEnrollmentRequest
  promoEnrollmentRequests: [PromoEnrollmentRequests]!
}

type Mutation {
  enrollToPromo(id: ID!): Boolean! # this for the member

  processPromoEnrollmentRequest(id: ID!): Boolean!
  approvePromoEnrollmentRequest(id: ID!): Boolean!
  rejectPromoEnrollmentRequest(id: ID!): Boolean!
}
```

A member could file a request to a specific promo.
- `promo` is required

- `status` only accepts `PENDING`, `REJECTED`, `PROCESSING`, and `APPROVED`
    - the default value of `status` is `PENDING`

## MISC

### Dockerfile
Add this to your root of `koa-crud/`.

```dockerfile
FROM node:12.18.2-alpine

WORKDIR /srv/node

COPY ./build /srv/node/build
COPY ./node_modules /srv/node/node_modules
COPY ./package.json /srv/node/package.json

CMD npm start
```

### Docker Compose
Add a `docker-compose.yml` file at the root of `koa-crud/`

```yml
version: '3.8'
services:
  mongo:
    image: mongo:4.4.3-bionic
    ports:
      - 27017:27017

```

### Testing mongoose via In-memory
Try to get the average of your current test speed and record it.

And try installing this as `devDependency`:
- [mongodb-memory-server](https://github.com/nodkz/mongodb-memory-server)
Apply it to your tests
And record it your new average test speed, if there is any improvements.

### Custom Errors
Add custom errors for each different validation.

Example:
When a member who do not have a `bankAccount` tries to enroll to a promo that have a `requireMemberFields` of **`BANK_ACCOUNT`** then it would propagate an error:

1. `code` - **`REQUIRE_MEMBER_FIELDS_NOT_MET`**
2. `message` - Member does not have the following fields: **`BANK_ACCOUNT`**

The error code should ONLY contain the context on what the error is. For example:
1. `MEMBER_NOT_FOUND`
2. `INVALID_VENDOR_TYPE`

The class name should have a suffix of `Error`. For example:
1. `MemberNotFoundError`
2. `InvalidVendorTypeError`

### Logger
These are the recommended loggers, you can either choose one(1) out of the three(3).
1. [winston](https://github.com/winstonjs/winston)
2. [signale](https://github.com/klaussinani/signale)
3. [pino](https://github.com/pinojs/pino)