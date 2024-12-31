# React

## 从一个 demo 开始

[demo](https://github.com/JacobSuCHN/react-doc/tree/main/code/00-demo)

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

### 初始 React

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

#### 创建React 项目

- 创建React项目的方式

  - create-react-app
  - create-next-app
  - vite

- `create-react-app`创建项目

  - ```sh
    npx create-react-app@5 pizza-menu
    ```

    

#### 组件

- React 应用程序完全由组件组成
- React 中用户界面的构建模块
- 拥有自己的数据、逻辑和外观的用户界面组件
- 我们通过构建多个组件并将它们组合在一起来构建复杂的用户界面
- 组件可以重复使用、相互嵌套并在它们之间传递数据

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

