#vue 

当我们在Vue.js中定义组件时，`data`属性用于存储组件的数据。通常情况下，`data`属性的值是一个对象，其中每个属性都是一个数据项。例如：

```js
data() {
  return {
    message: 'Hello World',
    count: 0
  }
}
```

这个`data`属性返回了一个包含`message`和`count`两个属性的对象。

但是有些情况下，我们需要动态计算数据。在这种情况下，`data`属性的值就应该是一个方法，该方法返回一个包含数据项的对象。例如：

```js
data() {
  return {
    message: this.getMessage(),
    count: 0
  }
},
methods: {
  getMessage() {
    return 'Hello World'
  }
}
```

在这个例子中，`data`属性的值是一个方法，它返回了一个包含`message`和`count`两个属性的对象。其中，`message`属性的值是通过调用组件中的`getMessage`方法动态计算得到的。

使用方法返回`data`属性可以让我们在组件每次使用时都获得一个新的数据对象，避免了多个组件实例共享同一个数据对象的问题。