


> Written with [StackEdit中文版](https://stackedit.cn/).

# 组件的导入导出

| 语法 | 导出语句 | 导入语句 |
|--|--|--|
| 默认 | `export default function Button() {}` | `import Button from './Button.js';` |
| 具名 | `export function Button() {}` | `import { Button } from './Button.js';` |
**同一文件中，有且仅有一个默认导出，但可以有多个具名导出！**

当使用默认导入时，你可以在 `import` 语句后面进行任意命名。比如 `import Banana from './Button.js'`，如此你能获得与默认导出一致的内容。相反，对于具名导入，导入和导出的名字必须一致。这也是称其为 **具名** 导入的原因！

# 将 Props 传递给组件
## 步骤 1: 将 props 传递给子组件

首先，将一些 props 传递给 `Avatar`。例如，让我们传递两个 props：`person`（一个对象）和 `size`（一个数字）：

```typescript
export default function Profile() {  
		return (  
			<Avatar  
				person={{ name: 'Lin Lanying', imageId: '1bX5QH6' }}  
				size={100}  
			/>  
	);  
}
```

现在，你可以在 `Avatar` 组件中读取这些 props 了。

## 步骤 2: 在子组件中读取 props

你可以通过在 `function Avatar` 之后直接列出它们的名字 `person, size` 来读取这些 props。这些 props 在 `({` 和 `})` 之间，并由逗号分隔。这样，你可以在 `Avatar` 的代码中使用它们，就像使用变量一样。

```typescript
function Avatar({ person, size }) {
  return (
    <img
      className="avatar"
      src={getImageUrl(person)}
      alt={person.name}
      width={size}
      height={size}
    />
  );
}
```

向使用 `person` 和 `size` props 渲染的 `Avatar` 添加一些逻辑，你就完成了。

你可以将 props 想象成可以调整的“旋钮”。它们的作用与函数的参数相同 —— 事实上，props **正是** 组件的唯一参数！ React 组件函数接受一个参数，一个 `props` 对象：

```typescript
function Avatar(props) {  
	let person = props.person;  
	let size = props.size;  
	// ...  
}
```

通常你不需要整个 `props` 对象，所以可以将它解构为单独的 props。

在声明 props 时， 不要忘记 ( 和 ) 之间的一对花括号 { 和 }  ：
```typescript
function Avatar({ person, size }) {
  // ...
}
```
这种语法被称为 “解构”，等价于于从函数参数中读取属性：
```typescript
function Avatar(props) {
  let person = props.person;
  let size = props.size;
  // ...
}
```
## 给 prop 指定一个默认值 
如果你想在没有指定值的情况下给 prop 一个默认值，你可以通过在参数后面写 = 和默认值来进行解构：
```typescript
function Avatar({ person, size = 100 }) {
  // ...
}
```
现在， 如果 <Avatar person={...} /> 渲染时没有 size prop，  size 将被赋值为 100。

默认值仅在缺少 size prop 或 size={undefined} 时生效。 但是如果你传递了 size={null} 或 size={0}，默认值将 不 被使用。
# 在 JSX 中通过大括号使用 JavaScript
-   在 JSX 的大括号内引用 JavaScript 变量
-   在 JSX 的大括号内调用 JavaScript 函数
-   在 JSX 的大括号内使用 JavaScript 对象

# 条件渲染
你可以认为，_“如果 `isPacked` 为 true 时，则（`?`）渲染 `name + ' ✅'`，否则（`:`）渲染 `name`。”_
你可以添加更多的换行和括号，以便在各种情况下更好地去嵌套 JSX：
```typescript
function Item({ name, isPacked }) {
  return (
    <li className="item">
      {isPacked ? (
        <del>
          {name + ' ✅'}
        </del>
      ) : (
        name
      )}
    </li>
  );
}
```

你会遇到的另一个常见的快捷表达式是 JavaScript 逻辑与（`&&`）运算符在 React 组件里，通常用在当条件成立时，你想渲染一些 JSX，**或者不做任何渲染**。使用 `&&`，你也可以实现仅当 `isPacked` 为 `true` 时，渲染勾选符号。
你可以认为，_“当 `isPacked` 为真值时，则（`&&`）渲染勾选符号，否则，不渲染。”_
```typescript
function Item({ name, isPacked }) {
  return (
    <li className="item">
      {name} {isPacked && '✅'}
    </li>
  );
}
```
当 JavaScript && 表达式 的左侧（我们的条件）为 true 时，它则返回其右侧的值（在我们的例子里是勾选符号）。但条件的结果是 false，则整个表达式会变成 false。在 JSX 里，React 会将 false 视为一个“空值”，就像 null 或者 undefined，这样 React 就不会在这里进行任何渲染。

>**切勿将数字放在 `&&` 左侧.**
>JavaScript 会自动将左侧的值转换成布尔类型以判断条件成立与否。然而，如果左侧是 `0`，整个表达式将变成左侧的值（`0`），React 此时则会渲染 `0` 而不是不进行渲染。
>例如，一个常见的错误是 `messageCount && <p>New messages</p>`。其原本是想当 `messageCount` 为 0 的时候不进行渲染，但实际上却渲染了 `0`。
>为了更正，可以将左侧的值改成布尔类型：`messageCount > 0 && <p>New messages</p>`。
# 保持组件纯粹
-   一个组件必须是纯粹的，就意味着：
    -   **只负责自己的任务。** 它不会更改在该函数调用前就已存在的对象或变量。
    -   **输入相同，则输出相同。** 给定相同的输入，组件应该总是返回相同的 JSX。
-   渲染随时可能发生，因此组件不应依赖于彼此的渲染顺序。
-   你不应该改变任何用于组件渲染的输入。这包括 props、state 和 context。通过 “设置” state来更新界面，而不要改变预先存在的对象。
-   努力在你返回的 JSX 中表达你的组件逻辑。当你需要“改变事物”时，你通常希望在事件处理程序中进行。作为最后的手段，你可以使用 `useEffect`。
-   编写纯函数需要一些练习，但它充分释放了 React 范式的能力。

# state：组件的记忆
`handleClick()` 事件处理函数正在更新局部变量 `index`。但存在两个原因使得变化不可见：

1.  **局部变量无法在多次渲染中持久保存。** 当 React 再次渲染这个组件时，它会从头开始渲染——不会考虑之前对局部变量的任何更改。
2.  **更改局部变量不会触发渲染。** React 没有意识到它需要使用新数据再次渲染组件。

要使用新数据更新组件，需要做两件事：

1.  **保留** 渲染之间的数据。
2.  **触发** React 使用新数据渲染组件（重新渲染）。

`useState`Hook 提供了这两个功能：
3.  **State 变量** 用于保存渲染间的数据。
4. **State setter 函数** 更新变量并触发 React 再次渲染组件。
# 渲染和提交
## 步骤 1: 触发一次渲染[](https://zh-hans.react.dev/learn/render-and-commit#step-1-trigger-a-render "Link for 步骤 1: 触发一次渲染 ")

有两种原因会导致组件的渲染:

1.  组件的 **初次渲染。**
2.  组件（或者其祖先之一）的 **状态发生了改变。**

### 初次渲染[](https://zh-hans.react.dev/learn/render-and-commit#initial-render "Link for 初次渲染 ")

当应用启动时，会触发初次渲染。框架和沙箱有时会隐藏这部分代码，但它是通过调用 [`createRoot`](https://zh-hans.react.dev/reference/react-dom/client/createRoot) 方法并传入目标 DOM 节点，然后用你的组件调用 `render` 函数完成的：
```javascript
import Image from './Image.js';
import { createRoot } from 'react-dom/client';

const root = createRoot(document.getElementById('root'))
root.render(<Image />);
```
### 状态更新时重新渲染[](https://zh-hans.react.dev/learn/render-and-commit#re-renders-when-state-updates "Link for 状态更新时重新渲染 ")

一旦组件被初次渲染，你就可以通过使用 [`set` 函数](https://zh-hans.react.dev/reference/react/useState#setstate) 更新其状态来触发之后的渲染。更新组件的状态会自动将一次渲染送入队列。（你可以把这种情况想象成餐厅客人在第一次下单之后又点了茶、点心和各种东西，具体取决于他们的胃口。）
## 步骤 2: React 渲染你的组件[](https://zh-hans.react.dev/learn/render-and-commit#step-2-react-renders-your-components "Link for 步骤 2: React 渲染你的组件 ")

在你触发渲染后，React 会调用你的组件来确定要在屏幕上显示的内容。**“渲染中” 即 React 在调用你的组件。**

-   **在进行初次渲染时,** React 会调用根组件。
-   **对于后续的渲染,** React 会调用内部状态更新触发了渲染的函数组件。

这个过程是递归的：如果更新后的组件会返回某个另外的组件，那么 React 接下来就会渲染 _那个_ 组件，而如果那个组件又返回了某个组件，那么 React 接下来就会渲染 _那个_ 组件，以此类推。这个过程会持续下去，直到没有更多的嵌套组件并且 React 确切知道哪些东西应该显示到屏幕上为止。
```javascript
export default function Gallery() {
  return (
    <section>
      <h1>鼓舞人心的雕塑</h1>
      <Image />
      <Image />
      <Image />
    </section>
  );
}

function Image() {
  return (
    <img
      src="https://i.imgur.com/ZF6s192.jpg"
      alt="'Floralis Genérica' by Eduardo Catalano: a gigantic metallic flower sculpture with reflective petals"
    />
  );
}
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbMzMzODQ2NjYyLC0xNDc0MDM1NTEwLC0xNz
MzNjk2NzI0LDcyMzE4OTcyMywtODAzNDA4MDkwLDk1MjUyNjgw
OSw2NDgzNTI3OTMsMjEzODU3MjExNCw0MDMzMTY1MzZdfQ==
-->