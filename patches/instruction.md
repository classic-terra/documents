# Fix ASA-2024-007 vulnerability

If you are a validator on Terrad, please fix a critical IBC vulnerability by following theses steps:

1. Stop your `terrad` client
2. download the patched binary:
```
$ wget https://github.com/classic-terra/documents/raw/main/patches/terrad-v2.4.2-patch-asa-2024-007.tar.gz
```
3. unpack it:
```
$ tar -xvf terrad-v2.4.2-patch-asa-2024-007.tar.gz
```
4. determine the installation location of your `terrad` binary and save it in an env variable:
```
$ TERRAD_LOC=$(which terrad)
```
5. install the patched terrad
```
$ mv terrad $TERRAD_LOC
```
6. make sure the version is right
```
$ terrad version --long | grep ibc-go
- github.com/cosmos/ibc-go/v6@v6.2.1 => ../ibc-go@(devel)
```
7. restart the client
```
$ terrad start
```

Happy fixing
