---
description: Becoming a Mix validator in a few simple steps
---

# Getting started as a validator

## Pre-requirements

In order to be a Mix validator, you first must see that you meet the pre-requirements:

* You know what it means to be a Mix validator - [Becoming a validator](how-to-become-a-validator.md#what-it-means-to-be-a-validator).
* You have at least 100k MIX tokens or you will have an aggregated delegation of at least 100k MIX tokens \(you can purchase MIX token on [Uniswap](https://uniswap.exchange/swap/0x970b9bb2c0444f5e81e9d0efb84c8ccdcdcaf84d)\).
* You have an always-on hardware that meets the pre-requisites - [Running a validator node](run-your-own-validator.md#pre-requisites)

## How to become a Mix validator

To quickly become a validator, follow this steps:

### Step 1: Download the \`quickstart.sh\` script and an \`.env\` example file:

```text
mkdir fuse-validator
cd fuse-validator
wget -O quickstart.sh https://raw.githubusercontent.com/EclatDev/Mix/master/scripts/quickstart.sh
chmod 777 quickstart.sh
wget -O .env https://raw.githubusercontent.com/EclatDev/Mix/master/scripts/examples/.env.validator.example
```

### Step 2: Update the \`.env\` file:

```text
set "sudo" on `PERMISSION_PREFIX` if running docker/docker-compose requires root

set `<YOUR_API_KEY>` to your infura api key on `FOREIGN_RPC_URL`
(or replace entirely with your Ethereum mainnet rpc endpoint)
```

### Step 3: Run the script as a validator:

```text
./quickstart.sh
```

{% hint style="success" %}
After running the script successfully, you will see your address in the [health](https://status.miexs.com/) site.
{% endhint %}

### Step 5: Stake and/or delegate!

#### Stake

To stake MIX tokens, all you should do is send your MIX tokens to the Mix Consensus contract address over the Mix network from the validator address.

{% hint style="success" %}
The Mix Consensus contract address: `0x1c7DFFd9313A0f3f20518E88735932D02bef4F28`
{% endhint %}

The easiest way to do so, is to import your private key or key-store file to your favourite wallet \(for example Metamask\), switch network to Mix and send the MIX tokens \(native tokens\) to the Consensus contract address.

{% hint style="info" %}
You can find your key-store \(containing your private key\) and the password for the created account in:

`$HOME/fusenet/config/keys/FuseNetwork/UTC--xxxx`

`$HOME/fusenet/config/pass.pwd`
{% endhint %}

#### Delegate

To delegate, just send the MIX tokens from any address to the Consensus contract address with the data: `0x5c19a95c000000000000000000000000<address without 0x>`.

{% hint style="success" %}
Example:

For the address: `0xb8ce4a040e8aa33bbe2de62e92851b7d7afd52de`  
Use: `0x5c19a95c000000000000000000000000b8ce4a040e8aa33bbe2de62e92851b7d7afd52de` as the data.

`5c19a95c` is for the `delegate(address)` function signature.

`b8ce4a040e8aa33bbe2de62e92851b7d7afd52de`in this example is an address you're delegating to \(without the `0x` prefix\)
{% endhint %}

### Step 6: Wait for 1 cycle \(approximately 48 hours\).

Wait until the next cycle is started.

{% hint style="success" %}
You can see that you are validating both in the [health](https://status.miexs.com/) site and on the [explorer](https://miexs.com) site.
{% endhint %}

For live support, contact us on [Telegram](https://t.me/) or [Discord](https://discord.gg/). Good luck and happy validating!

