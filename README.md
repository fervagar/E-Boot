
# E-BOOT Linux kernel patch



## Description

This kernel patch is a proof of concept implementation of E-BOOT for Linux v5.3. This feature allows hypervisors to provide high-quality randomness to guest kernels through a pre-reserved memory area. This randomness can be used at the earliest stages of the boot process to satisfy the entropy demand of kernel components requiring high-quality entropy (e.g., to initialize the CSPRNG). E-BOOT is particularly designed to overcome the boot-time entropy starvation problem in virtualized environments, which can produce potential security risks and long delays in the startup of some userland applications.

For more details, please refer to this [research article](https://ieeexplore.ieee.org/document/9050782). It provides a comprehensive description and analysis of the problem and a detailed discussion of the proposed solution.

This feature can be enabled under:

```
-> Processor type and features
   -> Linux guest support
      -> Enable Hypervisor-provided Boot-Time Entropy
```



## How to compile

>  Compiler used: GCC 8.4.0

Download the Linux kernel source v5.3:

```
https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git/snapshot/linux-5.3.tar.gz
```

Decompress the source:

```
$ tar xf linux-5.3.tar.gz
```

Apply the patch:

```
$ cd linux-5.3/
$ patch -p1 < ../e-boot.patch 
```

Prepare the kernel source:

```
$ make x86_64_defconfig ; make kvmconfig
```

Compile it:

```
make -j $(nproc)
```



## Reference

[E-BOOT: Preventing Boot-Time Entropy Starvation in Cloud Systems](https://ieeexplore.ieee.org/document/9050782)

**Authors:** Fernando Vano-Garcia && Hector Marco-Gisbert

