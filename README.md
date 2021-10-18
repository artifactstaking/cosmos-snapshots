# cosmos-snapshots  
List of snapshots:   
http://135.181.60.250/      - Akash Network (Mainnet)  
http://135.181.60.250:8081/ - Sifchain (Betanet)  
http://135.181.60.250:8083/ - Sentinel (Mainnet)  
http://135.181.60.250:8084/ - Desmos (Mainnet)  
http://135.181.60.250:8085/ - Osmosis (Mainnet)  
http://135.181.60.250:8086/ - Bitcanna (Mainnet)  
http://95.216.45.250:8081/  - Oasis (Mainnet)  
https://snapshots.stakecraft.com/ - Juno (Mainnet)  
http://cosmos-snap.staketab.com/ixo - IXO (Mainnet)  
http://cosmos-snap.staketab.com/medibloc - Medibloc (Mainnet)  
https://www.notion.so/Stake-Systems-Fast-Sync-Service-5cb0dffb78174d3494b93f87d242939d
- juno
- osmosis
- agoric
- regen
- cosmoshub
- irishub
- matic
- emoney
- bitsong
- terra
- kava
- certik
- microtick
- celo-baklava non-archive

[Akash snapshot instruction](https://github.com/c29r3/cosmos-snapshots/blob/main/Akash.md)  
[Sifchain snapshot instruction](https://github.com/c29r3/cosmos-snapshots/blob/main/Sifchain.md)  
[Sentinel snapshot instruction](https://github.com/c29r3/cosmos-snapshots/blob/main/Sentinel.md)  
[Desmos snapshot instruction](https://github.com/c29r3/cosmos-snapshots/blob/main/Desmos.md)  
[Osmosis snapshot instruction](https://github.com/c29r3/cosmos-snapshots/blob/main/Osmosis.md)  
[Bitcanna snapshot instruction](https://github.com/c29r3/cosmos-snapshots/blob/main/Bitcanna.md)  
[Oasis snapshot instruction](https://github.com/Bambarello/cosmos-snapshots/blob/main/Oasis.md)  
[IXO snapshot instruction](https://github.com/staketab/nginx-cosmos-snap/blob/main/ixo.md)  
[Medibloc snapshot instruction](https://github.com/staketab/nginx-cosmos-snap/blob/main/medibloc.md)  


## MIRRORS  
http://rpc01-skynet.paullovette.com/ - provided by Paul Lovette  
https://snapshots.stakecraft.com/    - provided by Alex Novy  
http://95.216.45.250:8081/  - provided by Bambarello  
http://cosmos-snap.staketab.com/  - provided by Staketab  
https://www.notion.so/Stake-Systems-Fast-Sync-Service-5cb0dffb78174d3494b93f87d242939d - provided by Stake Systems  


## Run your own backup server with snapshots  
Install requirements  
```bash
sudo apt update && \
sudo apt install curl git docker.io -y
```

Clone github repo  
`git clone https://github.com/c29r3/cosmos-snapshots.git && cd cosmos-snapshots`  

Create folder for snapshots  
`mkdir $HOME/akash`

Start Nginx via docker  
```bash
cd $HOME; \
docker run --name nginx \
--restart always \
-v $(pwd)/default.conf:/etc/nginx/conf.d/default.conf \
-v $(pwd)/akash/:/root/ \
-p 80:80 \
-d nginx
```

Fill in the variables in the file `akash_snapshot.sh`  
```
CHAIN_ID="akashnet-2"
SNAP_PATH="$HOME/akash/akash"
LOG_PATH="$HOME/akash/akash_log.txt"
DATA_PATH="$HOME/.akash/data/"
SERVICE_NAME="akash.service"
```
Create new snapshot  
`./akash_snapshot.sh`  

Check snapshot  
```bash
MY_IP=$(curl -s 2ip.ru); \
curl -s http://${MY_IP}
```

## Automation  
You can add script to the cron  
```cron
# start every day at 00:00
0 0 * * * /bin/bash -c '/root/akash_snapshot.sh'
```
