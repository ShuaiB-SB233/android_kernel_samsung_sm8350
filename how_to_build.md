## 1. How to Build

- Get toolchain
  - From Android Git server, source code mirror, LineageOS repositories, etc.
    - `gcc/linux-x86/aarch64/aarch64-linux-android-4.9/`
    - `clang/host/linux-x86/`
  - If you want to directly download the tar.gz:
    - https://android.googlesource.com/platform/prebuilts/gcc/linux-x86/aarch64/aarch64-linux-android-4.9/+archive/refs/heads/android12-release.tar.gz
    - https://android.googlesource.com/platform/prebuilts/clang/host/linux-x86/+archive/refs/heads/android11-release/clang-r383902b.tar.gz

- Configure environment variables

```bash
export PATH=/path/to/gcc/linux-x86/aarch64/aarch64-linux-android-4.9/bin:/path/to/clang/host/linux-x86/bin/:$PATH
```

- To build

```bash
make -C $(pwd) DTC_EXT=$(pwd)/tools/dtc ARCH=arm64 CC=clang CLANG_TRIPLE=aarch64-linux-gnu- CROSS_COMPILE=aarch64-linux-android- CONFIG_BUILD_ARM64_DT_OVERLAY=y O=$(pwd)/out vendor/o1q_chn_openx_defconfig -j$(nproc)
make -C $(pwd) DTC_EXT=$(pwd)/tools/dtc ARCH=arm64 CC=clang CLANG_TRIPLE=aarch64-linux-gnu- CROSS_COMPILE=aarch64-linux-android- CONFIG_BUILD_ARM64_DT_OVERLAY=y O=$(pwd)/out -j$(nproc)
```

## 2. Output files

- kernel: `out/arch/arm64/boot/Image`
- modules: `out/drivers/*/*.ko`

## 3. How to Clean

```bash
make O=$(pwd)/out distclean
```
