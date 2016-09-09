## How to cross compile Nodejs for OpenWRT

In this guide, we will explain how to compile Nodejs for any cpu-architecture supported.

We will use the **OpenWRT Toolchain**/**RPI Toolchain**. Before continuing, I recommend reading this useful [guide](https://github.com/netbeast-co/router/wiki/Cross-compile-test-application) where that tool is introduced.

- [Prerequisites](#pre)
- [Cross-compiling](#cc)
 - [Configuration file](#conf)
- [Testing](#testing)

***

<a name="pre">
## Prerequisites
</a>

**Option 1**: You should have downloaded and compiled the **OpenWRT Toolchain** according to your cpu-architecture. 

**Option 2**: You should have downloaded the **RPI Toolchain** (only raspberry pi architectures)

***

<a name="cc">
## Cross-compiling
</a>

Firstly, We need to download node source files. 

`git clone https://github.com/nodejs/node`

A folder named "node" will be created. 

`cd node`

Now, we need to define some global variables. This is the most important step.

**Option 1: OpenWRT Toolchain:**

```
export AR=/route/to/openwrt/folder/staging_dir/toolchain-name-of-your-architecture-something/bin/your-architecture-ar
export CC=/route/to/openwrt/folder/staging_dir/toolchain-name-of-your-architecture-something/bin/your-architecture-gcc
export CXX=/route/to/openwrt/folder/staging_dir/toolchain-name-of-your-architecture-something/bin/your-architecture-g++
export LINK=/route/to/openwrt/folder/staging_dir/toolchain-name-of-your-architecture-something/bin/your-architecture-g++
export RANLIB=/route/to/openwrt/folder/staging_dir/toolchain-name-of-your-architecture-something/bin/your-architecture-ranlib
export STAGING_DIR=/route/to/openwrt/folder/staging_dir
export LIBPATH=/route/to/openwrt/folder/staging_dir/toolchain-name-of-your-architecture-something/lib
export LDFLAGS='-Wl,-rpath-link '${LIBPATH}
```

**Option 2: RPI Toolchain**

```
export AR=tools/arm-bcm2708/gcc-linaro-arm-linux-gnuebihf-raspbian/bin/arm-linux-gnueabihf-ar
export CC =tools/arm-bcm2708/gcc-linaro-arm-linux-gnuebihf-raspbian/bin/arm-linux-gnueabihf-gcc
export CXX =tools/arm-bcm2708/gcc-linaro-arm-linux-gnuebihf-raspbian/bin/arm-linux-gnueabihf-g++
export LINK =tools/arm-bcm2708/gcc-linaro-arm-linux-gnuebihf-raspbian/bin/arm-linux-gnueabihf-g++
```

<a name="conf">
### Configuration file
</a>

**Option 1: OpenWRT Toolchain:**
```
./configure --without-snapshot --without-npm 
```
**Option 2: RPI Toolchain**
```
./configure --without-snapshot --without-npm --dest-cpu=YOUR_ARCHITECTURE --dest-os=YOUR_OPERATIVE_SYSTEM --fully-static
```

* Compile 
```
make
```

* If all went fine, you will get your compiled version of nodejs in node/out/Release/node

<a name="testing">
## Testing
</a>

Copy node file to your OpenWRT device and execute
```
./node
console.log("Hello Netbeast Wolrd")
```

You will see "Hello Netbeast World" on the terminal.

You have cross compiled NodeJS successfully.
