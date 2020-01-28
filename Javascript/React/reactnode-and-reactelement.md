# ReactNode and ReactElement in Typescript
react component 받을때 type 선언

```js
// ReactNode
type ReactNode = ReactChild | ReactFragment | ReactPortal | boolean | null | undefined;
```
- `ReactElement`, `ReactFragment`, `ReactPortal`, `boolean`, `null`, `undefined` 중 하나.
- `render()`와 `children`의 기본 type

```js
// ReactElement
interface ReactElement<P = any, T extends string | JSXElementConstructor<any> = string | JSXElementConstructor<any>> {
  type: T;
  props: P;
  key: Key | null;
}

// JSX.Element
declare global {
  namespace JSX {
    interface Element extends React.ReactElement<any, any> { }
  }
}
```
- **ReactElement**은 type과 props로 이루어진 객체.
- **JSX.Element**와 동일하며 type과 props의 generic type은 any.
- **JSX.Element**는 다양한 라이브러리가 자체 방식으로 JSX를 구현할 수 있으므로 JSX는 라이브러리에 의해 설정되는 글로벌 네임스페이스.

```js
// ElementType
type ElementType<P = any> = {
  [K in keyof JSX.IntrinsicElements]: P extends JSX.IntrinsicElements[K] ? K : never
}[keyof JSX.IntrinsicElements] | ComponentType<P>;

// ex: react native
const Wrap: React.ElementType = item.onPress ? TouchableOpacity : View;
```
- Wrapper로 쓰임
- ts(2604) 에러