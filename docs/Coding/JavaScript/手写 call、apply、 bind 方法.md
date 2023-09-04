#js #手写 #calll #bind #apply

## call

```js
Function.prototype.myCall = function (context, ...args) {
  context = (context ?? window) || new Object(context);
  const key = Symbol();
  context[key] = this;
  const result = context[key](...args);
  delete context[key];
  return result;
};

```

## apply

```js
Function.prototype.myApply = function (context, args) {
  context = (context ?? window) || new Object(context);
  const key = Symbol();
  context[key] = this;
  const result = context[key](...args);
  delete context[key];
  return result;
};

```

## bind

```js
Function.prototype.myBind = function (context, ...args) {
  const fn = this;
  const bindFn = function (...newFnArgs) {
    return fn.call(this instanceof bindFn ? this : context, ...args, ...newFnArgs);
  };
  bindFn.prototype = Object.create(fn.prototype);
  return bindFn;
};

```