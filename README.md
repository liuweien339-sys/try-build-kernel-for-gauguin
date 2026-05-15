# 如何为gauguin构建内核?

# 克隆源码
首先 克隆你的内核源码 这里以LineageOS23.2举例
```shell
git clone https://github.com/LineageOS/android_kernel_xiaomi_gauguin.git -b lineage-23.2 --depth=1
```
# 下载工具链
首先 更新一下包管理
```shell
sudo apt update
```
随后 下载工具链
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
wget https://android.googlesource.com/platform/prebuilts/gcc/linux-x86/aarch64/aarch64-linux-android-4.9/+archive/refs/heads/android12L-release.tar.gz
```
