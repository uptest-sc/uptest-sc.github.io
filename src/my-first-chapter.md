# Install and utilize Uptest:  


## Libuptest can be found at crates.io and github:   
```shell 
$ cargo new --bin try_uptest  
$ cd try_uptest/
$ cat rust-toolchain
[toolchain]
channel = "nightly-2023-04-24"
targets = ["wasm32-unknown-unknown"]
profile = "default"
host = "x86_64-unknown-linux-gnu"
$ cat Cargo.toml  
[package]
name = "uptest-cli"
version = "0.1.0"
edition = "2021"

[dependencies]
libuptest = "0.1.1"
```

Note: Libuptest is currently only avaliable in the nightly edition, so you need to configure your rust-toolchain for that.  

## Libuptest feature flags  
We wanted to make uptest a minimal and stand-alone library so Libuptest comes with multiple feature flags that you can enable:

#### metadatadecode
This feature flag is used for adding extrinsic decoding functionality to uptest. By enabling this flag you unlock the following functions:
unctions with metadatadecode flag:  
https://github.com/search?q=repo%3Auptest-sc%2Fuptest%20%23%5Bcfg(feature%20%3D%20%22metadatadecode%22)%5D&type=code"

#### Subxt:  
Feature flag not yet published.   


#### ALL
The "ALL" feature flag does exactly what the name entails. It enables all avaliable feature flags.    



[All current feature flags on doc.rs](https://docs.rs/crate/libuptest/0.1.1/features)  


#### Limitations of uptest:  
*  Currently only supports metadata version 14 format  
*  Does not properly render the StorageValue's raw type's, storagemap type works doe       
*  Is running nightly rust and contains several unwrap's  


