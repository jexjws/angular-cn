# Introduction to Angular concepts
# Angular 概念简介

Angular is a platform and framework for building single-page client applications using HTML and TypeScript.
Angular is written in TypeScript.
It implements core and optional functionality as a set of TypeScript libraries that you import into your applications.

Angular 是一个用 HTML 和 TypeScript 构建客户端应用的平台与框架。
Angular 本身就是用 TypeScript 写成的。
它将核心功能和可选功能作为一组 TypeScript 库进行实现，你可以把它们导入你的应用中。

The architecture of an Angular application relies on certain fundamental concepts.
The basic building blocks of the Angular framework are Angular components.

Angular应用程序的架构依赖于某些基本概念。
Angular框架的基本构造块是Angular*组件*。

Components define *views*, which are sets of screen elements that Angular can choose among and modify according to your program logic and data

组件定义*视图*。视图是一组可见的屏幕元素，Angular 可以根据你的程序逻辑和数据来选择和修改它们。

Components use *services*, which provide background functionality not directly related to views such as fetching data.
Such services can be *injected* into components as *dependencies*, making your code modular, reusable, and efficient.

组件使用*服务*，它提供与视图无直接关系的后台功能，例如从后端获取数据。
这些服务可以作为*依赖*被*注入*到组件中，使你的代码更加模块化、更加可复用、更加高效。

Components and services are classes marked with *decorators*.
These decorators provide metadata that tells Angular how to use them.

组件和服务是带有*装饰器*的类。
这些装饰器会提供元数据，以告知 Angular 该如何使用它们。

*   The metadata for a component class associates it with a *template* that defines a view.
    A template combines ordinary HTML with Angular *directives* and *binding markup* that allow Angular to modify the HTML before rendering it for display.

	组件类的元数据将组件类和一个用来定义视图的*模板*关联起来。
	模板将普通的 HTML 与 Angular *指令*与*绑定标记（markup）* 结合在一起，这样 Angular 就可以在渲染 HTML 之前先修改这些 HTML。

*   The metadata for a service class provides the information Angular needs to make it available to components through *dependency injection \(DI\)*

	服务类的元数据提供了一些信息，Angular 要用这些信息来让组件可以通过*依赖注入（DI）*使用该服务。

An application's components typically define many views, arranged hierarchically.
Angular provides the `Router` service to help you define navigation paths among views.
The router provides sophisticated in-browser navigational capabilities.

应用的组件通常会定义很多视图，并进行分级组织。
Angular 提供了 `Router` 服务来帮助你定义视图之间的导航路径。
路由器提供了先进的浏览器内导航功能。

<div class="alert is-helpful">

See the [Angular Glossary](guide/glossary) for basic definitions of important Angular terms and usage.

参阅 [Angular 词汇表](guide/glossary) 以了解对 Angular 重要名词和用法的基本定义。

</div>

<div class="alert is-helpful">

For the sample application that this page describes, see the <live-example></live-example>.

要想查看本页所讲的范例程序，参阅<live-example></live-example>。

</div>

## Components

Every Angular application has at least one component, the *root component* that connects a component hierarchy with the page document object model \(DOM\).
Each component defines a class that contains application data and logic, and is associated with an HTML *template* that defines a view to be displayed in a target environment.

每个 Angular 应用程序至少有一个组件，即*根组件*，它会把组件树和页面中的 DOM 连接起来。
每个组件都会定义一个包含应用程序数据和逻辑的类，并与一个 HTML *模板*相关联，该模板定义了一个供目标环境下显示的视图。

The `@Component()` decorator identifies the class immediately below it as a component, and provides the template and related component-specific metadata.

`@Component()` 装饰器表明紧随它的那个类是一个组件，并提供模板和该组件专属的元数据。

<div class="alert is-helpful">

Decorators are functions that modify JavaScript classes.
Angular defines a number of decorators that attach specific kinds of metadata to classes, so that the system knows what those classes mean and how they should work.

装饰器是一些用于修饰 JavaScript 类的函数。Angular 定义了许多装饰器，这些装饰器会把一些特定种类的元数据附加到类上，以便 Angular 了解这些类的含义以及该如何使用它们。

<a href="https://medium.com/google-developers/exploring-es7-decorators-76ecb65fb841#.x5c2ndtx0">Learn more about decorators on the web.</a>

<a href="https://medium.com/google-developers/exploring-es7-decorators-76ecb65fb841#.x5c2ndtx0">到网上学习关于装饰器的更多知识。</a>

</div>

### Templates, directives, and data binding

### 模板、指令和数据绑定

A template combines HTML with Angular markup that can modify HTML elements before they are displayed.
Template *directives* provide program logic, and *binding markup* connects your application data and the DOM.
There are two types of data binding:

模板会把 HTML 和 Angular 的标记（markup）组合起来，这些标记可以在 HTML 元素显示出来之前修改它们。
模板中的*指令*会提供程序逻辑，而*绑定标记*会把你应用中的数据和 DOM 连接在一起。
有两种类型的数据绑定：

| Data bindings    | Details                                                                                                  |
| :--------------- | :------------------------------------------------------------------------------------------------------- |
| 数据绑定         | 详情                                                                                                     |
| Event binding    | Lets your application respond to user input in the target environment by updating your application data. |
| 事件绑定         | 让你的应用可以通过更新应用的数据来响应目标环境下的用户输入。|
| Property binding | Lets you interpolate values that are computed from your application data into the HTML.                  |
| 属性绑定         | 让你将从应用数据中计算出来的值插入到 HTML 中。|


Before a view is displayed, Angular evaluates the directives and resolves the binding syntax in the template to modify the HTML elements and the DOM, according to your program data and logic.
Angular supports *two-way data binding*, meaning that changes in the DOM, such as user choices, are also reflected in your program data.

在视图显示出来之前，Angular 会先根据你的应用数据和逻辑来运行模板中的指令并解析绑定表达式，以修改 HTML 元素和 DOM。
Angular 支持*双向数据绑定*，这意味着 DOM 中发生的变化（比如用户的选择）同样可以反映回你的程序数据中。

Your templates can use *pipes* to improve the user experience by transforming values for display.
For example, use pipes to display dates and currency values that are appropriate for a user's locale.
Angular provides predefined pipes for common transformations, and you can also define your own pipes.

你的模板也可以用*管道*转换要显示的值以增强用户体验。
比如，可以使用管道来显示适合用户所在本地环境的日期和货币格式。
Angular 为一些常见的转换提供了预定义管道，你也可以定义自己的管道。

<div class="alert is-helpful">

For a more detailed discussion of these concepts, see [Introduction to components](guide/architecture-components).

要了解对这些概念的深入讨论，参阅[组件介绍](guide/architecture-components)。

</div>

<a id="dependency-injection"></a>

## Services and dependency injection

## 服务与依赖注入

For data or logic that isn't associated with a specific view, and that you want to share across components, you create a *service* class.
A service class definition is immediately preceded by the `@Injectable()` decorator.
The decorator provides the metadata that allows other providers to be **injected** as dependencies into your class.

对于与特定视图无关、希望跨组件共享的的数据或逻辑，你可以创建*服务*类。
服务类的定义通常紧跟在 `@Injectable()` 装饰器之后。
装饰器提供元数据，可以让你的服务作为依赖被*注入*到你写的类（class）中。

*Dependency injection* \(DI\) lets you keep your component classes lean and efficient.
They don't fetch data from the server, validate user input, or log directly to the console; they delegate such tasks to services.

*依赖注入*（或 DI）使你的组件类保持精简和高效。
有了 DI，组件就不用从服务器获取数据、验证用户输入或直接把日志写到控制台，而是会把这些任务委托给服务。

<div class="alert is-helpful">

For a more detailed discussion, see [Introduction to services and DI](guide/architecture-services).

更深入的讨论，参阅[服务和 DI 简介](guide/architecture-services)。

</div>

### Routing

### 路由

The Angular `Router` package provides a service that lets you define a navigation path among the different application states and view hierarchies in your application.
It is modeled on the familiar browser navigation conventions:

Angular 的 `Router` 包提供了一个服务，让您可以在应用程序中定义不同应用状态和视图层次之间导航时要使用的路径。它的工作模型基于人们熟知的浏览器导航约定：


*   Enter a URL in the address bar and the browser navigates to a corresponding page

	在地址栏输入 URL，浏览器就会导航到相应的页面。

*   Click links on the page and the browser navigates to a new page

	在页面中点击链接，浏览器就会导航到一个新页面。

*   Click the browser's back and forward buttons and the browser navigates backward and forward through the history of pages you've seen

	点击浏览器的前进和后退按钮，浏览器就会在你的浏览历史中向前或向后导航。

The router maps URL-like paths to components instead of pages.
When a user performs an action, such as clicking a link, that would load a new component in the browser, the router intercepts the browser's behavior, and shows or hides that component (and its child components).

路由器将类似URL的路径映射到组件而不是页面。当用户执行一个动作时（比如点击链接），本应该在浏览器中加载一个新页面，但是路由器拦截了浏览器的这个行为，并显示或隐藏该组件（及其子组件）。

If the router determines that the current application state requires a component that hasn't been loaded, the router can *lazy-load* that component and its related dependencies.

如果路由器确定当前的应用程序状态需要加载尚未加载的组件，路由器就会按需*惰性加载*这些要加载的组件。

The router interprets a link URL according to your application's view navigation rules and data state.
You can navigate to new views when the user clicks a button or selects from a drop box, or in response to some other stimulus from any source.
The router logs activity in the browser's history, so the back and forward buttons work as well.

路由器会根据你应用中的导航规则和数据状态来拦截 URL。
当用户点击按钮、选择下拉框或收到其它任何来源的刺激时，你可以导航到一个新视图。
路由器会在浏览器的历史日志中记录这个动作，所以前进和后退按钮也能正常工作。

To define navigation rules, you associate *navigation paths* with your components.
A path uses a URL-like syntax that integrates your program data, in much the same way that template syntax integrates your views with your program data.
You can then apply program logic to choose which views to show or to hide, in response to user input and your own access rules.

要定义导航规则，你就要把*导航路径*和你的组件关联起来。
路径（path）使用类似 URL 的语法来和程序数据整合在一起，就像模板语法会把你的视图和程序数据整合起来一样。
然后你就可以用程序逻辑来决定要显示或隐藏的视图，以响应用户输入和您自己的访问规则。


<div class="alert is-helpful">

For a more detailed discussion, see [Routing and navigation](guide/router).

更深入的讨论，参阅[路由与导航](guide/router)。

</div>

## What's next

You've discovered the main building blocks of an Angular application.
Learn a bit more about them in the following architecture pages.

你已经了解了 Angular 应用程序的主要构造块的基础知识。
在以下页面中了解更多相关信息。

* [Introduction to Components](guide/architecture-components)

  [组件简介](guide/architecture-components)

  * [Templates and views](guide/architecture-components#templates-and-views)

    [模板与视图](guide/architecture-components#templates-and-views)

  * [Component metadata](guide/architecture-components#component-metadata)

    [组件元数据](guide/architecture-components#component-metadata)

  * [Data binding](guide/architecture-components#data-binding)

    [数据绑定](guide/architecture-components#data-binding)

  * [Directives](guide/architecture-components#directives)

    [指令](guide/architecture-components#directives)

  * [Pipes](guide/architecture-components#pipes)

    [管道](guide/architecture-components#pipes)

* [Introduction to services and dependency injection](guide/architecture-services)

  [服务与依赖注入简介](guide/architecture-services)


When you're familiar with these fundamental building blocks, you can explore them in greater detail in the documentation.

当你熟悉了这些基础构造块之后，就可以在本文档中进一步查看它们的详情了。

You may also be interested in [tools and techniques](guide/architecture-next-steps) to help you build and deploy Angular applications.

你可能还对帮助您构建和部署Angular应用的[工具和技巧](guide/architecture-next-steps)感兴趣。

</div>

<!-- links -->

<!-- external links -->

<!-- end links -->

@reviewed 2023-09-25
