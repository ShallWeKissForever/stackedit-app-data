


> Written with [StackEdit中文版](https://stackedit.cn/).

# 组件的导入导出

| 语法 | 导出语句 | 导入语句 |
|--|--|--|
| 默认 | `export default function Button() {}` | `import Button from './Button.js';` |
| 具名 | `export function Button() {}` | `import { Button } from './Button.js';` |
**同一文件中，有且仅有一个默认导出，但可以有多个具名导出！**

当使用默认导入时，你可以在 `import` 语句后面进行任意命名。比如 `import Banana from './Button.js'`，如此你能获得与默认导出一致的内容。相反，对于具名导入，导入和导出的名字必须一致。这也是称其为 **具名** 导入的原因！

# 
<!--stackedit_data:
eyJoaXN0b3J5IjpbODk2MjIyMDc1LDQwMzMxNjUzNl19
-->