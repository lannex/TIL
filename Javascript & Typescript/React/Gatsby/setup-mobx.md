# Setup MobX

## package.json
```bash
$ yarn add -E -D mobx mobx-react @babel/plugin-proposal-decorators babel-preset-gatsby
```

## .babelrc
```json
{
  "presets": ["babel-preset-gatsby"],
  "plugins": [["@babel/plugin-proposal-decorators", { "legacy": true }]]
}
```

## Root Environment
### `src/stores/Provider.tsx`
```ts
import * as React from 'react';
import { Provider, ProviderProps } from 'mobx-react';

// stores
import RootStore from './index';

const stores = new RootStore();

const MobXProvider: React.FunctionComponent<ProviderProps> = ({ element }) => {
  return <Provider stores={stores}>{element}</Provider>;
};

export default MobXProvider;

```

### `gatsby-browser.js` and `gatsby-ssr.js`
```ts
import Provider from './src/stores/Provider';

import './src/css/index.css';

export const wrapRootElement = Provider;

```

## Stores
### `src/stores/index.ts`
```ts
import CustomStore from './customStore';

class RootStore {
  customStore;

  constructor() {
    this.customStore = new CustomStore();
  }
}
export default RootStore;

```

### `src/stores/useStores.tsx`
```ts
import React from 'react';
import { MobXProviderContext } from 'mobx-react';

function useStores() {
  return React.useContext(MobXProviderContext);
}

export default useStores;

```

### `src/stores/customStore.ts`
```ts
import {
  observable,
  // action,
  // computed
} from 'mobx';

interface ItemProps {
}

export default class CustomStore {
  @observable item: ItemProps = {
  };
}

```