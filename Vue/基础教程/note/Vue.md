# Vue基础教程

## Vue项目搭建

### 安装与启动项目

使用npm安装

```shell
npm install vue
```

推荐使用脚手架命令安装(CLI)

```shell
# 安装vue-cli
# npm安装
npm install -g @vue/cli
# OR
yarn global add @vue/cli

# 创建vue项目(项目名称不能包含驼峰命名和中文)
vue create 项目名称

# cd到项目根目录
# 启动项目
yarn serve 
# OR
npm run serve

# 可以修改package.json文件中启动命令
"scripts": {
  "serve": "vue-cli-service serve", # 可以把 serve 修改为start，则启动命令变为 yarn start
  "build": "vue-cli-service build"
},

# 打包命令
yarn build
```

### 创建组件

如果需要支持语法高亮的话，安装`vetur`的插件即可。

```vue
<!-- 定义Banner.vue组件 -->
<template>
    <!-- 只能有一个根标签 -->
    <div>
        <h2>我是Banner轮播组件</h2>
        <p>我是测试组件</p>
    </div>
</template>

<script>
export default {
    
}
</script>

<style lang="less" scoped>
</style>

<!-- 使用Banner.vue组件 -->
<template>
  <div id="app">
    <!-- 3.使用组件 -->
    <Banner/>
  </div>
</template>

<script>
// 1. 引入组件
import Banner from './components/Banner.vue'
  
export default {
  name: "App",
  components: {
    // 2.注册组件
    Banner
  },
};
</script>
```

### Vue指令



