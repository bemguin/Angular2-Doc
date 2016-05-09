# Angular 2 快速入门上手教程

> 本节官方原文：<https://angular.io/docs/ts/latest/quickstart.html>

>导航目录：[Angular 2 中文教程文档](./README.md)

---

我们快速入门的目标是建立并运行一个基于 TypeScript 的超级简单的 Angular 2 的应用程序。

## 下载源码

[下载快速入门的源码](https://github.com/angular/quickstart/blob/master/README.md)，开始 coding。

## 跑起来看看

试试这个[实例](https://angular.io/resources/live-examples/quickstart/ts/plnkr.html)，它运行于[Plunker](http://plnkr.co/)，加载一个简单的应用程序，并显示一个信息：

![](https://angular.io/resources/images/devguide/quickstart/my-first-app.png)

## 学习

当然，我们不会去构建运行在Plunker里的App。按下面的步骤，我们建立一个开发环境的样本文档，同时也为我们实际应用奠定了基础。在较高的水平，我们将：

* 建立[开发环境](#devenv)
* 编写应用程序的Angular [根组件(root component)](#component)
* 编写 [main.ts](#main) 告诉Angular显示根组件
* 编写 [主页](#index)（`index.html`）

### 开发环境

我们需要建立开发环境：

* 安装 [node](#) 和 [npm](#)
* 创建一个应用项目目录
* 添加一个 [tsconfig.json](#) 来引导 TypeScript 编译器
* 添加一个 [typings.json](#) 来标识缺失的 TypeScript 定义文件
* 添加一个 [package.json](#) 来定义我们需要的 packages 和 scripts
* 添加一个 [systemjs.config.js](#) 来设置 system.js
* 安装 npm packages 和 typings 文件
 
**请安装 [node 和 npm](https://nodejs.org/en/download/) ，如果你的机子还没有的话。**

创建一个**项目文件夹**

```
mkdir angular2-quickstart
cd    angular2-quickstart
```

在项目文件夹创建 `tsconfig.json` 文件并复制粘贴下面的代码:

*`tsconfig.json`*

```
{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "moduleResolution": "node",
    "sourceMap": true,
    "emitDecoratorMetadata": true,
    "experimentalDecorators": true,
    "removeComments": false,
    "noImplicitAny": false
  },
  "exclude": [
    "node_modules",
    "typings/main",
    "typings/main.d.ts"
  ]
}

```

这个 `tsconfig.json` 文件引导 TypeScript 编辑器。 想了解更多，可以查看 [TypeScript Configuration](https://angular.io/docs/ts/latest/guide/typescript-configuration.html#tsconfig) 章节。


在项目文件夹创建 `typings.json` 文件并复制粘贴下面的代码:

*`typings.json`*

```
{
  "ambientDependencies": {
    "es6-shim": "registry:dt/es6-shim#0.31.2+20160317120654",
    "jasmine": "registry:dt/jasmine#2.2.0+20160412134438"
  }
}

```

在项目文件夹创建 `package.json` 文件并复制粘贴下面的代码:

*`package.json`*

```
{
  "name": "angular2-quickstart",
  "version": "1.0.0",
  "scripts": {
    "start": "tsc && concurrently \"npm run tsc:w\" \"npm run lite\" ",
    "lite": "lite-server",
    "postinstall": "typings install",
    "tsc": "tsc",
    "tsc:w": "tsc -w",
    "typings": "typings"
  },
  "license": "ISC",
  "dependencies": {
    "@angular/common":  "2.0.0-rc.1",
    "@angular/compiler":  "2.0.0-rc.1",
    "@angular/core":  "2.0.0-rc.1",
    "@angular/http":  "2.0.0-rc.1",
    "@angular/platform-browser":  "2.0.0-rc.1",
    "@angular/platform-browser-dynamic":  "2.0.0-rc.1",
    "@angular/router":  "2.0.0-rc.1",
    "@angular/router-deprecated":  "2.0.0-rc.1",
    "@angular/upgrade":  "2.0.0-rc.1",

    "systemjs": "0.19.27",
    "es6-shim": "^0.35.0",
    "reflect-metadata": "^0.1.3",
    "rxjs": "5.0.0-beta.6",
    "zone.js": "^0.6.12",

    "angular2-in-memory-web-api": "0.0.7",
    "bootstrap": "^3.3.6"
  },
  "devDependencies": {
    "concurrently": "^2.0.0",
    "lite-server": "^2.2.0",
    "typescript": "^1.8.10",
    "typings":"^0.8.1"
  }
}


```

**安装这些包**，在终端窗口，输入下面的 npm 命令：

```
npm install
```

**所有设置完成**。让我们开始编写一些代码吧。

### 我们的第一个Angular 组件

让我们来创建一个文件夹来装载我们的应用，并添加一个超级简单的Angular组件。

在根目录下创建一个 `app` 的子文件夹，并设置为当前目录。

```
mkdir app
cd    app

```

创建一个组件文件，命名为 `app.component.ts` 并粘贴下面的代码：

`app/app.component.ts`

```
import { Component } from '@angular/core';

@Component({
  selector: 'my-app',
  template: '<h1>My First Angular 2 App</h1>'
})
export class AppComponent { }

```

* **`AppComponent`是应用程序的根组件（root component）**
    
    每个Angular应用都至少有一个根组件（root component），常规命名为 `AppComponent`，承载客户端的用户体验。
    
    组件（component）是Angular应用程序的基本构建块。一个组件，通过其关联的模板，控制着屏幕的一部分 —— 视图。
    
    麻雀虽小，五脏俱全。该快速入门虽然只有一个非常简单的组件，但以后我们写每一个组件的基本结构，都在里面：
    
    * 一个或多个 `import` 语句引用我们需要的东西。

    * 一个 `@Component` 装饰器，告诉Angular 使用哪个模板，以及如何创建组件。

    * 一个组件类，其通过它的模板，控制一个视图的外观和行为。

* **Import 导入**

    Angular应用程序是模块化的。它们包括许多专用于一个目的的文件。

    Angular本身也是模块化的。它是模块库的集合，每个模块由几个相关的功能构成，我们将用它们来构建应用程序。
    
    当我们需要的一个模块中的某些功能，就将其导入。在这里，我们从 `@angular/core` 导入了 Angular `Component` 装饰器函数，因为我们需要它来定义我们的组件。

    *`app/app.component.ts (import)`*
    
    ```
    import { Component } from '@angular/core';
    ```
    
* **@Component decorator 装饰器**
    
    `Component` 是一个装饰器函数，需要一个元数据对象。元数据告诉Angular如何创建和使用这个组件。

    我们通过 @符号前缀给一个组件类应用此功能，并用刚才这个带有元数据对象的组件类调用它：
    
    *`app/app.component.ts (metadata)`*
    
    ```
    @Component({
      selector: 'my-app',
     template: '<h1>My First Angular 2 App</h1>'
    })
    ```
    
    这个特定的元数据对象具有两个字段，一个 `selector` 和一个 `template`。

    **`selector`** 指定一个HTML元素的简单CSS选择器，来代表组件。

        * 此组件的元素被命名为 `my-app`。Angular 只要在主页面，遇到一个 `my-app`元素，就会创建并显示 `AppComponent` 的一个实例。

    **`template`**指定组件的配套模板，用HTML增强格式编写，告诉Angular如何渲染这个组件的视图。

        我们的模板是一个单行的HTML，以宣布 ”My First Angular App”。

        更高级的模板可能包含数据绑定到组件属性，可能会标识有自己的模板的其他应用程序组件。这些模板可能又标识了另外的其它部件。这样一个Angular应用程序就变成了组件树。
        
* **Component class 组件类**

    文件的底部是空的, 这个叫做 `AppComponent` 的类没有做任何事情。
    
    *`app/app.component.ts (class)`*
    
    ```
    export class AppComponent { }
    ```
    当我们准备建立一个实体应用，我们可以扩展这个类的属性和应用程序逻辑。我们的 `AppComponent` 类是空的,那是因为在这个快速入门里，我们不需要它做任何事情我。
    
    我们输出(**export**) `AppComponent`，这样应用程序就可以在其他地方导入(**import**)它，在我们创建 `main.ts` 时，就会看到.

---

2016-05-09 末完代续 ...