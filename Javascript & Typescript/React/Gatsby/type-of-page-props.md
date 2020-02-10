# Type of Page Props
Typescript기반으로 Gatsby를 만들때 페이지의 props types를 모를 경우 types helper.

외부 type 선언 컴포넌트를 만듦.

```js
// ./src/types/gatsby.d.ts
import { ReplaceComponentRendererArgs } from 'gatsby';

export type PageProps<T> = ReplaceComponentRendererArgs['props'] & {
  pageContext: {
    isCreatedByStatefulCreatePages: boolean;
  } & T;
};
```

사용하고자 하는 페이지 컴포넌트에서 주입.

```js
// .src/pages/index.tsx
import { PageProps } from '../types/gatsby';

// type or interface
type Props = PageProps<{
  // add properties
  test: string;
  test2: string;
  test3: string;
}>;

const Page: React.FunctionComponent<Props> = props => {
  return (
    <div>{}</div>
  )
}
```