# Using Refs

## Functional Components
- 함수 컴포넌트에서 사용
```ts
// hooks
const divRef = React.useRef<HTMLDivElement>(null);

return <div ref={divRef} style={{ width: "100%" }} />;

// with Lifecycle
React.useEffect(() => {
  if (divRef.current) {
    console.log(divRef.current);
  }
}, []);
```

## Class Components
- 클래스 컴포넌트에서 사용
```ts
// this
divRef = React.createRef<HTMLDivElement>();

render() {
  return <div ref={this.divRef} style={{ width: "100%" }} />;
}

// with Lifecycle
componentDidMount() {
  if (this.divRef.current) {
    console.log(this.divRef.current);
  }
}
```

## Callback
- current말고 callback으로 사용
```ts
// this
divRef: HTMLDivElement | null = null;

setDivRef = (element: HTMLDivElement) => {
  this.divRef = element;
};

render() {
  return <div ref={this.setDivRef} style={{ width: "100%" }} />;
}

// with Lifecycle
componentDidMount() {
  if (this.divRef) {
    console.log(this.divRef.clientWidth);
  }
}
```

## Forwarding Refs
- 자식 컴포넌트 ref를 부모 컴포넌트에서 사용
```ts
const Forward = React.forwardRef((props, ref: React.Ref<HTMLDivElement>) => (
  <div ref={ref} style={{ width: "100%" }} />
));

function ForwardRefRef() {
  const divRef = React.useRef<HTMLDivElement>(null);
  React.useEffect(() => {
    if (divRef.current) {
      console.log(divRef.current.clientWidth);
    }
  });
  return <Forward ref={divRef} />;
}
```
