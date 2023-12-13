# Libuptest auto-test

Libuptest supports automatically generating types for the storage entry types:   
-  [x] u8  
-  [x] u32 
-  [x] u64  
-  [x] u128   
-  [x] Boolean  
-  [x] Balances(to a certain degree)
-  [x] TypeDef::Composite types   
-  [x] Tuples   

#### Interact with InputHelper  
The auto-test module use `InputHelper` to generate random input for the user.     

## Cargo.toml:  
Enable the `auto-test` feature flag.  
```toml
libuptest = { git = "https://github.com/uptest-sc/uptest", version = "0.1.4", features = ["auto-test"]}
```

## Libuptest:  


Code example:
```rust
use libuptest::error::Error;
use libuptest::jsonrpseeclient::JsonrpseeClient;
use libuptest::test_generation::autogen::{generate_auto_test, generate_test_std, AutoTestSummary, AutoTests};


/// generate a summary(AutoTestSummary) of suggested generated ways to query each storage item
async fn generate_tests(client: JsonrpseeClient) -> Result<AutoTests, Error> {
	// parse each storage entry and recommend a way to query it, similar to cli auto-test
	let auto_tests: Vec<AutoTestSummary> = generate_auto_test(client).await?:
	Ok(AutoTests)
}

/// cli version, this outputs the same data but directly to stdout with a old fashion print
async fn generate_cli_output(client: JsonrpseeClient) -> Result<(), Error> {
	// print info about quering each storage entry
	let _out = generate_test_std(client).await?;
	Ok(())
}
```


### Resources:  
[cli auto-test](https://github.com/uptest-sc/uptest/blob/main/cli/src/helper.rs#L31)     
[auto-test module code](https://github.com/uptest-sc/uptest/tree/main/libuptest/src/test_generation)  

