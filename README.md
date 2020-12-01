# tdlib for Raspberry

A plug&play **libtdjson.so** built for **Raspberry Pi**

## How to build

If you want to build by your own follow these steps:

```bash
git clone https://github.com/tdlib/td.git
cd td
git checkout v1.7.0
rm -rf build
mkdir build

sudo nano tdutils/td/utils/Time.cpp
```

- Now follow these [guide](https://github.com/tdlib/td/issues/1191#issue-700415611) and add the lines marked with (+) approximately at the end of the file.

```bash
 if (CMAKE_HOST_SYSTEM_NAME MATCHES "NetBSD")
   target_link_libraries(tdutils PUBLIC /usr/pkg/gcc5/i486--netbsdelf/lib/libatomic.so)
+else()
+  target_link_libraries(tdutils PUBLIC atomic)
 endif()
```

- Now you are able to build

```bash
cd build
cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX:PATH=../tdlib ..
cmake --build . --target install
cd ..
cd ..
ls -l td/tdlib
```

## Compatibility
Tested on: 
- **Raspberry Pi 3B+ 
Linux raspberrypi 5.4.51-v7+ #1333 SMP Mon Aug 10 16:45:19 BST 2020 armv7l GNU/Linux**
