


> Written with [StackEdit中文版](https://stackedit.cn/).

- [ ] 1. 显示NFT
- [ ] 2. 如何刷新NFT
- [x] 3. 从链上获取Pool信息
- `LiquidityPoolConfigs`中的`all_pools: SmartVector<Object<LiquidityPool>>`中的`Object<LiquidityPool>`等于`Object<Metadata>`
- 先用一个view方法返回all_pools，再循环调用view查询名称、符号和 URI，再加到本地储存中

- [ ] 4. 移除流动性界面显示LP Token Balance
- `lp_token_supply`
- [ ] 5. 输入框自动小数填充&转换
- [ ] 6. 优化UI

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTYxMDMxMjgyLDE1MzY3MDUyMjgsLTE5MD
IxMDcyOTAsLTEyNzMxNzkzNTYsMjAxNjg0NTU2NCwtMTI2NDMx
NTIxNl19
-->