# Updating via binary

## Downloading

`wget "https://github.com/classic-terra/documents/raw/refs/heads/main/binary-updates/terra_v3.6.2_Linux_x86_64.tar.gz"`

## Extracting

`tar xzf terra_v3.6.2_Linux_x86_64.tar.gz`

## Verifying

`wget -O - "https://raw.githubusercontent.com/classic-terra/documents/refs/heads/main/binary-updates/terra_v3.6.2.sha256" | sha256sum -c`

## Installing

Depending on your location of terrad.

* Stop terrad
* Copy the extracted binary to your location, e.g. `/usr/local/bin/terrad` or `/home/terrad/go/bin/terrad`
* Verify version, e.g. `terrad version` and `terrad version --long`
* Start terrad
