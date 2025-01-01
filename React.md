# React

> This article is a [React](https://www.udemy.com/course/the-ultimate-react-course/) course note.
> If there is any infringement, please contact me.

## 从一个 demo 开始

[react-doc/00-demo](https://github.com/JacobSuCHN/react-doc/tree/main/code/00-demo)

```js
import { useState, useEffect } from "react";
export default function App() {
  const [advice, setAdvice] = useState("");
  const [count, setCount] = useState(0);

  async function getAdvice() {
    const res = await fetch("https://api.adviceslip.com/advice");
    const data = await res.json();
    console.log(data.slip.advice);
    setAdvice(data.slip.advice);
    setCount((c) => c + 1);
  }

  useEffect(function () {
    getAdvice();
  }, []);

  return (
    <div>
      <h1>{advice}</h1>
      <button onClick={getAdvice}>Get advie</button>
      <Message count={count} />
    </div>
  );
}

function Message(props) {
  return <p>{props.count}</p>;
}
```

## React 基础

### 初识 React

[react-doc/01-pure-react](https://github.com/JacobSuCHN/react-doc/tree/main/code/01-pure-react)

#### 什么是 React

- 以组件为基础
- 使用 JSX
- 状态驱动
- React 是 JavaScript 库
- 非常受欢迎

#### 纯 React

- 纯 React（Pure React）

  ```html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>Hello React!</title>
    </head>
    <body>
      <div id="root"></div>

      <script
        src="https://unpkg.com/react@18/umd/react.development.js"
        crossorigin
      ></script>
      <script
        src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"
        crossorigin
      ></script>

      <script>
        function App() {
          // const time = new Date().toLocaleTimeString();
          const [time, setTime] = React.useState(
            new Date().toLocaleTimeString()
          );

          React.useEffect(function () {
            setInterval(function () {
              setTime(new Date().toLocaleTimeString());
            }, 1000);
          }, []);

          return React.createElement(
            "header",
            null,
            `Hello React! It's ${time}`
          );
        }

        const root = ReactDOM.createRoot(document.getElementById("root"));
        root.render(React.createElement(App));
      </script>
    </body>
  </html>
  ```

  - 缺陷：没有模块系统、无法转换 JSX 等

#### 创建 React 项目

- 创建 React 项目的方式

  - create-react-app
  - create-next-app
  - vite

- `create-react-app`创建项目

  - ```sh
    npx create-react-app@5 pizza-menu
    ```

### 组件 属性 JSX

[react-doc/02-pizza-menu](https://github.com/JacobSuCHN/react-doc/tree/main/code/02-pizza-menu)

#### 组件

- React 应用程序完全由组件组成
- React 中用户界面的构建模块
- 拥有自己的数据、逻辑和外观的用户界面组件
- 我们通过构建多个组件并将它们组合在一起来构建复杂的用户界面
- 组件可以重复使用、相互嵌套并在它们之间传递数据
- 组件可以用命名函数定义，也可以使用箭头函数赋值给对象定义

#### 属性

- props 用于将父组件数据传递给子组件
- props 用于配置和自定义组件
- props 用于父组件控制子组件的外观和工作方式
- props 可以是任意类型
- props 不能修改
  - 修改 props 会影响父类，产生副作用（不纯粹）
  - 组件的 props 和状态必须是纯函数
- 每个组件都有 props，没有传值则是空对象

```jsx
function Menu() {
  return (
    <main>
      <h2>Our menu</h2>
      <Pizza
        name="Pizza Funghi"
        ingredients="Tomato, mushrooms"
        price={12}
        photoName="pizzas/funghi.jpg"
      />
    </main>
  );
}
function Pizza(props) {
  return (
    <li>
      <img src={props.photoName} alt={props.name} />
      <div>
        <h3>{props.name}</h3>
        <p>{props.ingredients}</p>
      </div>
    </li>
  );
}
```

#### JSX

- 声明式语法可描述组件的外观和工作方式
- 组件必须返回一个 JSX 块
- JavaScript 的扩展，允许我们在 HTML 中嵌入 JavaScript、CSS 和 React 组件
- 每个 JSX 元素都会转换为 React.createElement 函数调用
- 我们可以在没有 JSX 的情况下使用 React
- 声明式
  - 根据当前数据，使用 JSX 描述用户界面的样子
  - React 是对 DOM 的抽象：我们从不接触 DOM
  - 相反，我们认为用户界面是对当前数据的反映
- JSX 使用规则
  - JSX 的工作原理与 HTML 基本相同，但我们可以通过使用 {}（文本或属性）
  - 进入 "JavaScript 模式"，我们可以将 JavaScript 表达式（有返回值的式子）放在 {} 中
  - 不允许使用语句（if/else、for、switch）
  - 一个 JSX 片段只能有一个根元素；如果需要更多，请使用 （或短 <>）

#### 组件样式

- 组件添加样式

  ```jsx
  const style = { color: "red", fontSize: "48px", textTransform: "uppercase" };
  return (
    <div>
      <h1 style={{ color: "red" }}>h1</h1>
      <h2 style={style}>h2</h2>
    </div>
  );
  ```

  ```jsx
  return <header className="header"></header>;
  ```

####

#### 列表渲染

```jsx
<ul className="pizzas">
  {pizzas.map((pizza) => (
    <Pizza pizzaObj={pizza} key={pizza.name} />
  ))}
</ul>
```

- 列表的每一项都必须包含 key 值，唯一

#### 条件渲染

```jsx
<footer className="footer">
  {isOpen && <Order closeHour={closeHour} openHour={openHour} />}
</footer>
```

```jsx
<footer className="footer">
  {isOpen ? (
    <Order closeHour={closeHour} openHour={openHour} />
  ) : (
    <p>
      We're happy to welcome you between {openHour}:00 and {closeHour}:00.
    </p>
  )}
</footer>
```

```jsx
if (!isOpen) return <p>CLOSED</p>;

return (
  <p>
    We're happy to welcome you between {openHour}:00 and {closeHour}:00.
  </p>
);
```

#### 解构 props

```jsx
function Pizza({ pizzaObj }) {
  return (
    <li className={`pizza ${pizzaObj.soldOut ? "sold-out" : ""}`}>
      <img src={pizzaObj.photoName} alt={pizzaObj.name} />
      <div>
        <h3>{pizzaObj.name}</h3>
        <p>{pizzaObj.ingredients}</p>

        <span>{pizzaObj.soldOut ? "SOLD OUT" : pizzaObj.price}</span>
      </div>
    </li>
  );
}
```

#### React 片段

- 解决 JSX 返回单根元素的问题
- React 片段不会插入 DOM 树中

```jsx
<>
  <p></p>
  <p></p>
</>
```

```jsx
<React.Fragment>
  <p></p>
  <p></p>
</React.Fragment>
```

```jsx
function Menu() {
  const pizzas = pizzaData;
  const numPizzas = pizzas.length;

  return (
    <main className="menu">
      <h2>Our menu</h2>

      {numPizzas > 0 ? (
        <>
          <p>
            Authentic Italian cuisine. 6 creative dishes to choose from. All
            from our stone oven, all organic, all delicious.
          </p>

          <ul className="pizzas">
            {pizzas.map((pizza) => (
              <Pizza pizzaObj={pizza} key={pizza.name} />
            ))}
          </ul>
        </>
      ) : (
        <p>We're still working on our menu. Please come back later :)</p>
      )}

      {/* <Pizza
        name="Pizza Spinaci"
        ingredients="Tomato, mozarella, spinach, and ricotta cheese"
        photoName="pizzas/spinaci.jpg"
        price={10}
      /> */}
    </main>
  );
}
```

- 注意：每个`{}`都是一个 JSX 片段，每个 JSX 都需要返回单根元素
- 注意：注释也需要包裹进`{}`才可以使用

### 状态、事件和表单

[react-doc/03-steps](https://github.com/JacobSuCHN/react-doc/tree/main/code/03-steps)
[react-doc/04-travel-list](https://github.com/JacobSuCHN/react-doc/tree/main/code/04-travel-list)

#### 事件

- `onClick={}`：`{}`传入函数，传入的是本身，而不是函数调用
- 函数传参时可以使用箭头函数
- 函数可以定义在组件内

#### 状态

- 组件可长期保存的数据，是在整个应用程序生命周期中需要记住的必要信息
- 组件内存
- 状态变量"/"状态片段"：单个
- 更新组件状态时触发 React 重新渲染组件
- 状态的作用

  - 更新组件视图（重新渲染）
  - 在两次渲染之间持续保持本地变量

  ```jsx
  import { useState } from "react";
  function Steps() {
    const [step, setStep] = useState(1);
    function handleNext() {
      setStep(step + 1);
    }
  }
  ```

  - 只能在函数组件或自定义钩子内部调用：useState 不能在类组件中使用，它也不能在普通的 JavaScript 函数中使用，除非这些函数是作为自定义钩子被定义的
  - 仅在顶层调用：useState 必须在函数组件或自定义钩子的最顶层调用，不能在条件语句、循环或嵌套函数中调用
  - 更新状态使用状态更新函数，而不是修改状态（虽然对象的属性变换能监听到）
  - 若基于当前状态更新，建议使用回调函数

  ```jsx
  function Steps() {
    const [step, setStep] = useState(1);
    function handleNext() {
      setStep((s) => s + 1);
    }
  }
  ```

  - `UI = f(state)`
  - 状态使用
    - 使用状态变量来表示组件应长期跟踪（"记住"）的任何数据
    - 每当希望组件中的某样东西是动态的，就创建一段与该 "东西" 相关的状态，并在该 "东西" 发生变化时更新状态（又称 "动态"）
    - 如果要更改组件的外观或显示的数据，请更新其状态
    - 构建组件时，将其视图想象为随时间变化的状态的反映
    - 对于不应触发组件重新渲染的数据，不要使用状态。而应使用常规变量
  - 同一组件的状态是独立的

#### 表单

```jsx
function Form() {
  function handleSubmit(e) {
    e.preventDefault();
  }

  return (
    <form className="add-form" onSubmit={handleSubmit}>
      <h3>What do you need for your 😍 trip?</h3>
      <select
        value={quantity}
        onChange={(e) => setQuantity(Number(e.target.value))}
      >
        {Array.from({ length: 20 }, (_, i) => i + 1).map((num) => (
          <option value={num} key={num}>
            {num}
          </option>
        ))}
      </select>
      <input type="text" placeholder="Item..." />
      <button>Add</button>
    </form>
  );
}
```

#### 受控元素

- 它指的是其视图状态完全由 React 组件的 state 数据控制的元素

```jsx
function Form() {
  const [description, setDescription] = useState("");
  const [quantity, setQuantity] = useState(1);

  function handleSubmit(e) {
    e.preventDefault();

    if (!description) return;

    const newItem = { description, quantity, packed: false, id: Date.now() };

    setDescription("");
    setQuantity(1);
  }

  return (
    <form className="add-form" onSubmit={handleSubmit}>
      <h3>What do you need for your 😍 trip?</h3>
      <select
        value={quantity}
        onChange={(e) => setQuantity(Number(e.target.value))}
      >
        {Array.from({ length: 20 }, (_, i) => i + 1).map((num) => (
          <option value={num} key={num}>
            {num}
          </option>
        ))}
      </select>
      <input
        type="text"
        placeholder="Item..."
        value={description}
        onChange={(e) => setDescription(e.target.value)}
      />
      <button>Add</button>
    </form>
  );
}
```

#### 状态与属性

- 状态
  - 由组件拥有的内部数据
  - 组件 "存储器"
  - 可由组件本身更新
  - 更新状态会导致组件重新渲染
  - 用于组件交互
- 属性
  - 外部数据，由父组件所有
  - 与函数参数类似
  - 只读
  - 接收新属性（接受状态作为属性）会导致组件重新渲染，通常是在父节点的状态更新后
  - 用于父组件配置子组件（设置）

### 状态管理

#### React 思维

- 将所需的用户界面分解为多个组件，并建立组件树
- 构建静态版本（无状态）
- 考虑状态
  - 何时使用状态
  - 状态的类型：局部与全局
  - 在何处放置每个状态片段
- 建立数据流
  - 单向数据流
  - 父子组件通信
  - 访问全局状态

#### 局部状态与全局状态

- 局部状态
  - 只有一个或少数几个组件需要的状态
  - 在一个组件中定义的状态，且只有该组件和子组件能访问它（通过属性传递）
  - 应始终从局部状态出发
- 全局状态
  - 状态许多组件可能需要
  - 每个组件都能访问的共享状态

#### 状态提升

- 状态提升（State Lifting）是一种设计模式，主要用于解决多个组件需要共享相同状态的情况
  - 在父组件中定义状态：使用 React 的 useState 或类组件的 constructor 来定义状态
  - 通过 props 传递状态及其更新函数：父组件通过 props 将状态及其更新函数传递给子组件
  - 子组件使用 props 中的状态和更新函数：子组件通过 props 接收状态和更新函数，并在需要时调用更新函数来修改状态

```jsx
function App() {
  const [items, setItems] = useState([]);

  function handleAddItems(item) {
    setItems((items) => [...items, item]);
  }
  return (
    <div className="app">
      <Logo />
      <Form onAddItems={handleAddItems} />
      <PackingList items={items} />
      <Stats />
    </div>
  );
}
```

```jsx
function PackingList ( {items} ) {
  return (
    <div className="list">
      <ul>
        {items.map((item) => (
          <Item
            item={item}
            key={item.id}
          />
        ))}
      </ul>
  );
}
```

```jsx
function Form({ onAddItems }) {
  const [description, setDescription] = useState("");
  const [quantity, setQuantity] = useState(1);

  function handleSubmit(e) {
    e.preventDefault();

    if (!description) return;

    const newItem = { description, quantity, packed: false, id: Date.now() };
    onAddItems(newItem);
    setDescription("");
    setQuantity(1);
  }

  return (
    <form className="add-form" onSubmit={handleSubmit}>
      <h3>What do you need for your 😍 trip?</h3>
      <select
        value={quantity}
        onChange={(e) => setQuantity(Number(e.target.value))}
      >
        {Array.from({ length: 20 }, (_, i) => i + 1).map((num) => (
          <option value={num} key={num}>
            {num}
          </option>
        ))}
      </select>
      <input
        type="text"
        placeholder="Item..."
        value={description}
        onChange={(e) => setDescription(e.target.value)}
      />
      <button>Add</button>
    </form>
  );
}
```

- 注意：`setItems((items) => [...items, item])`，不能使用`items.push(item)`，React 不允许，因为这改变了原数据

#### 传递参数

```jsx
function Item({ item, onDeleteItem, onToggleItem }) {
  return (
    <li>
      <input
        type="checkbox"
        value={item.packed}
        onChange={() => onToggleItem(item.id)}
      />
      <span style={item.packed ? { textDecoration: "line-through" } : {}}>
        {item.quantity} {item.description}
      </span>
      <button onClick={() => onDeleteItem(item.id)}>❌</button>
    </li>
  );
}
```

- 若直接使用`onClick={onDeleteItem}`，React 会将事件对象作为参数传入
- `{}`应传入函数本身而不是函数调用，此处应改为`onClick={() => onDeleteItem(item.id)}`

#### 派生状态

- 指从现有状态或属性（props）中计算得出的状态
- 组件重新渲染时会自动重新计算派生状态

```js
const [cart, setCart] = useState([
  { name: "cart1", price: 10 },
  { name: "cart2", price: 20 },
]);
const [numItems, setNumItems] = useState(2);
const [totalPrice, setTotalPrice] = useState(30);
```

```js
const [cart, setCart] = useState([
  { name: "cart1", price: 10 },
  { name: "cart2", price: 20 },
]);
const numItems = cart.length;
const totalPrice = cart.reduce((acc, cur) => acc + cur.price, 0);
```

#### 拆分组件

```jsx
import { useState } from "react";
import Logo from "./Logo";
import Form from "./Form";
import PackingList from "./PackingList";
import Stats from "./Stats";

export default function App() {
  const [items, setItems] = useState([]);

  function handleAddItems(item) {
    setItems((items) => [...items, item]);
  }

  function handleDeleteItem(id) {
    setItems((items) => items.filter((item) => item.id !== id));
  }

  function handleToggleItem(id) {
    setItems((items) =>
      items.map((item) =>
        item.id === id ? { ...item, packed: !item.packed } : item
      )
    );
  }

  function handleClearList() {
    const confirmed = window.confirm(
      "Are you sure you want to delete all items?"
    );

    if (confirmed) setItems([]);
  }

  return (
    <div className="app">
      <Logo />
      <Form onAddItems={handleAddItems} />
      <PackingList
        items={items}
        onDeleteItem={handleDeleteItem}
        onToggleItem={handleToggleItem}
        onClearList={handleClearList}
      />
      <Stats items={items} />
    </div>
  );
}
```

```jsx
export default function Logo() {
  ...
}

```

```jsx
export default function Form({ onAddItems }) {
  ...
}

```

```jsx
import Item from "./Item";

export default function PackingList({
  items,
  onDeleteItem,
  onToggleItem,
  onClearList,
}) {
  ...
}

```

```jsx
export default function Stats({ items }) {
  ...
}

```

```jsx
export default function Item({ item, onDeleteItem, onToggleItem }) {
  ...
}

```

#### children 属性

- children 属性允许我们将 JSX 传递到元素中（除常规常规外）
- 制作可重用和可配置组件（尤其是组件内容）的基本工具
- 对于在使用前不知道其内容的通用组件（如模态）非常有用
- 通过 props.children 访问

```jsx
function Steps() {
  function handlePrevious() {}

  function handleNext() {}

  return (
    <div className="buttons">
      <Button bgColor="#7950f2" textColor="#fff" onClick={handlePrevious}>
        <span>👈</span> Previous
      </Button>

      <Button bgColor="#7950f2" textColor="#fff" onClick={handleNext}>
        Next <span>👉</span>
      </Button>
    </div>
  );
}
```

```jsx
function Button({ textColor, bgColor, onClick, children }) {
  return (
    <button
      style={{ backgroundColor: bgColor, color: textColor }}
      onClick={onClick}
    >
      {children}
    </button>
  );
}
```
