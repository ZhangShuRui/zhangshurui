#原型链 #js

## 原型链继承

### 代码例子

```js
// 父类: 公共属性和方法
function Person() {
  this.name = "why"
}

Person.prototype.eating = function() {
  console.log(this.name + " eating~")
}

// 子类: 特有属性和方法
function Student() {
  this.sno = 111
}
/********** 核心代码 **************/
var p = new Person()
Student.prototype = p
/********************************/
Student.prototype.studying = function() {
  console.log(this.name + " studying~")
}
```

### 原型链图

默认两个对象的原型链

![[00 Attachment/Pasted image 20230817112705.png]]

核心代码，这段代码放的位置不能随便放，不然会放错对象，导致数据错误

```js

var p = new Person()
Student.prototype = p

```

然后原型链变成下面的样子

![[00 Attachment/Pasted image 20230817113415.png]]

### 存在弊端

#### 打印 stu 对象, 继承的属性是看不到的

![[00 Attachment/Pasted image 20230817113923.png]]

#### 创建出来两个stu的对象，**获取引用**，修改stu1引用中的值, 会相互影响

```js
// 父类: 公共属性和方法
function Person() {
  this.name = "why"
  this.friends = []   // 父类添加一个引用类型数据
}

var stu1 = new Student()
var stu2 = new Student()

// 直接修改对象上的属性, 是给本对象添加了一个新属性
stu1.name = "kobe"
console.log(stu2.name)

// 获取引用, 修改引用中的值, 会相互影响
stu1.friends.push("kobe")

console.log(stu1.friends)
console.log(stu2.friends)

```

![[00 Attachment/Pasted image 20230817133231.png]]

在父类中添加 `friends` 属性，然后在子类的实例 `stu1` 中添加数据 `kobe` ，发现在 `stu2` 的实例中也能访问到。

**注意：** 但是如果是直接给当前实例对象赋值，那么就不会有问题

![[00 Attachment/Pasted image 20230817134016.png]]

如上图， `name` 属性会直接添加在  `stu1` 身上，那么就不会有影响。

#### 在前面实现类的过程中都没有传递参数

```js
var stu3 = new Student("lilei", 112)
```

## 借用构造函数继承

解决了[[03 Coding/JavaScript/js 实现继承的方式#原型链继承|原型链继承]]的3个弊端
### 代码例子

```js
// 父类: 公共属性和方法
function Person() {
  this.name = name
  this.friends = []
}

Person.prototype.eating = function() {
  console.log(this.name + " eating~")
}

// 子类
function Student() {
  this.sno = 111
}

var p = new Person()
Student.prototype = p

Student.prototype.studying = function() {
  console.log(this.name + " studying~")
}
```

改造后的实现

```js
// 父类: 公共属性和方法
function Person(name, age, friends) {
  // 这里 this 是 stu
  this.name = name;
  this.age = age;
  this.friends = friends;
}

Person.prototype.eating = function () {
  console.log(this.name + " eating~");
};

// 子类: 特有属性和方法
function Student(name, age, friends, sno) {
  /********* 核心语句 **************/
  Person.call(this, name, age, friends);
  /********************************/
  this.sno = 111;
}

var p = new Person();
Student.prototype = p;

Student.prototype.studying = function () {
  console.log(this.name + " studying~");
};

```

在子类 `Student`  的构造函数中，先执行 `Person.call(this,...args)` 方法，把子类的实例 `this` 传递到父类的构造函数中去初始化，那么在父类中初始化的字段就是绑定在子类的实例对象上了。

### 原型链图

![[00 Attachment/Pasted image 20230817140051.png]]

### 存在弊端

#### Person() 至少被执行了2遍

#### p对象存在多出来但是没有必要存在的属性

![[00 Attachment/Pasted image 20230817140703.png]]

## 组合继承

为了解决借用构造函数实现继承的问题，我们第一反应就是：直接把父类的原型赋值给子类，作为子类的原型，代码实现如下：

```js

// 父类: 公共属性和方法
function Person(name, age, friends) {
  this.name = name
  this.age = age
  this.friends = friends
}

Person.prototype.eating = function() {
  console.log(this.name + " eating~")
}

// 子类: 特有属性和方法
function Student(name, age, friends, sno) {
  Person.call(this, name, age, friends)
  this.sno = 111
}

// 直接将父类的原型赋值给子类, 作为子类的原型
Student.prototype = Person.prototype

Student.prototype.studying = function() {
  console.log(this.name + " studying~")
}

var stu = new Student("why", 18, ["kobe"], 111)
console.log(stu)
stu.eating()

```

从原型链图上看如下：

![[00 Attachment/Pasted image 20230817142836.png]]

举个例子：如果我们在 `Student.prototype` 中添加自己的方法，由于子类的原型对象现在已经指向了 `Person.prototype` 了，这样子类自己独有的方法会被添加到父类中，导致所有继承父类的子类都可以访问到这个方法，这显然是不对的。

#### 代码例子

```js

function Parent() {
    console.log('call Parent');
    this.name = 'parent';
    this.arr = [1, 2, 3];
}

Parent.prototype.getName = function() {
    return this.name;
}


function Child() {
    Parent.call(this); //* 1
}

Child.prototype = new Parent(); //* 2
const child1 = new Child();
const child2 = new Child();
child1.arr.push(999);
console.log('child1', child1);
console.log('child2', child2);

```

### 原型链图

![[00 Attachment/Pasted image 20230817152854.png]]

## 寄生组合式继承

### 实现属性继承

```js

function Person(name, age, friends) {
  this.name = name
  this.age = age
  this.friends = friends
}

Person.prototype.running = function() {
  console.log("running~")
}

Person.prototype.eating = function() {
  console.log("eating~")
}


function Student(name, age, friends, sno, score) {
  Person.call(this, name, age, friends)
  this.sno = sno
  this.score = score
}

Student.prototype.studying = function() {
  console.log("studying~")
}
```

### 实现方法的继承

最简单的方法

```js

function Person(name, age, friends) {
  this.name = name
  this.age = age
  this.friends = friends
}

Person.prototype.running = function() {
  console.log("running~")
}

Person.prototype.eating = function() {
  console.log("eating~")
}


function Student(name, age, friends, sno, score) {
  Person.call(this, name, age, friends)
  this.sno = sno
  this.score = score
}

/************************/

Student.prototype = Object.create(Person.prototype)

/************************/

Student.prototype.studying = function() {
  console.log("studying~")
}
```

一些小问题：

![[00 Attachment/Pasted image 20230817155220.png]]

当我们打印 new 出来的 Student 对象的时候，发现打印的是 Person 对象，这是怎么回事呢？

当执行 console.log 的时候，会调用对象原型上的 `constructor` (即方法对象) 的 `name` 属性，当时当我们执行 `Object.create()` 方法返回的对象中是没有 `constructor` 属性的，所以会沿着作用域找到 `Person` 的`constructor`。

下面是示意图

![[00 Attachment/Pasted image 20230817160444.png]]

解决方法

把缺少的 `constructor` 字段补上，并且指向子类构造函数

```js
  Object.defineProperty(Student.prototype, "constructor", {
    enumerable: false,
    configurable: true,
    writable: true,
    value: Student
  })

```

再优化一下，把继承和创建constructor 的代码封装起来形成工具函数，方便代码复用

```js

/**********核心代码 工具方法***********/
function inheritPrototype(SubType, SuperType) {
  SubType.prototype = Objec.create(SuperType.prototype)
  Object.defineProperty(SubType.prototype, "constructor", {
    enumerable: false,
    configurable: true,
    writable: true,
    value: SubType
  })
}
/*********************/
function Person(name, age, friends) {
  this.name = name
  this.age = age
  this.friends = friends
}

Person.prototype.running = function() {
  console.log("running~")
}

Person.prototype.eating = function() {
  console.log("eating~")
}


function Student(name, age, friends, sno, score) {
  Person.call(this, name, age, friends)
  this.sno = sno
  this.score = score
}

inheritPrototype(Student, Person)

Student.prototype.studying = function() {
  console.log("studying~")
}

var stu = new Student("why", 18, ["kobe"], 111, 100)
console.log(stu)
stu.studying()
stu.running()
stu.eating()

console.log(stu.constructor.name)


```