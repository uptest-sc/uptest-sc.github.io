# Tutorial #1 preventing breaking upgrades  

### Summary:  
In this tutorial we will take a look on how you can utilize uptest-cli to detect storage changes and how the chain can break if those are not migrated properly. Three runtime upgrades will be pushed, changing the type of a storage value, then inproperly `unwraping` the new value without migrating it. 

#### Requirements:  
*  Rust and Cargo   
*  git  
*  [uptest-cli](https://github.com/uptest-sc/uptest)  
`$ git clone https://github.com/uptest-sc/uptest && cd uptest/ && cargo build --release`
*  [submit-runtime-upgrade](https://github.com/uptest-sc/submit-runtime-upgrade)   
`$ git clone https://github.com/uptest-sc/submit-runtime-upgrade && cd submit-runtime-upgrade/ && cargo build --release`



## Step one: 
Clone and compile substrate-node-template-hack  
```
$ git clone -b tutorial_1 https://github.com/uptest-sc/substrate-node-template-hack
$ cd substrate-node-template-hack/  
```

#### Change the spec_version to 100:  
Head over to `runtime/src/lib.rs` and edit spec_version to 100.

#### Compile the node:   
`$ cargo build --release`

#### Copy the binary to another file: 
`cp target/release/substrate-node-template version_100 `

#### Start the node:  
`$ RUST_LOG=runtime=debug ./version_100 --dev --ws-external --base-path=/tmp/temp_node`

#### Verify that spec_version is 100  
```
./target/release/uptest -i ws://127.0.0.1:9944
Uptest command line tool
----Chain-Info----
Chain Name: "node-template"
Runtime version: 100
Authoring Version: 1
State Version: 1
--E-O-L--
``` 


## Step two:

#### Change the spec_version to 101:  
Head over to `runtime/src/lib.rs` and edit spec_version to 101.   

```rust
#[sp_version::runtime_version]
pub const VERSION: RuntimeVersion = RuntimeVersion {
	spec_name: create_runtime_str!("node-template"),
	impl_name: create_runtime_str!("node-template"),
	authoring_version: 1,
	spec_version: 100, // change me to 101
	impl_version: 3,
	apis: RUNTIME_API_VERSIONS,
	transaction_version: 1,
	state_version: 1,
};
```
 
[https://github.com/uptest-sc/substrate-node-template-hack/blob/tutorial_1/runtime/src/lib.rs#L106C2-L106C14](https://github.com/uptest-sc/substrate-node-template-hack/blob/tutorial_1/runtime/src/lib.rs#L106C2-L106C14)


#### Modify Pallet-template   
We are going to be focusing on a storage item in pallet-template. 
Our example storage item is the `Something2` storageValue:

```rust 
#[pallet::storage]
#[pallet::getter(fn something2)]
pub type Something2<T> = StorageValue<_, u64>;
```

We want to change the storage type from a u64 to a boolean:

```rust
#[pallet::storage]
#[pallet::getter(fn something2)]
pub type Something2<T> = StorageValue<_, bool>;
```

Change the on_initialize function from u64 to bool type, this function runs on the start of every block:

```rust
fn on_initialize(n: BlockNumberFor<T>) -> Weight {
			let printme = format!("on_initialize(#{:?})", n);
			print(printme.as_str());
			let second: Option<u64> = Something2::<T>::get(); //bool here
//			let to_print: u64 = second.unwrap();//change me to bool
			let sp = format!("second is: {:?}", second);
			print(sp.as_str());
			Weight::from_parts(2175, 0)
		}

```


Change the do_something_second function:
```rust
pub fn do_something_second(origin: OriginFor<T>, something2: u64) -> DispatchResult { // change me
			let who = ensure_signed(origin)?;
			<Something2<T>>::put(something2);
			Ok(())
		}
```


#### Start the node with the copied binary and the same base-path:   
`$ RUST_LOG=runtime=debug ./version_100 --dev --ws-external --base-path=/tmp/temp_node`   
```
…1cec), ⬇ 0 ⬆ 0
INFO tokio-runtime-worker sc_basic_authorship::basic_authorship: 🙌 Startin
p of parent 0x6a60f1d4241c4678f6a860edea30a13ab4903a0a5414ea31a521eb8d625df

EBUG tokio-runtime-worker runtime: on_initialize(#2)                      
EBUG tokio-runtime-worker runtime: second is: None                        
EBUG tokio-runtime-worker runtime: Finalized block: #2                    
EBUG tokio-runtime-worker runtime::system: [2] 0 extrinsics, length: 11 (no
```

The node should start and should be able to see the value of *Something2* storage item in the logs.  

## Step three: 
Head over to Polkadot.js.apps and connect to your chain. Then go to Developer > extrinsics > Pallet templateModule and function doSomethingSecond and set the boolean to true. Submit the transaction and in your node log file you should see that the value is set to true in your logs.   
 

## Step four:   
Now we have two version of our node, version 100 that is running and our new version, the 101.
#### Use uptest-cli to display changes made  
Use uptest-cli with the '-c' flag to see changes made, we want to start this before we push the upgrade and then check back once we have pushed the upgrade:
```
./target/release/uptest  -c ws://127.0.0.1:9944
Uptest command line tool
running ws host: "ws://127.0.0.1:9944"
Connected to chain
Gathered current storage types
Waiting for runtime upgrade
```

#### We now want to push a runtime upgrade.
Clone the [submit-runtime-upgrade](https://github.com/uptest-sc/submit-runtime-upgrade) repo. Modify it to your needs and compile it.

Run it:  
```
./target/release/submit-runtime-upgrade 
Current Runtime Version: 100
sending tx
Sent tx: 0xb91bc8ed09a7a3e0accbaa92720412f382f4ae211218acece279a251bd67189c
Runtime Version changed from 100 to 101
```


#### Check back at uptest-cli
The rest of our output should have been caught by uptest now:
```
./target/release/uptest  -c ws://127.0.0.1:9944
...
Runtime upgrade in block: 0xb91bc8ed09a7a3e0accbaa92720412f382f4ae211218acece279a251bd67189c
Having a coffee break before next block...
Scanning the new metadata for changes
Runtime upgraded from version: 108 to new version: 109
Pallet name:  "TemplateModule"
    Storage item name:  "Something2" 
    Storage item type:  StorageValue 
    Old storage type:  Primitive(U64)
    New storage type: Primitive(bool)

```


#### Check the spec_version with uptest:  
We want to make sure our chain has started and that the correct spec_version was set.  
```
./target/release/uptest -i ws://127.0.0.1:9944
Uptest command line tool
----Chain-Info----
Chain Name: "node-template"
Runtime version: 101
Authoring Version: 1
State Version: 1
--E-O-L--
``` 


## Step five:    

Now we pushed the runtime upgrade but not migrated the data stored so we should still have the bool stored where it's now u64. 

#### Change the spec_version to 102:  
`runtime/src/lib.rs` and edit spec_version to 102.   

Create an unwrap statement to assume that our value is set to a u64.: 
```rust
fn on_initialize(n: BlockNumberFor<T>) -> Weight {
			let printme = format!("on_initialize(#{:?})", n);
			print(printme.as_str());
			let second: Option<u64> = Something2::<T>::get(); //bool here
//			let to_print: u64 = second.unwrap();//change me to bool
			let sp = format!("second is: {:?}", second);
			print(sp.as_str());
			Weight::from_parts(2175, 0)
		}

```

Push the runtime upgrade just like you did previously with submite-runtime-upgrade.  

restart node and you should see it fail:
```
ces
DEBUG tokio-runtime-worker runtime::frame-support: ✅ no migration for TransactionPayment
DEBUG tokio-runtime-worker runtime::frame-support: ✅ no migration for Sudo
 DEBUG tokio-runtime-worker runtime::frame-support: ✅ no migration for TemplateModule
 DEBUG tokio-runtime-worker runtime: on_initialize(#672)                    
 ERROR tokio-runtime-worker runtime::storage: Corrupted state at `[23, 126, 104, 87, 251, 29, 14, 64, 147, 118, 18, 47, 238, 58, 212, 248, 59, 217, 88, 236, 134, 13, 139, 180, 170, 77, 234, 152, 3, 48, 17, 235]: Error`
 ERROR tokio-runtime-worker runtime: panicked at 'called `Option::unwrap()` on a `None` value', /tmp/substrate-node-template/pallets/template/src/lib.rs:46:40                  
  WARN tokio-runtime-worker aura: Proposing failed: Import failed: Error at calling runtime api: Execution failed: Execution aborted due to trap: wasm trap: wasm `unreachable` instruction executed
WASM backtrace:
error while executing at wasm backtrace:
    0: 0x641a8 - <unknown>!rust_begin_unwind
    1: 0x2938 - <unknown>!core::panicking::panic_fmt::hca80ede79c2b9c5b                            
    2: 0x298b - <unknown>!core::panicking::panic::hed93247151462aff                                
    3: 0x1ccc5 - <unknown>!<pallet_template::pallet::Pallet<T> as frame_support::traits::hooks::OnInitialize<<T as frame_system::pallet::Config>::BlockNumber>>::on_initialize::h493bf697531cf5b3      
    4: 0x25a40 - <unknown>!frame_executive::Executive<System,Block,Context,UnsignedValidator,AllPalletsWithSystem,COnRuntimeUpgrade>::initialize_block::h066e78a766ca61bb                              
    5: 0x4900e - <unknown>!Core_initialize_block
note: using the `WASMTIME_BACKTRACE_DETAILS=1` environment variable may show more debugging information
2023-07-28 13:16:36.194  INFO tokio-runtime-worker substrate: 💤 Idle (0 peers), best: #671 (0x2b63…7b5f), finalized #669 (0xd406…b775), ⬇ 0 ⬆ 0
```

Block production have now stopped


## WIP tutorial
