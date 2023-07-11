# Libuptest types   

Libuptest comes prepackaged with several different types that will make debugging a bit easier.




Name:    
H256    

Description:  
A H256 hash from [fixed-hash](https://crates.io/crates/fixed-hash), used as default blockhash.   
Manually set a block hash:  
```rust 
let blockhash: H256 = H256::from_str("0x89a5dde6705d345117f442dfacf02f4a59bf5cea3ab713a5c07fc4cd78be3a31").unwrap();//get_latest_finalized_head(client.clone()).await.unwrap();
```

Used in code examples:    
[detect_runtime_upgrade](https://github.com/uptest-sc/uptest/blob/main/examples/examples/detect_runtime_upgrade.rs)     
[get_block_event](https://github.com/uptest-sc/uptest/blob/main/examples/examples/get_block_events.rs)    

----


Name: 
Header struct   
Description:
Block Header containing the block nr

Used in code examples:
Define a block header standard that subscribe to finalized heads returns:   
[get_block_events](https://github.com/uptest-sc/uptest/blob/main/examples/examples/get_block_events.rs)

----




Name:   
event_summary struct  
 
Description:   
event_summary is an easy high level way for developers to define a custom event.    
Create a generic event in the form of:   
```rust
let myevent: event_summary = event_summary {
	pub pallet_name: "Sudo".to_string(),
	pub pallet_method: "secret_function".to_string(),
 }
```
Used in code examples:    
[decode_extrinsics](https://github.com/uptest-sc/uptest/blob/main/examples/examples/decode_extrinsics.rs)      
[get_block_events](https://github.com/uptest-sc/uptest/blob/main/examples/examples/get_block_events.rs)    
[schedule_check](https://github.com/uptest-sc/uptest/blob/main/examples/examples/schedule_check.rs)    
[upgrade_change_diff](https://github.com/uptest-sc/uptest/blob/main/examples/examples/upgrade_change_diff.rs)   


----




Name:   
storage_types     

Description:  
enum for defining what type of storage entry it is, is it a StorageValue, StorageMap or Unknown type?

Used in code examples:   
[pallet_storage_parse module](https://github.com/uptest-sc/uptest/blob/main/libuptest/src/pallet_storage_parse.rs)  


----



Name:
Block struct   
 
Description:  
Generic substrate sp-runtime block containing header and extrinsics.  

Used in code examples:   

----



Name:
PreBlock struct 

Description:
A pre-block containing a block and justifications.  

Used in code examples:   
[block_events](https://github.com/uptest-sc/uptest/blob/main/examples/examples/block_events.rs)    
[detect_runtime_upgrade](https://github.com/uptest-sc/uptest/blob/main/examples/examples/detect_runtime_upgrade.rs)    


----



Name:  
generic_block
Description:   
A generic block format containing a Header and a Vector of strings.

Used in code examples:   


----


Name:   
RuntimeVersionEvent  

Description:  
Runtime Version Event struct containing a spec version number(u32).

Used in code examples:   

----


Name:
RuntimeEvent   

Description:  
Runtime event, returning a RuntimeVersionEvent if it has a value, if not it returns an error

Used in code examples:   

----



Name:  
storage_map_info struct 

Description: 
```rust
    pub pallet_name: String,
    pub storage_item_name: String, // name of storagemap
    pub type_id: u32,              // take the type id and query the type_id to type function
    pub raw_type: desub_current::scale_info::TypeDef<PortableForm>,
    pub storage_type: storage_types,
```


Used in code examples:  
[upgrade_change_diff](https://github.com/uptest-sc/uptest/blob/main/examples/examples/upgrade_change_diff.rs)    
[get_pallet_storagemaps_storagevalues](https://github.com/uptest-sc/uptest/blob/main/examples/examples/get_pallet_storagemaps_storagevalues.rs)




### External links: 


[Libuptest docs.rs type documentation](https://docs.rs/libuptest/0.1.1/libuptest/types/index.html)  

