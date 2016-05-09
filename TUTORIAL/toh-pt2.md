# 主要/明细
> 我们来创建一个带英雄榜的 “主要/明细” 页面

## 它需要许多英雄

我们的故事需要更多英雄。我们将扩大我们英雄app的导览，用来显示一个英雄列表，而且允许用户选择一个英雄，并显示该英雄的详细信息。

[运行 Part2 的实例](https://angular.io/resources/live-examples/toh-2/ts/plnkr.html)

现在让我们盘算一下显示一个英雄榜，我们需要什么？首先，我们需要一个英雄列表。我们希望在一个视图模板中显示那些英雄，所以我们需要一种方式来做到这一点。

------

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

------

### 显示我们的英雄

* #### 创建英雄

  让我们在 `app.component.ts` 里创建一个10位英雄的数组。

  *`app.component.ts (Hero array)` *

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

* #### 输出英雄

  让我们在`AppComponent`中创建一个属性，输出英雄，以用来绑定。
  
  *`app.component.ts (Hero array property)`*

  ```
  public heroes = HEROES;
  ```

  我们并没有定义`heroes`的类型，TypeScript会从`HEROES`数组中自动推断。

  > 我们可以在这个组件类中定义英雄列表数据。但我们知道，最终我们会从数据服务器中获得的英雄数据。因为我们知道我们要走向哪，英雄数据从一开始的类实现中分离，才是有意义的。

  #### 在一个模板中显示英雄们
  我们组件有 `heroes`。让我们在我们的模板中创建一个无序列表，用来显示他们。我们在标题下方和英雄明细上方插入下面的HTML块。

  *`app.component.ts (Heroes template)`*
  ```
  <h2>My Heroes</h2>
  <ul class="heroes">
    <li>
      <!-- each hero goes here -->
    </li>
  </ul>
  ```

  现在我们有了一个可以用英雄们来填充的模板了。

* #### 用 `ngFor` 列出英雄们

  我们想要在组件中给模板绑定 `heroes` 数组，遍历它们，并分别显示出来。我们需要从Angular中获取一些帮助来实现它。让我们一步一步来。

  首先个性 `<li>` 标签，增加内置指令 `*ngFor`。
  
  *`app.component.ts (ngFor)`*

  ```
  <li *ngFor="let hero of heroes">
  ```

  > * 在 `ngFor` 前面的前导星号（`*`）是此语法的重要组成部分。

  > 在`ngFor`加前缀（`*`）表明`<li>`元素及其子元素构成了一个主模板。 
   
  > 该 `ngFor` 指令遍历 `heroes` 数组，由 `AppComponent.heroes` 属性返回，并冲压出该模板的实例。  
  
  > `ngFor` 双引号中代码的意思为 *“在 `heros` 数组中取出每个 `hero` ，存储到本地 `hero` 变量，并且将其提供给相应的模板实例 ”*。  
  
  > “hero”之前的 `let` 关键字标识了 `hero` 做为模板的一个输入变量。我们可引用这个变量，在模板来访问一个英雄的属性。  
  
  > 关于 `ngFor` 及模板的输入变量的更多内容，请查看章节：[Displaying Data](https://angular.io/docs/ts/latest/guide/displaying-data.html#ngFor) 和 [Template Syntax](https://angular.io/docs/ts/latest/guide/template-syntax.html#ngFor) 

  现在我们在 `<li>` 标签之间插入一些内容，使用 `hero` 模板变量，来显示英雄的属性。
  
  *`app.component.ts (ngFor template)`*

  ```
  <li *ngFor="let hero of heroes">
    <span class="badge">{{hero.id}}</span> {{hero.name}}
  </li>
  ```

  当浏览器刷新时，我们应该看到一个英雄列表了！

* #### 美化英雄们

  我们的英雄名单看起来相当乏味。我们要在视觉上让用户明显的区分开，鼠标悬停在哪位英雄上，又有哪位英雄被选中了。

  *`app.component.ts (Styling)`*

  ```
  styles:[`
    .selected {
      background-color: #CFD8DC !important;
      color: white;
    }
    .heroes {
      margin: 0 0 2em 0;
      list-style-type: none;
      padding: 0;
      width: 15em;
    }
    .heroes li {
      cursor: pointer;
      position: relative;
      left: 0;
      background-color: #EEE;
      margin: .5em;
      padding: .3em 0;
      height: 1.6em;
      border-radius: 4px;
    }
    .heroes li.selected:hover {
      background-color: #BBD8DC !important;
      color: white;
    }
    .heroes li:hover {
      color: #607D8B;
      background-color: #DDD;
      left: .1em;
    }
    .heroes .text {
      position: relative;
      top: -3px;
    }
    .heroes .badge {
      display: inline-block;
      font-size: small;
      color: white;
      padding: 0.8em 0.7em 0 0.7em;
      background-color: #607D8B;
      line-height: 1em;
      position: relative;
      left: -1px;
      top: -4px;
      height: 1.8em;
      margin-right: .8em;
      border-radius: 4px 0 0 4px;
    }
  `]

  ```

  请注意，我们再次使用多行字符串反向单引号（`）。

  当我们给组件指定样式时，它们只作用于该特定组件。我们的样式将只适用于我们的 `AppComponent` 并且 不会“泄漏”到外部HTML去。

  我们展示英雄的模板现在应该看起来想这样：
  
  *`app.component.ts (Styled heroes)`*
  
  ```
  <h2>My Heroes</h2>
  <ul class="heroes">
    <li *ngFor="let hero of heroes">
      <span class="badge">{{hero.id}}</span> {{hero.name}}
    </li>
  </ul>
  ```

  这里有许多样式内容！我们可以像展示的那样使用内嵌 (inline) 模式，或者我们可以把它们移到一个独立的文件，这样可以让我们的组件更简洁。我将在后面的章节这样做，但现在，让我们继续吧...

------

### 选中一个英雄

  现在，在我们的 app 中有一个英雄列表，以及单个英雄的展示。列表和单英雄没有以任何方式进行连接。我们希望用户从我们的列表中选择一个英雄，并出现在详细信息视图。这种UI模式被广泛地称为“主 - 明细”。在我们这个案例，主即是英雄列表和明细则是所选择的英雄。

  我们给一个 `selectedHero` 组件属性绑定一个 `click` 事件，通过它，来连接 "主 --> 明细"。

* #### 点击事件

  修改 `<li>` 标签，输入一个Angular事件来绑定它的click事件。

  *`app.component.ts (Capturing the click event)`*

  ```
  <li *ngFor="let hero of heroes" (click)="onSelect(hero)">
    <span class="badge">{{hero.id}}</span> {{hero.name}}
  </li>
  ```

  我们来看事件绑定

  ```
  (click)="onSelect(hero)"
  ```

  括号标识的 `<li>` 元素的click事件作为目标。等号右边的表达式调用 `AppComponent` 方法，`onSelect()` ，传递模板输入变量 `hero` 作为参数。这是我们之前在 `ngFor` 定义的同一个 `hero` 变量。

  > 关于事件绑定的更多内容，请查看章节：[User Input](https://angular.io/docs/ts/latest/guide/user-input.html) 和 [Template Syntax](https://angular.io/docs/ts/latest/guide/template-syntax.html#ngFor) 

* #### 添加 click 处理程序

  我们的事件绑定指向的 `onSelect` 方法还不存在。现在，我们将这个方法添加到我们的组件中。

  这个方法要做什么呢？它应把该组件的已选择英雄，设置为用户单击的英雄。

  而我们的组件还没有一个“已选择英雄”。我们将会从这里开始。

* #### 暴露属性：已选择的英雄

  我们不再需要 `AppComponent` 的静态 `hero` 属性。用这个简单的 `selectedHero` 属性来**替换**：

  *`app.component.ts (selectedHero)`*
  
  ```
  selectedHero: Hero;
  ```

  我们已经决定，如果用户没有点中一个英雄，那就不应该有任何英雄是选中状态的。所以我们不会用 `hero` 去初始化 `selectedHero`。

  现在，添加一个 `onSelect` 方法，设置 `selectedHero` 属性为用户点击的 `hero`。

  *`app.component.ts (onSelect)`*
  
  ```
  onSelect(hero: Hero) { this.selectedHero = hero; }
  ```

  我们把选择的英雄详情显示到模板中。此刻，它仍然映射旧 `hero` 属性。让我们固定模板绑定到新 `selectedHero` 属性。

  *`app.component.ts (Binding to the selectedHero's name)`*
  
  ```
  <h2>{{selectedHero.name}} details!</h2>
  <div><label>id: </label>{{selectedHero.id}}</div>
  <div>
      <label>name: </label>
      <input [(ngModel)]="selectedHero.name" placeholder="name"/>
  </div>

  ```