Suspense - React Native

```js
const MyComponent = React.lazy(async () => {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve(import("./src/Dummy/Component"));
        // return resolve(SusContent);
    }, 3000);
  });
});

const SusWait = () => {
   return (
     <View>
       <Text>WAIT</Text>
     </View>
   )
}
```

## Usage
```js
<Suspense fallback={<SusWait/>}>
   <MyComponent/>
</Suspense>
```
