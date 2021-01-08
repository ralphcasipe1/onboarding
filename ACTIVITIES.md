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

____________
## Activity 2 Part 2 Member
> Use the koa-crud, the activity #2

- Can create, list, select, update and delete member.
- member have a `username`, `password`, and `realName`
    - `username` should be required and unique
    - `password` should not be visible in member's details and members' list
    - `realName` is optional.

## Activity 2 Part 3 Authentication
**Member should go through authentication to have access to `vendors` and `promos`**

## Activity 2 Part 4 Promo
.....

As an admin/operator you can create a promo

A promo should have `name`, `template`, `title`, `description`, `submitted`, `enabled`, and `status`.
- `name` is required
- `template` only accepts `DEPOSIT` and `SIGN_UP`
- `title` is require
- `description` is required
- `status` only accepts `DRAFT`, `ACTIVE` and `INACTIVE`

## Activity 2 Part 5 Promo Enrollment Request
.....

A member could file a request to a specific promo.

- `promo` is required
- `status` only accepts `PENDING`, `REJECTED`, `PROCESSING`, and `APPROVED`