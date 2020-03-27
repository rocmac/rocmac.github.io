---
layout: post
title:  React Bootstrap
date:   2020-03-27 00:00:00 +0300
categories: REACT,Bootstrap
tag: [FRONTEND] # add tag
---

* content
{:toc}


## 前言

前端UI框架繁多，当前国内主要使用的基本是阿里的antd，全球流行的应该就是twitter的Bootstrap了。当然Bootstrap无论从文档的成熟从程度，易用度等感觉都更胜一筹，尤其是对于React的支持上。

当然两个框架的比较网上一搜一大把，这次就写写React和Bootstrap中使用到的一些周边技术和插件吧，权当流水账记录一下。

## React-Bootstrap

[https://react-bootstrap.netlify.com/getting-started/introduction](https://react-bootstrap.netlify.com/getting-started/introduction)

划重点：React-Bootstrap是Bootstrap的javascript重新实现版本

- 与reactstrp对比

两者定位差不多，但是如下面链接所示，还是React-Bootstrap更胜一筹
  
[https://www.npmtrends.com/react-bootstrap-vs-reactstrap](https://www.npmtrends.com/react-bootstrap-vs-reactstrap)

- 实现参考

发现结合css使用起来在定义名称时候有点不方便
  
```
import { Container, Row, Col } from 'react-bootstrap';
                
<Container>
    <Row className="rows">
        <Col className="columns">
            <button>1 of 2</button>
        </Col>
        <Col className="columns">2 of 2</Col>
    </Row>
    <Row className="rows">
        <Col className="columns">1 of 3</Col>
        <Col className="columns">2 of 3</Col>
        <Col className="columns">3 of 3</Col>
    </Row>
</Container>
```

- container布局flexbox

可以参考官网

[https://css-tricks.com/snippets/css/a-guide-to-flexbox/](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

参考代码

```
.container-1 {
    display: flex;
    /* align-items: flex-end; */
    /* flex-direction: column; */
    div {
        border: 1px #ccc solid;
        padding: 10px;
    }
}
.container-1 div .box-1 {
    flex: 2;
    order: 2;
}
.box-2 {
    flex: 1;
    order: 1;
}
.box-3 {
    flex: 1;
    order: 3;
}
```

## 其他

- Sass

css对于我简直如天书一般神奇，一直没有深入研究，照葫芦画瓢。贴个指南后面慢慢研究吧

[https://sass-lang.com/guide](https://sass-lang.com/guide)

- styled-components

在React中更加方便的定义和使用css

看一个Button的组件

```
import styled from 'styled-components';

const Button = styled.button`
    appearance: none;
    background-color: ${(props) => props.theme.Navy};
    color: white;
    border: 1px solid white;
    padding: 0.25em 0.25em;
    transition: backgroud-color 0.25s, color 0.25s;
    ${(props) => {
        switch (props.size) {
            case 'sm':
                return 'font-size:12px;';
            case 'lg':
                return 'font-size:20px;';
        }
        return 'font-size:16px;';
    }};
    &:hover {
        background-color: white;
        color: ${(props) => props.theme.Navy};
        cursor: pointer;
    }
`;
export default Button;
```

添加全局样式

```
import { ThemeProvider } from 'styled-components';
import * as theme from './config/theme';

ReactDOM.render(
    <ThemeProvider theme={theme}>
        <React.StrictMode>
            <App />
        </React.StrictMode>
    </ThemeProvider>,
    document.getElementById('root'),
);
```

使用

```
${(props) => props.theme.Navy};
```

theme.js

```
export const Navy = '#9E8B00';
export const dimGray = '#636363';
```


## 结论

前端变化真是一日千里，迭代速度非常快，也有繁多的工具和包供大家选择。要多关注业内动态，一些新的技术和方法确实可以节省非常多的时间。