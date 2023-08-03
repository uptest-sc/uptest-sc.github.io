# Submitting runtime upgrades 


There are 2 main ways of submitting a runtime upgrade:


### Sudo:   
If the chain has a sudo key enabled, comonly enabled by dev chainspec's. A ` System::SetCode` wrapped in a `Sudo sudo_unchecked_weight` transaction can overwrite the runtime and trigger a runtime upgrade with the submitted wasm file submitted with the setcode transaction.

Code example:

```rust
use std::path::Path;
use libuptest::metadata::read_wasm_binary_correct;
use subxt::{OnlineClient, PolkadotConfig};
...

let wasm_path = Path::new("/tmp/substrate-node-template/target/release/wbuild/node-template-runtime/node_template_runtime.compact.wasm");
// read binary
let code: Vec<u8> = read_wasm_binary_correct(wasm_path).await;
// create system set_code call
let call = nodetemplate::runtime_types::node_template_runtime::RuntimeCall::System(
SystemCall::set_code {
    code: code.into(),
},
); //Call::System(
let weight = Weight {
ref_time: 0,
proof_size: 0,
};

// create the sudo tx
let sudo_tx = nodetemplate::tx()
.sudo()
.sudo_unchecked_weight(call, weight);
```


Source code:   
[https://github.com/uptest-sc/submit-runtime-upgrade](https://github.com/uptest-sc/submit-runtime-upgrade)




### Democracy vote:   
#### Create a preimage of the runtime upgrade set code:  
The user can submit a preimaged of the system setcode call. Then submit the preimage to democracy by submitting a democracy > note preimage transaction. 

#### Submit the preimage for a democracy vote   
Make a democracy > propose transaction with your preimage hash.  
Your proposal is now created!  


#### Get votes!  
All you need to do now is to get enough votes for your proposal so the chain will execute it. If you are running a dev node we recommend modifying the time lenght for the life cycle of a proposal to make debugging faster and easier. 


## Note:  
Chains differentiate in how you submit the upgrade, depending on implementation.  
If you have a chain that submits a runtime upgrade in a different way, submit a pr:   
[https://github.com/uptest-sc/uptest-sc.github.io/pulls](https://github.com/uptest-sc/uptest-sc.github.io/pulls)

