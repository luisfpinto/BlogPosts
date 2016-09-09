## How to cross compile NPM modules for OpenWRT

In this guide, we will explain how to compile *npm modules* for any cpu-architecture supported by node js.

We will use the *OpenWRT Toolchain*. Before continuing, I recommend reading these useful guides:

[Cross Compile Nodejs](https://github.com/netbeast-co/router/wiki/Cross-Compile-Nodejs-for-OpenWrt)

[What is Cross-Compilation?](https://github.com/netbeast-co/router/wiki/Cross-compile-test-application)

**Listen Up!** : Not all npm modules need to be cross compiled. 

- [Prerequisites](#pre)
- [Coss-compiling npm modules](#cc)
- [Testing](#test)

<a name="pre">
## Prerequisites
</a>

You will need: 
* *OpenWRT tool chain* compiled according to your cpu architecture. If you haven't done yet. Go [here](https://github.com/netbeast-co/router/wiki/Cross-compile-test-application)

* To have <a href="http://npmjs.com">*npm*</a> installed. 

<a name="cc">
## Cross-compiling NPM modules
</a>

* Firstly, we need to define some global variables:
```
export CC=/route/to/openwrt/folder/staging_dir/toolchain-name-of-your-architecture-something/bin/your-architecture-gcc
export CXX=/route/to/openwrt/folder/staging_dir/toolchain-name-of-your-architecture-something/bin/your-architecture-g++
export STAGING_DIR=/route/to/openwrt/folder/staging_dir
```

* Secondly, create a folder for your npm module and run:
```
cd folder_name
npm --arch=<name> install <npm module>
```

* If all went well, you will have your npm module cross-compiled.

<a name="test">
## Testing
</a>

Copy the cross compiled npm module to your device and create one app in order to test it. 

If there are no errors, you have cross compiled your npm module successfully.
