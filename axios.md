# Axios - React Native

## Run
```shell
yarn add axios
```

## Service
```js
import axios from "axios";

const instance = axios.create({
  // baseURL: "https://mocki.io/v1/",
  timeout: 5000,
  // headers: { "Content-Type": "application/json" },
});

instance.defaults.baseURL = "https://mocki.io/v1/";
// instance.defaults.headers.common['Authorization'] = AUTH_TOKEN;
instance.defaults.headers.post["Content-Type"] = "application/json";

instance.interceptors.request.use((config) => {
  console.log("axios", "request", "before", "Do something before request is sent");
  return config;
}, (error) => {
  console.log("axios", "request", "after", "Do something with request error");
  return Promise.reject(error);
});
instance.interceptors.response.use((response) => {
  console.log("axios", "response", "after", "Do something with response data", " range of 2xx");
  return response;
}, (error) => {
  console.log("axios", "response", "after", "Do something with response error", " range of 2xx");
  return Promise.reject(error);
});

export default instance;
```
## Usage
```js
const apiResponse = await instance.get('d4867d8b-b5d5-4a48-a4ab-79131b5809b8');
```
