# Cockatrice

Cockatrice is an open-source multiplatform software for playing card games over a network. It is fully client-server based
to prevent any kind of cheating, though it supports single-player games without
a network interface as well. Both client and server are written in Qt 4.

# License

Cockatrice is free software, licensed under the GPLv2; see COPYING for details.

# Building

Dependencies:

- [Qt](http://qt-project.org/) 

- [protobuf](http://code.google.com/p/protobuf/)

- [CMake](http://www.cmake.org/)

The server requires an additional dependency:

- [libgcrypt](http://www.gnu.org/software/libgcrypt/)

```
mkdir build
cd build
cmake ..
make
make install
```

The following flags can be passed to `cmake`:

- `-DWITH_SERVER=1` build the server

- `-DWITHOUT_CLIENT=1` do not build the client

# Windows full build instructions

- Install TDM ([tdm-gcc.tdragon.net/download](http://tdm-gcc.tdragon.net/download))
  - Get Bundle Installer, 32 bit version


- Get MSYS [sourceforge.net/projects/mingw-w64/files/...](http://sourceforge.net/projects/mingw-w64/files/External%20binary%20packages%20%28Win64%20hosted%29/MSYS%20%2832-bit%29/)
  - Get most recent non-src build


- Copy MSYS into the TDM folder (C:/MinGW32)


- Download proto full lib 2.4.1 (http://code.google.com/p/protobuf/)
  - In the MinGW shell (MSYS), go to protobuf folder:

```
./configure --prefix=`cd /c/MinGW32; pwd -W`
```

- **NOTE** These are ` not '

```
make
make install
```
- Delete 'libprotobuf.dll.a' and 'libprotobuf-lite.dll.a' from MinGW\lib folder (no clue why, but they were causing conflicts for me)

  
- Qt for Windows ([sourceforge.net/projects/mingwbuilds/...](http://sourceforge.net/projects/mingwbuilds/files/external-binary-packages/Qt-Builds/))
  - Get most recent 4.X x32 build
  - Extract to C:\Qt\4.8.4\
  - Edit C:\Qt\4.8.4\bin\qt.conf
  
```  
Prefix = c:/Qt/4.8.4/
```

- Install CMake ([cmake.org/cmake/resources/software.html](http://www.cmake.org/cmake/resources/software.html))
- Remove cygwin from system path if it is there
- Run CMake:
  - Either add these environment variables or pass them with -D: (eg. -DQT_QMAKE_EXECUTABLE=...)
    - QT_QMAKE_EXECUTABLE=C:\Qt\4.8.4\bin\qmake.exe
    - PROTOBUF_INCLUDE_DIR=C:\MinGW32\lib
    - PROTOBUF_LIBRARY=C:\MinGW32\bin\libprotobuf-7.dll
  - If Visual Studio is installed, do: cmake -G "MinGW Makefiles" ..
  - Run in Cockatrice folder:
  
```
mkdir build
cd build
cmake -G "MinGW Makefiles" -DQT_QMAKE_EXECUTABLE=C:\Qt\4.8.4\bin\qmake.exe -DPROTOBUF_INCLUDE_DIR=C:\MinGW32\lib -DPROTOBUF_LIBRARY=C:\MinGW32\bin\libprotobuf-7.dll ..
```
   
- Run in build folder:
```
mingw32-make
```

- Copy the following files from MinGW32\bin to the folder with cockatrice.exe
  - libgcc_s_sjlj-1.dll
  - libprotobuf-7.dll
  - libstdc++-6.dll
  - mingwm10.dll

- Copy the following files from Qt\4.8.4\bin to the folder with cockatrice.exe
  - QtCore4.dll
  - QtGui4.dll
  - QtMultimedia4.dll
  - QtNetwork4.dll
  - QtSvg4.dll
  - QtXml4.dll
  - libwinpthread-1.dll

- Copy the following files from Qt\4.8.4\plugins to a subfolder named plugins, maintain the directory structure
  - codecs\qcncodecs4.dll
  - codecs\qjpcodecs4.dll
  - codecs\qkrcodecs4.dll
  - codecs\qtwcodecs4.dll
  - iconengines\qsvgicon4.dll
  - imageformats\qjpeg4.dll
  - imageformats\qsvg4.dll

# Running

`oracle` fetches card data

`cockatrice` is the game client

`servatrice` is the server
