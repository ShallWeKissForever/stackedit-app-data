


> Written with [StackEdit中文版](https://stackedit.cn/).

# 组件的导入导出

| 语法 | 导出语句 | 导入语句 |
|--|--|--|
| 默认 | `export default function Button() {}` | `import Button from './Button.js';` |
| 具名 | `export function Button() {}` | `import { Button } from './Button.js';` |
**同一文件中，有且仅有一个默认导出，但可以有多个具名导出！**

当使用默认导入时，你可以在 `import` 语句后面进行任意命名。比如 `import Banana from './Button.js'`，如此你能获得与默认导出一致的内容。相反，对于具名导入，导入和导出的名字必须一致。这也是称其为 **具名** 导入的原因！

# 将 Props 传递给组件
### 步骤 1: 将 props 传递给子组件[](https://zh-hans.react.dev/learn/passing-props-to-a-component#step-1-pass-props-to-the-child-component "Link for 步骤 1: 将 props 传递给子组件 ")

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

### 步骤 2: 在子组件中读取 props[](https://zh-hans.react.dev/learn/passing-props-to-a-component#step-2-read-props-inside-the-child-component "Link for 步骤 2: 在子组件中读取 props ")

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
# 给 prop 指定一个默认值 
如果你想在没有指定值的情况下给 prop 一个默认值，你可以通过在参数后面写 = 和默认值来进行解构：
```typescript
function Avatar({ person, size = 100 }) {
  // ...
}
```
现在， 如果 <Avatar person={...} /> 渲染时没有 size prop，  size 将被赋值为 100。

默认值仅在缺少 size prop 或 size={undefined} 时生效。 但是如果你传递了 size={null} 或 size={0}，默认值将 不 被使用。


<!--stackedit_data:
eyJoaXN0b3J5IjpbMjEzODU3MjExNCw0MDMzMTY1MzZdfQ==
-->