# MMKV for Redux-Persist - React Native
## Storage.js
```
import { MMKV } from "react-native-mmkv";

const storage = new MMKV();

export const mmkvStorage = {
  setItem: (key, value) => {
    storage.set(key, value);
    return Promise.resolve(true);
  },
  getItem: (key) => {
    const value = storage.getString(key);
    return Promise.resolve(value);
  },
  removeItem: (key) => {
    storage.delete(key);
    return Promise.resolve();
  },
};
```
## Usage
```
import { mmkvStorage } from "./persist/storage";

const persistConfig = {
  ...
  storage: mmkvStorage,
};
```
