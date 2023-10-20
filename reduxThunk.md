# Redux - React Native

## Run
```shell
yarn add redux react-redux redux-thunk
```
## types.js
```js
export const DUMMY = {
  LOADING:'DUMMY/LOADING',
  SUCCESS:'DUMMY/SUCCESS',
  FAILED:'DUMMY/FAILED',
}
```

## mainReducer.js
```js
import { DUMMY } from "../types/types";

const initialState = {
  dummy:{
    loading:false,
    data:[],
    error:null
  }
};

export default (state=initialState,action) => {
  switch (action.type) {
    case DUMMY.LOADING : return {
      ...state,
      loading: true,
    }
    case DUMMY.SUCCESS : return {
      ...state,
      loading: false,
      data: action.payload,
    }
    case DUMMY.FAILED : return {
      ...state,
      loading: false,
      error: action.payload,
    }
    default : return state
  }
}
```

## rootReducer.js
```js
import { combineReducers } from "redux";
import dummyReducer from "./dummyReducer";

const rootReducer=  combineReducers({
  dummy:dummyReducer
});

export default rootReducer
```

## action.js
```js
import { DUMMY } from "../types/types";
import { delay } from "../../utils/common";

const dummyActionCurry = () => async (dispatch, getState) => {
  try {
    dispatch({ type: DUMMY.LOADING });
    await delay();
    dispatch({ type: DUMMY.SUCCESS, payload: 'success' });

  } catch (e) {
    dispatch({ type: DUMMY.FAILED, payload: e });
  }
}

export const DummyFunctions = {
  dummyActionCurry
}
```

## store.js
```js
import { applyMiddleware, createStore } from "redux";
import rootReducer from "./reducer";
import thunk from "redux-thunk";
import { logger } from "redux-logger/src";

export const store = createStore(
  rootReducer,
  applyMiddleware(...[thunk, logger]),
);
```

## Usage
```js
import { Provider } from "react-redux";
import { store } from "./redux/store";

<Provider store={store}>
   {children}
</Provider>
```
