# Yuzu on Mac

Compiling Yuzu on Mac.

## Prerequisite

### Dependencies

- XCode
- Homebrew

```sh
brew install autoconf automake ccache ffmpeg glslang hidapi libtool libusb lz4 ninja nlohmann-json openssl pkg-config qt@5 sdl2 speexdsp zlib zlib zstd llvm@17
export PATH="$(brew --prefix llvm@17)/bin:$PATH" # Optionally add this to your .zshrc
```

#### Manual Older Version Dependencies Homebrew

You will have to install the following dependencies manually with `brew install <package>.rb` after downloading the following `.rb` files in the current directory (you may have to unlink the existing formulas if you have them):

`fmt@9`: https://raw.githubusercontent.com/Homebrew/homebrew-core/199127ec9184b3be2d6d3a17a3bfc2fd13c6c39a/Formula/fmt.rb

`boost@1.79`: https://github.com/Homebrew/homebrew-core/blob/024a865129f4183c350535ccbd94ce9d01014c41/Formula/boost.rb

## Build

Most of the build steps are from the MacOS build CI script in the `.github/workflows/verify.yml` file.

```sh
mkdir build && cd build
export Qt5_DIR="$(brew --prefix qt@5)/lib/cmake"
cmake .. -GNinja -DCMAKE_BUILD_TYPE=RelWithDebInfo -DYUZU_USE_BUNDLED_VCPKG=OFF -DYUZU_TESTS=OFF -DENABLE_WEB_SERVICE=OFF -DENABLE_LIBUSB=OFF
ninja
```

## Run

```sh
open bin/yuzu.app
```
