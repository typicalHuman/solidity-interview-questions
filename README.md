# solidity-interview-questions (and answers)

Questions taken from - https://www.rareskills.io/post/solidity-interview-questions

## Easy

<details open>
<summary><b><font size="+1">1. What is the difference between private, internal, public, and external functions?</font></b></summary>

`private` can only be used within the current contract, `internal` can also be used within derived contracts, `public` functions can be used inside and outside the current contract (by users and the contract itself), `external` functions can only be used by users.

_Reference_: https://docs.soliditylang.org/en/latest/contracts.html#state-variable-visibility

</details>

<br>

<details open>
<summary><b><font size="+1">2. Approximately, how large can a smart contract be?</font></b></summary>

About 24,000 bytes and (4.7 million gas). According to EIP-170: In short, the point of this EIP is to minimize the overloading of nodes (especially light nodes) and to prevent possible DOS attacks.

_Reference_: https://docs.soliditylang.org/en/latest/cheatsheet.html#function-visibility-specifiers

</details>

<br>

<details open>
<summary><b><font size="+1">3. What is the difference between create and create2?</font></b></summary>

`CREATE` is used in the default scenario when you deploy a smart contract via `new` for example. `CREATE2` is also used to deploy smart contracts, but it has a special parameter - `salt`, which allows you to predetermine the future address of the contract.

_Reference_: https://vinta.ws/code/solidity-create-vs-create2.html

</details>

<br>

<details open>
<summary><b><font size="+1">4. What major change with arithmetic happened with Solidity 0.8.0?</font></b></summary>

More secure arithmetic operations without explicitly using the `SafeMath` library (preventing underflows and overflows).

_Reference_: https://docs.soliditylang.org/en/latest/080-breaking-changes.html

</details>

<br>

<details open>
<summary><b><font size="+1">5. What special CALL is required for proxies to work?</font></b></summary>

`DELEGATECALL` because it allows you to pass all the call context to the proxy contract and also to keep the storage states.

_Reference_: https://eips.ethereum.org/EIPS/eip-1967

</details>

<br>
<details open>
<summary><b><font size="+1">6. Prior to EIP-1559, how do you calculate the dollar cost of an Ethereum transaction?</font></b></summary>

It used a simple gas price auction system and this system had some downsides such as: highly volatile gas price and delays for users.

_Reference_: https://eips.ethereum.org/EIPS/eip-1559

</details>

<br>

<details open>
<summary><b><font size="+1">7. What are the challenges of creating a random number on the blockchain?</font></b></summary>

Because blockchain is a fully open system it means you can simulate and predict almost everything on it and all attempts to create true RNG were failed so for RNG on blockchain builders usually use some oracles like - https://docs.chain.link/vrf.

_Reference_: https://www.sitepoint.com/solidity-pitfalls-random-number-generation-for-ethereum/

</details>

<br>

<details open>
<summary><b><font size="+1">8. What is the difference between a Dutch Auction and an English Auction?</font></b></summary>

In an English auction, the auctioneer sets a base price and bidders compete to see who can offer a higher price. In a Dutch auction, it's the other way round - the auctioneer sets a high price and goes lower and lower until someone agrees to accept the price.

_Reference_: https://saylordotorg.github.io/text_introduction-to-economic-analysis/s21-auctions.html

</details>

<br>

<details open>
<summary><b><font size="+1">9. What is the difference between transfer and transferFrom in ERC20?</font></b></summary>

`transfer` only transfers the amount of tokens from `msg.sender`. `transferFrom` uses an allowance system, so for example if you want the contract to use your ERC20 token you can set an allowance for it to use your tokens so it can send the tokens on your behalf: `transferFrom(you, someone, amount)`.

_Reference_: https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#IERC20-transferFrom-address-address-uint256-

</details>

<br>

<details open>
<summary><b><font size="+1">10. Which is better to use for an address allowlist: a mapping or an array? Why?</font></b></summary>

It's better to use a mapping, because it's cheaper to check an allowance, and the array can lead to a DOS attack if the number of users is too large.

_Reference_: https://ethereum.stackexchange.com/a/2597/99105

</details>

<br>

<details open>
<summary><b><font size="+1">11. Why shouldn’t tx.origin be used for authentication?</font></b></summary>

This is because if the contract the user is calling is malicious - the malicious contract can act on behalf of the initial caller, but this will not happen if you use `msg.sender` instead, because in this situation the caller would be the malicious contract itself, not the user.

_Reference_: https://solidity-by-example.org/hacks/phishing-with-tx-origin/

</details>

<br>
<details open>
<summary><b><font size="+1">12. What hash function does Ethereum primarily use?</font></b></summary>

Keccak-256

_Reference_: https://www.oreilly.com/library/view/mastering-ethereum/9781491971932/ch04.html#:~:text=Ethereum%20uses%20the%20Keccak%2D256,Institute%20of%20Science%20and%20Technology.

</details>

<br>

<details open>
<summary><b><font size="+1">13. How much is 1 gwei of Ether?</font></b></summary>

1 \* 10^-9 | 0.000000001 | 1 / 1,000,000,000

_Reference_: https://docs.soliditylang.org/en/v0.8.24/units-and-global-variables.html#ether-units

</details>

<br>

<details open>
<summary><b><font size="+1">14. How much is 1 wei of Ether?</font></b></summary>

1 \* 10^-18 | 0.000000000000000001 | 1 / 1,000,000,000,000,000,000

_Reference_: https://docs.soliditylang.org/en/v0.8.24/units-and-global-variables.html#ether-units

</details>

<br>

<details open>
<summary><b><font size="+1">14. How much is 1 wei of Ether?</font></b></summary>

1 \* 10^-18 | 0.000000000000000001 | 1 / 1,000,000,000,000,000,000

_Reference_: https://docs.soliditylang.org/en/v0.8.24/units-and-global-variables.html#ether-units

</details>

<br>

<details open>
<summary><b><font size="+1">15. What is the difference between assert and require?</font></b></summary>

`assert` is usually used to check for internal errors (e.g. invariants), since this call is also used natively in the Solidity compiler itself, and also asserting panic errors should not happen in a well-tested contract, otherwise you have a bug in it. The `require` keyword is usually used to check for errors in user input/actions.

_Reference_: https://docs.soliditylang.org/en/v0.8.24/control-structures.html#panic-via-assert-and-error-via-require

</details>

<br>

<details open>
<summary><b><font size="+1">16. What is a flash loan?</font></b></summary>

Flashloan is a DeFi operation where you can borrow some tokens for the time of executing a single transaction and return those tokens in the same transaction (most of the time with some fees on top).

_Reference_: https://docs.aave.com/faq/flash-loans

</details>

<br>

<details open>
<summary><b><font size="+1">17. What is the check-effects pattern?</font></b></summary>

Check-Effects (and Interactions) is a structural pattern of code that allows you to avoid some cases of `reentrancy`, because first you do all the necessary checks, then you change a local state, and only then you interact with other contracts, otherwise you could be open to `reentrancy` attacks.

_Reference_: https://docs.soliditylang.org/en/latest/security-considerations.html#reentrancy

</details>

<br>

<details open>
<summary><b><font size="+1">18. What is the minimum amount of Ether required to run a solo staking node?</font></b></summary>

32 ETH.

_Reference_: https://ethereum.org/en/staking/

</details>

<br>

<details open>
<summary><b><font size="+1">19. What is the difference between fallback and receive?</font></b></summary>

The `receive` function is only triggered when an ETH event is received (with empty calldata), but the `fallback` function is triggered at any time if you call some data that didn't exist in the contract's ABI. And to make these functions work, you need to specify them explicitly.

_Reference_: https://docs.soliditylang.org/en/v0.8.24/contracts.html#receive-ether-function

</details>

<br>

<details open>
<summary><b><font size="+1">20. What is reentrancy?</font></b></summary>

Reentrancy is a type of attack where the attacker re-enters your function and performs repetitive actions without any constraints (this action could be updating the state of the contract/draining tokens/creating votes and so on). Reentrancy is usually performed in functions where external interactions occur before the local state changes.

_Reference_: https://docs.soliditylang.org/en/latest/security-considerations.html#reentrancy

</details>

<br>

<details open>
<summary><b><font size="+1">21. As of the Shanghai upgrade, what is the gas limit per block?</font></b></summary>

30 million gas.

_Reference_: https://ethereum.org/en/developers/docs/gas/#block-size

</details>

<br>

<details open>
<summary><b><font size="+1">22. What prevents infinite loops from running forever?</font></b></summary>

There's a maximum cap for executing a transaction, and because the transaction requires an infinite amount of gas to execute - it can't be executed in the Ethereum ecosystem because the block has a cap of 30M gas per block.

_Reference_: https://ethereum.org/en/developers/docs/gas/#block-size

</details>

<br>

<details open>
<summary><b><font size="+1">23. What is the difference between tx.origin and msg.sender?</font></b></summary>

`tx.origin` - initial user address that started execution of the transaction, `msg.sender` address that called current function, it can be another contract for example.

_Reference_: https://docs.soliditylang.org/en/v0.8.24/cheatsheet.html#block-and-transaction-properties

</details>

<br>

<details open>
<summary><b><font size="+1">24. How do you send Ether to a contract that does not have payable functions, or a receive or fallback?</font></b></summary>

You can do this using the `selfdestruct` operation, because when the contract is destroyed all its value would be sent to the specified address.

_Reference_: https://docs.soliditylang.org/en/v0.8.24/introduction-to-smart-contracts.html#deactivate-and-self-destruct

</details>

<br>

<details open>
<summary><b><font size="+1">25. What is the difference between view and pure?</font></b></summary>

`view` functions can read contract states, `pure` functions cannot, they can only use the input data provided.

_Reference_: https://docs.soliditylang.org/en/v0.8.24/contracts.html#state-mutability

</details>

<br>

<details open>
<summary><b><font size="+1">26. What is the difference between transferFrom and safeTransferFrom in ERC721?</font></b></summary>

`safeTransferFrom` checks if the receiver is a contract and if it is a contract - it requires it to implement the `IERC721Receiver` interface, so you won't send your NFT to the contract without any way of getting it back, just `transferFrom` doesn't do this check.

_Reference_: https://docs.openzeppelin.com/contracts/4.x/api/token/erc721#IERC721-safeTransferFrom-address-address-uint256-

</details>

<br>

<details open>
<summary><b><font size="+1">27. How can an ERC1155 token be made into a non-fungible token?</font></b></summary>

It's possible to set the maximum amount of each token to 1, so that each token has only 1 copy of itself. This can be done by setting the number of token copies when minting the token.

_Reference_: https://docs.openzeppelin.com/contracts/4.x/api/token/erc1155#ERC1155-_mint-address-uint256-uint256-bytes-

</details>

<br>

<details open>
<summary><b><font size="+1">28. What is access control and why is it important?</font></b></summary>

Access control is a restriction mechanism that ensures that only users with certain roles/responsibilities can call some of the functions. For example, you don't want your users to have access to the `mint' function, because they can just mint a lot of tokens for themselves, defeating the purpose of NFT collection.

_Reference_: https://docs.openzeppelin.com/contracts/2.x/access-control

</details>

<br>

<details open>
<summary><b><font size="+1">29. What does a modifier do?</font></b></summary>

Modifiers allow you to check some function call conditions before a function is actually executed.

_Reference_: https://docs.soliditylang.org/en/v0.8.24/contracts.html#function-modifiers

</details>

<br>

<details open>
<summary><b><font size="+1">29. What does a modifier do?</font></b></summary>

Modifiers allow you to check some function call conditions before a function is actually executed.

_Reference_: https://docs.soliditylang.org/en/v0.8.24/contracts.html#function-modifiers

</details>

<br>

<details open>
<summary><b><font size="+1">30. What is the largest value a uint256 can store?</font></b></summary>

2^256 - 1 (-1 because 1 space for the symbol)

_Reference_: https://ethereum.stackexchange.com/questions/58981/what-is-the-maximum-value-an-int-and-uint-can-store

</details>

<br>

<details open>
<summary><b><font size="+1">31. What is variable and fixed interest rate?</font></b></summary>

Fixed interest rate - remains the same for the whole period (of loan for example), Variable interest fixed rate - can change during the period. Variable rates involve more risks, but they can save you more money or you will lose more money if some of the conditions would change (like economic ones or some internal policies).

_Reference_: https://www.investopedia.com/ask/answers/07/fixed-variable.asp

</details>

<br>

## Medium

<details open>
<summary><b><font size="+1">1. What is the difference between transfer and send? Why should they not be used?</font></b></summary>

`transfer` throws an error on failure, `send` returns false on failure. It's better to use `call` because `transfer` and `send` have hardcoded 2300 gas and if some of the EVM opcodes start using more gas - all transfers and calls might not work anymore.

_Reference_: https://docs.soliditylang.org/en/v0.8.24/cheatsheet.html#members-of-address, https://consensys.io/diligence/blog/2019/09/stop-using-soliditys-transfer-now/

</details>

<br>

<details open>
<summary><b><font size="+1">2. How do you write a gas-efficient for loop in Solidity?</font></b></summary>

```js
uint256 length = array.length;
for(uint256 i; i < length;){
 unchecked{++i}
}
```

_Reference_: https://gist.github.com/grGred/9bab8b9bad0cd42fc23d4e31e7347144#for-loops-improvement

</details>

<br>

<details open>
<summary><b><font size="+1">3. What is a storage collision in a proxy contract?</font></b></summary>

Storage collision is a mechanism of proxy contracts when storage states from the source contract collide with the new proxy contract and the memory states are passed on to the new contract. Small example: we have a contract with the first variable uint256 a = 3; if we are going to update the proxy and the first state variable of the proxy is also uint256 - then this variable will also store the number "3", and that's why it's important not to change the order of states when dealing with proxy updates.

_Reference_: https://ethereum-blockchain-developer.com/110-upgrade-smart-contracts/06-storage-collisions/

</details>

<br>

<details open>
<summary><b><font size="+1">4. What is the difference between abi.encode and abi.encodePacked?</font></b></summary>

`abi.encode` simply encodes the arguments to `bytes32` format (if the value is not big enough for `bytes32` it will be adjusted with zeros), `abi.encodePacked` encodes all the values compactly without filling empty bytes with zeros, and allows to encode multiple values in one `bytes32` slot.

_Reference_: https://docs.soliditylang.org/en/v0.8.24/abi-spec.html#non-standard-packed-mode

</details>

<br>

<details open>
<summary><b><font size="+1">5. uint8, uint32, uint64, uint128, uint256 are all valid uint sizes. Are there others?</font></b></summary>

Yes, for example uint16, uint40, uint80, because uint type has a step of 8.

_Reference_: https://docs.soliditylang.org/en/v0.8.24/grammar.html#a4.SolidityLexer.UnsignedIntegerType

</details>

<br>

<details open>
<summary><b><font size="+1">6. What changed with block.timestamp before and after proof of stake?</font></b></summary>

Before the merge, `block.timestamp` could be manipulated by miners, but after the merge, the block is mined exactly every 12 seconds, so `block.timestamp` is predictable.

_Reference_: https://ethereum.stackexchange.com/questions/135445/miner-modifiability-of-block-timestamp-after-the-merge

</details>

<br>

<details open>
<summary><b><font size="+1">7. What is frontrunning?</font></b></summary>

Frontrunning is a method of placing your transaction ahead of some targeted transaction, often the purpose of frontrunning is to make a profit. For example: Bot sees that some whale is buying a large amount of some token (and it will defintely drive the price up because there would be less liquidity of that token in some pool or market), so it sends its own buy transaction with higher gas because it wants to buy tokens for lower price. Then the bot can sell those tokens at a higher price after the whale's buy transaction, because the price has gone up. This is called a Sanwich attack.

_Reference_: https://support.uniswap.org/hc/en-us/articles/19387081481741-What-is-a-sandwich-attack

</details>

<br>

<details open>
<summary><b><font size="+1">8. What is a commit-reveal scheme and when would you use it?</font></b></summary>

Commit-reveal scheme is a technique used to protect against frontrunning, where you upload some sensitive value to the smart contract in an encrypted format, and then reveal it using some kind of hash that verifies that you actually put that value in and not some other value. Also, commit-reveal schemes often have logic to close commits for some time, so that frontrunners cannot commit any useful data in the last few seconds. One of the use-cases might be an implementation of the rock-paper-scissors game.

_Reference_: https://medium.com/coinmonks/commit-reveal-scheme-in-solidity-c06eba4091bb

</details>

<br>

<details open>
<summary><b><font size="+1">9. Under what circumstances could abi.encodePacked create a vulnerability?</font></b></summary>

If the values that you are trying to encode are dynamic arrays - this could affect the end result, for example `abi.encodePacked([a,b], [c,d])` would have the same hash as a `abi.encodePacked([a,b,c], [d])`.
_Reference_: https://swcregistry.io/docs/SWC-133/

</details>

<br>
<details open>
<summary><b><font size="+1">10. How does Ethereum determine the BASEFEE in EIP-1559?</font></b></summary>

It's based on network demand and the fullness of the block, if the block was full before - baseFee would go up (it can't go higher/lower than 12.5% compared to the previous one).

_Reference_: https://www.blocknative.com/blog/eip-1559-fees

</details>

<br>
