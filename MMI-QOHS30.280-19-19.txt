#!/bin/bash

me=$(readlink -f $0)
mydir=$(dirname $me)

mkdir -p $mydir/kernel/out/target/product/generic/obj/kernel

kernel_out_dir=$mydir/kernel/out/target/product/generic/obj/kernel

cross=$mydir/prebuilts/gcc/linux-x86/arm/arm-linux-androideabi-4.9/bin/arm-linux-androideabi-

make -j8 -w -C kernel KBUILD_RELSRC=$mydir/kernel O=$kernel_out_dir ARCH=arm CROSS_COMPILE=$cross KBUILD_BUILD_USER= KBUILD_BUILD_HOST= KCFLAGS=-mno-android sprd_sharkl3_defconfig

make -j8 -w -C kernel KBUILD_RELSRC=$mydir/kernel O=$kernel_out_dir ARCH=arm CROSS_COMPILE=$cross KBUILD_BUILD_USER= KBUILD_BUILD_HOST= KCFLAGS=-mno-android

make -j8 -w -C kernel KBUILD_RELSRC=$mydir/kernel O=$kernel_out_dir ARCH=arm CROSS_COMPILE=$cross KBUILD_BUILD_USER= KBUILD_BUILD_HOST= KCFLAGS=-mno-android dtbs

make -j8 -w -C kernel KBUILD_RELSRC=$mydir/kernel O=$kernel_out_dir ARCH=arm CROSS_COMPILE=$cross KBUILD_BUILD_USER= KBUILD_BUILD_HOST= KCFLAGS=-mno-android modules

make -j8 -w -C kernel KBUILD_RELSRC=$mydir/kernel O=$kernel_out_dir INSTALL_MOD_PATH=$mydir/kernel/out/target/product/generic INSTALL_MOD_STRIP="--strip-debug --remove-section=.note.gnu.build-id" ARCH=arm CROSS_COMPILE=$cross KBUILD_BUILD_USER= KBUILD_BUILD_HOST= modules_install
