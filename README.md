# BritishPoundCoin

Links
=============
Project website: http://www.britishpoundcoin.co.uk/

Explorer: http://explorer.britishpoundcoin.co.uk/


 Features
=============

* British Pound Coin - Masternode
* PHI1612 PoW/MN algorithm
* MN Reward

British Pound Coin is a community coin, created in anonimity with only 1 milion coins pre-mine in order to setup the network and a total of 66 650 000 milions to be ever in existence, it is a decentralised coin free to be explored by all the community with no collateral interest from other parties, all the development and promotion of the coin stay on the community power, there is no team involved, the community is the team. Because publishing on exchanges require funds you are free to donate any amount of LTC or BTC to these accounts to support the development:

LTC donation account: LM3qZd3UKnfbFWfxyUPLjUuNBZuzPqrj1Z

BTC donation account: 1PoNdCDc6A4jeA1XfBBamwWSJgtRRq24W1

The British Pound Coin is a decentralized peer-to-peer banking financial platform to replace the classic British Pound Coin GBP in the cryptocurrency market, created under an open source license, featuring a built-in cryptocurrency, end-to-end encrypted messaging and decentralized marketplace. The decentralized network aims to provide anonymity and privacy for everyone through a simple user-friendly interface by taking care of all the advanced cryptography in the background.

## Coin Specifications

| Specification | Value |
|:-----------|:-----------|
| Block Size | `4MB` |
| Block Time | `60s` |
| PoW Reward | `140 GPBS` |*
| Masternode Requirement | `30,000 GPBS` |
| Port | `25676` |
| RPC Port | `25674` |
| Masternode Port | `25676` |
| Reward Method  | `Hybrid - POW and Masternode Reward` | 
Total coins: 66 650 000
  
Build British Pound Wallet
----------

### Building for 64-bit Windows

The first step is to install the mingw-w64 cross-compilation tool chain. Due to different Ubuntu packages for each distribution and problems with the Xenial packages the steps for each are different.

Common steps to install mingw32 cross compiler tool chain:

    sudo apt install g++-mingw-w64-x86-64
    
Ubuntu Xenial 16.04 and Windows Subsystem for Linux

    sudo apt install software-properties-common
    sudo add-apt-repository "deb http://archive.ubuntu.com/ubuntu zesty universe"
    sudo apt update
    sudo apt upgrade
    sudo update-alternatives --config x86_64-w64-mingw32-g++ # Set the default mingw32 g++ compiler option to posix.
    
Once the tool chain is installed the build steps are common:

Note that for WSL the British Pound Core source path MUST be somewhere in the default mount file system, for example /usr/src/britishpound, AND not under /mnt/d/. If this is not the case the dependency autoconf scripts will fail. This means you cannot use a directory that located directly on the host Windows file system to perform the build.

The next three steps are an example of how to acquire the source in an appropriate way.

    cd /usr/src
    sudo git clone https://github.com/robinhoodgb/BritishPoundCoin.git
    sudo chmod -R a+r+w britishpound
    
Once the source code is ready the build steps are below.

    PATH=$(echo "$PATH" | sed -e 's/:\/mnt.*//g') # strip out problematic Windows %PATH% imported var
    cd depends
    make HOST=x86_64-w64-mingw32 -j4
    cd ..
    ./autogen.sh # not required when building from tarball
    CONFIG_SITE=$PWD/depends/x86_64-w64-mingw32/share/config.site 
    ./configure --prefix=`pwd`/depends/x86_64-w64-mingw32 --disable-tests
    make HOST=x86_64-w64-mingw32 -j4

### Build on Ubuntu

    sudo apt-get install build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils git cmake libboost-all-dev
    sudo apt-get install software-properties-common
    sudo add-apt-repository ppa:bitcoin/bitcoin
    sudo apt-get update
    sudo apt-get install libdb4.8-dev libdb4.8++-dev

    # If you want to build the Qt GUI:
    sudo apt-get install libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools libprotobuf-dev protobuf-compiler

    git clone https://github.com/robinhoodgb/BritishPoundCoin.git --recursive
    
    cd britishpound

    # Note autogen will prompt to install some more dependencies if needed
    ./autogen.sh
    ./configure 
    make

### Build on OSX

The commands in this guide should be executed in a Terminal application.
The built-in one is located in `/Applications/Utilities/Terminal.app`.

#### Preparation

Install the OS X command line tools:

`xcode-select --install`

When the popup appears, click `Install`.

Then install [Homebrew](https://brew.sh).

#### Dependencies

    brew install cmake automake berkeley-db4 libtool boost --c++11 --without-single --without-static miniupnpc openssl pkg-config protobuf qt5 libevent imagemagick --with-librsvg

NOTE: Building with Qt4 is still supported, however, could result in a broken UI. Building with Qt5 is recommended.

#### Build British Pound Core

1. Clone the britishpound source code and cd into `britishpound`

        git clone --recursive https://github.com/robinhoodgb/BritishPoundCoin.git
        cd britishpound

2.  Build British Pound Core:

    Configure and build the headless britishpound binaries as well as the GUI (if Qt is found).

    You can disable the GUI build by passing `--without-gui` to configure.

        ./autogen.sh
        ./configure
        make

3.  It is recommended to build and run the unit tests:

        make check

### Run

Then you can either run the command-line daemon using `src/britishpoundd` and `src/britishpound-cli`, or you can run the Qt GUI using `src/qt/britishpound-qt`

For in-depth description of Sparknet and how to use britishpound for interacting with contracts, please see [sparknet-guide](doc/sparknet-guide.md).

License
-------

britishpoundcore is GPLv3 licensed.

Development Process
-------------------

The `master` branch is regularly built and tested, but is not guaranteed to be
completely stable. [Tags](https://github.com/britishpound/britishpound/tags) are created
regularly to indicate new official, stable release versions of britishpound.

The contribution workflow is described in [CONTRIBUTING.md](CONTRIBUTING.md).


Testing
-------

Testing and code review is the bottleneck for development; we get more pull
requests than we can review and test on short notice. Please be patient and help out by testing
other people's pull requests, and remember this is a security-critical project where any mistake might cost people
lots of money.

### Automated Testing

Developers are strongly encouraged to write [unit tests](src/test/README.md) for new code, and to
submit new unit tests for old code. Unit tests can be compiled and run
(assuming they weren't disabled in configure) with: `make check`. Further details on running
and extending unit tests can be found in [/src/test/README.md](/src/test/README.md).

There are also [regression and integration tests](/qa) of the RPC interface, written
in Python, that are run automatically on the build server.
These tests can be run (if the [test dependencies](/qa) are installed) with: `qa/pull-tester/rpc-tests.py`

### Manual Quality Assurance (QA) Testing

Changes should be tested by somebody other than the developer who wrote the
code. This is especially important for large or high-risk changes. It is useful
to add a test plan to the pull request description if testing the changes is
not straightforward.

