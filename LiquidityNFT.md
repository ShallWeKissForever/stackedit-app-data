


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
- [ ] 5. 输入框自动小数填充&转换
- [ ] 6. 选择币对的功能添加一键交换token1&2的按钮
- [ ] 7. 优化UI
- [ ] 8. 考虑把前端拉取pool后获取token 的名称、符号和 URI的部分写进合约里，这样发一个view就行了
- [ ] 9. 考虑在拉取pool完成之前把“选择代币”按钮改为“拉取Pool中...”


### 解决方案：

1. **给 Nginx 用户访问权限**
   确认后，需要给 Nginx 用户（比如 `www-data`）访问文件的权限。将 Nginx 用户添加到 `lighthouse` 用户组，或者简单地调整权限以允许所有用户读取和执行目录和文件。

   - 给 Nginx 用户添加读取权限：
     ```bash
     sudo chmod -R o+r /home/lighthouse/Liquidity_NFT/liquiditynft_frontend/dist
     ```

   - 确保对所有相关目录有执行权限：
     ```bash
     sudo chmod -R o+x /home/lighthouse /home/lighthouse/Liquidity_NFT /home/lighthouse/Liquidity_NFT/liquiditynft_frontend
     ```
Nginx 在你的服务器上是以 `www-data` 用户运行的。现在我们可以为 `www-data` 用户赋予正确的权限，确保它可以访问 `/home/lighthouse/Liquidity_NFT/liquiditynft_frontend/dist` 目录及其文件。

1. **为 `www-data` 用户赋予读取权限**
   确保 `www-data` 用户对相关目录和文件具有读取权限：
   ```bash
   sudo chmod -R o+r /home/lighthouse/Liquidity_NFT/liquiditynft_frontend/dist
   ```

2. **赋予执行权限给目录**
   确保 `www-data` 用户可以进入每一级目录，通过为这些目录添加执行权限：
   ```bash
   sudo chmod o+x /home/lighthouse
   sudo chmod o+x /home/lighthouse/Liquidity_NFT
   sudo chmod o+x /home/lighthouse/Liquidity_NFT/liquiditynft_frontend
   ```

3. **重启 Nginx**
   在权限调整之后，重启 Nginx 以应用更改：
   ```bash
   sudo systemctl restart nginx
   ```

![问号](https://github.com/user-attachments/assets/dc64f23b-c14b-4c57-b8c0-1078e35ac54c)

<!--stackedit_data:
eyJoaXN0b3J5IjpbMzIyMzI3NjE5LC05NzE5NTAwMjcsMTExNz
QwMjQ0NiwtMzg2NzM2OTE0LDE5MTkyMTcxMzQsMTc1ODc3MjAx
MywzNTc1MzIzMDksMTYwMDEzNDUxNywyMDY2MTkxMTgwXX0=
-->