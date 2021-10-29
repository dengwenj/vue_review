# vue_review

vue 复习

## ref 属性

1 被用来给元素或子组件注册引用信息（id 的替代者）
2 应用在 html 标签上获取的是真实 dom 元素，应用在组件标签上是组件实例对象（vc）
3 使用方式：

```
打标识：<h1 ref="xxx">...</h1> 或 <School ref="xxx"></School>
获取：this.$refs.xxx
```

## 配置项 props

功能：让组件接收外部传过来的数据
（1）.传递数据：
第一种方式（只接收）：

```
props:['name']
```

第二种方式（限制类型）：

```
props:{
name:String
}
```

第三种方式（限制类型、限制必要性、指定默认值）：

```
props:{
name:{
type:String // 类型
required:true // 必要性
default:'默认值'
}
}
```

注：props 是只读的，Vue 底层会监测你对 props 的修改，若业务需求需要修改，那么复制 props 的内容到 data 中一份，然后去修改 data 中的数据，props 的优先级比 data 高

## mixin(混入)

功能：可以把多个组件公用的配置提取成一个混入对象
使用方式：
第一步定义混合：

```
{
data(){...},
methods:{...}
...
}
```

第二步使用混入，
（1）全局混入：Vue.mixin(xxx)
(2)局部混入:mixins:[xxx] (配置项)

## 浏览器本地存储

1 SessionStorage 存储的内容会随着浏览器窗口关闭而消失
2 LocalStorage 存储的内容，需要手动清除才会消失

## 组件自定义事件

1 一种组件间通信的方式，适用于：子组件===>父组件
2 使用场景：A 是父组件，B 是组件件，B 想给 A 传数据，那么就要在 A 中给 B 绑定自定义事件（事件的回调在 A 中）

3 绑定自定义事件：

```
(1)第一种方式，在父组件中：<Demo @dwj="test"/>
methods:{test(数据){}}（父组件里面）

(2)第二种方式，在父组件中：<Demo ref="demo">
mounted(){this.$refs.demo.$on('dwj',(数据)=>{})} （父组件里面）
```

(3)想要只触发一次 once 修饰符，$once 方法

4 触发自定义事件：this.$emit('dwj',数据)（在子组件里面）
5 解绑自定义事件：this.$off('dwj')
6 组件上也可以绑定原生 DOM 事件，需要使用 native 修饰符

## 全局事件总线

1 一种组件间通信的方式，适用于任意组件间通信
2 安装全局事件总线：

```
new Vue({
...
beforeCreate(){
Vue.prototype.$bus = this // 安装全局事件总线，$bus 就是当前应用的 vm
}
})
```

3 使用事件总线：
(1)接收数据：A 组件想接收数据，则在 A 组件中给 $bus 绑定自定义事件，事件的回调留在 A 组件自身

```
mounted(){
  this.$bus.$on('xxx',()=>{})
}
```

(2)提供数据：this.$bus.$emit('xxx',数据)

4 最好在 beforeDestroy 钩子中，用 $off 去解绑当前组件所用到的事件

## $nextTick

1 语法：this.$nextTick(回调函数)
2 作用：在下一次 DOM 更新结束后执行其指定的回调
3 什么时候用：当改变数据后，要基于更新后的新 DOM 进行某些操作时，要在 nextTick 所指定的回调函数中执行

## 插槽

1 作用：让父组件可以向子组件指定位置插入 html 结构，也是一种组件间通信的方式，适合于 父组件==>子组件
2 分类：默认插槽、具名插槽、作用域插槽
作用插槽：数据在组件的自身，但根据数据生成的结构需要组件的使用者来决定

```
<slot :dwj="dwj"></slot>(这个数据就传到父组件中的子组件去了)
<Person>
  <template solt-scope="fe">
    <h4 v-for="item in fe.dwj" :key="item">{{item}}</h4>
  </template>
</Person>
```
