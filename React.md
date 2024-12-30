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
