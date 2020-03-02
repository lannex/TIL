# useReducer
- `useState`를 여러개 사용해야할 경우 `useReducer`를 사용

```ts
// State types
interface State {
  userId: string;
  isLoading: boolean;
}

// Action types
type Action =
  | { type: 'setUserId'; value: string }
  | { type: 'setIsLoading' };

// Initialize State
const initialState: State = {
  userId: '',
  isLoading: false,
};

// Reducer
const reducer = (state: State, action: Action): State => {
  switch (action.type) {
    case 'setUserId':
      return {
        ...state,
        userId: action.value,
      };

    case 'setIsLoading':
      return {
        ...state,
        isLoading: !state.isLoading,
      };

    default:
      return state;
  }
};
```

```ts
// Stateless Component
// ...
const [state, dispatch] = React.useReducer(reducer, initialState);
// ...
dispatch({ type: 'setUserId', value: e.target.value });
```
