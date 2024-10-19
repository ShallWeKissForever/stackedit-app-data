


> Written with [StackEdit中文版](https://stackedit.cn/).

- [ ] 1. 显示NFT
- [ ] 2. 如何刷新NFT
- [x] 3. 从链上获取Pool信息
- `LiquidityPoolConfigs`中的`all_pools: SmartVector<Object<LiquidityPool>>`中的`Object<LiquidityPool>`等于`Object<Metadata>`
- 先用一个view方法返回all_pools，再循环调用 `lp_token_supply`，再加到本地储存中

- [ ] 4. 移除流动性界面显示LP Token Balance
- [ ] 5. 输入框自动小数填充&转换
- [ ] 6. 优化UI

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0Nzc4ODYzMTYsMTUzNjcwNTIyOCwtMT
kwMjEwNzI5MCwtMTI3MzE3OTM1NiwyMDE2ODQ1NTY0LC0xMjY0
MzE1MjE2XX0=
-->