# vue3_ts_todolist
    
    本项目是一个vue3+ts的一个todoList项目,相当于一个计事的小项目

## 如何让项目跑起来,首先我们再gitee中找到项目的地址

  1.通过 git clone   https://gitee.com/tan-bangxu/vue3_ts_todolist.git 把项目下载到本地

  2.再次通过npm install 也可以 cnpm install  下载node_modules依赖包

## 小DOM结构解析

    1.本项目为三大部分结构,头部Header,中间列表List,底部区域Footer

    2.中间列表List包含Item组件,

    3.本项目用了typescript(TS) 我们就要先把数据的类型给封装一下,
     再src目录下创建types文件,interface 接口

    4.在App组件里面引入Header组件 和List,Footer组件,同时也要引入Todo数据类型限定

    5.因为vue3是组合式API,所以我们要去setup里面去操作,setup(){}方法里面要返回一个对象return {}

## JS功能部分

        1.先创建一个state数据源 reactive变成响应式的数据,这个用于对象的然后返回出去toRefs(state)
