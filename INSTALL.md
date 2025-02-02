## Compilation

RocksDB's library should be able to compile without any dependency installed,
although we recommend installing some compression libraries (see below).
We do depend on newer gcc with C++11 support.

There are few options when compiling RocksDB:

* [recommended] `make static_lib` will compile librocksdb.a, RocksDB static library.

* `make shared_lib` will compile librocksdb.so, RocksDB shared library.

* `make check` will compile and run all the unit tests

* `make all` will compile our static library, and all our tools and unit tests. Our tools
depend on gflags. You will need to have gflags installed to run `make all`.

* if Intel SSE instruction set is supported, set USE_SSE=" -msse -msse4.2 " to make sure
SSE4.2 is used to speed up CRC32 when calculating data checksum.


## Dependencies

* You can link RocksDB with following compression libraries:
  - [zlib](http://www.zlib.net/) - a library for data compression.
  - [bzip2](http://www.bzip.org/) - a library for data compression.
  - [snappy](https://code.google.com/p/snappy/) - a library for fast
      data compression.

* All our tools depend on:
  - [gflags](https://code.google.com/p/gflags/) - a library that handles
      command line flags processing. You can compile rocksdb library even
      if you don't have gflags installed.

## Supported platforms

* **Linux - Ubuntu**
    * Upgrade your gcc to version at least 4.7 to get C++11 support.
    * Install gflags. First, try: `sudo apt-get install libgflags-dev`
      If this doesn't work and you're using Ubuntu, here's a nice tutorial:
      (http://askubuntu.com/questions/312173/installing-gflags-12-04)
    * Install snappy. This is usually as easy as:
      `sudo apt-get install libsnappy-dev`.
    * Install zlib. Try: `sudo apt-get install zlib1g-dev`.
    * Install bzip2: `sudo apt-get install libbz2-dev`.
* **Linux - CentOS**
    * Upgrade your gcc to version at least 4.7 to get C++11 support:
      `yum install gcc47-c++`
    * Install gflags:

              wget https://gflags.googlecode.com/files/gflags-2.0-no-svn-files.tar.gz
              tar -xzvf gflags-2.0-no-svn-files.tar.gz
              cd gflags-2.0
              ./configure && make && sudo make install

    * Install snappy:

              wget https://snappy.googlecode.com/files/snappy-1.1.1.tar.gz
              tar -xzvf snappy-1.1.1.tar.gz
              cd snappy-1.1.1
              ./configure && make && sudo make install

    * Install zlib:

              sudo yum install zlib
              sudo yum install zlib-devel

    * Install bzip2:

              sudo yum install bzip2
              sudo yum install bzip2-devel

* **OS X**:
    * Install latest C++ compiler that supports C++ 11:
        * Update XCode:  run `xcode-select --install` (or install it from XCode App's settting).
        * Install via [homebrew](http://brew.sh/).
            * If you're first time developer in MacOS, you still need to run: `xcode-select --install` in your command line.
            * run `brew tap homebrew/dupes; brew install gcc47 --use-llvm` to install gcc 4.7 (or higher).
    * Install zlib, bzip2 and snappy libraries for compression.
    * Install gflags. We have included a script
    `build_tools/mac-install-gflags.sh`, which should automatically install it (execute this file instead of runing using "source" command).
    If you installed gflags by other means (for example, `brew install gflags`),
    please set `LIBRARY_PATH` and `CPATH` accordingly.
    * Please note that some of the optimizations/features are disabled in OSX.
    We did not run any production workloads on it.

* **iOS**:
  * Run: `TARGET_OS=IOS make static_lib`
