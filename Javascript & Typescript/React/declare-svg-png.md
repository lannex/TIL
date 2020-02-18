# Declare svg, png
`src > types > custom.d.ts`

## svg
```ts
declare module '*.svg' {
  import React = require('react');
  export const ReactComponent: React.SFC<React.SVGProps<SVGSVGElement>>;
  const src: string;
  export default src;
}
```

## png
```ts
declare module '*.png' {
  const value: any;
  export = value;
}
```
