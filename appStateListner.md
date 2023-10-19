# APP STATE - React Native

### import 
```
import { AppState } from "react-native";
```


### Listener
```
useEffect(() => {
  const appStateListener = AppState.addEventListener("change", (state) => {
    console.log("APP STATE ", state);
  });
  return () => {
    appStateListener?.remove();
  };
}, []);
```
### Output
```
 LOG  APP STATE  active
 LOG  APP STATE  inactive
 LOG  APP STATE  background
```
