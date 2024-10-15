# Unichain-Node
Uniswap OP L2 - UniChain Node Setup 

- Uniswap raised $189M

- Unichain is a DeFi-native Ethereum L2, built to be the home for liquidity across chains.

- Unichain, a faster, cheaper L2 designed to be the home for DeFi and the home for multichain liquidity.

Site : [Unichain](https://www.unichain.org/) | X : [UnicahinX](https://x.com/unichain) | Docs : [Unichain docs](https://docs.unichain.org/docs)

---

## Hardware requirements:

| **Hardware** | **Minimum Requirement** |
|--------------|-------------------------|
| **CPU**      | 6 Cores                 |
| **RAM**      | 8 GB                    | 
| **Disk**     | 100  GB  SSD            |

---
### Testnet
Bridge Eth from sepolia to Unichain. Use both bridges

Super Bridge: [Link](https://superbridge.app/unichain-sepolia)

Bird Bridge: [Link](https://testnet.brid.gg/unichain-sepolia?amount=&originChainId=11155111&token=ETH)

Bridge back some amount

### Update and Upgrade VPS
```
sudo apt update && sudo apt upgrade
sudo apt-get install ca-certificates curl
```
### Install Docker:
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
docker version
```
### Install Docker-Compose:
```
VER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep tag_name | cut -d '"' -f 4)
curl -L "https://github.com/docker/compose/releases/download/"$VER"/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
docker-compose --version
```
### Docker Permission to User
```
sudo groupadd docker
sudo usermod -aG docker $USER
```
### Clone UniChain Node :
```
git clone https://github.com/Uniswap/unichain-node
cd unichain-node
```
### Edit env:
```
nano .env.sepolia
``` 
Get L1 RPC : [Drpc.org](https://drpc.org?ref=a0821e)
![Picture](https://github.com/ToanBm/unichain-node/blob/main/RPC.jpg)
### Start Node: 
```
docker compose up -d
```
### Check logs: 
```
docker compose logs -f
```
### curl Unichain Status:
```
curl -d '{"id":1,"jsonrpc":"2.0","method":"eth_getBlockByNumber","params":["latest",false]}' -H "Content-Type: application/json" http://localhost:8545
```

-------------------------------------------------------------------------


## Contract Deployment

### Install foundry
```
curl -L https://foundry.paradigm.xyz | bash
```
```
source /root/.bashrc
```
```
foundryup
```
```
forge --version
```
### Edit foundry.toml

```
nano foundry.toml
```

Paste :
```
[rpc_endpoints]
unichain = "https://sepolia.unichain.org"
```

CTRL+X, then Y and ENTER

### Clone OpenZeppelin
```
git clone https://github.com/OpenZeppelin/openzeppelin-contracts.git "openzeppelin"
```
### Clone CryptoConsole Repo
```
git clone https://github.com/stealeruv/Unichain-Node.git "ccuniscripts"
```
### Deploy Helloworld
```
forge create ccuniscripts/helloworld.sol:HelloWorld --rpc-url unichain --private-key {YourPrivateKey}
```

**Explorer** : https://sepolia.uniscan.xyz/

### Deploy ERC20 token
```
forge create ccuniscripts/erc20.sol:Console --constructor-args <youraddress> --rpc-url unichain --private-key {YourPrivateKey}
```
### Send to Another Address
```
cast send <ContractAddress> "transfer(address,uint256)" <receiveraddress> 100000000000000000000  --rpc-url unichain  --private-key <yourprivkey>
```

**Follow Crypto Console**: https://x.com/cryptoconsol  🫰
