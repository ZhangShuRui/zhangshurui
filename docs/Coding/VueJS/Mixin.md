#vue #mixin

## 概念

Vue.js 中的 Mixin 是一种可复用 Vue 组件选项的方式，它可以让我们将一组组件选项合并为一个新的组件选项。Mixin 的作用类似于 JavaScript 中的混入（mix-in），可以将多个对象合并为一个对象，从而达到代码复用的目的。

使用 Mixin 可以将一些通用的逻辑和代码封装为一个 Mixin 对象，并将其混入到多个组件中。这样可以让我们避免在多个组件中重复编写相同的代码，并且可以使代码更加清晰和易于维护。

下面是一个简单的 Mixin 示例，假设我们需要为多个组件添加一个 `created` 钩子函数，该函数会在组件实例创建时打印一条日志：

```vue
// mixin.js
export default {
  created() {
    console.log('Mixin created hook called.')
  }
}

// MyComponent.vue
<template>
  <div>{{ message }}</div>
</template>

<script>
import mixin from './mixin'

export default {
  mixins: [mixin],
  data() {
    return {
      message: 'Hello World'
    }
  }
}
</script>

```

在这个例子中，我们定义了一个名为 `mixin` 的 Mixin 对象，并在 `MyComponent` 组件中使用 `mixins` 选项将其混入。这样，`MyComponent` 组件就会继承 `mixin` 中的所有选项，包括 `created` 钩子函数。

当 `MyComponent` 组件实例被创建时，`mixin` 中的 `created` 钩子函数会被调用，从而打印出一条日志。这样我们就可以通过 Mixin 来为多个组件添加通用的逻辑和代码，避免了重复编写相同的代码，提高了代码的复用性和可维护性。

## mixin中的 created 函数会和组件中created 函数的冲突吗？

如果一个 Mixin 对象中定义了 `created` 钩子函数，并且该 Mixin 对象被多个组件使用，则在这些组件中都会执行该 `created` 钩子函数。如果组件本身也定义了 `created` 钩子函数，则该组件的 `created` 钩子函数会与 Mixin 中的 `created` 钩子函数合并，形成一个钩子函数队列。

具体来说，当一个组件使用了一个或多个 Mixin 对象时，Vue.js 会将组件的选项和 Mixin 对象的选项进行合并，形成一个新的选项对象。如果多个对象中有相同的属性，则 Vue.js 会进行适当的合并处理。

在钩子函数的合并过程中，如果组件和 Mixin 对象中都定义了同名的钩子函数，则这些钩子函数会形成一个队列，依次被调用。具体来说，组件自身的钩子函数总是会先被调用，然后是 Mixin 中的钩子函数，最后是 Vue.js 内置的钩子函数。

因此，如果一个 Mixin 对象中定义了 `created` 钩子函数，并且该 Mixin 对象被多个组件使用，那么在这些组件中执行 `created` 钩子函数时，会依次执行组件自身的 `created` 钩子函数和 Mixin 中的 `created` 钩子函数，不会发生冲突。