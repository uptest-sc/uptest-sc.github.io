# Libuptest JsonRPCClient

Uptest use a modified version of [Jsonrpsee](https://github.com/paritytech/jsonrpsee/) from parity to connect to a chain.  
This makes uptest compatible with standard JsonRpsee syntax.

## Connect to chain: 
```rust
use libuptest::jsonrpseeclient::JsonrpseeClient;

let custom_client: JsonrpseeClient = JsonrpseeClient::new("ws://my_node.local:9944");   
```

## Default endpoints to chains


Out of the box 5 pre-configured endpoints have been added: 

```rust 
// connect to ws://127.0.0.1:9944
let local_client: JsonrpseeClient = JsonrpseeClient::with_default_url();   

// connect to wss://edgeware.jelliedowl.net:443
let edgeware_client: JsonrpseeClient = JsonrpseeClient::edgeware_default_url();   

// connect to wss://polkadot-rpc-tn.dwellir.com:443
let polkadot_client: JsonrpseeClient = JsonrpseeClient::polkadot_default_url();   

// connect to wss://kusama-rpc-tn.dwellir.com:443
let kusama_client: JsonrpseeClient = JsonrpseeClient::kusama_default_url();   

// connect to wss://ws.mof.sora.org:443
let sora_client: JsonrpseeClient = JsonrpseeClient::sora_default_url();

```
 


## Subscribe to chain 

```rust
use libuptest::jsonrpseeclient::subscription::{HandleSubscription, Request};
use libuptest::jsonrpseeclient::subscription::Subscribe;

```



