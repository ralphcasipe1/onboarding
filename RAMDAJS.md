> You can use JavaScript first to familiarize yourself in RamdaJS
> 
> Then you can use TypeScript

# Use ramda

Shape of the car object
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

## Rewrite this function using compose

```typescript
type IsLastInStock = (cars: Car[]): boolean;

const isLastInStock: IsLastInStock = (cars) => {
  const lastCar = R.last(cars);
  return R.prop('inStock', lastCar);
};
```

## Create an function

Create a helper function that receive car objects and calculate it's average.

```typescript
type averageDollarValue = (cars: Car[]) => number
```

## Use compose
```typescript
const fastestCar = (cars) => {
  const sorted = R.sortBy(car => car.horsepower, cars);
  const fastest = R.last(sorted);
  return R.concat(fastest.name, ' is the fastest');
};
```