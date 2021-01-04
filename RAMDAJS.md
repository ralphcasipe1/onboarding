# RamdaJS Exercises

> 💡 **TAKE NOTE**: See [`SETUP.md`](https://github.com/ralphcasipe1/onboarding/blob/main/SETUP.md)

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


