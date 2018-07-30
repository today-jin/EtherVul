# RemiCoin (RMC)
https://etherscan.io/address/0x7dc4f41294697a7903c4027f6ac528c5d14cd7eb
```javascript
    function mintToken(address target, uint256 mintedAmount) onlyOwner{
        balances[target] += mintedAmount;
        totalSupply += mintedAmount;
        
        Transfer(0,owner,mintedAmount);
        Transfer(owner,target,mintedAmount);
    }
```
The RMC token has a function mintToken() which could be used to arbitrary minted by its owner . Besides,  balances[target] and  mintedAmount are uint256 value, so oprator '+' would definitely cause an integer overflow.

 Initial amount of B is 0.
 
[![ Initial amount](http://wx3.sinaimg.cn/mw690/0060lm7Tly1fts5tbpr10j30u10b7mx8.jpg " Initial amount")](http://wx3.sinaimg.cn/mw690/0060lm7Tly1fts5tbpr10j30u10b7mx8.jpg " Initial amount")

After the owner of the contract mint  0x8000000000000000000000000000000000000000000000000000000000000000 RMC twice to the target , balances[target] would be 0 with integer overflow.

Send once.

[![Send once](http://wx4.sinaimg.cn/mw690/0060lm7Tly1fts5tbpgzoj30um07kaa1.jpg "Send once")](http://wx4.sinaimg.cn/mw690/0060lm7Tly1fts5tbpgzoj30um07kaa1.jpg "Send once")
[![send twice](http://wx4.sinaimg.cn/mw690/0060lm7Tly1fts5tbtr4gj30tg08mt93.jpg "tax1")](http://wx4.sinaimg.cn/mw690/0060lm7Tly1fts5tbtr4gj30tg08mt93.jpg "tax1")
[![amount once](http://wx2.sinaimg.cn/mw690/0060lm7Tly1fts5tbsrc6j30u8086t8r.jpg "amount once")](http://wx2.sinaimg.cn/mw690/0060lm7Tly1fts5tbsrc6j30u8086t8r.jpg "amount once")

Then send twice.

[![Tax](http://wx1.sinaimg.cn/mw690/0060lm7Tly1fts5tbseu9j30ti08mwev.jpg "tax2")](http://wx1.sinaimg.cn/mw690/0060lm7Tly1fts5tbseu9j30ti08mwev.jpg "tax2")


The amount is return to 0.

[![amount twice](http://wx1.sinaimg.cn/mw690/0060lm7Tly1fts5tbslg9j30u408oaa1.jpg "amount twice")](http://wx1.sinaimg.cn/mw690/0060lm7Tly1fts5tbslg9j30u408oaa1.jpg "amount twice")
