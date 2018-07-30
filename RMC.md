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
The RMC token has a function mintToken() which could be used to arbitrary minted by its owner. Besides,  balances[target] and  mintedAmount are uint256 value, so oprator '+' would definitely cause an integer overflow.

If the owner of the contract mint  0x8000000000000000000000000000000000000000000000000000000000000000 RMC twice to the target , balances[target] would be 0 with integer overflow.
