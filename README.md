# EasyDAI Subgraph

## Setup

### Prerequisites

* Global Yarn Packages
  * ganache-cli
  * truffle
  * graph-cli
* Docker 

### Services

Start a ganache chain using 0.0.0.0 as a host so docker can connect

```
ganache-cli -h 0.0.0.0 -d -l 4294967295 --allowUnlimitedContractSize
```

Run a local graph node

```
git clone https://github.com/graphprotocol/graph-node/
```

Update ethereum value in docker-compose.yml to ganache:http://host.docker.internal:8545

```
cd graph-node/docker
docker-compose up
```

To blow away graph-node settings

```
docker-compose kill && docker-compose rm -f && rm -rf data
```


### Subgraph

Clone the balancer subgraph

```
git clone git@github.com:balancer-labs/balancer-subgraph.git
```

Update factory address in subgraph.yaml to the one listed as part of the deploy

Install dependencies

```
yarn
```

Generate the graph code

```
yarn codegen
```

Create local node

```
yarn create:local
```

Deploy locally

```
yarn deploy:local
```

Any updates can be made to this repo and re-running yarn deploy:local without needing to re-initialize the environment.


## Calculate balance, profit, accrued interest 

Underlying Balance = `AccountBond.normalizedBalance` * `Market.exchangeRate`

Current Profit = Underlying balance - `AccountBond.principalBalance`

Accrued Interest = Underlying balance + `AccountBond.totalUnderlyingRedeemed` - `AccountBond.totalUnderlyingSupplied`

测试币
USDT -> 0x550FB60524bc6115108289E1048757B81688e362

OK链测试
WOKT -> 0xd580f978c1F6Df02384f439662c7214f83cCcCf1
MDX -> 0x2103c8E3C6aea0067F61337f8548f3B8a1653D1c
MdexFactory -> 0x208Ead7bb6cAEDFDA6A040e56900B4CB278C411C
MdexRouter -> 0x1D32C0922FCe1498cf33131DeFaaE47f82b78147
Oracle -> 0x1f0a6390B1D4cA8c4d89adEAC9Bb13efE017C558
SwapMining -> 0x570B258382722AEd0ACaD78d7d1D3430621b0c03
HecoPool -> 0xBB38a2616A19bA08D45966e55e5774A7476d2951

MdexFactory -> setFeeTo
MdexFactory -> setFeeToRate 

MDX/USDT Lp -> 0x3121A195330f8B3C6a006145FFD7F20c4c398134
WOKT/USDT Lp -> 0x4164D61787eC20c7d46824aADFBc64EFF2BAF7d0