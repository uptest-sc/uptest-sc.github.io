# Libuptest ws_mod helper  

`use libuptest::ws_mod` is a collection of seperate functions that utilize the ws socket(Default port 9944) to talk directly to the chain and then render the results.  



----

Name of Function:   
event_watch  
Function description:   
The event_watch function subscribes to the latest finalized blocks, every time their is a new block(normally every 6 seconds), the function will look at the event's triggered in the block and match that against a user defined event. If it finds the event in a block it will return the H256 block hash of that block. Select how many blocks to wait for with the block_limit parameter.   

inputs:
*  client: JsonrpseeClient   
*  event: event_summary   
*  block_limit: u32  

outputs:
*  Result<H256, crate::error::Error>

Used in code example:
[upgrade_change_diff](https://github.com/uptest-sc/uptest/blob/main/examples/examples/upgrade_change_diff.rs)     
[schedule_check](https://github.com/uptest-sc/uptest/blob/main/examples/examples/schedule_check.rs)  

Special feature flag needed:
Yes - feature = "metadatadecode")

----


Name of Function:
get_runtime_version

Function description:
Queries the `state.getRuntimeVersion` endpoint in order to get the runtime version information.

inputs:
    client: JsonrpseeClient,
outputs:
RuntimeVersion Struct

Used in code example:  
[upgrade_change_diff](https://github.com/uptest-sc/uptest/blob/main/examples/examples/upgrade_change_diff.rs)  
[detect_runtime_upgrade](https://github.com/uptest-sc/uptest/blob/main/examples/examples/detect_runtime_upgrade.rs)  


Special feature flag needed:
No



----


Name of Function:
get_decoded_extrinsics_from_blockhash

Function description:
Takes in a blockhash as input and decodes the extriniscs into the nice human readable format with event_summary struct.  
 
inputs:
*    blockhash: H256,
*    metadatablob: Vec<u8>,
*    client: JsonrpseeClient,

outputs:
*  Result<Vec<event_summary>

Used in code example:

Special feature flag needed:
Yes - feature = "metadatadecode"



----



Name of Function:
get_block_events
Function description:
Return the PreBlock of the block from the block's hash.   
inputs:
    blockhash: H256,
    client: JsonrpseeClient,

outputs:
	Result<PreBlock, crate::error::Error>

Used in code example:

Special feature flag needed:
No




----




Name of Function:
get_latest_finalized_head
Function description:
Get the latest finalized block and return it as a H256 hash.  

inputs:
    client: JsonrpseeClient,
outputs:
	Result<H256, crate::error::Error>
Used in code example:

Special feature flag needed:
No



----



Name of Function:
get_metadata_version

Function description:
Returns the metadata version(1-14)

inputs:
client: JsonrpseeClient
outputs:
u8
Used in code example:

Special feature flag needed:
No



----


Name of Function:   
blockhash_to_block   
Function description:   
Convert a block_hash in H256 format to a [Preblock](https://docs.rs/libuptest/0.1.1/libuptest/types/struct.PreBlock.html)  

inputs:
    client: JsonrpseeClient,
    block_hash: H256,

outputs:
Preblock

Used in code example:

Special feature flag needed:
No


----



Name of Function:
blocknumber_to_blockhash

Function description:
Convert the block number to a block hash, function queries the chain's chain.getBlockHash endpoint.  

inputs:
    client: JsonrpseeClient,
    block_nr: String,

outputs:
	Result<H256, crate::error::Error>

Used in code example:

Special feature flag needed:
No




----



Name of Function:
get_raw_metadata

Function description:
The the chain's metadata in a raw format(Vector of u8's).   

inputs:
    client: JsonrpseeClient,

outputs:
	anyhow::Result<Vec<u8>, crate::error::Error>
Used in code example:

Special feature flag needed:
No


----


Name of Function:
get_metadata_version

Function description:
get the metadata version of chain X

Function description:

inputs:
    client: JsonrpseeClient,

outputs:
Result<u8, crate::error::Error>

Used in code example:

Special feature flag needed:
No


----





Add your own custom rpc/ws functions:  

```rust 
libuptest/src/ws_mod.rs:



#[maybe_async::maybe_async(?Send)] /// use maybe-async crate to make the async code a bit easier to work with 
pub async fn get_custom_thing(
    client: JsonrpseeClient,
) -> anyhow::Result<MYTYPE, crate::error::Error> { // replace MYTYPE with the output you wish to get
    let hex_data: String = client
        .request("chain_getFinalizedHead", RpcParams::new())// replace chain_getFinalizedHead with module_function, if an input is required, pass it along with rpc_params![input1, input2] instead of RpcParamns::new(), which returns an empty list
        .await?;
    let myoutput: MYTYPE = H256::from_str(&hex_data.as_str())?; // make sure your type matches with the response output, serde comes in very handy for building structs based on the returned json rpc response 
    Ok(myoutput)
}

```



