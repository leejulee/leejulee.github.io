---
layout: post
category : article
title : React - MVC Project Example - Hello World (JSX)
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
- View Add Html & Script
    ```
    <div id="root">
        <!-- This div's content will be managed by React. -->
    </div>
    
    <script type="text/babel">
        ReactDOM.render(
        <h3>Hello, world!</h3>,
        document.getElementById('root')
        );
    </script>
    ```
- View JS & Result 

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20161108/0008.png" alt="0008"/>

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20161108/0007.png" alt="0007"/>

## 參考資料
- [react](https://facebook.github.io/react/docs/hello-world.html)
- [react-quick-tutorial(Jason Chung)](https://github.com/shiningjason1989/react-quick-tutorial/tree/master/level-02_initial-project)