---
layout: post
category : article
title : React - Syntax JSX
tags : [Javascript,React]
---

## JSX Example 1
- const 是es6的語法，類似[c#的const](https://msdn.microsoft.com/zh-tw/library/e6w8fe1b.aspx)，簡易來說就是一個不可改變的常數，但JSX予許使用Html與JS混合使用。

    ```
    <script  type="text/babel">
        const element = <h3>Hello, world!</h3>;
        ReactDOM.render(<div>{element}</div>,document.getElementById('root'));
    </script>
    ```

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20161108/0007.png" alt="0007"/>

## JSX Example 2
- { } 使用大括號是處理JSX 參數、方法等標示方式。

    ```
    <script type="text/babel">
        function fullName(user){
            return user.firstName+' '+ user.lastName;
        }
        const user={
            firstName:'Leo',
            lastName:'Li'
        }
        const element =<h3>Hello, {fullName(user)}!</h3>;
        ReactDOM.render(<div>{element}</div>,document.getElementById('root'));
    </script>
    ```

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20161108/0010.png" alt="0010"/>

    ```
    <script type="text/babel">
        const divStyle={color:'blue'}
        const element = <h3>Hello, world!</h3>;
        ReactDOM.render(<div style={divStyle}>{element}</div>,document.getElementById('root'));
    </script>
    ```

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20161108/0011.png" alt="0011"/>

## JSX Example 3
- Dynamic Children 可用陣列產生多個節點，但需加key(唯一值)關鍵字讓React Virtual DOM 識別處理。

    ```
    <script type="text/babel">
        var data=["leo","lee"];

        const element =
        <ol>
            {data.map(function(item,index){
                return <li key={index}>Hi, {item}</li>;
            })}
        </ol>;
        ReactDOM.render(
        <div>{element}</div>,document.getElementById('root'));
    </script>
    ```

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20161108/0012.png" alt="0012"/>

## 參考資料
- [http://React Docs JSX](https://facebook.github.io/react/docs/introducing-jsx.html)
- [React 入門實例教程 - JSX](http://www.ruanyifeng.com/blog/2015/03/react.html)
- [ECMAScript 6 入門 - const](http://es6.ruanyifeng.com/#docs/let#const命令) 
- [React Docs Dynamic Children](http://reactjs.cn/react/docs/multiple-components.html#dynamic-children)

## 延伸閱讀
- [js-array-operations](https://github.com/tooto1985/js-array-operations)