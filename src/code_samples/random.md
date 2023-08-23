# Libuptest random input generation

```rust 
use libuptest::test_helper::InputHelper;
```

### Generate u128, u64, u32, u8:  
```rust
let rand_u128: u128 = InputHelper::get_u128();
println!("u128: {}", rand_u128);
let rand_u64: u64 = InputHelper::get_u64();
println!("u64: {}", rand_u64);
let rand_u32: u32 = InputHelper::get_u32();
println!("u32: {}", rand_u32);
let rand_u8: u8 = InputHelper::get_u8();
println!("u8: {}", rand_u8);
```

##### Output: 
```
u128: 225864167899979897207776191162143802327
u64: 15697195152894034115
u32: 986567393
u8: 247
```


### Generate f32 and f64:
```rust
let rand_f64: f64 = InputHelper::get_f64();
println!("f64: {}", rand_f64);
let rand_f32: f32 = InputHelper::get_f32();
println!("f32: {}", rand_f32);
```

##### Output: 
```
f64: 0.07036028431640629
f32: 0.48309267
```



### Generate boolean:  
```rust
let rand_boolean: bool = InputHelper::get_boolean();
println!("boolean: {}", rand_boolean);
```

##### Output: 
```
boolean: true
```

### Generate Addresses/AccountId32:   
```rust
let rand_address = InputHelper::get_address();
println!("Address: {}", rand_address.to_string());
```
##### Output: 
```
Address: 5HjAev48u9TC5A3QAyu8WBZuWo4asVx1Z72jNoNcAWzsZpU8
```


#### Documentation:
[https://docs.rs/libuptest/latest/libuptest/test_helper/struct.InputHelper.html](https://docs.rs/libuptest/latest/libuptest/test_helper/struct.InputHelper.html)
[Libuptest random input example code](https://github.com/uptest-sc/uptest/blob/main/examples/examples/test_input_gen.rs)   
