# Bitcanna_mainnet
![ALT-logo](https://raw.githubusercontent.com/MaxFoton/Bitcanna_mainnet/main/BitCanna.png)

`Validator` maxfoton

`Delegate` https://main.anode.team/bitcanna/staking/bcnavaloper13qnxglysulcam3csjl3husxn4cxrjl3vnzu6t0
`Valoper` bcnavaloper13qnxglysulcam3csjl3husxn4cxrjl3vnzu6t0

**RPC**
`RPC 95.165.89.222:26758`

**Peer**
`Peer` 88497ab3bbbcc1e8545771f45020e738bcce590f@95.165.89.222:26756

**Start whith state-sync**

```sudo systemctl stop bcnad && bcnad tendermint unsafe-reset-all --home $HOME/.bcna --keep-addr-book`
curl https://raw.githubusercontent.com/MaxFoton/Bitcanna_mainnet/main/addrbook.json > ~/.bcna/config/addrbook.json```

```peers="88497ab3bbbcc1e8545771f45020e738bcce590f@95.165.89.222:26756"
sed -i.bak -e  "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.bcna/config/config.toml```

```SNAP_RPC=95.165.89.222:26758 && \
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 2000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash) && \
echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH```

```sed -i.bak -e  "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.persistenceCore/config/config.toml
sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.bcna/config/config.toml```


**Enable service and start**

```sudo systemctl daemon-reload && sudo systemctl enable bcnad
sudo systemctl restart bcnad && sudo journalctl -fu bcnad -o cat```
