title:  前端学习step
date: 2021-12-31 10:51:12
tags: [编程, 前端]

---

```
目前主流的语言和思想都是相通的，或者说是相互借鉴学习的，web标准也会汲取里面的精
华作为参考加入到标准中，这里来说一下主流的框架学习步骤: 构建，指令，表单，组
件(通讯，生命周期)，路由，状态管理1
```

<!--more-->

## 构建
一般构建有前端引入和后端构建两种方式，前端引入的方式主流的就是jit（java的方法），提倡的是运行时编译，好处是比较灵活，可以充分历用vm的性能。后端构建就是提前代码在后端编译好，一次构建不需要在每次运行时花费额外的时间。两种方式各有优缺点，所以主流语言都采用两种方式相结合。
```
两种方式的名词了解一下：jit和aot
```

#### vue的前端引入
这种方式其实就是前端jit的方式，目前只有学习的时候用一下，主流方式还是后端构建，主流库cdn推荐：unpkg.com
```
<script src="static/js/vue.global.prod.js"></script>
```

#### vue 后端构建
目前vue最新版本是3，所以这里使用vite构建
```
# npm 6.x
$ npm init vite@latest <project-name> --template vue

# npm 7+，需要加上额外的双短横线
$ npm init vite@latest <project-name> -- --template vue

$ cd <project-name>
$ npm install
$ npm run dev
```
 
----

## 开始
目前前端语言的学习都离不开node，这个是构建的基础，webpack这个也要了解一下，构建的工具都是基于它来实现的，想要优化还是要深入了解一下。

#### 目录结构
```
demo
  | node_modules
  | public
  | src
      | main.js
      | App.vue
  | index.html
  | package.json
  | vite.config.js
```
说明：  
1. vite.config.js 构建使用的配置文件   
2. index.html 首页   
3. main.js 入口文件，第三方模块，路由，插件都在这里引入   
4. App.vue 具体的模板组件，其他组件参考着写就可以了         

#### 组件模板
书写vue模板根据IDE自动生成，跟传统的前端一样：html模板，js脚本，css样式三部分。
```
<template>

</template>

<script>
    export default {
    }
</script>

<style scoped>

</style>
```

#### 模板指令
模板中使用最多的就是各种指令，常用指令集
```
v-text
v-html
v-show
v-if
v-else
v-else-if
v-for
v-on
v-bind
v-model
v-pre
v-cloak
v-once
```

#### js脚本
脚本中有数据和处理方法等，还有生命周期钩子函数
```
export default {
    components: { // 使用组件 },
    data(){
        // 定义数据
        return {
            name:"hello"
        }
    },
    methods:{
        // 定义方法
        changeUsername(){
            this.name = 'name' + Math.random()
        }
    }
    created(){
        // 生命周期钩子函数
        console.log("create ....")
    }
}
```

#### css样式
样式中如果加入scoped就代表当前组件的样式，不污染全局
```
<style scoped>

</style>
```

----

## 小结
组件包含很多内容，涉及组件通讯和生命周期管理等内容，篇幅较大不在这里赘述，另外路由的使用和状态管理都属于第三方插件内容，本次也不介绍了。
