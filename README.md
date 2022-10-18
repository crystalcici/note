## vue进阶用法
### 特征一: 模板化
#### 插槽
##### 默认插槽
组件外部维护参数以及结构，内部安排位置
##### 具名插槽
以name标识插槽身份，从而在组件内部做到可区分
##### 作用域插槽
外面做结构描述勾勒，内部传递参数
#### 模版数据的二次加工
1. watch、computed => 响应流过于复杂
2. 方案一： 函数（created阶段做一些init操作）独立、管道 / 无法响应式
   方案二：v-html
```
举例
<template>
    // 期望大于99显示赋值否则显示99
    <h1 v-html="money>99 ? money : 99"></h1>
</template>
<script>
export default {
    data() {
        return {
            money: 100
        }
    }
}
</script>
```
   方案三：过滤器
   过滤器特点：不包含上下文，是一个纯函数
```
<template>
    // 期望大于99显示赋值否则显示99
    <h1 >{{ money || moneyFilter }}</h1>
</template>
<script>
export default {
    data() {
        return {
            money: 100,
            filters: {
                moneyFilter(money) {
                    return money > 99 ? money : 99
                }
            }
        }
    }
}
</script>
```
#### jsx 更自由的基于js书写
* 1. v-model 如何实现 =》双向绑定 =》 外部bind:value,内部@input
* 2. 写jsx好处 =》vue的编译路径：template->render->vm.render->vm.render()
d
### 特征二: 组件化
#### 传统模板化
* 1. 抽象复用
* 2. 精简 & 聚合
#### 混入mixin
* 1. 应用：抽离公共逻辑（逻辑相同，模板不同，可用mixiin）
* 2. 缺点：数据来源不明确
* 3. 合并策略
    a.递归合并
    b. data合并冲突，组件优先
    c. 生命周期回调函数不会覆盖，会先后执行，优先级为先mixin后组件
#### 继承拓展extends -逻辑拓展(效果同mixin)

#### vue.use - 插件
* 1. 注册外部插件，作为整体实例的补充
