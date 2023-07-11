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


...

   /// create a subscription socket to chain_subscribeFinalizedHeads
   println!("Subscribing to latest finalized blocks");
    let mut subscrib: SubscriptionWrapper<Header> = client
        .clone()
        .subscribe::<Header>(
            "chain_subscribeFinalizedHeads",
            RpcParams::new(),
            "chain_unsubscribeFinalizedHeads",
        )?;

  for _ in 0..3 { // loop
        let tmp_client = JsonrpseeClient::polkadot_default_url().unwrap();
        let nextone = subscrib.next();// get the next Finalized block number
        let blocknr = nextone.unwrap().unwrap().number;
        println!("Latest finalized block: {:?}", blocknr);
        let blockhash: H256 = blocknumber_to_blockhash(tmp_client.clone(), blocknr.clone()) // convert blocknr to blockhash with libuptest
            .await?;
	}
// unsubscribe
   let _ = subscrib.unsubscribe();
    Ok(())

```



