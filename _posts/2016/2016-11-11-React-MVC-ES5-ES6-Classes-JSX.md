---
layout: post
category : article
title : React - MVC Project ES5 & ES6 Classes Example (JSX)
tags : [Javascript,React]
---

## 環境
- VS2013
- React V.14.7

## Skill
- [reactjs](https://facebook.github.io/react/)

## 操作步驟
{% include react-create-project.md %}

- View Include [babel-core 5.8.34](https://cdnjs.com/libraries/babel-core/5.8.34) js

    ```
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.34/browser-polyfill.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.34/browser.js"></script>
    ```
- View include React js

    ```
    <script src="~/Scripts/react/react.js"></script>
    <script src="~/Scripts/react/react-dom.js"></script>
    ```
- html tag

    ```
    <div id="root">
        <!-- This div's content will be managed by React. -->
    </div>
    ```
- ES5

    ```
    <script  type="text/babel">
        var Message = React.createClass({
            render: function () {
                return  (<h3>Hello, world!</h3>)
            }
        });
    
        ReactDOM.render(<Message/>,document.getElementById('root'));
    </script>
    ```
- ES6

    ```
    <script  type="text/babel">
        class Message extends React.Component{
            render(){
                return <h3>Hello, world!</h3>
            }
        }
    
        ReactDOM.render(<Message/>,document.getElementById('root'));
    </script>
    ```

- View JS & Result 

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20161108/0009.png" alt="0009"/>

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20161108/0007.png" alt="0007"/>

## 參考資料
- [[Bebel] React on ES6+](https://babeljs.io/blog/2015/06/07/react-on-es6-plus)
- [一看就懂的 React ES5、ES6+ 常見用法對照表](http://blog.techbridge.cc/2016/04/04/react-react-native-es5-es6-cheat-sheet/)

## 延伸閱讀
- [ECMAScript 6 入門 - Classes](http://es6.ruanyifeng.com/#docs/class)