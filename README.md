riscv32 のクロスコンパイル toolchain を自分でコンパイルしてみたかった。
msys2 の mingw64 の riscv64 toolchain の設定をコピー、改変してビルドしてみた。

## How to Build

Quoted: <https://github.com/msys2/MINGW-packages/blob/master/README.md#using-packages>

Build:

```console
$ cd ${package-name}
$ MINGW_ARCH=mingw64 makepkg-mingw -sLf
```

Install a built:

```console
$ pacman -U ${package-name}*.pkg.tar.zst
```

## Full procedure

```console
$ cd mingw-w64-riscv32-unknown-elf-binutils
$ MINGW_ARCH=mingw64 makepkg-mingw -sLf
$ package -U mingw-w64-riscv32-unknown-elf-binutils-2.42-1-any.pkg.tar.zst
$ cd ..

$ cd mingw-w64-riscv32-unknown-elf-newlib
# rewrite `_bootstrap` to `1` in PKGBUILD
$ sed -i -e 's/_bootstrap=0/_bootstrap=1/' PKGBUILD
$ MINGW_ARCH=mingw64 makepkg-mingw -sLf
$ package -U mingw-w64-riscv32-unknown-elf-mingw-4.4.0.20231231-1-any.pkg.tar.zst
# rewrite `_bootstrap` to `0` in PKGBUILD
$ sed -i -e 's/_bootstrap=1/_bootstrap=0/' PKGBUILD
$ cd ..

$ cd mingw-w64-riscv32-unknown-elf-gcc
$ MINGW_ARCH=mingw64 makepkg-mingw -sLf
$ package -U mingw-w64-riscv32-unknown-elf-gcc-13.2.0-1-any.pkg.tar.zst
$ cd ..

# Maybe optional
$ cd mingw-w64-riscv32-unknown-elf-newlib
$ MINGW_ARCH=mingw64 makepkg-mingw -sLf
$ package -U mingw-w64-riscv32-unknown-elf-mingw-4.4.0.20231231-1-any.pkg.tar.zst
$ cd ..

```
