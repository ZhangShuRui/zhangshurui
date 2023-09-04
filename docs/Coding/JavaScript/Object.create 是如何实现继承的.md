#原型链 #js 

在JavaScript中，Object.create方法是一种实现原型继承的方式。它接受一个原型对象作为参数，并创建一个新对象，该对象的原型链指向该原型对象。

具体来说，Object.create方法内部实现了以下步骤：

1.  创建一个空函数（称为中介构造函数）。
2.  将该函数的原型对象设置为传入的原型对象。
3.  返回通过该函数调用构造函数生成的新对象。

例如，以下代码创建了一个名为Person的构造函数，并使用Object.create方法以Person的实例作为原型对象创建了一个新对象tom：

```js

function Person(name) {
  this.name = name;
}

var tom = Object.create(new Person("Tom"));

console.log(tom instanceof Person); // true
console.log(tom.name); // "Tom"

```

在这个例子中，Object.create方法接收一个Person的实例作为原型对象，并使用中介构造函数创建了一个新对象tom。由于tom的原型链指向Person的实例，因此tom实例具有Person的所有属性和方法。

需要注意的是，Object.create方法创建的新对象不会调用传入的构造函数，因此无法在创建时为其设置属性值。如果需要设置属性值，可以使用其他的继承方式，例如通过构造函数创建实例或使用ES6的class语法。