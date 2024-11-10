# 第13章

`Vue.js`: 基础与应用

`Vue.js`是一个用于构建用户界面的渐进式框架。它因简单性、灵活性和易于集成而闻名。让我们探索`Vue.js`的基础知识，理解响应式组件和属性，学习指令和生命周期方法。这些知识将是创建现代高效应用程序的基础。

`Vue.js Fundamentals`

`Vue.js`由`Evan You`创建，并于2014年发布。它的设计是可扩展的，意味着您可以用它为现有页面添加交互性，或构建完整的单页面应用（SPA）。`Vue`因其平滑的学习曲线和清晰的文档而尤其受欢迎。

为什么使用`Vue.js`？

- 简单性：`Vue`易于学习和使用。它的语法直观明了，使得初学者和有经验的开发者都能轻松上手。

- 响应性：`Vue`提供了一种响应式系统，促进应用逻辑与用户界面之间的数据同步。

- 灵活性：您可以将`Vue`用于小型简单项目或大型复杂应用。它具有高度的模块化，可以根据需要进行扩展。

- 社区和生态系统：`Vue`拥有一个活跃的社区和不断增长的生态系统，许多库和工具可辅助开发。

响应式组件和属性

组件是`Vue.js`应用的基础。它们允许您将用户界面划分为更小的可重用部分，每个部分管理自己的状态和逻辑。

创建基本组件

`Vue`组件可以在`.vue`文件中定义或直接在脚本中定义。

```jsview

<template>

<div>

<h1>{{ message }}</h1>

</div>

</template>

<script>

export default {

data() {

return {

message: 'Hello, Vue!'

};

}

};

</script>

<style>

h1 {

color: green;

}

</style>

```

在上述示例中，我们有一个显示消息的组件。`data`对象返回组件的本地状态，消息在模板中使用`{{ message }}`插值显示。

属性（props）

属性用于将数据从父组件传递到子组件。它们在子组件中声明，并作为参数接收。

```jsview

<template>

<div>

<h2>{{ title }}</h2>

</div>

</template>

<script>

export default {

props: ['title']

};

</script>

```

在上述示例中，`title`是可以传递给子组件的一个属性。在父组件中，您可以使用子组件并传递该属性：

```jsview

<template>

<div>

<Child title="Child Component Title" />

</div>

</template>

<script>

import Filho from './Filho.vue';

export default {

components: {

Son

}

};

</script>

```

响应性

响应性是`Vue`的一个关键特性。当组件的数据发生变化时，用户界面会自动更新以反映这些变化。

```jsview

<template>

<div>

<h1>{{ counter }}</h1>

<button @click="incrementar">Incrementar</button>

</div>

</template>

<script>

export default {

data() {

return {

counter: 0

};

},

methods: {

increase() {

this.contador++;

}

}

};

</script>

```

在这个示例中，`counter`的值在用户界面中显示，并在按钮点击时自动更新，这要归功于`Vue`的响应式系统。

生命周期政策和方法

指令

指令是模板中的特殊属性，提供对DOM的指令。最常见的指令包括`v-bind`、`v-model`、`v-if`、`v-for`和`v-on`。

- `v-bind`：将属性或属性绑定到JavaScript表达式。

```jsview

<img v-bind:src="imagemUrl" />

```

- `v-model`：创建表单元素与数据之间的双向链接。

```jsview

<input v-model="nome" />

```

- `v-if`：条件渲染一个块。

```jsview

<p v-if="show">This text is conditional</p>

```

- `v-for`：使用循环渲染项目列表。

```jsview

<ul>

<li v-for="item in itens":key="item.id">{{item.name}}</li>

</ul>

```

- `v-on`：将事件链接到方法。

```jsview

<button v-on:click="dizerOi">Dizer oi</button>

```

生命周期方法

生命周期方法允许您在组件生命周期的特定步骤运行代码。一些最重要的生命周期方法包括：

- `created`：在组件实例创建后调用。

- `mounted`：在组件插入到`DOM`后调用。

- `updated`：在响应式更新后调用。

- `destroyed`：在组件被销毁后调用。

使用生命周期方法的示例：

```jsview

<script>

export default {

data() {

return {

message: 'Component created'

};

},

created() {

console.log('Component created');

},

mounted() {

console.log('Component mounted');

},

updated() {

console.log('Component updated');

},

destroyed() {

console.log('Component destroyed');

}

};

</script>

```

我们探索了`Vue.js`的基础，理解了组件的创建与使用、响应式属性、指令和生命周期方法。`Vue.js`提供了一种简单而强大的用户界面开发方法，使您能够构建动态和高效的Web应用程序。继续练习并应用这些概念，以掌握`Vue.js`并创建现代、响应式的应用程序。

# 第14章

JavaScript中的测试

测试您的代码是一种基本实践，以确保其正常工作并保持质量。测试有助于及早发现错误，促进维护，并提高应用程序的可靠性。让我们探索测试的重要性，了解一些流行的测试工具，如`Jest`、`Mocha`和`Chai`，并理解不同类型的测试：单元测试、集成测试和端到端测试。

测试的重要性

测试您的代码是出于多个原因至关重要：

- 错误检测：测试有助于在代码中找到错误，避免它们在生产环境中成为问题。

- 可维护性：测试通过确保更改不会引入新错误，使代码重构变得更容易。

- 可靠性：测试提供了一个可靠的基础，以信任代码按预期工作。

- 文档：测试作为一种活文档，展示了代码在不同情况下应如何表现。

测试工具

有几种工具可用于测试JavaScript应用程序。让我们关注三种最流行的工具：`Jest`、`Mocha`和`Chai`。

是

`Jest`是一个由`Facebook`开发的测试框架，旨在与`React`应用程序一起使用，但也可以用于测试任何JavaScript代码。它配备了编写测试所需的一切，包括测试运行器、断言框架以及对模拟和间谍的支持。

使用`Jest`的基本测试示例：

```jsjavascript

const somar = (a, b) => a + b;

test('sum 1 + 2 equals 3', () => {

expect(summar(1, 2)).toBe(3);

});

```

在此示例中，我们正在测试`add`函数，以确保`1 + 2`的结果为`3`。

`Mocha`

`Mocha`是一个灵活且可扩展的测试框架，可以在`Node.js`和浏览器中运行。它因其简单性和允许您使用自己选择的断言库（如`Chai`）而脱颖而出。

使用`Mocha`和`Chai`的基本测试示例：

```jsjavascript

const { expect } = require('chai');

const somar = (a, b) => a + b;

describe('Sum function', () => {

it('must add 1 + 2 and result in 3', () => {

expect(somar(1, 2)).to.equal(3);

});

});

```

在这里，我们使用`Mocha`定义测试结构，使用`Chai`进行断言。

`Chai`

`Chai`是一个可以与多种测试框架（如`Mocha`）一起使用的断言库。它提供了一个表达性和可读性的接口，用于编写断言。

使用`Chai`的示例：

```jsjavascript

const { expect } = require('chai');

describe('Basic assertions with Chai', () => {

it('must check for equality of values', () => {

expect(2 + 2).to.equal(4);

});

it('should check if a value is true', () => {

expect(true).to.be.true;

});

});

```

测试类型

有不同类型的测试，每种测试都有特定的目的。让我们探索单元测试、集成测试和端到端测试。

单元测试

`Unit tests check isolated parts of code, such as functions or methods, ensuring that they work correctly. They are quick to execute and provide immediate feedback on tested functionality.`

`Example of a unit test with Jest:`  

```jsjavascript

const multiply = (a, b) => a * b;

test('multiplies 2 * 3 is equal to 6', () => {

expect(multiply(2, 3)).toBe(6);

});

```

`Integration Tests`

`Integration tests verify the interaction between different parts of the system, ensuring that the components work correctly together. They are more complex and can take longer to perform, but they are essential to ensuring that the parts of the system are integrated correctly.`  

`Example of an integration test with Mocha and Chai:`  

```jsjavascript

const { expect } = require('chai');

const { add, multiply } = require('./math');

describe('Integration tests', () => {

it('must add and multiply correctly', () => {

const result = add(multiply(2, 3), 4);

expect(result).to.equal(10);

});

});

```

`Testes end-to-end`  

`端到端（E2E）测试模拟用户行为，并验证整个系统是否正常工作。它们在一个尽可能接近生产环境的环境中运行，测试完整的应用程序使用流程。`

`流行的端到端测试工具包括Cypress和Selenium。`

`Cypress的端到端测试基本示例：`

```jsjavascript

describe('Testes end-to-end com Cypress', () => {

it('must load the home page', () => {

cy.visit('http://localhost:3000');

cy.contains('Welcome');

});

it('must allow the user to log in', () => {

cy.get('input[name="username"]').type('meuUsuario');

cy.get('input[name="password"]').type('minhaSenha');

cy.get('button[type="submit"]').click();

cy.contains('Logout');

});

});

```

`测试你的代码是确保JavaScript应用程序质量和可靠性的基本实践。我们理解测试的重要性，探索流行工具如Jest、Mocha和Chai，并了解不同类型的测试：单元测试、集成测试和端到端测试。通过实施全面的测试策略，你可以开发出更强健的应用程序，并保持对代码按预期运行的信心。继续提升你的测试技能，并应用这些概念来创建高质量的软件。`
