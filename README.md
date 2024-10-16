# Unichain Node

![image](logo.png)

This repository contains the relevant configuration to run your own node on the Unichain network.

### Troubleshooting

If you encounter problems with your node, please open a [GitHub issue](https://github.com/Uniswap/unichain-node/issues)

### Supported Networks

| Network           | Status |
| ----------------- | ------ |
| Testnet (Sepolia) | ✅     |

## Pre requisite

1. You need docker installed and docker compose (if you already have it installed move to the Usage section)

Follow the instruction from the official documentation : https://docs.docker.com/engine/install/ubuntu/

Or use the command below

```
sudo apt update -y && sudo apt upgrade -y
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done

sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update -y && sudo apt upgrade -y

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Test Docker
sudo docker run hello-world

```

### Usage

1. Clone this Repo

```

git clone https://github.com/0xAJPanda/unichain-node.git

```

2. Set up RPC

"Ensure you have an Ethereum L1 full node RPC available, and set `OP_NODE_L1_ETH_RPC` & `OP_NODE_L1_BEACON` (in the `.env.sepolia` file). If running your own L1 node, it needs to be synced before Unichain will be able to fully sync"

You can use infera or quicknode select sepolia and copy the RPC url

```
cd unichain-node && nano .env.sepolia

```

Replace OP_NODE_L1_ETH_RPC and OP_NODE_L1_BEACON values with your RPC values

![image](RPC.png)

Save and Exit

```
CTRL+X
ENTER

```

2. Run:

```
docker compose up -d
```

3. You should now be able to `curl` your Unichain node:

```
curl -d '{"id":1,"jsonrpc":"2.0","method":"eth_getBlockByNumber","params":["latest",false]}' \
  -H "Content-Type: application/json" http://localhost:8545
```

4. To stop your node, run:

```
docker compose down
```

#### Persisting Data

By default, the data directory is stored in `${PROJECT_ROOT}/geth-data`. You can override this by modifying the value of
`HOST_DATA_DIR` variable in the [`.env`](./.env) file.

## Make sure to back up your node key located at :

```
cat ~/unichain-node/geth-data/geth/nodekey
```

Congrats you made it!!
