# solidity-interview-questions (and answers)

Questions taken from - https://www.rareskills.io/post/solidity-interview-questions

## Easy

<details>
<summary><b><font size="+1">1. What is the difference between private, internal, public, and external functions?</font></b></summary>

`private` can only be used within the current contract, `internal` can also be used within derived contracts, `public` functions can be used inside and outside the current contract (by users and the contract itself), `external` functions can only be used by users.

_Reference_: https://docs.soliditylang.org/en/latest/contracts.html#state-variable-visibility

</details>

<br>

<details>
<summary><b><font size="+1">2. Approximately, how large can a smart contract be?</font></b></summary>

About 24,000 bytes and (4.7 million gas). According to EIP-170: In short, the point of this EIP is to minimize the overloading of nodes (especially light nodes) and to prevent possible DOS attacks.

_Reference_: https://docs.soliditylang.org/en/latest/cheatsheet.html#function-visibility-specifiers

</details>

<br>

<details>
<summary><b><font size="+1">3. What is the difference between create and create2?</font></b></summary>

`CREATE` is used in the default scenario when you deploy a smart contract via `new` for example. `CREATE2` is also used to deploy smart contracts, but it has a special parameter - `salt`, which allows you to predetermine the future address of the contract.

_Reference_: https://vinta.ws/code/solidity-create-vs-create2.html

</details>

<br>

<details>
<summary><b><font size="+1">4. What major change with arithmetic happened with Solidity 0.8.0?</font></b></summary>

More secure arithmetic operations without explicitly using the `SafeMath` library (preventing underflows and overflows).

_Reference_: https://docs.soliditylang.org/en/latest/080-breaking-changes.html

</details>

<br>

<details>
<summary><b><font size="+1">5. What special CALL is required for proxies to work?</font></b></summary>

`DELEGATECALL` because it allows you to pass all the call context to the proxy contract and also to keep the storage states.

_Reference_: https://eips.ethereum.org/EIPS/eip-1967

</details>

<br>
<details>
<summary><b><font size="+1">6. Prior to EIP-1559, how do you calculate the dollar cost of an Ethereum transaction?</font></b></summary>

It used a simple gas price auction system and this system had some downsides such as: highly volatile gas price and delays for users.

_Reference_: https://eips.ethereum.org/EIPS/eip-1559

</details>

<br>

<details>
<summary><b><font size="+1">7. What are the challenges of creating a random number on the blockchain?</font></b></summary>

Because blockchain is a fully open system it means you can simulate and predict almost everything on it and all attempts to create true RNG were failed so for RNG on blockchain builders usually use some oracles like - https://docs.chain.link/vrf.

_Reference_: https://www.sitepoint.com/solidity-pitfalls-random-number-generation-for-ethereum/

</details>

<br>

<details>
<summary><b><font size="+1">8. What is the difference between a Dutch Auction and an English Auction?</font></b></summary>

In an English auction, the auctioneer sets a base price and bidders compete to see who can offer a higher price. In a Dutch auction, it's the other way round - the auctioneer sets a high price and goes lower and lower until someone agrees to accept the price.

_Reference_: https://saylordotorg.github.io/text_introduction-to-economic-analysis/s21-auctions.html

</details>

<br>

<details>
<summary><b><font size="+1">9. What is the difference between transfer and transferFrom in ERC20?</font></b></summary>

`transfer` only transfers the amount of tokens from `msg.sender`. `transferFrom` uses an allowance system, so for example if you want the contract to use your ERC20 token you can set an allowance for it to use your tokens so it can send the tokens on your behalf: `transferFrom(you, someone, amount)`.

_Reference_: https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#IERC20-transferFrom-address-address-uint256-

</details>

<br>

<details>
<summary><b><font size="+1">10. Which is better to use for an address allowlist: a mapping or an array? Why?</font></b></summary>

It's better to use a mapping, because it's cheaper to check an allowance, and the array can lead to a DOS attack if the number of users is too large.

_Reference_: https://ethereum.stackexchange.com/a/2597/99105

</details>

<br>
