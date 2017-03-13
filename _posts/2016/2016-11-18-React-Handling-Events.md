---
layout: post
category : article
title : React - Handling Events
tags : [Javascript,React]
---

## React Example 1 - Html & React

- Html & Scripts

    ```
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.34/browser-polyfill.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.34/browser.js"></script>
    <script src="~/Scripts/react/react.js"></script>
    <script src="~/Scripts/react/react-dom.js"></script>
    
    <h2>React Demo</h2>
    ```

- Add btnClick function

    ```
    <script type="text/javascript">
        function btnClick() {
            console.info('click')
        }
    </script>
    ```

- Html JS Event

    ```
    <button onclick="btnClick()">Click Event</button>
    ```

- React Event

    ```
    <script type="text/babel">
    //注意onClick大小寫，並用大括號{}呼叫方法
    const element = <button onClick={btnClick} >React Click Event</button>
    ReactDOM.render(
    element,
    document.getElementById('root')
    );
    </script>
    ```

## React Example 2 - ES6 Class

- Html & Scripts

    ```
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.34/browser-polyfill.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.34/browser.js"></script>
    <script src="~/Scripts/react/react.js"></script>
    <script src="~/Scripts/react/react-dom.js"></script>
    
    <h2>React Demo</h2>
    ```

 - ES6 Class
  
    ```
    class Toggle extends React.Component{
        constructor(){
        super()
            //梆定事件 (This binding is necessary to make `this` work in the callback)
            this.btnClick=this.btnClick.bind(this);
        }
        btnClick(){
            console.info('react Click')
        }
        //注意onClick大小寫，並用大括號{}呼叫方法
        render(){
            return <button onClick={this.btnClick}>React Click Event</button>
        }
    }
    const element = <Toggle />
    ReactDOM.render(
    element,
    document.getElementById('root')
    );
    ```

## 參考資料
- [Handling Events](https://facebook.github.io/react/docs/handling-events.html)    