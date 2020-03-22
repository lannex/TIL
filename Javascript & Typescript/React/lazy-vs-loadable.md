# React.lazy vs Loadable components
- 코드 분할을 위해 동적 import 방법
- 기본적으로 코드 분할은 라우터에 사용하고 그 외 필요한 곳에 추가
- lazy경우 ssr지원을 하지 않고 lodable은 ssr지원
- 사실상 lodable을 사용하는게 더 유리

## `lazy` and `Suspense`
- `lazy`는 `Suspense` 하위에서 동작

```js
import React, { Suspense, lazy } from 'react';
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';

const Home = lazy(() => import('./routes/Home'));
const About = lazy(() => import('./routes/About'));

const App = () => (
  <Router>
    <Suspense fallback={<div>Loading...</div>}>
      <Switch>
        <Route exact path="/" component={Home}/>
        <Route path="/about" component={About}/>
      </Switch>
    </Suspense>
  </Router>
);
```

## `lodable`
- `lazy`는 `Suspense`가 필요한 반면 `loadable`은 단독으로 사용

```js
import loadable from '@loadable/component'

const OtherComponent = loadable(() => import('./OtherComponent'))

function MyComponent() {
  return (
    <div>
      <OtherComponent fallback={<div>Loading...</div>} />
    </div>
  )
}
```
