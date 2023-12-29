# Consensus-Algorithm

## Contents
- [Environment]()
- [Installation]()
  - [NS-3 (version 3.38)]()
  - [OpenSSL]()
  - [liboqs]()
- [Getting Started]()
  - [add library]()
  - [Blockchain Simulator]()
  - [Network Helper]()
  - [Consensus Algorithm]()
  - [NS-3 build]()
  - [Run Simulator]()
  - [if you want to change algorithm.]()
- [Reference]()


## Environment

## Installation
  ### NS-3 (version 3.38)
  
    git clone https://gitlab.com/nsnam/ns-3-dev.git
    cd ns-3-dev
    git checkout -b ns-3.38-branch ns-3.38

---
  
  ### OpenSSL

  install dependencies.
  
    sudo apt-get update
    sudo apt-get install -y build-essential git cmake python3 libssl-dev

  clone `liboqs` repo.

    git clone https://github.com/open-quantum-safe/liboqs.git

  install `liboqs`.

    cd liboqs
    mkdir build
    cd build
    cmake -GNinja -DOQS_USE_OPENSSL=1 ..
    ninja
    sudo ninja install

  clone `OQS-OpenSSL` repo.

    cd ~
    git clone https://github.com/open-quantum-safe/openssl.git

  build `OQS-OpenSSL`.

    cd openssl
    ./Configure shared --prefix=/usr/local/ssl --openssldir=/usr/local/ssl linux-x86_64
    make -j
    sudo make install

  update `LD_LIBRARY_PATH` environment variable.
  
    export LD_LIBRARY_PATH=/usr/local/ssl/lib:$LD_LIBRARY_PATH

  if you do not have `liboqs.so` in `/usr/local/lib`

    cd ~/openssl
    ./Configure shared --prefix=/usr/local/ssl --openssldir=/usr/local/ssl linux-x86_64 -I/usr/local/include -L/usr/local/lib -DOQS_DIR=/usr/local
    make -j
    sudo make install

---
  
  ### liboqs

  install `liboqs`

    sudo apt install astyle cmake gcc ninja-build libssl-dev python3-pytest python3-pytest-xdist unzip xsltproc doxygen graphviz python3-yaml valgrind
    cd ~
    git clone -b main https://github.com/openquantum-safe/liboqs.git
    cd liboqs
    mkdir build && cd build
    cmake -GNinja -DBUILD_SHARED_LIBS=ON ..
    ninja

  
## Getting Started
  ### 1. add library (liboqs, openssl)
  edit `CMakeLists.txt` in `scratch` folder
  
  before

    # Get source absolute path and transform into relative path
      get_filename_component(scratch_src ${scratch_src} ABSOLUTE)
      get_filename_component(scratch_absolute_directory ${scratch_src} DIRECTORY)
      string(REPLACE "${PROJECT_SOURCE_DIR}" "${CMAKE_OUTPUT_DIRECTORY}"
        scratch_directory ${scratch_absolute_directory}
        )
    
    build_exec(
      EXECNAME ${scratch_name}
      EXECNAME_PREFIX ${target_prefix}
    	SOURCE_FILES "${source_files}"
    	LIBRARIES_TO_LINK "${ns3-libs}" "${ns3-contrib-libs}"
    	EXECUTABLE_DIRECTORY_PATH ${scratch_directory}/
  	)

   after

     # Get source absolute path and transform into relative path
       get_filename_component(scratch_src ${scratch_src} ABSOLUTE)
       get_filename_component(scratch_absolute_directory ${scratch_src} DIRECTORY)
       string(REPLACE "${PROJECT_SOURCE_DIR}" "${CMAKE_OUTPUT_DIRECTORY}"
         scratch_directory ${scratch_absolute_directory}
         )
  
     find_external_library(
       DEPENDENCY_NAME oqs
       HEADER_NAMES oqs.h
       LIBRARY_NAMES oqs
       SEARCH_PATHS "~/liboqs/build/lib/"
     )
  
    set(include_dir "~/liboqs/build/include/")
    include_directories(${include_dir})
    link_libraries(${oqs_LIBRARIES})
    
    find_package(OpenSSL)
  
    build_exec(
  	  EXECNAME ${scratch_name}
  	  EXECNAME_PREFIX ${target_prefix}
  	  SOURCE_FILES "${source_files}"
  	  LIBRARIES_TO_LINK "${ns3-libs}" "${ns3-contrib-libs}" "${OPENSSL_LIBRARIES}" "${oqs_LIBRARIES}"
  	  EXECUTABLE_DIRECTORY_PATH ${scratch_directory}/
  	)

  
  3. Blockchain Simulator
  4. Network Helper
  5. Consensus Algorithm
  6. NS-3 build
  7. Run Simulator
  8. if you want to change algorithm
  
## Reference
  ### [Blockchain Simulator & Network Helper](https://github.com/zhayujie/blockchain-simulator)
  ### [OpenSSL](https://askubuntu.com/questions/1462945/make-j-failing-for-oqs-openssl)
  ### [liboqs](https://github.com/open-quantum-safe/liboqs)

## Contributor
## License

