---
description: An overview of the network's contracts with descriptions and links
---

# Mix Consensus \(technical\)

Consensus is a fault-tolerant mechanism that is used in blockchain systems to achieve the necessary agreement on the single state of the network. Mix network is using a Delegated Proof of Stake \(DPoS\) consensus model, which may sound complex but it's not. DPoS consensus is a variation of Proof of Stake. In PoS there are a set of validators that are responsible for keeping the network updated and validating the network's state. They do this in turns, every validator has their turn in line. On their turn the validator updates the network's state, and the rest of the validators check that the update is valid.

Being a validator is technically complex. In addition to staking Mix, validators need to run specialist software and have 100% uptime hardware. To lower the bar and allow anyone to take part and ownership of the network, the DPoS consensus mechanism was introduced. With Delegated Proof of Stake consensus mechanism, a token holder can delegate his validation rights to a third-party validator who will perform the validation for them, while getting part of the reward according to the predefined agreement.

{% hint style="info" %}
All the contracts in this section are available on our [Github](https://github.com/fuseio/fuse-network/tree/master/contracts)
{% endhint %}

## [Consensus - 0x1c7DFFd9313A0f3f20518E88735932D02bef4F28](https://miexs.com/address/0x1c7DFFd9313A0f3f20518E88735932D02bef4F28)

This contract is responsible for handling the network DPos consensus. The contract stores the current validator set and chooses a new validator set at the end of each cycle. The logic for updating the validator set is to select a random snapshot from the snapshots taken during the cycle.

The snapshots are taken of pending validators, who are those which staked more than the minimum stake needed to become a network validator. Therefore the contract is also responsible for staking, delegating and withdrawing those funds.

Stake amount for a validator is the sum of staked and delegated amount to it's address.

This contract is based on `non-reporting ValidatorSet` [described in Parity Wiki](https://wiki.parity.io/Validator-Set.html#non-reporting-contract).

{% hint style="info" %}
minimum stake amount = 100,000 Mix token

cycle duration blocks = 1440 \(approximately 2 hours\)

snapshots taken per cycle = 10
{% endhint %}

## [Block Reward - 0x9ECEd53BE4EA8564E4dC6C6AfCB1d4374C5B5F14](https://miexs.com/address/0x63d4efed2e3da070247bea3073bcab896dff6c9b)

This contract is responsible for generating and distributing block rewards to the network validators according to the network specs \(5% yearly inflation\).

Another role of this contract is to call the snapshot/cycle logic on the Consensus contract

This contract is based on `BlockReward` [described in Parity Wiki](https://wiki.parity.io/Block-Reward-Contract).

## [Voting - 0x81368e7C4f2968A1C773CC427d61f0Af3d912bb3](https://miexs.com/address/0x81368e7C4f2968A1C773CC427d61f0Af3d912bb3)

This contract is responsible for opening new ballots and voting to accept/reject them. Ballots are basically offers to change other network contracts implementation.

Only network validators can open new ballots, everyone can vote on them, but only validators votes count when the ballot is closed.

Ballots are opened/closed on cycle end.

{% hint style="info" %}
max number of open ballots = 100

max number of open ballots per validator = 100 / number of validators

minimum ballot duration \(cycles\) = 2

maximum ballot duration \(cycles\) = 14
{% endhint %}

## [Proxy Storage](https://miexs.com/address/0x702030B337E484BfF60155e74B51f428567DbC31)

This contract is responsible for holding network contracts implementation addresses and upgrading them if necessary \(via voting\).

