# uptest-cli auto-test


```shell
$ uptest-cli -a ws://127.0.0.1:9944
Uptest command line tool
Connect to chain
Scanning storage...
Pallet: "System"
Raw Type: Composite(TypeDefComposite { fields: [Field { name: Some("nonce"), ty: UntrackedSymbol { id: 4, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("Index"), docs: [] }, Field { name: Some("consumers"), ty: UntrackedSymbol { id: 4, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("RefCount"), docs: [] }, Field { name: Some("providers"), ty: UntrackedSymbol { id: 4, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("RefCount"), docs: [] }, Field { name: Some("sufficients"), ty: UntrackedSymbol { id: 4, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("RefCount"), docs: [] }, Field { name: Some("data"), ty: UntrackedSymbol { id: 5, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("AccountData"), docs: [] }] })
Storage Item name "Account"
Storage Item type StorageMap
Code:
random input is: "let output: Index = query_storage_map(Account)"
-------------------
Pallet: "System"
Raw Type: Primitive(U32)
Storage Item name "ExtrinsicCount"
Storage Item type StorageValue
Code:
fn submit_to_ExtrinsicCount(testinput)
random input is: "let testinput: u32 = 4156112247u32"
-------------------
Pallet: "System"
Raw Type: Composite(TypeDefComposite { fields: [Field { name: Some("normal"), ty: UntrackedSymbol { id: 8, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("T"), docs: [] }, Field { name: Some("operational"), ty: UntrackedSymbol { id: 8, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("T"), docs: [] }, Field { name: Some("mandatory"), ty: UntrackedSymbol { id: 8, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("T"), docs: [] }] })
Storage Item name "BlockWeight"
Storage Item type StorageValue
Code:
random input is: "let output: T = query_storage_map(BlockWeight)"
-------------------
Pallet: "System"
Raw Type: Primitive(U32)
Storage Item name "AllExtrinsicsLen"
Storage Item type StorageValue
Code:
fn submit_to_AllExtrinsicsLen(testinput)
random input is: "let testinput: u32 = 3905420446u32"
-------------------
Pallet: "System"
Raw Type: Composite(TypeDefComposite { fields: [Field { name: None, ty: UntrackedSymbol { id: 1, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("[u8; 32]"), docs: [] }] })
Storage Item name "BlockHash"
Storage Item type StorageMap
Code:
random input is: "let output: [u8; 32] = query_storage_map(BlockHash)"
-------------------
Pallet: "System"
Raw Type: Sequence(TypeDefSequence { type_param: UntrackedSymbol { id: 2, marker: PhantomData<fn() -> core::any::TypeId> } })
Storage Item name "ExtrinsicData"
Storage Item type StorageMap
Code:
random input is: "let Query_chain_state = System.ExtrinsicData(); // query the StorageMap | Sequence storage type"
-------------------
Pallet: "System"
Raw Type: Primitive(U32)
Storage Item name "Number"
Storage Item type StorageValue
Code:
fn submit_to_Number(testinput)
random input is: "let testinput: u32 = 1953627433u32"
-------------------
Pallet: "System"
Raw Type: Composite(TypeDefComposite { fields: [Field { name: None, ty: UntrackedSymbol { id: 1, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("[u8; 32]"), docs: [] }] })
Storage Item name "ParentHash"
Storage Item type StorageValue
Code:
random input is: "let output: [u8; 32] = query_storage_map(ParentHash)"
-------------------
Pallet: "System"
Raw Type: Composite(TypeDefComposite { fields: [Field { name: Some("logs"), ty: UntrackedSymbol { id: 14, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("Vec<DigestItem>"), docs: [] }] })
Storage Item name "Digest"
Storage Item type StorageValue
Code:
random input is: "let output: Vec<DigestItem> = query_storage_map(Digest)"
-------------------
Pallet: "System"
Raw Type: Sequence(TypeDefSequence { type_param: UntrackedSymbol { id: 18, marker: PhantomData<fn() -> core::any::TypeId> } })
Storage Item name "Events"
Storage Item type StorageValue
Code:
random input is: "let Query_chain_state = System.Events(); // query the StorageValue | Sequence storage type"
-------------------
Pallet: "System"
Raw Type: Primitive(U32)
Storage Item name "EventCount"
Storage Item type StorageValue
Code:
fn submit_to_EventCount(testinput)
random input is: "let testinput: u32 = 770744696u32"
-------------------
Pallet: "System"
Raw Type: Sequence(TypeDefSequence { type_param: UntrackedSymbol { id: 45, marker: PhantomData<fn() -> core::any::TypeId> } })
Storage Item name "EventTopics"
Storage Item type StorageMap
Code:
random input is: "let Query_chain_state = System.EventTopics(); // query the StorageMap | Sequence storage type"
-------------------
Pallet: "System"
Raw Type: Composite(TypeDefComposite { fields: [Field { name: Some("spec_version"), ty: UntrackedSymbol { id: 47, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("codec::Compact<u32>"), docs: [] }, Field { name: Some("spec_name"), ty: UntrackedSymbol { id: 48, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("sp_runtime::RuntimeString"), docs: [] }] })
Storage Item name "LastRuntimeUpgrade"
Storage Item type StorageValue
Code:
random input is: "let output: codec::Compact<u32> = query_storage_map(LastRuntimeUpgrade)"
-------------------
Pallet: "System"
Raw Type: Primitive(Bool)
Storage Item name "UpgradedToU32RefCount"
Storage Item type StorageValue
Code:
fn submit_to_UpgradedToU32RefCount(testinput)
random input is: "let testinput: bool = true"
-------------------
Pallet: "System"
Raw Type: Primitive(Bool)
Storage Item name "UpgradedToTripleRefCount"
Storage Item type StorageValue
Code:
fn submit_to_UpgradedToTripleRefCount(testinput)
random input is: "let testinput: bool = false"
-------------------
Pallet: "System"
Raw Type: Variant(TypeDefVariant { variants: [Variant { name: "ApplyExtrinsic", fields: [Field { name: None, ty: UntrackedSymbol { id: 4, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("u32"), docs: [] }], index: 0, docs: [] }, Variant { name: "Finalization", fields: [], index: 1, docs: [] }, Variant { name: "Initialization", fields: [], index: 2, docs: [] }] })
Storage Item name "ExecutionPhase"
Storage Item type StorageValue
Code:
Output could be any of the following:
"ApplyExtrinsic"
"Finalization"
"Initialization"
random input is: "let Query_chain_state = System.ExecutionPhase(); // query the StorageValue "
-------------------
Pallet: "Timestamp"
Raw Type: Primitive(U64)
Storage Item name "Now"
Storage Item type StorageValue
Code:
fn submit_to_Now(testinput)
random input is: "let testinput: u64 = 6356334091091031003u64"
-------------------
Pallet: "Timestamp"
Raw Type: Primitive(Bool)
Storage Item name "DidUpdate"
Storage Item type StorageValue
Code:
fn submit_to_DidUpdate(testinput)
random input is: "let testinput: bool = false"
-------------------
Pallet: "Aura"
Raw Type: Composite(TypeDefComposite { fields: [Field { name: None, ty: UntrackedSymbol { id: 72, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("Vec<T>"), docs: [] }] })
Storage Item name "Authorities"
Storage Item type StorageValue
Code:
random input is: "let output: Vec<T> = query_storage_map(Authorities)"
-------------------
Pallet: "Aura"
Raw Type: Composite(TypeDefComposite { fields: [Field { name: None, ty: UntrackedSymbol { id: 10, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("u64"), docs: [] }] })
Storage Item name "CurrentSlot"
Storage Item type StorageValue
Code:
random input is: "let output: u64 = query_storage_map(CurrentSlot)"
-------------------
Pallet: "Grandpa"
Raw Type: Variant(TypeDefVariant { variants: [Variant { name: "Live", fields: [], index: 0, docs: [] }, Variant { name: "PendingPause", fields: [Field { name: Some("scheduled_at"), ty: UntrackedSymbol { id: 4, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("N"), docs: [] }, Field { name: Some("delay"), ty: UntrackedSymbol { id: 4, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("N"), docs: [] }], index: 1, docs: [] }, Variant { name: "Paused", fields: [], index: 2, docs: [] }, Variant { name: "PendingResume", fields: [Field { name: Some("scheduled_at"), ty: UntrackedSymbol { id: 4, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("N"), docs: [] }, Field { name: Some("delay"), ty: UntrackedSymbol { id: 4, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("N"), docs: [] }], index: 3, docs: [] }] })
Storage Item name "State"
Storage Item type StorageValue
Code:
Output could be any of the following:
"Live"
"PendingPause"
"Paused"
"PendingResume"
random input is: "let Query_chain_state = Grandpa.State(); // query the StorageValue "
-------------------
Pallet: "Grandpa"
Raw Type: Composite(TypeDefComposite { fields: [Field { name: Some("scheduled_at"), ty: UntrackedSymbol { id: 4, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("N"), docs: [] }, Field { name: Some("delay"), ty: UntrackedSymbol { id: 4, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("N"), docs: [] }, Field { name: Some("next_authorities"), ty: UntrackedSymbol { id: 76, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("BoundedAuthorityList<Limit>"), docs: [] }, Field { name: Some("forced"), ty: UntrackedSymbol { id: 77, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("Option<N>"), docs: [] }] })
Storage Item name "PendingChange"
Storage Item type StorageValue
Code:
random input is: "let output: N = query_storage_map(PendingChange)"
-------------------
Pallet: "Grandpa"
Raw Type: Primitive(U32)
Storage Item name "NextForced"
Storage Item type StorageValue
Code:
fn submit_to_NextForced(testinput)
random input is: "let testinput: u32 = 3348882527u32"
-------------------
Pallet: "Grandpa"
Raw Type: Tuple(TypeDefTuple { fields: [UntrackedSymbol { id: 4, marker: PhantomData<fn() -> core::any::TypeId> }, UntrackedSymbol { id: 4, marker: PhantomData<fn() -> core::any::TypeId> }] })
Storage Item name "Stalled"
Storage Item type StorageValue
Code:
Type definition of tuple output: 
tuple (
Primitive(U32)
Primitive(U32)
) // end of tuple
random input is: "let Query_chain_state = Grandpa.Stalled(); // query the StorageValue, output is a tuple of "
-------------------
Pallet: "Grandpa"
Raw Type: Primitive(U64)
Storage Item name "CurrentSetId"
Storage Item type StorageValue
Code:
fn submit_to_CurrentSetId(testinput)
random input is: "let testinput: u64 = 10791354850851657412u64"
-------------------
Pallet: "Grandpa"
Raw Type: Primitive(U32)
Storage Item name "SetIdSession"
Storage Item type StorageMap
Code:
fn submit_to_SetIdSession(testinput)
random input is: "let testinput: u32 = 1303990955u32"
-------------------
Pallet: "Balances"
Raw Type: Primitive(U128)
Storage Item name "TotalIssuance"
Storage Item type StorageValue
Code:
fn submit_to_TotalIssuance(testinput)
random input is: "let testinput: u128 = 241209649674657693693679353451022133585u128"
-------------------
Pallet: "Balances"
Raw Type: Primitive(U128)
Storage Item name "InactiveIssuance"
Storage Item type StorageValue
Code:
fn submit_to_InactiveIssuance(testinput)
random input is: "let testinput: u128 = 70649824094909238760224179934204586030u128"
-------------------
Pallet: "Balances"
Raw Type: Composite(TypeDefComposite { fields: [Field { name: Some("free"), ty: UntrackedSymbol { id: 6, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("Balance"), docs: [] }, Field { name: Some("reserved"), ty: UntrackedSymbol { id: 6, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("Balance"), docs: [] }, Field { name: Some("misc_frozen"), ty: UntrackedSymbol { id: 6, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("Balance"), docs: [] }, Field { name: Some("fee_frozen"), ty: UntrackedSymbol { id: 6, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("Balance"), docs: [] }] })
Storage Item name "Account"
Storage Item type StorageMap
Code:
random input is: "let output: Balance = query_storage_map(Account)"
-------------------
Pallet: "Balances"
Raw Type: Composite(TypeDefComposite { fields: [Field { name: None, ty: UntrackedSymbol { id: 95, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("Vec<T>"), docs: [] }] })
Storage Item name "Locks"
Storage Item type StorageMap
Code:
random input is: "let output: Vec<T> = query_storage_map(Locks)"
-------------------
Pallet: "Balances"
Raw Type: Composite(TypeDefComposite { fields: [Field { name: None, ty: UntrackedSymbol { id: 98, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("Vec<T>"), docs: [] }] })
Storage Item name "Reserves"
Storage Item type StorageMap
Code:
random input is: "let output: Vec<T> = query_storage_map(Reserves)"
-------------------
Pallet: "TransactionPayment"
Raw Type: Composite(TypeDefComposite { fields: [Field { name: None, ty: UntrackedSymbol { id: 6, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("u128"), docs: [] }] })
Storage Item name "NextFeeMultiplier"
Storage Item type StorageValue
Code:
random input is: "let output: u128 = query_storage_map(NextFeeMultiplier)"
-------------------
Pallet: "TransactionPayment"
Raw Type: Variant(TypeDefVariant { variants: [Variant { name: "V1Ancient", fields: [], index: 0, docs: [] }, Variant { name: "V2", fields: [], index: 1, docs: [] }] })
Storage Item name "StorageVersion"
Storage Item type StorageValue
Code:
Output could be any of the following:
"V1Ancient"
"V2"
random input is: "let Query_chain_state = TransactionPayment.StorageVersion(); // query the StorageValue "
-------------------
Pallet: "Sudo"
Raw Type: Composite(TypeDefComposite { fields: [Field { name: None, ty: UntrackedSymbol { id: 1, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("[u8; 32]"), docs: [] }] })
Storage Item name "Key"
Storage Item type StorageValue
Code:
random input is: "let output: [u8; 32] = query_storage_map(Key)"
-------------------
Pallet: "TemplateModule"
Raw Type: Primitive(U32)
Storage Item name "Something"
Storage Item type StorageValue
Code:
fn submit_to_Something(testinput)
random input is: "let testinput: u32 = 2166200555u32"
-------------------
Pallet: "TemplateModule"
Raw Type: Primitive(U64)
Storage Item name "Something2"
Storage Item type StorageValue
Code:
fn submit_to_Something2(testinput)
random input is: "let testinput: u64 = 13381854620199913039u64"
-------------------
Pallet: "TemplateModule"
Raw Type: Primitive(U128)
Storage Item name "Something6"
Storage Item type StorageValue
Code:
fn submit_to_Something6(testinput)
random input is: "let testinput: u128 = 175114842145234008150363523808777702541u128"
-------------------
Pallet: "TemplateModule"
Raw Type: Composite(TypeDefComposite { fields: [Field { name: None, ty: UntrackedSymbol { id: 1, marker: PhantomData<fn() -> core::any::TypeId> }, type_name: Some("[u8; 32]"), docs: [] }] })
Storage Item name "SomeMapfirst"
Storage Item type StorageMap
Code:
random input is: "let output: [u8; 32] = query_storage_map(SomeMapfirst)"
-------------------
Pallet: "TemplateModule"
Raw Type: Primitive(U32)
Storage Item name "NumberResultQuery"
Storage Item type StorageValue
Code:
fn submit_to_NumberResultQuery(testinput)
random input is: "let testinput: u32 = 308558816u32"
-------------------
Pallet: "TemplateModule"
Raw Type: Primitive(U64)
Storage Item name "SomeMaptwos"
Storage Item type StorageValue
Code:
fn submit_to_SomeMaptwos(testinput)
random input is: "let testinput: u64 = 11545124980994761057u64"
-------------------
Pallet: "TemplateModule"
Raw Type: Primitive(U64)
Storage Item name "SomeMaptwo"
Storage Item type StorageMap
Code:
fn submit_to_SomeMaptwo(testinput)
random input is: "let testinput: u64 = 6774784951135778396u64"
-------------------
Pallet: "TemplateModule"
Raw Type: Primitive(U32)
Storage Item name "SomeMapthree"
Storage Item type StorageMap
Code:
fn submit_to_SomeMapthree(testinput)
random input is: "let testinput: u32 = 659067354u32"
-------------------


```

