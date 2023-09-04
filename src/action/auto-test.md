# Automatically generate tests  

Libuptest supports automatically generating suggested ways to query each storage item.  
This can be used to make writing tests faster.  


### Libuptest:  
```rust
use libuptest::test_generation::autogen::{generate_auto_test, generate_test_std, AutoTestSummary, AutoTests};
```

### Uptest-cli:   
```shell
$ uptest-cli -a ws://127.0.0.1:9944
```

Let's explore them more indept in the next part.
