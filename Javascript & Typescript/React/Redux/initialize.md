# Initialize Redux

## Dependencies
```bash
$ yarn add -E redux react-redux redux-logger redux-devtools-extension
```

## Actions
- 어플리케이션이 스토어로 보내는 데이터 묶음
- 데이터 묶음에는 액션 타입과 데이터(payload)가 있음

```js
// actions/index.js
import * as types from './types';

export const setProduct = product => ({
  type: types.SET_PRODUCT,
  payload: product,
});
```

```js
// actions/types.js
export const SET_PRODUCT = 'SET_PRODUCT';
```

## Reducers
- 액션을 받은 스토어는 액션 타입에 따라 스토어를 갱신하는데 이 역할을 리듀서가 실행

```js
// reducers/index.js
import { combineReducers } from 'redux';
import addProduct from './addProduct';

const rootReducer = combineReducers({
  addProduct,
});

export default rootReducer;
```

```js
// reducers/addProduct.js
import * as types from '../actions/types';

const initialState = {
  product: null,
};

const addProductReducer = (state = initialState, action) => {
  switch (action.type) {
    case types.SET_PRODUCT:
      return {
        ...state,
        product: action.payload,
      };
    default:
      return state;
  }
};

export default addProductReducer;
```

## Stores
- 결국 action과 reducer를 가지고 최종적으로 store를 만듦

```js
// createStore
// stores/configureStore.js
import { createStore, applyMiddleware } from 'redux';
import { createLogger } from 'redux-logger';
import { composeWithDevTools } from 'redux-devtools-extension';
import rootReducer from '../reducers';

const configureStore = () =>
  createStore(
    rootReducer,
    composeWithDevTools(applyMiddleware(createLogger())),
  );

export default configureStore;
```

## Bind to Root
- 루트에 `Provider` 바인딩
```js
// react
ReactDOM.render(
  <Provider store={store}>
    <Root />
  </Provider>,
  document.getElementById('app')
);
```

```js
// gatsby
// wrapRootElement.js
import * as React from 'react';
import { Provider } from 'react-redux';

import createStore from '../../stores/configureStore';

const store = createStore();

export default ({ element }): React.ReactNode => {
  return <Provider store={store}>{element}</Provider>;
};

// gatsby-browser.js,
// gatsby-ssr.js
import WrapRootElement from './src/components/WrapRootElement';

export const wrapRootElement = WrapRootElement;
```