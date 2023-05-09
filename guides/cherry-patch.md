# Cherry patch guide

This guide addresses: https://github.com/CosmWasm/advisories/blob/main/CWAs/CWA-2023-002.md

**WARNING: GO VERSION MUST BE 1.18**

```sh

#!/bin/sh

wget https://github.com/classic-terra/core/archive/refs/tags/v1.1.0.tar.gz
tar -xvf v1.1.0.tar.gz
cd core-1.1.0
go mod edit -replace github.com/CosmWasm/wasmvm=github.com/classic-terra/wasmvm@v0.16.8-beta5
go mod tidy
make install

terrad version --long | grep github.com/CosmWasm/wasmvm
```

this should be outcome when running check

"github.com/CosmWasm/wasmvm@v0.16.7 => github.com/classic-terra/wasmvm@v0.16.8-beta5"