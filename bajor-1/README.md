### `bajor-1` Testnet Parameters

These are testnet parameters for v0.45.x upgrade API and GUI breakage testing.
Will be reused for `wasmd` upgrade and API breakage testing.

-   Binary: 2.0.1
-   Chain ID: bajor-1
-   LCD [http://85.214.56.241:1317](http://85.214.56.241:1317)
-   FCD [http://85.214.56.241:3060](http://85.214.56.241:3060)
-   Swagger [http://85.214.56.241:1317/swagger/#](http://85.214.56.241:1317/swagger/#)
-   Genesis [genesis.json](https://network-rebel-2.s3.amazonaws.com/bajor-1/genesis.json)

Note `http` protocol being used. For Interchain Station to work with these parameters you are going to have to set up an `https` capable proxy. This is a `https` capable proxy (but support for this is subject to change):

-   https://test-lcd.lunc.foundation/node_info
