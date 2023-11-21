
## Debounce
```js
const debounce = (fn, time) => {
  let timeout;
  return (args) => {
    const assignArgs = () => fn(args);
    if (timeout) clearTimeout(timeout);
    timeout = setTimeout(assignArgs, time);
  };
};
```
### Usage
```js
const handleDebounce = debounce((e)=>{
   console.log('debounce  ',e);
},2000)
```
```js
return (
    <SafeAreaView>
        <View>
            <TextInput onChangeText={handleDebounce} placeholder={'debounce'}/>
        </View>
    </SafeAreaView>
);
```
## Throttle
```js
const throttle = (fn, time) => {
  let waiting = false;
  return (args) => {
    if (waiting) return;
    waiting = true;
    setTimeout(() => {
      fn(args);
      waiting = false;
    }, time);
  };
};
```
### Usage
```js
const handleThrottle = throttle((e)=>{
   console.log('throttle  ',e);
},2000)
```
```js
return (
    <SafeAreaView>
        <View>
            <TextInput onChangeText={handleThrottle} placeholder={'debounce'}/>
        </View>
    </SafeAreaView>
);
```
