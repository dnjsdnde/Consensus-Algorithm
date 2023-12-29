# Consensus-Algorithm

## Contents
- [사양]()
- [Prerequisite]()
- [Getting Started]()
- [Reference]()

## Installation
  ### NS-3 (version 3.38)
  
    git clone https://gitlab.com/nsnam/ns-3-dev.git
    cd ns-3-dev
    git checkout -b ns-3.38-branch ns-3.38

  ---
  
  ### OpenSSL

  install dependencies
  
    sudo apt-get update
    sudo apt-get install -y build-essential git cmake python3 libssl-dev

  clone `liboqs` repo

    git clone https://github.com/open-quantum-safe/liboqs.git

  install `liboqs`

    cd liboqs
    mkdir build
    cd build
    cmake -GNinja -DOQS_USE_OPENSSL=1 ..
    ninja
    sudo ninja install

  clone `OQS-OpenSSL` repo

    cd ~
    git clone https://github.com/open-quantum-safe/openssl.git

  build `OQS-OpenSSL`

    cd openssl
    ./Configure shared --prefix=/usr/local/ssl --openssldir=/usr/local/ssl linux-x86_64
    make -j

  
  ---  
  
  ### liboqs

## Getting Started
  1. 
  
## Reference
  ### [Blockchain Simulator & Network Helper](https://github.com/zhayujie/blockchain-simulator)
  ### [OpenSSL](https://askubuntu.com/questions/1462945/make-j-failing-for-oqs-openssl)
    





