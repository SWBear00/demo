# vue.js实战资料

## 一、vue基础

### 1.基本指令

Mustances：{{变量}} 之恩能够存在单行语句

v-once：只能渲染一次

v-html：解析HTML结构

v-bind：解析属性中的对象指令，简写为：“：”

v-if：条件渲染，如果为true，则显示标签内的内容，v-else/v-if-else:与v-if一起使用。

v-show：条件渲染，为true时显示

v-if、v-show的区别v-if是惰性渲染，只有条件为true是才会显示，v-show无论条件是否为true都会渲染，所以在频繁变化时可以使用v-if，不频繁变化时使用v-show。

v-for：列表渲染

语法：v-for=“（value,key,index）in obj” ：key=“index”

### 2.事件处理

使用`v-on` 指令监听 DOM 事件，并在触发时运行一些 JavaScript 代码。简写为：“@”

1.事件改变data数据，data数据改变会引起师徒的变化

2.事件传递参数：$event

3.数组更新检测

返回一个元数组还是一个新数组。

变异方法：

改变元数组，则可以引起视图更新

不改变原数组，创建新数组，则无法引起视图更新

#数组变更

- `push()`
- `pop()`
- `shift()`
- `unshift()`
- `splice()`
- `sort()`
- `reverse()`

#替换数组

`filter()`、`concat()` 和 `slice()`。它们不会变更原始数组，而**总是返回一个新数组**。

### 3.计算属性

使用computed:{}与data同级，如果数据没有改变，则不会重新计算

#计算属性vs方法

我们可以将同一函数定义为一个方法而不是一个计算属性。两种方式的最终结果确实是完全相同的。然而，不同的是**计算属性是基于它们的响应式依赖进行缓存的**。只在相关响应式依赖发生改变时它们才会重新求值。这就意味着只要 `message` 还没有发生改变，多次访问 `reversedMessage` 计算属性会立即返回之前的计算结果，而不必再次执行函数。

### 4.Class与Style绑定

#对象语法

```vue
<div
  class="static"
  v-bind:class="{ active: isActive, 'text-danger': hasError }"
></div>

data: {
  isActive: true,
  hasError: false
}
<--渲染结果-->
    <div class="static active"></div>
```

当isActive为true时 显示Class中的标签，如果为false则不显示，和原先的Class可以同时显示

#数组语法

```vue
<div v-bind:class="[activeClass, errorClass]"></div>

data: {
  activeClass: 'active',
  errorClass: 'text-danger'
}
<--渲染结果-->
    <div class="active text-danger"></div>
    
```

如果你也想根据条件切换列表中的 class，可以用三元表达式：

```vue
<div v-bind:class="[isActive ? activeClass : '', errorClass]"></div>
```

这样写将始终添加 `errorClass`，但是只有在 `isActive` 是 truthy[[1\]](https://cn.vuejs.org/v2/guide/class-and-style.html#footnote-1) 时才添加 `activeClass`。

不过，当有多个条件 class 时这样写有些繁琐。所以在数组语法中也可以使用对象语法：

```vue
<div v-bind:class="[{ active: isActive }, errorClass]"></div>
```

注意：对象中只能接受字符串，数组中可以接受对象

 

