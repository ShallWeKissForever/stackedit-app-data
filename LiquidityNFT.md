


> Written with [StackEdit中文版](https://stackedit.cn/).

- [x] 1. 显示NFT
```rust
#[view]  
fun get_nft_uri(  
    lp: address,  
    token_1: Object<Metadata>,  
    token_2: Object<Metadata>,  
    is_stable: bool,  
): String acquires ResourceAccountCap, MintedAddressStore {
```
- [x] 2. 如何刷新NFT
- 通过把update方法加入get_nft_uri 这个view方法，先update再return，确保每次更新都是最新的uri
- [x] 3. 从链上获取Pool信息
- `LiquidityPoolConfigs`中的`all_pools: SmartVector<Object<LiquidityPool>>`中的`Object<LiquidityPool>`等于`Object<Metadata>`
- 先用一个view方法返回all_pools，再循环调用view查询名称、符号和 URI，再加到本地储存中

- [x] 4. 移除流动性界面显示LP Token Balance
```rust
#[view]  
public fun lp_token_supply_frontend(  
    token_1: Object<Metadata>,  
    token_2: Object<Metadata>,  
    is_stable: bool,  
): u128 acquires ResourceAccountCap {
```
- [x] 5. 输入框自动小数填充&转换
- [ ] ~~6. 选择币对的功能添加一键交换token1&2的按钮~~
- [ ] 7.重新绘制NFT图片
- [ ] 8. 优化UI
- [ ] 9. 考虑把前端拉取pool后获取token 的名称、符号和 URI的部分写进合约里，这样发一个view就行了
- [x] 10. 考虑在拉取pool完成之前把“选择代币”按钮改为“拉取Pool中...”