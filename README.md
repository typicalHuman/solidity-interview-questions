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
<details open>
<summary><b><font size="+1">11. What is the difference between a cold read and a warm read?</font></b></summary>

The first time you read a variable from memory - it's a cold read, all reads after the first are warm.

_Reference_: https://ethereum.stackexchange.com/a/149670/99105

</details>

<br>
<details open>
<summary><b><font size="+1">12. How does an AMM price assets?</font></b></summary>

Based on the `x*y=k` formula, the price is basically based on the reserves of the tokens, if you had a pool of 30k USDT and 10 ETH this means that the correlation is 30,000/10 = 3000 USDT per ETH, if the reserve of USDT or ETH would change and it won't be equal to the actual price - arbitrage bots will use this opportunity to regulate the price (because if your asset costs more or less than a market price - bots can abuse it in order to get profit).

_Reference_: https://academy.binance.com/en/articles/what-is-an-automated-market-maker-amm

</details>

<br>
<details open>
<summary><b><font size="+1">13. What is a function selector clash in a proxy and how does it happen?</font></b></summary>

Function clashing is an exploit that allows some functions to be executed through the proxy that the user didn't intend to execute, by creating a function with the same signature. For example, we have a malicious contract owner (who can upgrade the proxy), if he creates a function on the proxy with the exact signature that the user will use later - it will be executed instead of the function that the user wanted to execute.

_Reference_: https://forum.openzeppelin.com/t/beware-of-the-proxy-learn-how-to-exploit-function-clashing/1070

</details>

<br>

<details open>
<summary><b><font size="+1">14. What is the effect on gas of making a function payable?</font></b></summary>

Actually, all functions are payable by default in EVM, so not specifying the `payable` keyword will add opcodes to reverse execution if the `msg.value` is greater than zero. So the payable function is cheaper than the non-payable one.

_Reference_: https://coinsbench.com/solidity-payable-vs-regular-functions-a-gas-usage-comparison-b4a387fe860d

</details>

<br>

<details open>
<summary><b><font size="+1">15. What is a signature replay attack?</font></b></summary>

The signature replay attack is an attack that allows some functionality to be performed multiple times using a signature, even if it was designed to be performed once, or allows someone else to perform functionality using the other person's signature. It can be solved by using the `msg.sender` check and also adding `nonce` logic to the code so that the signature can't be used more than once.

_Reference_: https://solidity-by-example.org/hacks/signature-replay/

</details>

<br>

<details open>
<summary><b><font size="+1">16. What is gas griefing?</font></b></summary>

Gas griefing is an attack technique that allows a malicious user to prevent users from executing transactions when there's no external call success check. It can be done by providing just enough gas to execute a top-level transaction, and then censoring the data so that the original user can't execute it later.

_Reference_: https://swcregistry.io/docs/SWC-126/

</details>

<br>
<details open>
<summary><b><font size="+1">17. How would you design a game of rock-paper-scissors in a smart contract such that players cannot cheat?</font></b></summary>

It can be done by using commit-reveal scheme.

_Reference_: https://github.com/ojroques/ethereum-rockpaperscissors

</details>

<br>
<details open>
<summary><b><font size="+1">18. What is the free memory pointer and where is it stored?</font></b></summary>

The free memory pointer is the pointer that shows where the last occupied byte of memory is, it's used when you create a new variable for example - it shows where to store this new variable.

_Reference_: https://ethereum.stackexchange.com/questions/137729/opcode-free-memory-pointer-and-offset

</details>

<br>
<details open>
<summary><b><font size="+1">19. What function modifiers are valid for interfaces?</font></b></summary>

All declared functions must be `external`

_Reference_: https://solidity-by-example.org/interface/

</details>

<br>
<details open>
<summary><b><font size="+1">20. What is the difference between memory and calldata in a function argument?</font></b></summary>

`memory` parameters are mutable and `calldata` parameters are immutable.

_Reference_: https://ethereum.stackexchange.com/questions/74442/when-should-i-use-calldata-and-when-should-i-use-memory

</details>

<br>

<details open>
<summary><b><font size="+1">21. Describe the three types of storage gas costs.</font></b></summary>

1. Store a new variable: 20,000 gas
2. Updating state: 5,000 gas
3. Reading state: 200 gas

_Reference_: https://hacken.io/discover/solidity-gas-optimization/

</details>

<br>

<details open>
<summary><b><font size="+1">22. Why shouldn’t upgradeable contracts use the constructor?</font></b></summary>

Because the constructor is called only once, and this code is not part of the runtime bytecode of a deployed smart contract. So this context won't be passed to the proxy contract. So it's better to use an `initializer` method instead.

_Reference_: https://docs.openzeppelin.com/upgrades-plugins/1.x/proxies#the-constructor-caveat

</details>

<br>
<details open>
<summary><b><font size="+1">23. What is the difference between UUPS and the Transparent Upgradeable Proxy pattern?</font></b></summary>

UUPS and Transparent Upgradeable Proxy are both transparent proxy patterns (https://blog.openzeppelin.com/the-transparent-proxy-pattern), but UUPS is cheaper because proxy management functions for proxy are not being duplicated in the proxy implementations.

_Reference_: https://docs.openzeppelin.com/contracts/4.x/api/proxy#transparent-vs-uups

</details>

<br>
<details open>
<summary><b><font size="+1">24. If a contract delegatecalls an empty address or an implementation that was previously self-destructed, what happens? What if it is a regular call instead of a delegatecall?</font></b></summary>

It will return true, because even though the storage is empty for that address, the EVM still recognizes the existence of this address and decides that the `call`/`delegatecall` was successful.

_Reference_: https://medium.com/@solidity101/understanding-contract-delegation-in-solidity-handling-selfdestruct-scenarios-%EF%B8%8F-37fe2f4198ee

</details>

<br>
<details open>
<summary><b><font size="+1">25. What danger do ERC777 tokens pose?</font></b></summary>

The killer feature of the ERC777 standard is the receive hook, which allows you to react to the incoming tokens, similar to onERC721Received for NFT. This can be handy, but it also opens up the possibility of reentrancy attacks by giving the attacker another way to re-enter the contract.

_Reference_: https://forum.openzeppelin.com/t/can-sombody-explain-why-erc777-was-removed/38105

</details>

<br>
<details open>
<summary><b><font size="+1">26. According to the solidity style guide, how should functions be ordered?</font></b></summary>

- constructor
- receive function (if exists)
- fallback function (if exists)
- external
- public
- internal
- private

Within a grouping, place the `view` and `pure` functions last.

_Reference_: https://docs.soliditylang.org/en/v0.8.24/style-guide.html#order-of-functions

</details>

<br>
<details open>
<summary><b><font size="+1">27. According to the solidity style guide, how should function modifiers be ordered?</font></b></summary>

The modifier order for a function should be:

- Visibility (public,private,external,internal)
- Mutability (pure,view) + payable
- `virtual`/`override`
- Custom modifiers

_Reference_: https://docs.soliditylang.org/en/v0.8.24/style-guide.html#function-declaration

</details>

<br>

<br>
<details open>
<summary><b><font size="+1">28. What is a bonding curve?</font></b></summary>

AMM mechanism for checking correlation between token supplies and calculating relative price for them.

![Curve](./images/boundingCureve.avif)

_Reference_: https://iq.wiki/wiki/bonding-curve

</details>

<br>
<details open>
<summary><b><font size="+1">29. How does safeMint differ from mint in the OpenZeppelin ERC721 implementation?</font></b></summary>

`safeMint` checks 2 things: 1. the existence of `tokenId` (it won't mint the same token twice), 2. if `to` is a contract - it should implement the `onERC721Received` function. `mint` function doesn't check these conditions.

_Reference_: https://docs.openzeppelin.com/contracts/3.x/api/token/erc721#ERC721-_safeMint-address-uint256-

</details>

<br>
<details open>
<summary><b><font size="+1">30. What keywords are provided in Solidity to measure time?</font></b></summary>

- 1 == 1 seconds
- 1 minutes == 60 seconds
- 1 hours == 60 minutes
- 1 days == 24 hours
- 1 weeks == 7 days

_Reference_: https://docs.soliditylang.org/en/v0.8.24/units-and-global-variables.html#time-units

</details>

<br>

<details open>
<summary><b><font size="+1">31. What is a sandwich attack?</font></b></summary>

Inserting a transaction before and after a targeted transaction in order to make a profit. Example: Bot sees that some whale is buying a large amount of some token (and it will defintely drive the price up because there would be less liquidity of that token in some pool or market), so it sends its own buy transaction with higher gas because it wants to buy tokens for lower price. Then the bot can sell those tokens at a higher price after the whale's buy transaction, because the price has gone up. This is called a Sanwich attack.

_Reference_: https://support.uniswap.org/hc/en-us/articles/19387081481741-What-is-a-sandwich-attack

</details>

<br>
<details open>
<summary><b><font size="+1">32. If a delegatecall is made to a function that reverts, what does the delegatecall do?</font></b></summary>

It will return `false` and won't revert the calling function.

_Reference_: https://docs.soliditylang.org/en/v0.8.24/security-considerations.html#call-stack-depth

</details>

<br>

<details open>
<summary><b><font size="+1">33. What is a gas efficient alternative to multiplying and dividing by a power of two?</font></b></summary>

You can shift right/left instead of division/multiplication. While the DIV opcode uses 5 gas, the SHR opcode only uses 3 gas.

_Reference_: https://betterprogramming.pub/solidity-gas-optimizations-and-tricks-2bcee0f9f1f2

</details>

<br>

<details open>
<summary><b><font size="+1">34. How large a uint can be packed with an address in one slot?</font></b></summary>

1 slot size = 32 bytes, address - 20 bytes, we have 12 free bytes - 8 \* 12 = 96, uint96.max = 79228162514264337593543950335

_Reference_: https://stackoverflow.com/questions/72752086/how-many-state-bytes-will-contract-address-variable-consume-in-solidity

</details>

<br>
<details open>
<summary><b><font size="+1">35. Which operations give a partial refund of gas?</font></b></summary>

1 slot size = 32 bytes, address - 20 bytes, we have 12 free bytes - 8 \* 12 = 96, uint96.max = 79228162514264337593543950335

_Reference_: https://stackoverflow.com/questions/72752086/how-many-state-bytes-will-contract-address-variable-consume-in-solidity

</details>

<br>
<details open>
<summary><b><font size="+1">36. What is ERC165 used for?</font></b></summary>

You can use it to check if the smart contract implements the interface and certain functions or not. It can be useful if you need to check if the contract is an ERC20 token or not. ERc165 uses `supportsInterface(bytes4 interfaceID)` for this purpose.

_Reference_: https://eips.ethereum.org/EIPS/eip-165

</details>

<br>

<details open>
<summary><b><font size="+1">37. If a proxy makes a delegatecall to A, and A does address(this).balance, whose balance is returned, the proxy's or A?</font></b></summary>

`address(this)` will return the address of the proxy, so it will return the proxy's balance.

_Reference_: https://forum.openzeppelin.com/t/proxy-contract-what-is-msg-sender-and-address-this-in-logic-contract/25824/3

</details>

<br>

<details open>
<summary><b><font size="+1">38. What is a slippage parameter useful for?</font></b></summary>

Slippage is a limit that shows how much the price could change during the trade. It's used in cases where liquidity is very volatile and you don't want to buy tokens at a much higher price or sell them at a much lower price than you wanted.

_Reference_: https://uniswapv3book.com/milestone_3/slippage-protection.html#:~:text=Slippage%20is%20a%20very%20important,when%20the%20swap%20is%20executed.

</details>

<br>

<details open>
<summary><b><font size="+1">39. What does ERC721A do to reduce mint costs? What is the tradeoff?</font></b></summary>

ERC721A is a new implementation of ERC721 pattern but with some upsides and downsides:
Upsides:

- mints are much cheaper

Downsides:

- transfers are more expensive

Mint optimization technique: it doesn't update all default mappings with info about token owner on each mint, it does it once during batch mint. Because of this, you don't have information about the tokenId owner, so you have to iterate the array first to find the owner of the token.

_Reference_: https://www.alchemy.com/blog/erc721-vs-erc721a-batch-minting-nfts

</details>

<br>

<details open>
<summary><b><font size="+1">40. Why doesn't Solidity support floating point arithmetic?</font></b></summary>

One of the main reasons is the fact that fixed-point arithmetic is not very predictable and can lead to forks on different nodes, which is why EVM itself doesn't want to deal with it, but Solidity has started to implement floating-point numbers using the same technique used in the ERC20 tokens - https://docs.soliditylang.org/en/develop/types.html#fixed-point-numbers.

_Reference_: https://ethereum.stackexchange.com/questions/87234/why-was-support-for-floating-point-numbers-not-natively-added-to-solidity-or-et

</details>

<br>
<details open>
<summary><b><font size="+1">41. What is TWAP?</font></b></summary>

TWAP (Time-Weighted Average Price) - is a pricing algorithm used to calculate the price of an asset for a period of time. It can be done by taking different prices at equally distant points in time and then dividing the sum of them by the length of the points:

For example, imagine we wanted to calculate the TWAP of an asset over one minute using 15-second price point intervals. If the prices were $100 at zero seconds, $102 at 15 seconds, $101 at 30 seconds, $98 at 45 seconds, and $103 at 60 seconds, then to calculate the TWAP we would sum all price points (100, 102, 101, 99, 103) and then divide them by the number of timepoints (five). In this example, the TWAP is $101.

_Reference_: https://chain.link/education-hub/twap-vs-vwap#:~:text=TWAP%20stands%20for%20%E2%80%9Ctime%2Dweighted,be%20used%20in%20other%20protocols.

</details>

<br>
<details open>
<summary><b><font size="+1">41. How does Compound Finance calculate utilization?</font></b></summary>

Utilization - percentage of actually borrowed funds in the lending pool compared to the total funds available for borrowing.

```js
Utilization = TotalBorrows / TotalSupply;
```

_Reference_: https://docs.compound.finance/interest-rates/#get-utilization

</details>

<br>
<details open>
<summary><b><font size="+1">42. If a delegatecall is made to a function that reads from an immutable variable, what will the value be?</font></b></summary>

It will return the value of immutable variable.

_POC_:

```js
// SPDX-License-Identifier: MIT
pragma solidity 0.8.20;
contract FirstContract {
    function doDelegate(address contr) external returns(bytes memory){
        (, bytes memory data) = address(contr).delegatecall(abi.encodeWithSignature("doCall()"));
        return data; // 0x00..1e = 30
    }

}

contract secondContract{
    uint256 immutable VALUE = 30;

    function doCall() external returns(uint256){
        return VALUE;
    }
}
```

</details>

<br>
<details open>
<summary><b><font size="+1">44. What is a fee-on-transfer token?</font></b></summary>

Fee-on-transfer token is a type of ERC20 token that takes a small fee after tokens are transferred.

_Reference:_ https://help.1inch.io/en/articles/5651059-what-is-a-fee-on-transfer-token

</details>

<br>
<details open>
<summary><b><font size="+1">45. What is a rebasing token?</font></b></summary>

Rebase token is a type of ERC20 token that changes its total supply (by burning/minting tokens) to maintain a peg to a certain value, they are very similar to stablecoins in idea but not in implementation.

_Reference:_ https://www.zenledger.io/blog/what-are-rebase-tokens-how-are-they-taxed/#:~:text=Rebase%20tokens%20are%20similar%20to,circulation%20or%20minting%20new%20tokens.

</details>

<br>

## Hard

<details open>
<summary><b><font size="+1">1. How does fixed point arithmetic represent numbers?</font></b></summary>

It reserves one part of the bits to the integer part and another to the fractional part. IIIII.FFFFF

_Reference:_ https://stackoverflow.com/a/7524916/12460603

</details>

<br>
<details open>
<summary><b><font size="+1">2. What is an ERC20 approval frontrunning attack?</font></b></summary>

If you set an allowance for an address to spend your tokens, you may be frontrun if you try to decrease or increase the allowance in the future. If the address sees your transaction in pending, it could frontrun you by spending all the tokens and then receiving another allowance that you just sent.

_Reference:_ https://www.adrianhetman.com/unboxing-erc20-approve-issues/

</details>

<br>
<details open>
<summary><b><font size="+1">3. What opcode accomplishes address(this).balance?</font></b></summary>

`SELFBALANCE` - Get balance of currently executing account

_Reference:_ https://www.evm.codes/#47?fork=shanghai

</details>

<br>
<details open>
<summary><b><font size="+1">4. How many arguments can a solidity event have?</font></b></summary>

Non-anonymous events can have up to 3 parameters and anonymous events can have up to 4 parameters.

_Reference:_ https://docs.soliditylang.org/en/v0.8.24/abi-spec.html#events

</details>

<br>

<details open>
<summary><b><font size="+1">5. What is an anonymous Solidity event?</font></b></summary>

Anonymous is an event type that doesn't store an event signature as the first parameter.

_Reference:_ https://docs.soliditylang.org/en/v0.8.24/cheatsheet.html#modifiers

</details>

<br>

<details open>
<summary><b><font size="+1">6. Under what circumstances can a function receive a mapping as an argument?</font></b></summary>

If the function is private or internal and also mapping parameter is from storage.

```js
// SPDX-License-Identifier: MIT
pragma solidity 0.8.20;
contract MappingContract {
   function doStuff(mapping(uint256 => uint256) storage _mapping) internal{} // will work
   function doStuff(mapping(uint256 => uint256) storage _mapping) external{} // will give you an error
}
```

_Reference:_ https://ethereum.stackexchange.com/a/7757/99105

</details>

<br>

<details open>
<summary><b><font size="+1">7. What is an inflation attack in ERC4626?</font></b></summary>

ERC4626 is the vault where users can deposit their tokens and get share tokens in return. When you deposit tokens via standard function - you will get some amount of share tokens, but if you will just send them to the contract - you will get nothing. So the attack is simple:

1. attacker sees a deposit from another user to the empty pool
2. attacker deposits 1 token and get in return 1 share
3. attacker deposits amount of token that the user is trying to deposit (10k for example)
4. user transaction executed and he deposits 10k tokens.
5. we have a formula: `shares_received = assets_deposited * totalSupply() / totalAssets();`. this means:

`shares_received = 10,000 * 1 / 10,001 => sharesToReceive = 0.99990000999` and because solidity doesn't support fixed point numbers - user won't receive any shares in the end.

_Reference:_ https://mixbytes.io/blog/overview-of-the-inflation-attack

</details>

<br>

<details open>
<summary><b><font size="+1">8. How many arguments can a solidity function have?</font></b></summary>

16, otherwise you will get "Stack is too deep" error.

_Reference:_ https://docs.soliditylang.org/en/v0.8.24/introduction-to-smart-contracts.html#storage-memory-and-the-stack

</details>

<br>

<details open>
<summary><b><font size="+1">9. How many storage slots does this use? uint64[] x = [1,2,3,4,5]? Does it differ from memory?</font></b></summary>

uint64 takes 16 bytes, 1 slot has 32 bytes.

1 slot for length

- # 3 slots for elements (1,2), (3,4), (5)
  4 slots in total

_Reference:_ https://docs.soliditylang.org/en/v0.8.24/introduction-to-smart-contracts.html#storage-memory-and-the-stack

</details>

<br>

<details open>
<summary><b><font size="+1">10. Prior to the Shanghai upgrade, under what circumstances is returndatasize() more efficient than push zero?</font></b></summary>

Before the Shangai upgrade it was cheaper to use the `RETURNDATASIZE` opcode (2 gas) to push 0 to the top of the stack than to use `PUSH1 0` (3 gas). With the Shangai upgrade EVM introduces a new opcode `PUSH0` which just pushes 0 to the top of the stack and costs 2 gas.

_Reference:_ https://eips.ethereum.org/EIPS/eip-3855

</details>

<br>