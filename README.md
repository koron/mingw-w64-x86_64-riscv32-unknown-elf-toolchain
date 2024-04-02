## How to Build

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
$ MINGW_ARCH=mingw64 makepkg-mingw -sLf
$ package -U mingw-w64-riscv32-unknown-elf-mingw-4.4.0.20231231-1-any.pkg.tar.zst
# rewrite `_bootstrap` to `0` in PKGBUILD
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
