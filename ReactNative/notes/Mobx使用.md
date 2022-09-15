**安装**

```yacas
 yarn add mobx mobx-react @babel/plugin-proposal-decorators
```

**配置**

在项目的babel.config.js中添加如下配置

```yacas
 plugins: [
    ['@babel/plugin-proposal-decorators', { 'legacy': true }]
  ]
```

