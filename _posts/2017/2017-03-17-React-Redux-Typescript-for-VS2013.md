---
layout: post
category : article
title : React - Redux Typescript for VS2013
tags : [Javascript,React]
---

## 環境
- [VS2013 Typescript 1.8.5](https://www.microsoft.com/en-us/download/details.aspx?id=48739)
- [Web Essentials 2013.5](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.WebEssentials20135)
- React V.14.7
- [node v6.9.1](https://nodejs.org/en/) 
- npm 3.10.9

## Skill
- [reactjs](https://facebook.github.io/react/)
- [redux](https://github.com/reactjs/redux)
- [react-redux](https://github.com/reactjs/react-redux)
- [Typescript](https://www.typescriptlang.org/docs/handbook/basic-types.html)
- [requirejs](http://requirejs.org/)
- [whatwg-fetch](https://github.com/github/fetch)

## 事先閱讀
- [Redux 中文文檔](http://cn.redux.js.org/docs/basics/index.html)
- [Redux tutorial 中文](https://github.com/react-guide/redux-tutorial-cn)

{% include react-create-project.md %}

- Nuget Install [RequireJS](https://www.nuget.org/packages/RequireJS/)

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170312/0001.png" alt="0001"/>

- download [React Typescript V0.14](https://github.com/DefinitelyTyped/DefinitelyTyped/tree/327d35fb7a24c60b4f829a3902a37d2e582269c9/react)

- Setting Typescript config  (Project Name -> Click Right ->Properties )

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170312/0003.png" alt="0003"/>

- npm download redux & add Project 

    ```
    npm install --save redux
    ```

    - 取資料夾的js加到專案

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170317/0001.png" alt="0001"/>

- npm download react-redux & add Project

    ```
    npm install --save react-redux
    ```

    - 取資料夾的js加到專案

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170317/0002.png" alt="0002"/>

- Nuget Install redux & react-redux typescript

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170317/0003.png" alt="0003"/>

- npm download whatwg-fetch & add Project

    ```
    npm install whatwg-fetch
    ```

    - 取資料夾的js加到專案

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170317/0004.png" alt="0004"/>

- Scripts folder

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170317/0005.png" alt="0005"/>

## Example 1 Without Redux

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
    <script src="~/Scripts/require.js"></script>
    <script type="text/javascript">
        requirejs.config({
            baseUrl: '/Scripts',
            paths: {
                react: 'react/react',
                'react-dom': 'react/react-dom',
                redux: 'redux/redux',
                'components/switch-select': 'home/components/switch-select'
            }
        })

        // Load the main app module to start the app
        requirejs(["/scripts/home/app.js"]);
    </script>
    <h1>Typescript Demo</h1>
    <div id="content"></div>
</body>
</html>
```

- switch-select.tsx

```
import * as React from 'react';

export default class SwitchSelect extends React.Component<any, any>{
    isDefault: boolean = false;

    constructor(props) {
        super(props);
        this.state = this.getDefault();
    }

    getDefault() {
        return {
            opts: [
                { value: 0, label: 'iphone' },
                { value: 1, label: 'android' },
            ]
        };
    }

    swdata(isDefault: boolean) {
        if (isDefault) {
            this.setState({
                opts: [
                    { value: 3, label: 'Leo' },
                    { value: 4, label: 'Lee' },
                ]
            })
        } else {
            this.setState(this.getDefault());
        }
        this.isDefault = isDefault;
    }

    render() {
        var items = this.state.opts || [];
        return <div>
            <select>
                {
                    items.map((item) => {
                        return <option key={'o-' + item.value} value={item.value}>{item.label}</option>
                    })
                }
            </select>
            <button type="button" onClick={e => this.swdata(!this.isDefault) } >switch</button>
        </div>
    }
}
``` 

- app.tsx

```
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import SwitchSelect from 'components/switch-select';

ReactDOM.render(
    <SwitchSelect />,
    document.getElementById('content')
);
```

## Example 2 Redux

- switch-select-store.tsx

```
import {createStore} from 'redux';//, combineReducers, applyMiddleware

export enum SwitchType {
    one = 1,
    two = 2
}

export const SwitchSelectStore = createStore(
    (state, action) => {
        switch (action.type) {
            case SwitchType.one:
                return {
                    opts: [
                        { value: 0, label: 'iphone' },
                        { value: 1, label: 'android' },
                    ]
                }
            case SwitchType.two:
                return {
                    opts: [
                        { value: 3, label: 'Leo' },
                        { value: 4, label: 'Lee' },
                    ]
                }
            default:
                return state;
        }
    }, { opts: [] });
```

- switch-select.tsx

```
import * as React from 'react';
import {SwitchSelectStore, SwitchType} from 'stores/switch-select-store';

export default class SwitchSelect extends React.Component<any, any>{
    isDefault: boolean = false;

    componentDidMount() {
        SwitchSelectStore.subscribe(() => this.forceUpdate());
        this.swdata(this.isDefault);
    }

    swdata(isDefault: boolean) {
        if (isDefault) {
            SwitchSelectStore.dispatch({ type: SwitchType.one })
        } else {
            SwitchSelectStore.dispatch({ type: SwitchType.two })
        }
        this.isDefault = isDefault;
    }

    render() {
        var items = SwitchSelectStore.getState().opts || [];
        return <div>
            <select>
                {
                    items.map((item) => {
                        return <option key={'o-' + item.value} value={item.value}>{item.label}</option>
                    })
                }
            </select>
            <button type="button" onClick={e => this.swdata(!this.isDefault) } >switch</button>
        </div>
    }
}
```

- app.tsx

```
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import SwitchSelect from 'components/switch-select';

ReactDOM.render(
    <SwitchSelect />,
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
    <script src="~/Scripts/require.js"></script>
    <script type="text/javascript">
        requirejs.config({
            baseUrl: '/Scripts',
            paths: {
                react: 'react/react',
                'react-dom': 'react/react-dom',
                redux: 'redux/redux',
                'components/switch-select': 'home/components/switch-select',
                'stores/switch-select-store': 'home/stores/switch-select-store'
            }
        })

        // Load the main app module to start the app
        requirejs(["/scripts/home/app.js"]);
    </script>
    <h1>Typescript Demo</h1>
    <div id="content"></div>
</body>
</html>
```

## Example 3 react-redux

- app.tsx

```
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import {Provider} from 'react-redux';
import SwitchSelect from 'components/switch-select';
import {SwitchSelectStore} from 'stores/switch-select-store';

ReactDOM.render(
    <Provider store={SwitchSelectStore}>
        <SwitchSelect />
    </Provider>,
    document.getElementById('content')
);
```

- switch-select.tsx

```
import * as React from 'react';
import {connect} from 'react-redux';

class SwitchSelect extends React.Component<any, any>{
    isDefault: boolean = false;

    constructor(props) {
        super(props);
    }

    componentDidMount() {
        this.swdata(this.isDefault);
    }

    swdata(isDefault: boolean) {
        if (isDefault) {
            this.props.getDefault();
        } else {
            this.props.getData();
        }
        this.isDefault = isDefault;
    }

    render() {
        var items = this.props.opts || [];
        return <div>
            <select>
                {
                    items.map((item) => {
                        return <option key={'o-' + item.value} value={item.value}>{item.label}</option>
                    })
                }
            </select>
            <button type="button" onClick={e => this.swdata(!this.isDefault) } >switch</button>
        </div>
    }
}

const mapStateToProps = (state) => state;

const mapDispatchToProps = (dispatch) => ({
    getData: () => {
        dispatch({ type: 1 });
    },
    getDefault: () => {
        dispatch({ type: 2 });
    }
});

export default connect(mapStateToProps, mapDispatchToProps)(SwitchSelect);
```

- switch-select-store.tsx

```
import {createStore} from 'redux';//, combineReducers, applyMiddleware

export const SwitchSelectStore = createStore(
    (state, action) => {
        switch (action.type) {
            case 1:
                return {
                    opts: [
                        { value: 0, label: 'iphone' },
                        { value: 1, label: 'android' },
                    ]
                }
            case 2:
                return {
                    opts: [
                        { value: 3, label: 'Leo' },
                        { value: 4, label: 'Lee' },
                    ]
                }
            default:
                return state;
        }
    }, { opts: [] });
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
    <script src="~/Scripts/require.js"></script>
    <script type="text/javascript">
        requirejs.config({
            baseUrl: '/Scripts',
            paths: {
                react: 'react/react',
                'react-dom': 'react/react-dom',
                redux: 'redux/redux',
                'react-redux': 'redux/react-redux',
                'components/switch-select': 'home/components/switch-select',
                'stores/switch-select-store': 'home/stores/switch-select-store'
            }
        })

        // Load the main app module to start the app
        requirejs(["/scripts/home/app.js"]);
    </script>
    <h1>Typescript Demo</h1>
    <div id="content"></div>
</body>
</html>
```

- Result
    
    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170317/0006.gif" alt="0006"/>

## 參考資料
- [使用Typescript編寫Redux+Reactjs應用程序](https://my.oschina.net/redhu/blog/648485)