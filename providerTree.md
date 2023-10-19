# ProviderTree - React Native

## builtProviderTree.js
```
export const buildProvidersTree = (componentWithProps) => {
  return componentWithProps.reduce((AccumulatedComps, [Provider, props = {}]) => ({ children }) => (
    <AccumulatedComps>
      <Provider {...props}>{children}</Provider>
    </AccumulatedComps>
  ), ({ children }) => <>{children}</>);
};
```

## Usage

```
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
