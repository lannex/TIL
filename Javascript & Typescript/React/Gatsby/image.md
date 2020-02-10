# Image
- Gatsby에서 이미지 처리를 GraphQL로 할 경우 컴포넌트 하나로 재사용 가능
- `filename`과 `alt`를 props로 전달

```js
import React from 'react';
import { StaticQuery, graphql } from 'gatsby';
import Img from 'gatsby-image';

interface Props {
  filename: string;
  alt: string;
}

const Image = (props: Props): React.ReactElement => (
  <StaticQuery
    query={graphql`
      query {
        images: allFile {
          edges {
            node {
              relativePath
              name
              childImageSharp {
                fluid(maxWidth: 1000) {
                  ...GatsbyImageSharpFluid
                }
              }
            }
          }
        }
      }
    `}
    render={(data): React.ReactNode => {
      const image = data.images.edges.find(n => {
        return n.node.relativePath.includes(props.filename);
      });
      if (!image) {
        return null;
      }

      // const imageSizes = image.node.childImageSharp.sizes; sizes={imageSizes}
      return <Img alt={props.alt} fluid={image.node.childImageSharp.fluid} />;
    }}
  />
);

export default Image;
```

- 이미지 불러올때 래핑한번 더해서 스타일 지정

```js
import Image from '../components/Image';

<div style={{ maxWidth: `300px` }}>
  <Image alt="Gatsby in Space" filename="gatsby-astronaut.png" />
</div>
```