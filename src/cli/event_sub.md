# Subscribe to block events   

One of uptest-cli features is to subscribe to a chain, wait for the latest finalized blocks and display the events triggered in each new block. 

### Uptest command line client -w 

```shell 
./target/release/uptest -w --help
Uptest command line tool
Usage example: uptest -w wshost blockamount
            
 Connect to polkadot and view the latest 40 blocks: uptest -w wss://polkadot-rpc-tn.dwellir.com:443 40 
            
 Latest 50 blocks from the locally running substrate node: ./target/release/uptest -w ws://127.0.0.1:9944 50
```
 
```shell 
./target/release/uptest -w wss://polkadot-rpc-tn.dwellir.com:443 40 
Uptest command line tool
Subscribing to latest finalized blocks at "wss://polkadot-rpc-tn.dwellir.com:443"
------------------------------------------------
Latest finalized block number: 0xfad2a1
Finalized block hash: 0xf8964fcc85bf7cc2edb793de86c78c912564754296806eddb1fa3e10a77781d2
[Triggered event] Pallet: Timestamp triggered event: Timestamp
[Triggered event] Pallet: ParaInherent triggered event: ParaInherent
[Triggered event] Pallet: Balances triggered event: Balances
------------------------------------------------

------------------------------------------------
Latest finalized block number: 0xfad2a2
Finalized block hash: 0x4fad277ab178625fec06fc156df24e4dad993f8bc100fa3a9b1adb96950509a0
[Triggered event] Pallet: Timestamp triggered event: Timestamp
[Triggered event] Pallet: ParaInherent triggered event: ParaInherent
------------------------------------------------

------------------------------------------------
Latest finalized block number: 0xfad2a3
Finalized block hash: 0xe1c13553b68688162f66f0e3a837357dc7b5ed0b88ab19d7ea4139ea5a48be7c
[Triggered event] Pallet: Timestamp triggered event: Timestamp
[Triggered event] Pallet: ParaInherent triggered event: ParaInherent
[Triggered event] Pallet: Balances triggered event: Balances
------------------------------------------------
```


### Code example:  
```rust
// get blocknr from subscription
println!("Latest finalized block number: #{}", blocknr);
let blockhash: H256 = blocknumber_to_blockhash(tmp_client.clone(), blocknr.clone())
    .await
    .unwrap();
println!("Finalized block hash: {blockhash:?}");

let preblock = get_block_events(blockhash, tmp_client).await.unwrap();

let extrinsics = preblock.block.extrinsics;

let decodedevent_list: Vec<event_summary> =  extrinsics.clone()
              .iter()
              .map(| n | { decodec_to_event_summary(
                       decode_extrinsic_hex_string(n.as_str(), &metadatablob))})
              .collect();

    for eventet in decodedevent_list.into_iter() {
        println !("[Triggered event] Pallet: {} triggered event: {}",
                  eventet.pallet_name, eventet.pallet_name);
      }

```

#### Source code:   
[uptest/examples/examples/sub_events.rs](https://github.com/uptest-sc/uptest/blob/main/examples/examples/sub_events.rs)   




