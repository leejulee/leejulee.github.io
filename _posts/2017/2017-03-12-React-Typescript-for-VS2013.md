---
layout: post
category : article
title : React - Typescript for VS2013
tags : [Javascript,React]
---

## 環境
- [VS2013 Typescript 1.8.5](https://www.microsoft.com/en-us/download/details.aspx?id=48739)
- [Web Essentials 2013.5](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.WebEssentials20135)
- React V.14.7

## Skill
- [reactjs](https://facebook.github.io/react/)
- [Typescript](https://www.typescriptlang.org/docs/handbook/basic-types.html)
- [requirejs](http://requirejs.org/)

## 操作步驟
{% include react-create-project.md %}

- Nuget Install [RequireJS](https://www.nuget.org/packages/RequireJS/)

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170312/0001.png" alt="0001"/>

- download [React Typescript V0.14](https://github.com/DefinitelyTyped/DefinitelyTyped/tree/327d35fb7a24c60b4f829a3902a37d2e582269c9/react)

- VS2013 folder Result

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170312/0002.png" alt="0002"/>

- Setting Typescript config  (Project Name -> Click Right ->Properties )

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170312/0003.png" alt="0003"/>

- Add jsx file to Scripts folder

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170312/0004.png" alt="0004"/>

- demo.tsx (jsx file)

    ```
    /// <reference path="typings/react/react.d.ts" />
    /// <reference path="typings/react/react-dom.d.ts" />
    
    import * as React from 'react';
    import * as ReactDOM from 'react-dom';
    
    var CommentBox = React.createClass({
        render: function () {
            return (
                <div className="commentBox">
                    Hello, world!I am a CommentBox.
                    </div>
            );
        }
    });
    
    ReactDOM.render(
        <CommentBox />,
        document.getElementById('content')
    );
    ```

- View

    ```
    @{
        Layout = null;
    }
    
    <html>
    <head>
        <title>Hello React</title>
    </head>
    <body>
        <script src="~/Scripts/react/react.js"></script>
        <script src="~/Scripts/react/react-dom.js"></script>
        <script src="~/Scripts/require.js"></script>
        <script type="text/javascript">
            requirejs.config({
                baseUrl: '/Scripts',
                paths: {
                    react: 'react/react',
                    'react-dom': 'react/react-dom'
                }
            })
    
            // Load the main app module to start the app
            requirejs(["/scripts/Tutorialts.js"]);
        </script>
        <h1>Typescript Demo</h1>
        <div id="content"></div>
    </body>
    </html>
    ```

- Result

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170312/0005.png" alt="0005"/>

## 延伸學習
- [requirejs](http://requirejs.org/docs/whyamd.html)
- [[Javascript] AMD 簡單介紹](https://dotblogs.com.tw/kirkchen/2012/06/20/javascript_amd_introduction)
