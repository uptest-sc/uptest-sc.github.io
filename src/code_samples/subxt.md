# Using Libuptest with Subxt   

Their are multiple ways of utilizing Libuptest combined with Subxt.


### With event_watch:  

Code example:  
 
```toml
$ cat Cargo.toml
[package]
name = "wait_for_event_then_submit_tx"
version = "0.1.0"
edition = "2021"

[dependencies]
subxt = "0.29.0"
subxt-macro = "0.29.0"
subxt-metadata = "0.29.0"
tokio = { version = "1.29.1", features = ["full"] }
sp-keyring = "24.0.0" 
sp-runtime = "24.0.0"
libuptest = { git = "https://github.com/uptest-sc/uptest/", branch = "main", features = ["metadatadecode"]}
```

src/main.rs:  
```rust  
use libuptest::jsonrpseeclient::JsonrpseeClient;
use libuptest::types::{event_summary, H256};
use libuptest::ws_mod::event_watch;
use sp_keyring::AccountKeyring;
use subxt::{tx::PairSigner, OnlineClient, PolkadotConfig};

/// connect to substrate node template
#[subxt::subxt(runtime_metadata_url = "ws://127.0.0.1:9944")]
mod nodetemplate {}

/// simple transfer function that will block until the user defined event is triggered
/// run an async task in a
pub async fn run_after_event() -> Result<(), Box<dyn std::error::Error>> {
    // wait and check the next 200 blocks
    let amount_of_blocks_to_queue_for: u32 = 200u32;
    // connect to chain at 127.0.0.1:9944
    let client = JsonrpseeClient::with_default_url().unwrap();
    // create an event we want to watch for then send our tx
    let event_to_wait_for: event_summary = event_summary {
        pallet_name: "Sudo".to_string(),
        pallet_method: "sudo_unchecked_weight".to_string(),
    };

    println!("waiting..");
    /// wait until the event is called and we get the block hash of the block that triggered the event
    match event_watch(client, event_to_wait_for, amount_of_blocks_to_queue_for).await {
        Ok(value) => {
            println!("Found event in block: {:?}", value);
            let _tx = send_tx().await;
            println!("all good");
        }
        _ => {
            println!("Event find failed..");
        }
    };
    println!("all good");
    Ok(())
}

#[tokio::main]
async fn main() -> Result<(), Box<dyn std::error::Error>> {
    let result = run_after_event().await;
    Ok(())
}

/// send a balance transfer from Alice to Bob
async fn send_tx() -> Result<(), Box<dyn std::error::Error>> {
    // Create a new API client, configured to talk to Polkadot nodes.
    let api = OnlineClient::<PolkadotConfig>::new().await?;

    // Build a balance transfer extrinsic.
    let dest = AccountKeyring::Bob.to_account_id().into();
    let balance_transfer_tx = nodetemplate::tx().balances().transfer(dest, 10_000);

    // Submit the balance transfer extrinsic from Alice, and wait for it to be successful
    let from = PairSigner::new(AccountKeyring::Alice.pair());
    println!("sending tx");
    let _output = api
        .tx()
        .sign_and_submit_then_watch_default(&balance_transfer_tx, &from)
        .await?
        .wait_for_finalized_success()
        .await?;
    println!("tx sent");

    Ok(())
}


```


### External links:   
[https://github.com/paritytech/subxt](https://github.com/paritytech/subxt)   
[Subxt Guide](https://docs.rs/subxt/latest/subxt/book/index.html)   
