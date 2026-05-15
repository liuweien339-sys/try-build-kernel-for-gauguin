# 如何为gauguin LineageOS23.2构建内核?

# 克隆源码
克隆你的内核源码
```shell
git clone https://github.com/LineageOS/android_kernel_xiaomi_gauguin.git -b lineage-23.2 --depth=1 kernel
```
# 下载工具链
更新一下包管理
```shell
sudo apt update
```
下载工具链
```shell
sudo apt install bc bison flex libssl-dev libelf-dev libdw-dev build-essential lz4 git python3 curl
dwarves cpio gcc-aarch64-linux-gnu
```
# 下载Clang
```shell
wget https://android.googlesource.com/platform/prebuilts/clang/host/linux-x86/+archive/refs/heads/android16-qpr2-release/clang-r563880c.tar.gz
```
创建clang解压目录
```shell
mkdir clang
```
解压clang
```shell
tar -xzf "clang-r563880c.tar.gz" -C ~/clang
```
# 下载 GCC
```shell
wget https://android.googlesource.com/platform/prebuilts/gcc/linux-x86/aarch64/aarch64-linux-android-4.9/+archive/refs/heads/android12L-release.tar.gz
```
创建GCC解压目录
```shell
mkdir gcc
```
解压GCC
```shell
tar -xzf android12L-release.tar.gz -C ~/gcc
```
# 设置PATH
```shell
export PATH="~/clang/bin:$PATH"
```
```shell
export PATH="~/gcc/bin:$PATH"
```
```shell
export ARCH=arm64
export SUBARCH=arm64
export LLVM=1
export LLVM_IAS=1
export CROSS_COMPILE=aarch64-linux-gnu-
```
# 让内核变得更好
这里我用的KernelSU当作内核的附加 你可以选择其他的

先进入内核源码目录
```shell
cd ~/kernel
```
集成KernelSU
```shell
wget https://raw.githubusercontent.com/backslashxx/KernelSU/refs/heads/master/kernel/setup.sh | bash -s master
```
# 制作内核的config
```shell
make vendor/lito-perf_defconfig vendor/xiaomi/gauguin.config
```
# 开始编译
```shell
make -j$(nproc) Image 2>&1 | tee ~/build.log
```
这个过程可能需要一些时间 稍等一会吧
# 结束
编译成功后 ~/kernel/arch/arm64/boot/里面会有一个Image 可以把它做成AnyKernel3刷入手机
