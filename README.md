# Electroneum GUI ( as for today  - not official release )

Copyright (c) 2014-2017, The Monero Project
Copyright (c) 2017, The Electroneum Project 



## Supporting the Project

Electroneum development can be supported directly through donations.


The Electroneum donation address is: `etnkAs4Lq4a4ME41hN7MFcDKFKjgaACtyTtnCyvvwNyb2frUS9TswQ1SnAapAxpUuqKjkss8Jvs6Wg8Bx88fb9Jb1KbkDSmDmj` 


The Bitcoin donation address is: `1L3SHpMuxrMDnvvWY4fuwzAgJbDuL7Pdt6`

### Build instructions

#### On Windows 32 bit:

Binaries for Windows are built on Windows using the MinGW toolchain within [MSYS2 environment](http://msys2.github.io). 

*Note: only build application for Windows x86. To build application for 64-bit Windows you will need Qt5 with MinGW for 64-bit Windows.

Install Qt5 from [official site](https://www.qt.io/download-open-source/)

   - download unified installer, run and select following options:

       - Qt > Qt 5.7 > MinGW 5.3.0 32 bit

       - Tools > MinGW 5.3.0

   - continue with installation 


**Preparing the Build Environment**

* Download and install the [MSYS2 installer](http://msys2.github.io), either the 64-bit or the 32-bit package, depending on your system.

        MSYS2 64 bit: http://repo.msys2.org/distrib/x86_64/msys2-x86_64-20161025.exe

        MSYS2 32 bit: http://repo.msys2.org/distrib/i686/msys2-i686-20161025.exe

* Correct MSYS2 install directories are: c:\msys32 for Windows 32-bit PC and c:\msys64 for Windows 64-bit.

** If MSYS2 already installed with path other then c:/msys64 (for Windows 64) or c:/msys32 (for 32 bit Windows)**

* Download both Electroneum package archives from:
      [GUI https://github.com/tviho/electroneum-core.git](https://github.com/tviho/electroneum-core.git)
      [Daemon https://github.com/electroneum/electroneum.git](https://github.com/electroneum/electroneum.git)

* Unpack GUI source to c:/build

* Unpack daemon source inside electroneum-core folder into the "electroneum" subdirectory. Daemon sources will have path:

       c:/build/electroneum-core/electroneum

* Edit daemon source file "Makefile": change path "MSYS2_FOLDER=c:/msys32" to correct MSYS2 path for your PC. Example: "MSYS2_FOLDER=d:/msys32"

* Edit GUI source QT file "electroneum-wallet-gui.pro": change path "c:/msys32" to correct MSYS2 path for your PC. Example: "d:/msys32"

* follow build instructions below

**Update or install required Dependencies**

* Update packages using pacman:  

        pacman -Syuu  

* Exit the MSYS shell using Alt+F4

* Edit the properties for the `MSYS2 Shell` shortcut changing "msys2_shell.bat" to "msys2_shell.cmd -mingw64" for 64-bit builds or "msys2_shell.cmd -mingw32" for 32-bit builds

* Restart MSYS shell via modified shortcut for Windows 32 "msys2_shell.cmd -mingw32" and update packages again using pacman:  

        pacman -Syuu  

* Install required tools:

        pacman -S git tar zlib wget

* Install dependencies:

    Build for 32-bit Windows:
 
        pacman -S mingw-w64-i686-toolchain make mingw-w64-i686-cmake mingw-w64-i686-boost

* Install the latest version of boost, specificly the required static libraries
    ```
    cd
    wget http://sourceforge.net/projects/boost/files/boost/1.64.0/boost_1_64_0.tar.bz2
    tar xjf boost_1_64_0.tar.bz2
    cd boost_1_64_0
    ./bootstrap.sh mingw
    ./b2 --prefix=/mingw32/boost --layout=tagged --without-mpi --without-python toolset=gcc address-model=32 variant=debug,release link=static threading=multi runtime-link=static -j$(nproc) install
    ``` 


**Building**

* run:

        cd /c/build/electroneum-core

        ./build.sh

* The Electroneum-core executable "electroneum-wallet-gui.exe" can be found in the "electroneum-core/build/release/bin"


### On Linux:

(Tested on Ubuntu 16.04 x86, 16.10 x64, Gentoo x64 and Linux Mint 18 "Sarah" - Cinnamon x64)

1. Install Electroneum dependencies

  - For Ubuntu and Mint

	`sudo apt install build-essential cmake libboost-all-dev miniupnpc libunbound-dev graphviz doxygen libunwind8-dev pkg-config libssl-dev`

  - For Gentoo

	`sudo emerge app-arch/xz-utils app-doc/doxygen dev-cpp/gtest dev-libs/boost dev-libs/expat dev-libs/openssl dev-util/cmake media-gfx/graphviz net-dns/unbound net-libs/ldns net-libs/miniupnpc sys-libs/libunwind`

2. Grab an up-to-date copy of the electroneum-core repository

	`git clone https://github.com/tviho/electroneum-core.git`

3. Go into the repository

	`cd electroneum-core`

4. Install the GUI dependencies

  - For Ubuntu 16.04 x86

	`sudo apt-get install qtbase5-dev qt5-default qtdeclarative5-dev qml-module-qtquick-controls qml-module-qtquick-xmllistmodel qttools5-dev-tools qml-module-qtquick-dialogs`

  - For Ubuntu 16.04+ x64

    `sudo apt-get install qtbase5-dev qt5-default qtdeclarative5-dev qml-module-qtquick-controls qml-module-qtquick-xmllistmodel qttools5-dev-tools qml-module-qtquick-dialogs qml-module-qt-labs-settings libqt5qml-graphicaleffects`

  - For Linux Mint 18 "Sarah" - Cinnamon x64

    `sudo apt install qml-module-qt-labs-settings qml-module-qtgraphicaleffects`

  - For Gentoo

    `sudo emerge dev-qt/qtcore:5 dev-qt/qtdeclarative:5 dev-qt/qtquickcontrols:5 dev-qt/qtquickcontrols2:5 dev-qt/qtgraphicaleffects:5`

  - Optional : To build the flag `WITH_SCANNER`

    - For Ubuntu and Mint

      `sudo apt install qtmultimedia5-dev qml-module-qtmultimedia libzbar-dev`

    - For Gentoo

      The *qml* USE flag must be enabled.

      `emerge dev-qt/qtmultimedia:5 media-gfx/zbar`

5. Build the GUI

  - For Ubuntu and Mint

	`./build.sh`

  - For Gentoo

    `QT_SELECT=5 ./build.sh`

The executable can be found in the build/release/bin folder.

