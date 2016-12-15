# Ethereum Docker

Get started creating Ethereum development and test single and multi-node clusters
rapidly using Docker.

We provide full Ethereum test nodes (using the [Ethereum Go client](https://github.com/ethereum/go-ethereum) with all APIs enabled by default as well as a monitoring dashboard (for the cluster version) provided
via [Netstats](https://github.com/cubedro/eth-netstats).

## Getting started

### Local Development

#### Standalone Ethereum node

```
docker-compose -f docker-compose-standalone.yml up -d
```

To access the JavaScript console:

```
./js-console.sh
```

#### Ethereum Cluster with netstats monitoring

To run an Ethereum Docker cluster run the following:

```
docker-compose up -d
```

By default this will create:

* 1 Ethereum Bootstrapped container
* 1 Ethereum container (which connects to the bootstrapped container on launch)
* 1 Netstats container (with a Web UI to view activity in the cluster)

To access the Netstats Web UI:

```
./dashboard.sh
```

##### Scaling the number of nodes/containers in the cluster

```
docker-compose scale eth=3
```

Will scale the number of Ethereum nodes upwards (replace 3 with however many nodes
you prefer). These nodes will connect to the P2P network (via the bootstrap node)
by default.

#### Test accounts ready for use

As part of the bootstrapping process we bootstrap 10 Ethereum accounts for use
pre-filled with 20 Ether for use in transactions by default.

If you want to change the amount of Ether for those accounts
See ```files/genesis.json```.

#### Use existing DAG

To speed up the process, you can use a pre-generated DAG. All you need to do is add something like this
```
ADD dag/full-R23-0000000000000000 /root/.ethash/full-R23-0000000000000000
```
to the monitored-geth-client Dockerfile.
