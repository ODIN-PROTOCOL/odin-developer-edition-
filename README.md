```bash
# To start
docker-compose up -d
# To see the status
docker-compose logs -f
```

#### Notes

* 1 Odin token equals 10^6 odin

# Example create data source:
```bash
bandd tx oracle create-data-source --name "some name" --description "some description" --script path/to/script/script.py --owner [owner-acc-address] --from [key-name] --chain-id odin --keyring-backend test 
```

# Example create oracle script:
```bash
bandd tx oracle create-oracle-script --name "some name" --description "some description" --script path/to/script/script.wasm --owner [owner-acc-address] --from [key-name] --chain-id odin --gas auto --keyring-backend test
 ```

# Example become Oracle validator:
```bash
bandd tx oracle activate --from [key-name] --chain-id odin --keyring-backend test
```

# Example become system validator:
```bash
bandd tx staking create-validator --amount 100000000odin --commission-max-change-rate 0.010000000000000000 --commission-max-rate 0.200000000000000000 --commission-rate 0.100000000000000000 --chain-id odin --from [key-name] --moniker "some moniker" --pubkey [validator-cons-pub-key] --min-self-delegation 1 --keyring-backend test
```

 # Example request create:
```bash
bandd tx oracle request [oracle-script-id:uint] [min-reports:uint] [max-reports:uint] -c [obi-encoded-calldata] --chain-id odin --from [key-name] --gas auto --keyring-backend test
``` 
OBI Encoded calldata example:
```json
{"symbol": "BTC", "multiplier": 1000000000} -> 00000003425443000000003b9aca00
```

# Example configuring reporters:
```bash 
# !!!deprecated!!! (use for loop with bank send)
bandd tx multi-send 1000000odin $(yoda keys list -a) --from [key-name] --keyring-backend test --chain-id odin
bandd tx oracle add-reporters $(yoda keys list -a) --from [key-name] --keyring-backend test --chain-id odin
```

# Example edit data source:
```bash
bandd tx oracle edit-data-source [data-source-id:uint] --script /path/to/script.py --owner [owner-acc-address] --from [key-name] --chain-id odin --keyring-backend test
```

# Example query report:
```bash
bandd query oracle request [request-id:uint] --chain-id odin --output json --indent
```