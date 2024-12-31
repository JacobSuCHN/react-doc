# React

> This article is a [React](https://www.udemy.com/course/the-ultimate-react-course/?srsltid=AfmBOoru8mEgkZL9W-1CvSSCrNJo6Wa8CFRjXaSN_BCuLNKOIeCYygpS&couponCode=V2JPLETSLEARN) course note.
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

### 组件 JSX props

[react-doc/02-pizza-menu](https://github.com/JacobSuCHN/react-doc/tree/main/code/02-pizza-menu)

#### 组件

- React 应用程序完全由组件组成
- React 中用户界面的构建模块
- 拥有自己的数据、逻辑和外观的用户界面组件
- 我们通过构建多个组件并将它们组合在一起来构建复杂的用户界面
- 组件可以重复使用、相互嵌套并在它们之间传递数据
- 组件可以用命名函数定义，也可以使用箭头函数赋值给对象定义

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

#### props

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
