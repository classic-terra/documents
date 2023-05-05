# Cherry patch guide

This guide addresses: https://github.com/CosmWasm/advisories/blob/main/CWAs/CWA-2023-002.md

```sh

#!/bin/sh

wget https://github.com/classic-terra/core/archive/refs/tags/v1.1.0.tar.gz
tar -xvf v1.1.0.tar.gz
cd core-1.1.0
go mod edit -replace github.com/CosmWasm/wasmvm=github.com/classic-terra/wasmvm@v0.16.8-beta5
go mod tidy
make install

TERRAD_API_ENABLE=true terrad start --home ~/.terra --pruning everything

```

Enabled LCD temporarily on your node to check, this should be outcome when running: `curl http://localhost:1317/node_info | jq '.application_version.build_deps' | grep 'wasmvm'`

"github.com/CosmWasm/wasmvm@v0.16.7 => github.com/classic-terra/wasmvm@v0.16.8-beta5"