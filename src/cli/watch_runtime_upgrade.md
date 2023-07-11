# Watch for runtime upgrades and custom events     

With uptest cli tool we can subscribe to the latest blocks and check them automatically for a certain event to be triggered. Once uptest finds our user defined event it will return the hash of the block that contains the event.


#### Create a custom event with event_summary:   
```
let detect_event = event_summary {
        pallet_name: "system".to_string(),
        pallet_method: "setCode".to_string(),
    }; 
```

#### Command line client example:   

```
./target/release/uptest -s Sudo sudo_unchecked_weight
Uptest command line tool
Matches: Some("pallet-method-sub")
Subscribing to Chain X, Metadata Version Y
Connecting to chain..
Looking for Pallet: "Sudo"
Checking block #"0x0"
Got block events... Decoding it..
Block: 0xab80e34ccc0b1201206b599b2d4e7a455afb9535287a8bfcf209cfb3db1503ca does not contain Pallet: "Sudo" with method: "sudo_unchecked_weight"
Checking block #"0x7"
Got block events... Decoding it..
Block: 0xf455c0485a2b6256b7f1314b1822a8502710e7d2cd710007938f3fc1509dc7ab does not contain Pallet: "Sudo" with method: "sudo_unchecked_weight"
Checking block #"0x8"
Got block events... Decoding it..
Block: 0x75eaf2d2e31cbb8f09706b4341e18c478eb4fc27c30b2060c6c854cfd153f376 does not contain Pallet: "Sudo" with method: "sudo_unchecked_weight"
Checking block #"0x9"
Got block events... Decoding it..
Block: 0x365275bbe42360026843f76d52945c5f4a1f476820a0212630eead7324f634b2 contains event
thread 'main' panicked at 'Exiting..', src/helper.rs:129:17
```


```rust  
./target/release/uptest -s --help
Uptest command line tool
Usage example: uptest -s Balance transfer 
uptest -s pallet_name pallet_method
$ ./target/release/uptest -s balance transfer   
```

Note:
The -s flag is case sensitive.

#### Example from code examples:  
[https://uptest-sc.github.io/code_samples/upgrade_change_diff.html](https://uptest-sc.github.io/code_samples/upgrade_change_diff.html)    

