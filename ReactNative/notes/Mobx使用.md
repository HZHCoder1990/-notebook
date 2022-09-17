**安装**

```yacas
 yarn add mobx@5.15.4 mobx-react@6.2.2 @babel/plugin-proposal-decorators@7.10.1
```

**配置**

在项目的babel.config.js中添加如下配置

```yacas
 plugins: [
    ['@babel/plugin-proposal-decorators', { 'legacy': true }]
  ]
```

