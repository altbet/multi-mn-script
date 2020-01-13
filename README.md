# Nodemaster

The **Nodemaster** scripts is a collection of utilities to manage, setup and update ABET masternode instances.

We are confident this is the single best and almost effortless way to setup multiple ABET masternodes, without bothering too much about the setup part.

Comparing with building from source manually, you will benefit from using this script in the following way(s):

* 100% auto-compilation and 99% of configuration on the masternode side of things. It is currently only tested on a vultr VPS but should work almost anywhere where IPv6 addresses are available
* Developed with recent Ubuntu versions in mind, currently only 16.04 is supported
* Installs 1-100 (or more!) masternodes in parallel on one machine, with individual config and data
* Compilation is currently from source for the desired git repo tag (configurable via config files)
  Some security hardening is done, including firewalling and a separate user
* Automatic startup for all masternode daemons
* This script needs to run as root, the masternodes will and should not!
* It's ipv6 enabled, tor/onion will follow

## **Vultr** is highly recommended for this kind of setup

Here is an [easy step-by-step guide for the VPS provider vultr](/docs/vultr-masternode_vps.md) that will guide you through the hardest parts.

## Installation

SSH to your VPS and clone the Github repository:

```bash
git clone https://github.com/altbet/multi-mn-script.git && cd multi-mn-script
```

Add executable permission to script:

```bash
chmod +x install.sh
```

Install & configure your ABET masternode with option:

```bash
./install.sh -p abet
```

## Examples for typical script invocation

These are only a couple of examples for typical setups. Check our [easy step-by-step guide for [Vultr](/docs/vultr-masternode_vps.md) that will guide you through the hardest parts.

**Install & configure 4 ABET masternodes (IPV6):**

```bash
./install.sh -p abet -c 4 -n "6"
```

**Update daemon of previously installed ABET masternodes:**

```bash
./install.sh -p abet -u -n "6"
```

**Install 6 ABET masternodes with the git release tag "tags/v3.4.0.0"**

```bash
./install.sh -p abet -c 6 -r "tags/v3.4.0.0"
```

**Wipe all ABET masternode data:**

```bash
./install.sh -p abet -w
```

**Install 2 ABET masternodes and configure sentinel monitoring:**

```bash
./install.sh -p abet -c 2 -s
```

## Options

The _install.sh_ script support the following parameters:

| Long Option  | Short Option | Values              | description                                                         |
| :----------- | :----------- | ------------------- | ------------------------------------------------------------------- |
| --project    | -p           | project, e.g. "abet"| shortname for the project                                           |
| --net        | -n           | "4" / "6"           | ip type for masternode. (ipv)6 is default                           |
| --release    | -r           | e.g. "tags/v3.4.0.0"| a specific git tag/branch, defaults to latest tested                |
| --count      | -c           | number              | amount of masternodes to be configured                              |
| --update     | -u           | --                  | update specified masternode daemon, combine with -p flag            |
| --sentinel   | -s           | --                  | install and configure sentinel for node monitoring                  |
| --wipe       | -w           | --                  | uninstall & wipe all related master node data, combine with -p flag |
| --help       | -h           | --                  | print help info                                                     |
| --startnodes | -x           | --                  | starts masternode(s) after installation                             |

## Troubleshooting the masternode on the VPS

If you want to check the status of your masternode, the best way is currently running the cli e.g. for $MUE via

```
/usr/local/bin/abet-cli -conf=/etc/masternodes/abet_n1.conf getinfo

{
  "version": 3040000,
  "protocolversion": 70917,
  "services": "NETWORK/BLOOM/",
  "walletversion": 61000,
  "balance": 0.00000000,
  "zerocoinbalance": 0.00000000,
  "blocks": 9252,
  "timeoffset": 0,
  "connections": 129,
  "proxy": "",
  "difficulty": 22974.76067187333,
  "testnet": false,
  "moneysupply": 2007131.13233737,
  "keypoololdest": 1576539264,
  "keypoolsize": 1001,
  "paytxfee": 0.00000000,
  "relayfee": 0.00010000,
  "staking status": "Staking Not Active",
  "errors": ""
}
```
# Helpful Commands

## Start Coin on initial install
```
/usr/local/bin/activate_masternodes_abet
```
## Stop coin
```
/usr/local/bin/abet-cli -conf=/etc/masternodes/abet_n1.conf stop
```
## Start Coin
```
/usr/local/bin/abetd -conf=/etc/masternodes/abet_n1.conf
```
## Getinfo
```
/usr/local/bin/abet-cli -conf=/etc/masternodes/abet_n1.conf getinfo
```

# Help, Issues and Questions

If you will experience issues with **Nodemaster**, don't hestitate to ask us for help in our [support discord channel](https://discord.gg/Ka5K9g5).

# Credits to Author

You can ping him via contact@marsmenschen.com for questions or you can donate him via BTC for this great script: 19U8Jgyb38XnbGyQq3SHXS614pmLbvwKeZ
