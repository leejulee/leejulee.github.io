---
layout: post
category : article
title : React - Props
tags : [Javascript,React]
---

## props 
- 通常使用在不變動的資料(可當常數來看)，用來處理資料流的傳遞，可以想像似Html 的設定屬性後，接著讀取屬性值做處理。

    ```
    <script type="text/babel">
    //建立一個Message Class，並開放屬性為 name 供資料傳遞
    class Message extends React.Component {
    render() {
        return <h3>Hello, {this.props.name}</h3>;
    }
    }
    //建立 Message element ，並設定屬性 name 的值
    const element = <Message name="Leo" />;
    //render view
    ReactDOM.render(
    element,
    document.getElementById('root')
    );    
    </script>
    ```

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20161108/0015.png" alt="0015"/>

## propTypes
- 可加強型別驗證，避免傳入非預期格式。

    ```
    <script type="text/babel">
    class Message extends React.Component {
    render() {
        return <h3>Age : {this.props.age}</h3>;
    }
    }
    //定義name屬性為字串格式
    Message.propTypes={
        age:React.PropTypes.number
    }
    //error
    const element = <Message age='test' />;
    //correct
    //const element = <Message age={123} />;
    ReactDOM.render(
    element,
    document.getElementById('root')
    );
    </script>
    ```

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20161108/0016.png" alt="0016"/>

## 參考資料
- [Typechecking With PropTypes](https://facebook.github.io/react/docs/typechecking-with-proptypes.html)