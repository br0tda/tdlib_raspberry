# tdlib for Raspberry

A plug&play **libtdjson.so v1.7.1** built for **Raspberry Pi**

## How to build

If you want to build by your own follow these steps:

`TDLib` depends on:

* C++14 compatible compiler (Clang 3.4+, GCC 4.9+, MSVC 19.0+ (Visual Studio 2015+), Intel C++ Compiler 17+)
* OpenSSL
* zlib
* gperf (build only)
* CMake (3.0.2+, build only)

```bash
git clone https://github.com/tdlib/td.git
cd td
rm -rf build
mkdir build

sudo nano tdutils/CMakeLists.txt
```

- Now add this instruction
```diff
 if (CMAKE_HOST_SYSTEM_NAME MATCHES "NetBSD")
   target_link_libraries(tdutils PUBLIC /usr/pkg/gcc5/i486--netbsdelf/lib/libatomic.so)
+++ else()
+++   target_link_libraries(tdutils PUBLIC atomic)
endif()
```

- Now you are able to build

```bash
cd build
cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX:PATH=../tdlib -DTD_ENABLE_LTO=ON ..
cmake --build . --target prepare_cross_compiling -j 4
cd ..
php SplitSource.php
cd build
cmake --build . --target install -j 4
cd ..
php SplitSource.php --undo
cd ..
ls -l td/tdlib
```
## Tips

You may have some issues due to low memory on your board: try to [increase your SWAP](https://wpitchoune.net/tricks/raspberry_pi3_increase_swap_size.html)

## Compatibility
Tested on: 
- **Raspberry Pi 3B+ 
Linux raspberrypi 5.4.51-v7+ #1333 SMP Mon Aug 10 16:45:19 BST 2020 armv7l GNU/Linux** 

- Language **Python**
