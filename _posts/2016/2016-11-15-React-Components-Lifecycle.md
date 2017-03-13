---
layout: post
category : article
title : React - Components & Lifecycle
tags : [Javascript,React]
---

## Component Example
- ES6

    ```
    <script type="text/babel">
    /*第一字需要大寫*/
    class Message extends React.Component {
    render() {
        return <h3>Hello world !</h3>;
    }
    }
    const element = <Message />;
    
    ReactDOM.render(
    element,
    document.getElementById('root')
    );
    </script>
    ```

- Without ES6

    ```
    <script type="text/babel">
    /*第一字需要大寫*/
    var Message = React.createClass({
        render: function () {
            return <h3>Hello world !</h3>
        }
    });
    const element = <Message />;
    
    ReactDOM.render(
        element,
        document.getElementById('root')
    );
    </script>
    ```
## Component Initial State
- ES6

    ```
    <script type="text/babel">
    /*第一字需要大寫*/
    class Message extends React.Component {
        constructor(props){
        super(props)
        this.state={count:this.props.initialCount}
        }
    render() {
        return <h3>Count: {this.state.count}</h3>;
    }
    }
    const element = <Message initialCount="2" />;
    ReactDOM.render(
    element,
    document.getElementById('root')
    );
    </script>
    ```
    
- Without ES6

    ```
    <script type="text/babel">
    /*第一字需要大寫*/
    var Message = React.createClass({
        getInitialState:function(){
        return {count:this.props.initialCount};
        },
        render: function () {
            return <h3>Count: {this.state.count}</h3>
        }
    });
    
    const element = <Message initialCount="2" />;
    ReactDOM.render(
        element,
        document.getElementById('root')
    );
    </script>
    ```

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20161108/0013.png" alt="0013"/>

## Component Initial State from Ajax

- ES6 

    ```
    <script type="text/babel">
    const url='@Url.Action("GetData")'
    /*第一字需要大寫*/
    class Message extends React.Component {
    constructor(props){
        super(props)
        this.state={count:0}
    }
    componentDidMount(){
            $.get(url,(result)=>{
                this.setState({count:result.count})
            })
    }
    render() {
        return <h3>Count: {this.state.count}</h3>;
    }
    }
    const element = <Message />;
    ReactDOM.render(
    element,
    document.getElementById('root')
    );
    </script>
    ```

- Without ES6

    ```
    <script type="text/babel">
    const url='@Url.Action("GetData")'
    /*第一字需要大寫*/
    var Message = React.createClass({
        getInitialState:function(){
        return {count:0};
        },
        componentDidMount:function(){
            let self=this;
            $.get(url,function (result){
                return self.setState({count:result.count})
            })
        },
        render: function () {
            return <h3>Count: {this.state.count}</h3>
        }
    });
    const element = <Message />;
    ReactDOM.render(
        element,
    document.getElementById('root')
    );
    </script>
    ```

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20161108/0014.png" alt="0014"/>

## Lifecycle

- Mounting (These methods are called when an instance of a component is being created and inserted into the DOM)
    - constructor()
    - componentWillMount()
    - render()
    - componentDidMount()
- Updating (An update can be caused by changes to props or state. These methods are called when a component is being re-rendered)
    - componentWillReceiveProps()
    - shouldComponentUpdate()
    - componentWillUpdate()
    - render()
    - componentDidUpdate()
- Unmounting (This method is called when a component is being removed from the DOM)
    - componentWillUnmount()

## 參考資料
- [React Component](https://facebook.github.io/react/docs/react-component.html)