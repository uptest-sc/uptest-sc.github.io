# Libuptest Decoding Extrinsics

When we query the chain for data we will get the raw data as a response. In order to decode this to a human readable format we need to know the metadata version and decode the hex string together with the raw metadata.    

The data is encoded in a format called SCALE (Simple Concatenated Aggregate Little-Endian). The encodment will be a bit different depending on your metadata version(latest and most widely used is V14). 


### Code sample:  
```rust
use libuptest::decode_extrinsic::decode_extrinsic_hex_string;
use libuptest::jsonrpseeclient::JsonrpseeClient;
use libuptest::types::event_summary;
use libuptest::ws_mod::get_raw_metadata;

#[tokio::main]
async fn main() -> anyhow::Result<()> {
    // define the raw extrinsic hex string we get from the chain, in this example its a simple time stamp
    let raw_extrinsic = "0x280403000ba0ada8438801"; // time stamp extrinsic taken from random polkadot block
    println!("Raw extrinsic value: {raw_extrinsic:?}");
    println!("Downloading metadata");
    // download the metadata in a raw u8 Vec 
    let metadata: Vec<u8> = get_raw_metadata(JsonrpseeClient::polkadot_default_url().unwrap())
        .await
        .unwrap(); // yolo
    println!("Metadata downloaded ok");
    // once we have the metadata downloaded we want to take that plus our raw extrinsic string and feed it into the decode_extrinsic_hex_string function from Uptest   
    let decoded_output = decode_extrinsic_hex_string(raw_extrinsic, &metadata);
    // use the decoded output and create an event struct from it
    let single_event: event_summary = event_summary {
        pallet_name: decoded_output.call_data.pallet_name.to_string(),
        pallet_method: decoded_output.call_data.ty.name().to_string(),
    };
    let string_vec_events: Vec<event_summary> = vec![single_event];
    // all good, we could now view the data
    println!(
        "Decoded output as:  {:?} ",
        string_vec_events[0].pallet_method
    );
    Ok(())
}

```


#### External links:   
[docs.substrate.io Scale Encoding](https://docs.substrate.io/reference/scale-codec/)   
[Uptest metadata version scanning survey](https://github.com/uptest-sc/uptest-sc.github.io/blob/main/markdown/metadata_stats.md)     

