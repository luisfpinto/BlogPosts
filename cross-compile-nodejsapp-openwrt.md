## How to cross compile an application for OpenWRT

Firstly, we will explain what cross-compilation is and why we do need this for our OpenWRT system.
Secondly, We will create a very simple example, a "Hello World" application.

- [About Cross-compilation](#about)
- ["Hello Netbeast World" example application](#hello)
 - [Source file](#src)
- [Cross-compiler](#ccr)
 - [RPi toolchain](#ccrpi)
 - [OpenWRT toolchain](#ccrow)
- [Cross-compilation](#cc)
 - [Cross-compilation with RPi toolchain](#ccpi)
 - [Cross-compilation with OpenWRT toolchain](#ccow)

***

<a name="about">
## About Cross-compilation
</a>

OpenWrt is described as a Linux distribution for embedded devices. 

However, you can't compile some applications like you do in Linux distributions (Ubuntu,Debian...) because OpenWRT doesn't have a make utility. 

If we want to compile an application that need a make utility we need to use a cross-compiler.

A cross-compiler is a compiler capable of creating executable code for a platform other than the one on which the compiler is running. 

Look at this scheme. 

  SOURCE ---------> CROSS COMPILER -------> COMPILED SOURCE

For this example we had:

1. A computer with debian and intel cpu architecture.

2. A RPi2 with OpenWRT and arm cpu architecture.

* We can't compile the "Source" file in the rpi because it doesn't have the make utility. 
* We can't compile the "Source" file in our pc and then copy that in the rpi because they have different cpu architectures (intel vs arm) and it doesn't work.

We need a cross-compiler that simulates RPi's arm architecture and compile it on our pc. 

The result will be a compiled source file which works in the arm platform. 

***

<a name="hello">
## "Hello Netbeast World" example application
</a>

We need a source file and a cross-compiler as we saw before.

<a name="src">
### Source File
</a>

In this case, we will use a simple hello world application programmed in c.

Copy this code and save it as example.c

```
#include<stdio.h>

int main () {
  printf("Hello Netbeast World\n");
  return 0;
}
```

<a name="ccr">
### Cross-Compiler
</a>

We will use two different cross-compilers (If you have a RPi use the first one, use the second one in other cases)

<a name="ccrpi">
#### RPi toolchain
</a>

This cross-compiler has been made for cross-compiling for the RPI. This **ONLY** works with this kind of device. 

You can download it here :  [Rpi cross-compiler ](https://github.com/raspberrypi/tools)

```
git clone https://github.com/raspberrypi/tools
```

<a name="ccrow">
#### OpenWRT toolchain
</a>

This cross-compiler has been provided by OpenWRT developers. This tool can support a lot of architectures (RPi included). You can check this [Table of Hardware](http://wiki.openwrt.org/toh/start) and find out if your device is supported. 

You need to download the OpenWRT system 

```
git clone git://git.openwrt.org/15.05/openwrt.git
```

Prepare system for compilation:

```
cd openwrt
./scripts/feeds update -a
./scripts/feeds install -a
```

Select your system architecture

```
make menuconfig
```

If no errors pop up a shell script menu will be showed.

Choose your correct system architecture:

![menu](https://github.com/netbeast-co/router/blob/master/img/menuToolchain.png)

Choose Package the OpenWrt-based toolchain (This is the most important thing because this is the cross compiler)

![toolchain](https://github.com/netbeast-co/router/blob/master/img/packageToolchain.png)

Exit and save

![exit_toolchain](https://github.com/netbeast-co/router/blob/master/img/saveToolchain.png)

Compile

```
make
```

Now relax. After some time, you will get your toolchain compiled for your selected architecture.

<a name="cc">
### Cross-compilation
</a>

If you want to do this with the Raspberry pi Toolchain go to [this section](#ccpi)

If you want to do this with the OpenWRT Toolchain go to [this section](#ccow)

<a name="ccpi">
#### Cross-Compilation With RPI toolchain
</a>

We have to choose the gcc compiler. Gcc is used for compiling C applications

```
tools/arm-bcm2708/gcc-linaro-arm-linux-gnuebihf-raspbian/bin/arm-linux-gnueabihf-gcc -static hello_world.c
```

The -static option allows to compile the application with required libraries statically. The result will be an a.out file. Copy it to your OpenWRT system and execute it

```
./a.out
```

You will see
```
"Hello Netbeast World"
```

You have cross-compiled your first application successfully.

<a name="ccow">
#### Cross-Compilation with OpenWRT toolchain
</a>

We have to choose the gcc compiler. As we said before, it is used for compiling C applications
```
openwrt/staging_dir/toochain-NAMEOFYOURARCHITETURE--SOMESTUFF/bin/yoursystem-gcc -static hello_world.c 
```
The -static option allow to compile the application with required libraries statically. 

The result will be an a.out file. 

Copy that to your OpenWRT sytem and execute it
```
./a.out
```

You will see
```
"Hello Netbeast World"
```

You have cross-compiled your first application successfully.

***