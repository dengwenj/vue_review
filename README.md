# vue_review

vue 复习

## ref 属性

1 被用来给元素或子组件注册引用信息（id 的替代者）
2 应用在 html 标签上获取的是真实 dom 元素，应用在组件标签上是组件实例对象（vc）
3 使用方式：
打标识：<h1 ref="xxx">...</h1> 或 <School ref="xxx"></School>
获取：this.$refs.xxx

## 配置项 props

功能：让组件接收外部传过来的数据
（1）.传递数据：
第一种方式（只接收）：
props:['name']
第二种方式（限制类型）：
props:{
name:String
}
第三种方式（限制类型、限制必要性、指定默认值）：
props:{
name:{
type:String // 类型
required:true // 必要性
default:'默认值'
}
}
注：props 是只读的，Vue 底层会监测你对 props 的修改，若业务需求需要修改，那么复制 props 的内容到 data 中一份，然后去修改 data 中的数据，props 的优先级比 data 高
