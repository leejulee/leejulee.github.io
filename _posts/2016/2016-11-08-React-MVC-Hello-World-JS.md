---
layout: post
category : article
title : React - MVC Project Example - Hello World (JS) 
tags : [Javascript,React]
---

## 環境
- VS2013
- React V.14.7

## Skill
- [reactjs](https://facebook.github.io/react/)

## 操作步驟

{% include react-create-project.md %}

- View Include React js

    ```
    <script src="~/Scripts/react/react.js"></script>
    <script src="~/Scripts/react/react-dom.js"></script>
    ```

- View Add Html & Script

    ```
    <div id="root">
        <!-- This div's content will be managed by React. -->
    </div>
    <script>
        var Message = React.createClass({
            render: function () {
                return (React.createElement("h3", null, "Hello, world!"));
            }
        });
        ReactDOM.render(React.createElement(Message, null), document.getElementById('root'));
    </script>
    ```

- View JS & Result

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20161108/0006.png" alt="0006"/>

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20161108/0007.png" alt="0007"/>
