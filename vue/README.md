# Vue

## 要点{#key}
* 尽量使用ES2015，遵循`CommonJs`规范
* 切勿直接操作DOM,所以也应该避免使用jQuery库
* data属性一定要是一个函数并且返回一个json对象
* 无论是公共组件还是页面都应该使用单文件组件`.vue`
* 不要在JS里绑定跟业务相关的事件，业务事件及逻辑，应该在HTML上绑定。在JS里绑定事件应该用于使用了第三方的插件等场景，如果主动绑定了事件，记得在相关生命周期接触绑定以及销毁相关实例，比如在组件内创建了一个百度editor，并加了一个定时器来更新数据，在组件销毁时，应该销毁这个editor实例，并将定时器clear。

```javascript
data(){
    return {a:}
},
mounted(){
    /* 注册ueditor */
    var $this = this;
    var id = this.$route.query.id;
        
    this.ue_editor = UE.getEditor('editor');
    this.ue_editor.addListener( 'contentChange', function( editor ) {
        $this.formData.content = $this.ue_editor.getContent();
        $this.$validator.validate('richtext',$this.formData.content);
    });
    if(id){
        this.editActivity(id);
        this.formData.edit = 1;  
    }
    this.interval = setInterval(function(){
        update($this.formData.conten);
    },1000);
},
beforeRouteLeave(to,from,next){
    /* 销毁百度编辑器 */
    this.ue_editor.destroy();
    this.ue_editor = null;
    clearInterval(this.interval);
    setTimeout(function(){
        next();
    },0)

    
},
```

## 组件{#components}
* 编写一个组件按照`<template>`、`<script>`、`<style>`的顺序编写
* 公共组件就是独立的一块，要将公共组件相关的东西写在一块，有利于重复调用
* 一个独立组件，视组件大小、API多少而定，小的应该在文件头部注释写明参数以及回调；比较大的组件要在组件文件夹内写明组件的README.md,README.md要编写得清晰明了，最好具备开源的基础

## template标签{#template}
* 尽量使用Vue的语法糖，比如可以用:style代替v-bind:style；用@click代替v-on:click
* 使用for列表循环要绑定`:key`，可以优化列表更新
* 简单的数据处理返回应该用过滤器
* 根元素应该根据具体情况给一个class控制样式，例如会员中心根模块首页：`home-index`

## script标签{#script}
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

## style标签{#style}
* 只存放本组件相关的css
* 其余规则参考css规范



