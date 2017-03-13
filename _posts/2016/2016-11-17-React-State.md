---
layout: post
category : article
title : React - State
tags : [Javascript,React]
---

## steate
- 通常是與使用者互動上資料更新、Server資料，並使用setState來更新資料。

    ```
    <script type="text/babel">
    class Clock extends React.Component {
    constructor(props) {
        /*父類別建構時(super)，傳遞props，才可使用this.props (可參考 http://cheng.logdown.com/posts/2016/03/26/683329 or http://es6.ruanyifeng.com/#docs/class 說明)*/
        super(props);
        this.state = {date: new Date()};
    }
    /*在render後執行 (可參考 https://facebook.github.io/react/docs/react-component.html)*/
    componentDidMount() {
        this.timerID = setInterval(
        () => this.tick(),
        1000
        );
    }
    /*在移除DOM前執行 (可參考 https://facebook.github.io/react/docs/react-component.html)*/
    componentWillUnmount() {
        clearInterval(this.timerID);
    }
    
    tick() {
        this.setState({
        date: new Date()
        });
    }
    
    render() {
        return (
        <div>
            <h3>Hello, world!</h3>
            <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
        </div>
        );
    }
    }
    
    ReactDOM.render(
    <Clock />,
    document.getElementById('root')
    );
    </script>
    ```

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20161108/0017.png" alt="0017"/>

## 參考資料
- [State and Lifecycle](https://facebook.github.io/react/docs/state-and-lifecycle.html)
- [React ES6 class constructor super](http://cheng.logdown.com/posts/2016/03/26/683329)
- [ECMAScript 6 入門 - Class](http://es6.ruanyifeng.com/#docs/class)
- [React.Component](https://facebook.github.io/react/docs/react-component.html)