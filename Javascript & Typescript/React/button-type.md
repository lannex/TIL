# Button Type
- `React.HTMLProps<HTMLButtonElement>`;
- 버튼 타입외에도 HTMLProps로 Element처리

```ts
class MyButton extends React.Component<MyButtonProps & React.HTMLProps<HTMLButtonElement>, {}> {
  render() {
    return <button {...this.props}/>;
  }
}
```
