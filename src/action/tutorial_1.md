# Tutorial #1 preventing breaking upgrades  

### Summary:  
In this tutorial we will take a look on how you can utilize uptest-cli to detect storage changes and how the chain can break if those are not migrated properly. Three runtime upgrades will be pushed, changing the type of a storage value, then inproperly `unwraping` the new value without migrating it. 

#### Requirements:  
*  Rust and Cargo   
*  git  
*  uptest-cli  
`$ git clone https://github.com/uptest-sc/uptest && cd uptest/ && cargo build --release`




## Step one 
Clone and compile substrate-node-template-hack  
```
$ git clone -b tutorial_1 https://github.com/uptest-sc/substrate-node-template-hack
$ cd substrate-node-template-hack/ && git checkout  
$ cargo build --release
```

#### Reset the spec_version:  
Head over to `runtime/src/lib.rs` and edit spec_version to 101.   

```rust
#[sp_version::runtime_version]
pub const VERSION: RuntimeVersion = RuntimeVersion {
	spec_name: create_runtime_str!("node-template"),
	impl_name: create_runtime_str!("node-template"),
	authoring_version: 1,
	spec_version: 109, // change me to 101
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

Note:


Change the do_something_second function:
```rust
pub fn do_something_second(origin: OriginFor<T>, something2: u64) -> DispatchResult { // change me
			let who = ensure_signed(origin)?;
			<Something2<T>>::put(something2);
			Ok(())
		}
```


#### Start the node:   
`$ RUST_LOG=runtime=debug ./target/release/node-template --dev --ws-external --base-path=/tmp/temp_node`   
```
…1cec), ⬇ 0 ⬆ 0
INFO tokio-runtime-worker sc_basic_authorship::basic_authorship: 🙌 Startin
p of parent 0x6a60f1d4241c4678f6a860edea30a13ab4903a0a5414ea31a521eb8d625df

EBUG tokio-runtime-worker runtime: on_initialize(#2)                      
EBUG tokio-runtime-worker runtime: second is: None                        
EBUG tokio-runtime-worker runtime: Finalized block: #2                    
EBUG tokio-runtime-worker runtime::system: [2] 0 extrinsics, length: 11 (no
```
Note: We want to set a `--base-path` and not just use `--`.   

The node should start and should be able to see the value of *Something2* storage item in the logs.  


Go to polkadot.js.org/apps >  


 and verify that spec_version is set to 101:
# INSERT UPTEST CHAIN INFO CHECK
spec_version: 101 

Compile the node

Change Something2 type from bool > u64

## Step two  

spec_version: 109

## Step three  

spec_version: 110  


restart node and you should see it fail:
```
ces
2023-07-28 13:16:36.000 DEBUG tokio-runtime-worker runtime::frame-support: ✅ no migration for TransactionPayment
2023-07-28 13:16:36.000 DEBUG tokio-runtime-worker runtime::frame-support: ✅ no migration for Sudo

2023-07-28 13:16:36.000 DEBUG tokio-runtime-worker runtime::frame-support: ✅ no migration for TemplateModule
2023-07-28 13:16:36.001 DEBUG tokio-runtime-worker runtime: on_initialize(#672)                    
2023-07-28 13:16:36.001 ERROR tokio-runtime-worker runtime::storage: Corrupted state at `[23, 126, 104, 87, 251, 29, 14, 64, 147, 118, 18, 47, 238, 58, 212, 248, 59, 217, 88, 236, 134, 13, 139, 180, 170, 77, 234, 152, 3, 48, 17, 235]: Error`
2023-07-28 13:16:36.001 ERROR tokio-runtime-worker runtime: panicked at 'called `Option::unwrap()` on a `None` value', /tmp/substrate-node-template/pallets/template/src/lib.rs:46:40                  
2023-07-28 13:16:36.001  WARN tokio-runtime-worker aura: Proposing failed: Import failed: Error at calling runtime api: Execution failed: Execution aborted due to trap: wasm trap: wasm `unreachable` instruction executed
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
