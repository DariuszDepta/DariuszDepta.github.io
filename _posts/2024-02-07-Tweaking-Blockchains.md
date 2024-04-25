# Tweaking blockchains

## Juno

Show wasm parameters
```shell
$ junod query wasm params --chain-id=juno-1 --node="tcp://88.99.164.158:1067"
```

List all code blobs
```shell
$ junod query wasm list-code --chain-id=juno-1 --node="tcp://88.99.164.158:1067"
```

Show code info of code blob with identifier 100
```shell
$ junod query wasm code-info 100 --chain-id=juno-1 --node="tcp://88.99.164.158:1067"
```

Show pinned code blobs
```shell
$ junod query wasm pinned --chain-id=juno-1 --node="tcp://88.99.164.158:1067"
```

List instances of contracts instantiated from code with identifier 1
```shell
$ junod query wasm list-contract-by-code 1 --chain-id=juno-1 --node="tcp://88.99.164.158:1067"
```

## Osmosis

Show wasm parameters
```shell
$ osmosisd query wasm params --chain-id=osmosis-1 --node="https://rpc.osmosis.zone:443"
```

List all code blobs
```shell
$ osmosisd query wasm list-code --chain-id=osmosis-1 --node="https://rpc.osmosis.zone:443"
```

Show code info of code blob with identifier 100
```shell
$ osmosisd query wasm code-info 100 --chain-id=osmosis-1 --node="https://rpc.osmosis.zone:443"
```

Show pinned code blobs
```shell
$ osmosisd query wasm pinned --chain-id=osmosis-1 --node="https://rpc.osmosis.zone:443"
```

Download code blob for contract with code id = 7 and save to file code12.wasm
```shell
$ osmosisd query wasm code 7 code12.wasm --chain-id=osmosis-1 --node="https://rpc.osmosis.zone:443"
```

List instances of contracts instantiated from code with identifier 100
```shell
$ osmosisd query wasm list-contract-by-code 100 --chain-id=osmosis-1 --node="https://rpc.osmosis.zone:443"
```

Query contract state
```shell
//wrong
$ osmosisd query wasm contract-state smart osmo1xwahguax578tvequeg70xn0ej78gn2ahugq92m7dx8hkklsyupmsqqh66x '{"all_tokens":{}}' --chain-id=osmosis-1 --node="https://rpc.osmosis.zone:443"

//correct
$ osmosisd query wasm contract-state smart osmo1xwahguax578tvequeg70xn0ej78gn2ahugq92m7dx8hkklsyupmsqqh66x '{"list_proposals":{}}' --chain-id=osmosis-1 --node="https://rpc.osmosis.zone:443" 
```

## Wasmd

### Creating single-node blockchain locally

Original instructions can be found [here](https://github.com/CosmWasm/wasmd/blob/main/README.md).

Below are the ones used on Linux, based on the general instructions.

Go to `wasmd` folder of freshly cloned [repository](https://github.com/CosmWasm/wasmd.git).

```shell
$ git clone https://github.com/CosmWasm/wasmd.git
$ cd wasmd
$ make install
$ sudo ln -s ~/go/bin/wasmd /usr/local/bin/wasmd
$ cd scripts/contrib/local
$ setup_wasmd.sh
$ start_node.sh
```

All the chain configuration files are stored in `~/.wasmd`.
To start the configuration from the very beginning, just remove this directory:
```shell
$ rm -rf ~/.wasmd
```

To list all smart contact codes on the chain, run:

```shell
$ wasmd query wasm list-code
code_infos: []
pagination:
  next_key: null
  total: "0"
```

### Some error messages reported by `wasmd query wasm code-info`:

#### code id: invalid

```shell
$ wasmd query wasm code-info 0
Error: rpc error: code = Unknown desc = 
github.com/cosmos/cosmos-sdk/baseapp.gRPCErrorToSDKError
	github.com/cosmos/cosmos-sdk@v0.47.5/baseapp/abci.go:720
[...]
net/http.(*conn).serve
	net/http/server.go:2009
code id: invalid: unknown request
```

#### code id 100: no such code

```shell
$ wasmd query wasm code-info 100
Error: rpc error: code = Unknown desc = 
github.com/cosmos/cosmos-sdk/baseapp.gRPCErrorToSDKError
	github.com/cosmos/cosmos-sdk@v0.47.5/baseapp/abci.go:720
[...]
net/http.(*conn).serve
	net/http/server.go:2009
code id 100: no such code: unknown request
```

```shell
$ wasmd query wasm code-info 18446744073709551615
Error: rpc error: code = Unknown desc = 
github.com/cosmos/cosmos-sdk/baseapp.gRPCErrorToSDKError
	github.com/cosmos/cosmos-sdk@v0.47.5/baseapp/abci.go:720
[...]
net/http.(*conn).serve
	net/http/server.go:2009
code id 18446744073709551615: no such code: unknown request
```

#### input parsing errors

```shell
$ wasmd query wasm code-info alfa
Error: strconv.ParseUint: parsing "alfa": invalid syntax
```

```shell
$ wasmd query wasm code-info 1.234
Error: strconv.ParseUint: parsing "1.234": invalid syntax
```

```shell
$ wasmd query wasm code-info 18446744073709551616
Error: strconv.ParseUint: parsing "18446744073709551616": value out of range 
```
