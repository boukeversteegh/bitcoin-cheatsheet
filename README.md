Bitcoin Cheatsheet [DRAFT]
====
Author: *Bouke Versteegh*

<a id="toc">Table of Contents</a>
---


**Bitcoin**:
  - [Bitcoin](#bitcoin)
  - [Blockchain](#blockchain)
  - [Blocks](#blocks)
  - [Transactions](#transactions)
  - [Confirmations](#confirmations)
  - [Proof of Work](#proof-of-work)
  - [Mining](#mining)
  - [Miner](#miner)
  - [Addresses](#addresses)
  - [Vanity address](#vanity-address)
  - [Difficulty](#difficulty)
  - [Base58Check](#base58check)


**Computer Terms**:
  - [Nonce](#nonce)
  - [Hash](#hash)
  - [Public-Key Cryptography](#public-key-cryptography)
    - [Public Key](#public-key)
    - [Private Key](#private-key)
  - [QR-code](#qr-code)


<a id="bitcoin">Bitcoin</a>
---------------------------
Bitcoin is a digital decentralized currency based on cryptography and mathematics.

Function:
- Allow people to hold and transfer value without a trusted third party
- Offer a better alternative to Fiat currency more suitable for this digital age.

Features:
  - electronic &mdash; use it online, you can back it up, on your phone
  - decentralized &mdash; not controlled by anyone
  - global &mdash; usable all over the world
  - deflationary &mdash; cannot be printed by anyone at will
  - irreversible &mdash; no-one can reclaim coins they have sent you
  - proof of ownership &mdash; you can prove to others that you own a certain amount of money
  - 100% sound money in accordance with Austrian Economics:
    - fungible &mdash; every coin is the same
    - portable &mdash; can easily be sent to anywhere on earth
    - durable &mdash; bitcoins don't expire
    - divisible &mdash; bitcoins can be spent in fractions up till 1 millionth
    - rare &mdash; only 21 million bitcoin will every be created
    - uncounterfeitable &mdash; mathematically impossible
    - desirable &mdash; due to it's utility and scarcity, people want them
    - unconsumable &mdash; bitcoin will never change its role as currency
  
<a id="blockchain">Blockchain</a>
---------------------------------
*Not to be confused with [blockchain.info](#blockchain.info).*

The **blockchain** is the core of Bitcoin. It is the *public ledger* that stores all bitcoin transactions in an independently verifiable way.

- Function:
  - Record the entire history of Bitcoin [transactions](#transactions)
  - Make sure everyone agrees on the transaction history
  - Solves the age-old problem of creating consensus without trust
- Features:
  - Independently verifiable
  - The blockchain contains:
    - [Genesis Block](#genesis-block) &mdash; The first block in the blockchain
    - All [blocks](#blocks) after it

<a id="blocks">Blocks</a>
---

**Blocks** in the [blockchain](#blockchain) group multiple [transactions](#transactions) together. Each block points back to the previous block, forming a long chain until the first block ([Genesis block](#genesis-block)). Blocks serve as checkpoints in the transaction-history that everyone agrees on. If there are multiple competing blocks the chain will split, and whichever chain becomes longer will win.

Function:
  - Store valid [transactions](#transactions)
  - Creating new [bitcoins](#bitcoins)
  - *Checkpoints*

Features:
  - a block contains:
    - multiple [transactions](#transactions) &mdash; *usually a few hundred*
    - a [nonce](#nonce) &mdash; *a meaningless random number*
    - a [reference](#prevblock) to a previous block
    - a [hash](#hash) of the above
    - the [difficulty](#difficulty) for the next block
  - Each block rewards the issuer with some number of Bitcoins, depending on the blockheight
  - **Block Size**

Mechanism:
  - To be accepted by the network, the block must be valid.
  - To be valid:
    - the referred previous block must also be valid
    - all transactions in the block must be valid
    - the hash must match the transactions/nonce/reference data
    - the hash must start with enough zeros, determined by the [difficulty](#difficulty)


<a id="transactions">Transactions</a>
---
**Transactions** are instructions to the Bitcoin-network to send bitcoins to other addresses, similar to *checks* in traditional banking. Transactions are issued by the sender, and verified by [miners](#miner). Transactions are not final until they are [confirmed](#confirmations) by the Bitcoin-network.

Function:
- Moving [bitcoins](#bitcoins) from one [address](#address) to another
- Modifying the [public ledger](#ledger)

Features:
- a transaction contains:
  - a [transaction-id](#txid)
  - zero or more [outputs](#outputs) &mdash; *which [addresses](#addresses) to send bitcoins and the amount*
  - one or more [inputs](#inputs) &mdash; *which bitcoins to use*
  
- transactions are created by bitcoin [clients](#clients)
- [clients](#clients) relay transactions to eachother and to [miners](#miners)

<a id="confirmations">Confirmations</a>
---
Bitcoin-software often shows the **confirmation** status of a [transaction](#transactions). An unconfirmed transaction means that it wasn't yet recorded in the [blockchain](#blockchain). The first confirmation happens when a [miner](#miners) includes the transaction in a [block](#blocks) and publishes the block and the [proof of work](#proof-of-work) to the network. The second confirmation is when another block is added to the blockchain, etcetera.

<a id="proofofwork">Proof of work</a>
-------------
In computer science and mathematics, a **proof of work** (POW) is a solution to a difficult problem that is easily and independently verifiable. Blocks require a *proof of work* to be accepted by the network. This limits the rate at which [blocks](#blocks) can be created. Through [difficulty](#difficulty), the average creation rate is maintained at 10 minutes, regardless of the available processing power in the network.

A block must contain a [hash](#hash) of the data in the block and a random [nonce](#nonce)-value, and this hash must begin with many zeros. The hash cannot be controlled directly, but by trying out many different nonce-values, a nonce that generates a valid hash can be found. The *proof of work* is the nonce in combination with the rest of the block.

Function:
- Making sure [blocks](#blocks) are added to the chain at regular intervals
- By extension, controlling Bitcoin inflation
- Randomizing who will get new [bitcoins](#bitcoin)
- Creating a delay between blocks, so they have time to spread through the network before the next one is found, and making sure everyone is up-to-date

Features:
- Hashing a block+nonce can be done very fast
- Anyone can hash the block and its nonce, to verify that the hash is valid
- The number of zero's to be found is controlled by the [difficulty](#difficulty)

Mechanism:
  - A block's [hash](#hash) depends on the [transactions](#transactions) and [nonce](#nonce)
  - The [nonce](#nonce) can be chosen by the miner
  - The block is re-hashed with random nonces, until it generates a hash with enough `0000`'s.

<a id="address">Addresses</a>
---
An **address** is where you send bitcoins, similar to how you use an *email-address* to send emails to.

A bitcoin address looks like:  
> `1LBmhMXR28xWJeQoZBU53w9EsFKnbn6Nqq`

and can also be shown as a [QR-code](#qrcode).

> ![qr](https://blockchain.info/qr?data=1LBmhMXR28xWJeQoZBU53w9EsFKnbn6Nqq&size=100)

Function:
- Distinguish between different accounts that can hold a bitcoin balance
- Establish ownership of bitcoin balances

Features:
- Generated by Bitcoin clients
- No central authority is needed to create an address
- Can be created offline
- Creating addresses is instant and free
- There is no limit to how many addresses you can own
- Contains error-checking mechanism, can't type it wrong  
  The chance of typing a wrong but valid address by accident is:  
1 in 232, that is, approximately 1 in 4.29 billion
- Generated by [public-key cryptography](#public-key-cryptography)
- The owner can mathematically proof to have created that address
- Cannot be counterfeited (takes millions of years to counterfeit an address)
- It is 27-34 characters long and sensitive to capital letters
- It is possible to find an address with words in them. This is called a [vanity address](#vanity-address).

Mechanism:
- Generation:
  - The [wallet](#wallet) generates a [private key](#private-key), and remembers it.
  - From the private key, the [public key](#public-key) is derived.
  - The public key is [hashed](#hash), and an error checking code is appended
  - This is then encoded in [Base58Check](#base58check) and becomes the address.
- Encoding:
  
  - It starts with a `1` or a `3`
  - It contains numbers, letters and capital letters
  - It includes only distinguishable characters, so `l/i`, `0/O` are excluded.
  - It is encoded using [Base58Check](#base58check)


<a id="vanity-address">Vanity Address</a>
----

<a id="block-nonce">Nonce</a>
---
In computer science, a **nonce** is a meaningless number. It is often added to data to make sure it's unpredictable or unique. In [Bitcoin](#bitcoin), nonces are used in:

- [Blocks](#blocks)
- Signatures(?)



<a id="difficulty">Difficulty</a>
-----

Function
- Maintain a fixed block creation rate, regardless of increases in computer speed or network size
- (todo)

<a id="hash">Hash</a>
---
In computer science, a **hash** is a string of characters that is uniquely derived from a piece of data. The same input always leads to the same hash, but it is impossible to calculate the input data from the hash. 

Example data and their hashes:

`This is a piece of text!` &mdash; `34f79yw587w94r7q0243ry057yrw935fw5hk`  
`This is a piece of text.` &mdash; `fodjxc98syfxeos4ifs3847rt9q34arfleuh`

