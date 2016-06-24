---
title: react-route
date: 2016-06-17 11:04:35
categories:
- react
tags:
- react
- react-route
---

## react-route使用

redux 单一数据源原则对于多页面应用有点找不着北的感觉，所以配合react-route使用可以完美解决该问题。

用redux首先保证单一数据源
{% codeblock lang:js %}
import React from 'react';
import ReactDOM from 'react-dom';
import route from './containers/route' //react-route文件夹
import { Provider } from 'react-redux'
import configureStore from './configureStore'
injectTapEventPlugin();
const store = configureStore();
const App = () => (
    <Provider store={store}>
        {route}
    </Provider>
);

ReactDOM.render(
    <App />,
    document.getElementById('app')
);
{% endcodeblock %}

react-route 运用
假设程序拥有
-App主体负责navbar&footer
-Home主页负责welcome信息
-Detail负责详细信息

{% codeblock lang:js %}
import React from 'react';
/*react-route*/
import { Router, Route, IndexRoute , hashHistory } from 'react-router';

import App from './App';
import Home from './Home';
import Detail from './Detail';

const route = (
    <Router history={hashHistory}>
        <Route path="/" component={App}>
            <IndexRoute component={Home} />
            <Route path="detail" component={Detail} />
        </Route>
    </Router>
);
export default route;
{% endcodeblock %}

这样路由和所需组件就绑定了，并且也能遵守redux单一数据源原则。

项目完整代码 ：{%link github https://github.com/timmyLan/amwares-manage %}