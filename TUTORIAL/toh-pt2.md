# 主要/明细
> 我们来创建一个带英雄榜的 “主要/明细” 页面

## 它需要许多英雄

我们的故事需要更多英雄。我们将扩大我们英雄app的导览，用来显示一个英雄列表，而且允许用户选择一个英雄，并显示该英雄的详细信息。

[运行 Part2 的实例](https://angular.io/resources/live-examples/toh-2/ts/plnkr.html)

现在让我们盘算一下显示一个英雄榜，我们需要什么？首先，我们需要一个英雄列表。我们希望在一个视图模板中显示那些英雄，所以我们需要一种方式来做到这一点。

### 我们做到哪了

在我们继续英雄导览的 Part2 之前，让我们来验证一下，在完成 Part1之后，我们应该有如下的文档结构，如果不是，那我们就需要回到Part1，并弄清我们错过了什么。
```
angular2-tour-of-heroes
 ├─ app
 │   ├─ app.component.ts
 │   └─ main.ts
 ├─ node_modules ...
 ├─ typings ...
 ├─ index.html
 ├─ package.json
 ├─ tsconfig.json
 └─ typings.json
```

**保持 app 在运行中**

我们要启动TypeScript编译器，让它时实监控我们修改，并启动我们的服务器。我们将通过如下命令做到这一点：

```
npm start
```
这样，当我们继续构建英雄导览时，这个应用能够保持在运行状态。

### 显示我们的英雄

#### 创建英雄

让我们在 `app.component.ts` 里创建一个10位英雄的数组。

```

var HEROES: Hero[] = [
  { "id": 11, "name": "Mr. Nice" },
  { "id": 12, "name": "Narco" },
  { "id": 13, "name": "Bombasto" },
  { "id": 14, "name": "Celeritas" },
  { "id": 15, "name": "Magneta" },
  { "id": 16, "name": "RubberMan" },
  { "id": 17, "name": "Dynama" },
  { "id": 18, "name": "Dr IQ" },
  { "id": 19, "name": "Magma" },
  { "id": 20, "name": "Tornado" }
];

```

这个`HEROES`数组是`Hero`类型，这个类在Part1已经定义了。我们期望从WebService中获取这份英雄名单，但还是让我们迈一小步，来显示模拟的英雄。

#### 输出英雄

让我们在`AppComponent`中创建一个属性，输出英雄，以用来绑定。

```
public heroes = HEROES;
```

我们并没有定义`heroes`的类型，TypeScript会从`HEROES`数组中自动推断。

> 我们可以在这个组件类中定义英雄列表数据。但我们知道，最终我们会从数据服务器中获得的英雄数据。因为我们知道我们要走向哪，英雄数据从一开始的类实现中分离，才是有意义的。

#### 在一个模板中显示英雄们
我们组件有 `heroes`。让我们在我们的模板中创建一个无序列表，用来显示他们。我们在标题下方和英雄明细上方插入下面的HTML块。

```
<h2>My Heroes</h2>
<ul class="heroes">
  <li>
    <!-- each hero goes here -->
  </li>
</ul>
```