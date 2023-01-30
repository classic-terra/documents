# Wasm cache

1. [Wasm cache](https://github.com/CosmWasm/cosmwasm/blob/main/packages/vm/src/cache.rs) stores VM instance of a smart contract
2. Everytime a Wasm action is invoked, it will get VM instance
3. There are four layers of storage VM instance will be in
4. Here is the priority for those four layers
    * [PinnedMemoryCache](https://github.com/CosmWasm/cosmwasm/blob/main/packages/vm/src/modules/pinned_memory_cache.rs)
    * [InMemoryCache](https://github.com/CosmWasm/cosmwasm/blob/main/packages/vm/src/modules/in_memory_cache.rs)
    * [FileSystemCache](https://github.com/CosmWasm/cosmwasm/blob/main/packages/vm/src/modules/file_system_cache.rs)
    * Disk

## PinnedMemoryCache (pinned_memory_cache)

* Written to HashMap structure in Rust
* Pins a Module that was previously stored via save_wasm.

## InMemoryCache (memory_cache)

* Written to LRU cache. If surpassed 2GB limit cache limit, old key - value will be removed to make space for new one

## FileSystemCache (fs_cache)

* Written to a folder “cache”
* Function `FileSystemCache::new` is marked unsafe, which implicitly assumes the disk contents are correct, and there's no way to ensure the artifacts stored in the cache haven't been corrupted or tampered with

## Saving a wasm VM instance

1. [https://github.com/CosmWasm/cosmwasm/blob/main/packages/vm/src/cache.rs#L155](https://github.com/CosmWasm/cosmwasm/blob/main/packages/vm/src/cache.rs#L155)
2. Compile wasm data into module
3. Persist wasm data into disk
4. Save module into fs_cache

## Loading a wasm VM instance

1. [https://github.com/CosmWasm/cosmwasm/blob/main/packages/vm/src/cache.rs#L273](https://github.com/CosmWasm/cosmwasm/blob/main/packages/vm/src/cache.rs#L273)
2. It will try to load module from pinned_memory_cache. If found, return module
3. Load module from memory_cache. If found, return module
4. Load module from fs_cache. If found, save module to memory_cache then return module
5. Load wasm data from disk. If found, re - compile wasm data into module, save module to fs_cache, save module to memory_cache then return module
6. An implementation example: [https://github.com/CosmWasm/cosmwasm/blob/main/packages/vm/src/cache.rs#L787](https://github.com/CosmWasm/cosmwasm/blob/main/packages/vm/src/cache.rs#L787)

## Store

Store is different from cache, it stores data from a smart contract.

### Store creation
1. tm-db store is parsed into [get_instance()](https://github.com/CosmWasm/cosmwasm/blob/main/packages/vm/src/cache.rs#L273) as backend.
2. During compile time, a temporary store is created for code compilation. This store comes from wasmer.
3. In the initial phase of constructing instance, compile - time store will be used for containing service registration in [from_module()](https://github.com/CosmWasm/cosmwasm/blob/main/packages/vm/src/instance.rs#L78). It will later be used to construct smart contract environment.
4. after environment creation, tm-db store is moved into env as wasm store.

### Store basic usage
* [do_db_write](https://github.com/CosmWasm/cosmwasm/blob/main/packages/vm/src/imports.rs#L86), store will be used to set data
* [do_db_read](https://github.com/CosmWasm/cosmwasm/blob/main/packages/vm/src/imports.rs#L68), store will be used to get data
* [do_db_remove](https://github.com/CosmWasm/cosmwasm/blob/main/packages/vm/src/imports.rs#L106), store will be used to remove data
