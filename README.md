MMI-NPN25.137-33 for Moto G 5

Kernel Modules:
---------------

Download prebuilts folder from Android distribution. Move it to $my_top_dir
For example: git clone https://android.googlesource.com/platform/prebuilts/gcc/linux-x86/arm/arm-linux-androideabi-4.9

mkdir -p  $my_top_dir/prebuilts/gcc/linux-x86/arm

mv arm-linux-androideabi-4.9 $my_top_dir/prebuilts/gcc/linux-x86/arm/.

Rename kernel-msm folder to $my_top_dir/kernel

Download motorola-kernel repo    

mkdir $my_top_dir/motorola

mv motorola-kernel $my_top_dir/motorola/kernel

Check if $my_top_dir/kernel/fs/f2fs points to the $my_top_dir/motorola/kernel/fs/f2fs/ folder

mkdir -p $PWD/out/target/product/potter/obj/kernel

kernel_out_dir=$PWD/out/target/product/potter/obj/kernel

cross=$my_top_dir/prebuilts/gcc/linux-x86/arm/arm-linux-androideabi-4.9/bin/arm-linux-androideabi-

cp $kernel_out_dir/mapphone_defconfig $kernel_out_dir/.config

perl -le 'print \"# This file was automatically generated from:\\n#\\t\" . join(\"\\n#\\t\", @ARGV) . \"\\n\"' kernel/arch/arm/configs/msmcortex-perf_defconfig kernel/arch/arm/configs/ext_config/moto-msmcortex.config kernel/arch/arm/configs/ext_config/mot8953-potter.config && cat kernel/arch/arm/configs/msmcortex-perf_defconfig kernel/arch/arm/configs/ext_config/moto-msmcortex.config kernel/arch/arm/configs/ext_config/mot8953-potter.config ) > out/target/product/potter/obj/KERNEL_OBJ/mapphone_defconfig || ( rm -f out/target/product/potter/obj/KERNEL_OBJ/mapphone_defconfig && false )

make -C kernel O=$kernel_out_dir ARCH=arm CROSS_COMPILE=$cross KBUILD_BUILD_USER= KBUILD_BUILD_HOST= defoldconfig

make -C kernel O=$kernel_out_dir ARCH=arm CROSS_COMPILE=$cross KBUILD_BUILD_USER= KBUILD_BUILD_HOST= headers_install

make -C kernel KBUILD_RELSRC=$my_top_dir/kernel O=$kernel_out_dir ARCH=arm CROSS_COMPILE=$cross KBUILD_BUILD_USER= KBUILD_BUILD_HOST= KCFLAGS=-mno-android

make -C kernel KBUILD_RELSRC=$my_top_dir/kernel O=$kernel_out_dir ARCH=arm CROSS_COMPILE=$cross KBUILD_BUILD_USER= KBUILD_BUILD_HOST= KCFLAGS=-mno-android dtbs

make -C kernel KBUILD_RELSRC=$my_top_dir/kernel O=$kernel_out_dir ARCH=arm CROSS_COMPILE=$cross KBUILD_BUILD_USER= KBUILD_BUILD_HOST= KCFLAGS=-mno-android modules

make -C kernel KBUILD_RELSRC=$my_top_dir/kernel O=$kernel_out_dir INSTALL_MOD_PATH=$my_top_dir/out/target/product/potter INSTALL_MOD_STRIP="--strip-debug --remove-section=.note.gnu.build-id" ARCH=arm CROSS_COMPILE=$cross KBUILD_BUILD_USER= KBUILD_BUILD_HOST= modules_install

WLAN Driver:
------------

cd $PWD/out/target/product/potter/obj
make -C kernel M=../vendor/qcom/opensource/wlan/prima O=$kernel_out_dir ARCH=arm CROSS_COMPILE=$cross KCFLAGS=-mno-android modules WLAN_ROOT=../vendor/qcom/opensource/wlan/prima MODNAME=wlan BOARD_PLATFORM=msm8953 CONFIG_PRONTO_WLAN=m
