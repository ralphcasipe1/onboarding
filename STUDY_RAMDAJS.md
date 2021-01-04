# Simple Combination

### `.complement`

```ts
const isEven = num => num % 2 === 0;

R.find(isEven)([1, 2, 3, 4]); // 2

R.find(R.complement(isEven))([1, 2, 3, 4]); // 1
```

**TLDR;**

It is equal to `!` operator

### `.both` and `.either`

```typescript
type Person = {
  birthCountry: string;
  naturalizationDate: Date;
  age: number;
};

const country = 'Philippines';

const person: Person = {
  birthCountry: country,
  naturalizationDate: new Date(),
  age: 18,
};

const bornInPhilppines = (person: Person) => person.birthCountry === country;

const naturalized = person => Boolean(person.naturalizationDate);

const over18 = person => person.age >= 18;

const isCitizen = person =>
  bornInPhilppines(person) || naturalized(person);

// const isCitizen = either(bornInPhilippines, naturalized)

const isEligibleToVote = person => over18(person) && isCitizen(person);

// isEligibleToVote = both(over18, isCitizen)
```

### `.pipe`

Given this functions
```typescript
const multiply = (a, b) => a * b;
const increment = (a) => a + 1;
const square = (a) => a * a;
```

Imperative way
```typescript
const operate = (a, b) => {
  const product = multiply(a, b);
  const incremented = increment(product);
  const squared = square(incremented);

  return squared;
}
```

Using `.pipe`
```typescript
const operate = R.pipe(multiply, increment, square);

operate(2, 2) // 25
```

### `.compose`
Given this functions
```typescript
const multiply = (a, b) => a * b;
const increment = (a) => a + 1;
const square = (a) => a * a;
```

Imperative way
```typescript
const operate = (a, b) => {
  const product = multiply(a, b);
  const incremented = increment(product);
  const squared = square(incremented);

  return squared;
}
```

Since you can write your function this way:

```typescript
const operate = square(increment(multiply(2, 2)));
```

Using `.compose`
```typescript
const operate = R.compose(square, increment, multiply);

operate(2, 2) // 25
```

## Partial Application

```ts
enum VendorType {
  Seamless = 'SEAMLESS',
  Transfer = 'TRANSFER'
}

type Vendor = {
  name: string;
  type: VendorType
};

const vendorByType = (vendor: Vendor, type: VendorType) => vendor.type === type;

const vendorsForType = (vendors: Vendor[], type: VendorType) => {
  const foundVendors = R.filter(
    vendor => vendorByType(vendor, type)
  )(vendors);

  return R.map(vendor => vendor.name)(foundVendors);
}
```

### Higher-order Function
```typescript
const vendorByType(type: VendorType) {
  return function(vendor: Vendor) {
    return vendor.type === type;
  }
}
// you can refactor to this:
const vendorByType = (type: VendorType) => (vendor: Vendor) => vendor.type === type;

const vendorsForType = (vendors: Vendor: [], type: VendorType) => {
  const foundVendors = R.filter(vendorByType(type))(vendors);

  return R.map(vendor => vendor.name)(foundVendors)
};
```

### Partial Application in Functions
```typescript
vendorByType(vendor, 'SEAMLESS');

vendorByType('SEAMLESS')(vendor);
```

We can use `.partial` or `.partialRight`

Reset our function first:

```typescript
const vendorByType = (vendor, type) => vendor.type === type;

const vendorsForType = (vendors: Vendor: [], type: VendorType) => {
  const foundVendors = R.filter(R.partialRight(vendorByType, [type]))(vendors);

  return R.map(vendor => vendor.name)(foundVendors);
};
```

Swap argument

```typescript
const vendorByType = (type, vendor) => vendor.type === type;

const vendorsForType = (vendors: Vendor: [], type: VendorType) => {
  const foundVendors = R.filter(R.partial(vendorByType, [type]))(vendors);

  return R.map(vendor => vendor.name)(foundVendors);
};
```

### Currying
```typescript
const vendorByType = R.curry((type, vendor) => vendor.type === type)

const vendorsForType = (vendors: Vendor: [], type: VendorType) => {
  const foundVendors = R.filter(vendorByType(type))(vendors);

  return R.map(vendor => vendor.name)(foundVendors);
};
```

What if we have this kind of order.

Then use `.flip`

```typescript
const vendorByType = R.curry((vendor, type) => vendor.type === type)
```

```typescript
const vendorsForType = (vendors: Vendor: [], type: VendorType) => {
  const foundVendors = R.filter(R.flip(vendorByType)(type))(vendors);

  return R.map(vendor => vendor.name)(foundVendors);
};
```

## Placeholder using `.__`

```typescript
const args = R.curry((x, y, z) => ...)

const callSecondArgumentForLater = args('foo', R.__, 'bar');

const secondArgumentOnly = args(R.__, 'foo', R.__);
```

We can use `.__` instead of `.flip`

```typescript
const vendorsForType = (vendors: Vendor: [], type: VendorType) => {
  const foundVendors = R.filter(vendorByType(R.__, type))(vendors);

  return R.map(vendor => vendor.name)(foundVendors);
};
```