---
layout: post
title:  React with TypeScript: Best Practices
date:   2020-03-15 00:00:00 +0300
categories: REACT,TYPESCRIPT
tag: [FRONTEND] # add tag
---

* content
{:toc}


## 前言

前端方向国内主流的还是Vue，网上的内容也比较多，公司前端框架也是采用的Vue。当前React在国内的资料相对能搜到的较少，而且React参考基本上是英文的会讲解的比较细致。当前负责产品前端模块还是隔离的比较好，也使用React做一些功能，顺便用一下FB的主推，配合上微软的Typescript，再加上Twitter的bootstrap，感觉是确实是参考资料还是十分全面的。

本文就重点写下Typescript对于React的支持，尤其是新的Hook等

## React with Typescript

最佳实践看这一篇就够了，讲解的我认为比较全面也比较详尽：
https://www.sitepoint.com/react-with-typescript-best-practices/

- create-react-app

```
npx create-react-app my-app --template typescript
```

- ESLint/Prettier

看上面文章介绍的配置就行

- interface & type

基本上interface主要给能否被外部引用的场景使用，type主要是内部类型定义场景使用

```
interface Props {
  name: string;
  color: string;
}

type OtherProps = {
  name: string;
  color: string;
}

```

Action定义type场景重点关注一下

```
type Action =
  | { type: "SET_ONE"; payload: string }
  | { type: "SET_TWO"; payload: number };
```

- 关键字 & tips

React.ReactNode

React.FC

const [user, setUser] = useState<User | null>(null);


- 第三方包的引入

```
yarn add @types/<package-name>
```


## 示例

注释部分是非hook非typescript写法，可以看到还是简化很多的

```
import React from 'react';
import ListView from '../component/ListView';
import api from '../api/getInfo';
import { usePromise } from 'promise-hook';

export interface IProps {
    data: {
        title: string;
        content: string;
        img: string;
    };
}

/** 解析接口返回数据 */
type chengpinInfo = {
    success: string;
    /** 解析接口返回数据 */
    chengpinInfo: Array<IProps>;
};

type IData = {
    isLoading: boolean;
    data: chengpinInfo;
};

const fetchWiKiInfo = () => api.getChengpinInfo().then((res) => res.json());

const List: React.FC = () => {
    // export default class List extends Component<{}, IState> {

    // constructor(props:any){
    //     super(props);
    //     this.state = ({
    //         dataInfo: {
    //             chengpinInfo: []
    //         }
    //     })
    // }

    // const [dataInfo, setDataInfo] = useState<any>({});

    //use awesome react hook - promise-hook
    const { isLoading, data }: IData = usePromise(fetchWiKiInfo, { resolve: true });

    // useEffect(() => {
    //     // (async () =>{
    //     // const response =  api.getChengpinInfo();
    //     // const data = response.json();
    //     // setDataInfo(data);
    //     // setLoading(false)
    //     // })();
    //     api.getChengpinInfo()
    //         .then(res => res.json())
    //         .then(data => {
    //             console.log(data);
    //             setDataInfo(data);
    //             setLoading(false);
    //         })
    // });

    // componentDidMount(){
    //     api.getChengpinInfo()
    //     .then(res => res.json())
    //     .then(data => {
    //         this.setState({
    //             dataInfo: data
    //         })
    //     })
    // }

    // render() {
    return (
        <div>
            {isLoading ? (
                <div>数据正在请求。。。</div>
            ) : (
                <ul>
                    {data.chengpinInfo.map((ele: any, index: number) => {
                        return <ListView key={index} data={ele}></ListView>;
                    })}
                </ul>
            )}
        </div>
    );
    // }
};

export default List;
```

## 结论

typescript是会避免一些问题的发生，但是还是需要多熟悉类型的写法，不然会花很多时间定义和调整类型