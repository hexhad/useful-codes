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
```
