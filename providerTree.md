# ProviderTree - React Native

## builtProviderTree.js
```js
export const buildProvidersTree = (componentWithProps) => {
  return componentWithProps.reduce((AccumulatedComps, [Provider, props = {}]) => ({ children }) => (
    <AccumulatedComps>
      <Provider {...props}>{children}</Provider>
    </AccumulatedComps>
  ), ({ children }) => <>{children}</>);
};
```

## Usage

```js
const ProviderTree = buildProvidersTree([
  [ThemeProvider],
  [Provider, { store }],
  [PersistGate, { persistor, loading: <LoaderComp /> }],
  [NavigationContainer, { ref }],
]);

return (
   <ProviderTree>
     {children}
   </ProviderTree>
)
```
