# VUE
- Vue是一套前端框架，免除原生JavaScript中的DOM操作，简化书写。
- 基于MVVM(Model-View-ViewModel)思想，实现数据的<font color=red>双向绑定</font>，将编程的关注点放在数据上
- 官网：<https://cn.vuejs.org>
- Vue快速入门
  1. 新建HTML页面，引入Vue.js文件
  2. 在JS代码区域，创建Vue核心对象，进行数据绑定
  3. 编写试图
- Vue常用指令
  - 指令：HTML标签上带有v-前缀的特殊属性，不同指令具有不同含义。例如：v-if，v-for...
  - 常用指令
    - v-bind，为HTML标签绑定属性值，如设置href，css样式等。`<a v-bind:hred="url">百度一下</a>`('v-bind'可以省略)
    - v-model，在表单元素上创建双向绑定数据
    - v-on为HTML标签绑定事件。`<input type="button" value="一个按钮" v-on:click="show()">`, `<input type="button" value="一个按钮" @click="show()">` 方法后的括号可以写可以不写，但是如果有传参必须写。
    - v-if、v-else、v-else-if，条件性的渲染某元素，判定为true时渲染，否则不渲染。`<div v-if="count==3">div1</div>`, `<div v-else-if="count==2">div2</div>`, `<div v-else>div3</div>`
    - v-show，根据条件展示某元素，区别在于切换的是display属性的值。`<div v-show="count==3">div4</div>`
    - v-for，列表渲染，遍历容器的元素或者对象的属性。
      - v-for: `<div v-for="addr in addrs"> {{addr}}<br> </div>`
      - 加索引：`<div v-for="(addr,i) in addrs"> {{i+1}} : {{addr}}<br> </div>`
- Vue生命周期
  - 生命周期的八个阶段：没触发一个生命周期事件，会自动执行一个生命周期方法（钩子）
  - |状态|阶段周期|
    |----|----|
    |beforeCreate|创建前|
    |created|创建后|
    |beforeMount|载入前|
    |mounted|挂载完成|
    |beforeUpdate|更新前|
    |updated|更新后|
    |beforeDestroy|销毁前|
    |destroyed|销毁后|
  - mounted：挂载完成，Vue初始化成功，HTML页面渲染成功。
    - 发送异步请求，加载数据。
  - 示例
    ```javascript
    new Vue({
      el:"#app",
      mounted(){
        alert("vue挂载完成，发送异步请求");
      }
    })
    ```
- 案例-品牌列表数据，使用Vue简化品牌列表数据查询和添加功能
