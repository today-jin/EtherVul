# Fujinto(NTO)
https://etherscan.io/address/0x8a99ed8a1b204903ee46e733f2c1286f6d20b177
```javascript
    function setBuyRate(uint newBuyRate) onlyOwner {
        buyRate = newBuyRate;
    }
    
    function setSelling(bool newStatus) onlyOwner {
        isSelling = newStatus;
    }

    function buy() payable {
        if(isSelling == false) revert();
        uint amount = msg.value * buyRate;                  // calculates the amount
        balanceOf[msg.sender] += amount;                   // adds the amount to buyer's balance
        balanceOf[owner] -= amount;                         // subtracts amount from seller's balance
        Transfer(owner, msg.sender, amount);                // execute an event reflecting the change
    }
```
The NTO contract has a function buy(), which sells NTO token to the buyer. 
But with the unrestricted msg.value(uint256) mul buyRate(uint256, controlled by owner), the amount may overflow! 
Besides, if the buyRate is 0, this function will become a non-returning ether collection machine.
Although at this time, "isSelling" is false. But the owner could change it by function setSelling. 

So it's still vulnerable.
