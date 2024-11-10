# 第12章

Angular：基础与应用

Angular是由`Google`开发的一个强大而完整的框架，用于创建健壮且可扩展的Web应用程序。让我们探讨Angular的基础，理解Angular应用程序的结构，并深入了解指令、服务和依赖注入等概念。到最后，您将能够开始使用Angular开发，充分利用其特性。

Angular基础

Angular是一个基于`TypeScript`的前端框架，提供了一种结构化的方法来开发Web应用程序。与专注于创建用户界面的库`React`不同，Angular是一个完整的框架，包含从头到尾构建应用程序所需的一切。

为什么使用Angular？

- TypeScript：Angular是用`TypeScript`编写的，TypeScript是`JavaScript`的超集，增加了可选的静态类型。这有助于在编译时检测错误，并提高代码的可维护性。

- 组件架构：Angular采用基于组件的架构，类似于`React`，允许创建模块化和可重用的用户界面。

- 集成工具：Angular CLI（`命令行界面`）使创建、开发、测试和部署Angular应用程序变得简单。

- 依赖注入：Angular有一个强大的依赖注入系统，使管理依赖关系和分离关注变得容易。

Angular应用程序的结构

Angular应用程序的结构定义明确，遵循模块化组织。让我们了解构成典型Angular项目的主要元素。

模块

Angular模块是一个用`@NgModule`装饰器装饰的类。模块将应用程序组织成紧密相关、可重用的部分。根模块通常称为`AppModule`。

```jstypescript

import { NgModule } from '@angular/core';

import { BrowserModule } from '@angular/platform-browser';

import { AppComponent } from './app.component';

@NgModule({

declarations: [AppComponent],

imports: [BrowserModule],

providers: [],

bootstrap: [AppComponent]

})

export class AppModule {}

```

在这个例子中，`AppModule`是根模块，导入了`BrowserModule`，声明了`AppComponent`，并定义了引导应用程序的入口点。

组件

组件是Angular用户界面的基础。每个组件由一个HTML模板、一个定义逻辑的TypeScript类和一个CSS样式文件组成。

```jstypescript

import { Component } from '@angular/core';

@Component({

selector: 'app-root',

template: `

<div>

<h1>{{ title }}</h1>

</div>

`,

styles: [`

h1 {

color: blue;

}

`]

})

export class AppComponent {

title = 'My First Angular App';

}

```

在上面的示例中，`AppComponent`定义了一个在模板中显示的标题。`app-root`选择器用于将组件嵌入到应用程序中。

指令、服务和依赖注入

指令

指令是可以修改DOM中元素行为的类。Angular中有三种主要类型的指令：

- 属性指令：改变元素的外观或行为。

- 结构指令：通过添加或删除元素来改变DOM的结构。

- 组件：带有关联模板的指令。

`ngIf`结构指令的示例：

```jshtml

<div *ngIf="show">This text is conditional</div>

```

在这个例子中，只有在表达式`show`为真时，文本才会显示。

`服务`

Angular 中的服务是封装了逻辑和数据的类，这些逻辑和数据可以在不同组件之间共享。它们非常适合处理后台操作、数据处理和业务逻辑。

简单服务的示例：

```jstypescript

import { Injectable } from '@angular/core';

@Injectable({

providedIn: 'root'

})

export class DadosService {

getData() {

return ['Given 1', 'Given 2', 'Given 3'];

}

}

```

在上面的示例中，`DataService` 是一个提供获取数据方法的服务。

依赖注入

依赖注入是一种设计模式，类通过外部来源接收其依赖项，而不是自己创建它们。Angular 通过使用像 `@Injectable` 的装饰器和 Angular 的依赖注入系统，使依赖注入变得简单。

组件中依赖注入的示例：

```jstypescript

import { Component, OnInit } from '@angular/core';

import { DadosService } from './dados.service';

@Component({

selector: 'app-root',

template: `

<div>

<ul>

<li *ngFor="let data of data">{{ data }}</li>

</ul>

</div>

`

})

export class AppComponent implements OnInit {

data: string[];

constructor(private dadosService: DadosService) {}

withOnInit() {

this.dados = this.dadosService.obterDados();

}

}

```

在这里，`AppComponent` 将 `DataService` 注入构造函数，并在组件初始化时使用 `obterDados` 方法获取数据。

在这一步，我们探索 Angular 的基本概念，了解 Angular 应用程序的结构，并讨论指令、服务和依赖注入。Angular 是一个强大的工具，可以让你创建健壮且可扩展的 web 应用程序。通过掌握这些概念，你将准备好使用 Angular 开发复杂且结构良好的应用程序。继续练习并应用这些知识，以在这个强大的框架中实现卓越的 web 开发。
