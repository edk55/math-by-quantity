# Math with frequency

Math functions to use with frequency table.

## Installation

Install `math-with-frequency` using [npm](https://www.npmjs.com/package/math-with-frequency):

    npm install math-with-frequency

## Why

Some math libraries ([mathjs](https://www.npmjs.com/package/mathjs), [simple-statistics](https://www.npmjs.com/package/simple-statistics)) accepts the array of numbers to calculate the result.
There are tasks when to use this type of libraries, you will have to create large arrays of numbers.

### Example task:

Given: Array of Bitcoin sales with price and trade volume. \
Task: Find the mean sale price.

```js
const btcSales = [
  { price: 57000, volume: 1500 },
  { price: 56000, volume: 2200 },
  { price: 59000, volume: 1900 },
];
```

#### `some-other-math-library` example:

```js
// salePrices.length === 5600
const salePrices = btcSales.flatMap((sale) => new Array(sale.volume).fill(sale.price));
mean(btcSalePrices); // 57285.71428571428
```

#### `math-with-frequency` example:

```js
// saleNumbers.length === 3
const saleNumbers = btcSales.map((sale) => ({ value: sale.price, frequency: sale.volume }));
mean(saleNumbers); // 57285.71428571428
```

If you don't see any problem with creating big arrays of same numbers, then maybe you don't need to use this library

## Common Input format

```ts
type Frequency = number; // int value, bigger than 0. Default is 1.

type FrequencyObject<Value> = { value: Value; frequency?: Frequency };
type FrequencyTuple<Value> = [Value] | [Value, Frequency];

type Item<Value> = Value | FrequencyObject<Value> | FrequencyTuple<Value>;

const validInput: Item<number>[] = [
  100, // frequency is 1
  { value: 100 }, // frequency is 1
  { value: 100, frequency: 5 },
  [100], // frequency is 1
  [100, 5],
];
```
