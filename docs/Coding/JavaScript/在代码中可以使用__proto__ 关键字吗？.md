#原型链 #js 

在ECMAScript 5中，`__proto__`是非标准但被广泛使用的属性，它可以用来访问对象的原型。但是在ECMAScript 6中，`__proto__`已经被正式标准化为内置属性，用来访问对象的原型，并且推荐使用`Object.getPrototypeOf()`和`Object.setPrototypeOf()`来替代。

虽然`__proto__`在一些旧的JavaScript引擎中仍然可以使用，但是为了保证代码的可移植性和兼容性，不建议在代码中使用`__proto__`关键字。建议使用标准化的`Object.getPrototypeOf()`和`Object.setPrototypeOf()`方法来操作对象原型。