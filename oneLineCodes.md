# One Line Codes

## Custom Delay
```js
export const delay = async (time) => new Promise(resolve => setTimeout(resolve, time ?? 1000));
```

## sortBy
```js
export const sortBy = (array=[],key=null,order='ase') => array?.sort((a,b)=>!!!key?order==='ase'?a-b:b-a:order==='ase'?a[key]-b[key]:b[key]-a[key]);

// OR

export const sortBy = (array = [], key = null, order = 'asc') => {
    return array.sort((a, b) => {
        const compareValue = key ? a[key] - b[key] : a - b;
        return order === 'asc' ? compareValue : -compareValue;
    });
};

// OR

const sortBy = (arr, key) => arr.sort((a, b) => a[key] > b[key] ? 1 : a[key] < b[key] ? -1 : 0);
```


## getRandomItem
```js
const getRandomItem = (items) =>  items[Math.floor(Math.random() * items.length)];
```

## dummyArray
```js
const dummyArray = (length,dummyItem) => Array(length).fill(dummyItem)
```

## countOccurrences
```js
const countOccurrences = (arr, value) => arr.reduce((a, v) => (v === value ? a + 1 : a), 0);
```

## pluck
```js
const pluck = (objs, key) => objs.map((obj) => obj[key]);
```

## insert
```js
const insert = (arr, index, newItem) => [...arr.slice(0, index), newItem, ...arr.slice(index)];
```

## removeDuplicates
```js
const removeDuplicates = (arr) => [...new Set(arr)];
```

## calculatePercent
```js
const calculatePercent = (value, total) => Math.round((value / total) * 100)
```

## shuffledArray
```js
const shuffledArray = array.sort(() => Math.random() - 0.5)
```

## reversedString
```js
const reversedString = string.split("").reverse().join("");
```

## numbersArray
```js
const numbersArray = (length) => [...Array(length).keys()]
```

## uppercaseWords
```js
const uppercaseWords = (str) => str.replace(/^(.)|\s+(.)/g, (c) => c.toUpperCase())
```

## randomString
```js
const randomString = () => Math.random().toString(36).slice(2)
```

## toCamelCase
```js
const toCamelCase = (str) => str.trim().replace(/[-_\s]+(.)?/g, (_, c) => (c ? c.toUpperCase() : ''));
```

## flatArray
```js
const flatArray = (arr) => arr.reduce((a, b) => (Array.isArray(b) ? [...a, ...flat(b)] : [...a, b]), [])

```

## removeFalsy
```js
const removeFalsy = (arr) => arr.filter(Boolean)
```

## isEven
```js
const isEven = num => num % 2 === 0
```

## randomBetween
```js
const randomBetween = (min, max) => Math.floor(Math.random() * (max - min + 1) + min)
```

## average
```js
const average = (...args) => args.reduce((a, b) => a + b) / args.length;
```

## round
```js
const round = (n, d) => Number(Math.round(n + "e" + d) + "e-" + d)
```

## diffDays
```js
const diffDays = (date, otherDate) => Math.ceil(Math.abs(date - otherDate) / (1000 * 60 * 60 * 24));
```

## dayOfYear
```js
const dayOfYear = (date) => Math.floor((date - new Date(date.getFullYear(), 0, 0)) / (1000 * 60 * 60 * 24))
```

## randomColor
```js
const randomColor = () => `#${Math.random().toString(16).slice(2, 8).padEnd(6, '0')}`
```

## rgbToHex
```js
const rgbToHex = (r, g, b) => "#" + ((1 << 24) + (r << 16) + (g << 8) + b).toString(16).slice(1)
```

## swap
```js
const swap = (firstNum,secNum) => [firstNum, secNum] = [secNum, firstNum]
```

## isNotEmpty
```js
const isNotEmpty = (arr) => Array.isArray(arr) && Object.keys(arr).length > 0
```

## swapKeysAndValues
```js
const swapKeysAndValues = (obj) => Object.fromEntries(Object.entries(obj).map(([k, v]) => [v, k]));
```
