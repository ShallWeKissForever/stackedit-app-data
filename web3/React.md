


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

```

```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjI4MDgxNzA1LDQwMzMxNjUzNl19
-->