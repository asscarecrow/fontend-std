# Vue
本规范提供了一种统一的编码规范来编写 Vue.js 代码。这使得代码具有如下的特性：

其它开发者或是团队成员更容易阅读和理解。
IDEs 更容易理解代码，从而提供高亮、格式化等辅助功能
更容易使用现有的工具
更容易实现缓存以及代码包的分拆
摘抄于--[Vue.js 组件编码规范](https://github.com/pablohpsilva/vuejs-component-style-guide/blob/master/README-CN.md#目录)
## 要点{#key}
* 尽量使用ES2015，遵循`CommonJs`规范
* 切勿直接操作DOM,所以也应该避免使用jQuery库
* data属性一定要是一个函数并且返回一个json对象
* 无论是公共组件还是页面都应该使用单文件组件`.vue`

```javascript
 data(){
        return {a:}
    }
```

## 组件{#components}
* 编写一个组件按照`<template>`、`<script>`、`<style>`的顺序编写
* 公共组件就是独立的一块，要将公共组件相关的东西写在一块，有利于重复调用
* 一个独立组件，视组件大小、API多少而定，小的应该在文件头部注释写明参数以及回调；比较大的组件要在组件文件夹内写组件的README.md,README.md要编写得清晰明了，最好具备开源的基础

## 模板标签<template>
* 尽量使用Vue的语法糖，比如可以用:style代替v-bind:style；用@click代替v-on:click
* 使用for列表循环要绑定`:key`
* 根元素应该根据具体情况给一个class控制样式，例如会员中心根模块首页：`home-index`

## script标签<template>
* 使用 name 属性。借助于 vue devtools 可以让你更方便的测试。指定 name 选项的另一个好处是便于调试--有名字的组件有更友好的警告信息。
* 对象的属性应该按照以下方法统一排序（考虑了数据之间的关联性与常用性）
* methods 里面的方法使用驼峰命名的动宾短语。
* 变量以及其他没有提及的问题参照js规范处理

```javascript
<script type="text/javascript">
  export default {
    name:'homePage'
    components: {},
    directives:{},
    props: {
      bar: {}, // 按字母顺序
      foo: {},
      fooBar: {}
    },
    data() {},
    computed: {},
    watch: {},
     // 生命周期函数
    beforeCreate() {},
    mounted() {},
    methods: {
        getType(){}
    }
   
  };
</script>
```

## style标签<style>{#style}
* 只存放本组件相关的css
* 其余规则参考css规范



