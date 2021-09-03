CMake & PREFIX variable in toolchain file
===

# Problem
If `PREFIX` variable is defined in file specified as `CMAKE_TOOLCHAIN_FILE` CMake is unable to recognize compiler version (`CMAKE_CXX_COMPILER_VERSION` is empty).

# Steps to reproduce
1. Make sure `g++` is available in `PATH`
2. Create directory `build-a` and run: `cmake -Wno-dev -G Ninja -S <this repository> -B build-a -DCMAKE_TOOLCHAIN_FILE=toolchain-a.cmake` (or any Makefiles generator)
    * CMake output will include `Compiler version found!` message
3. Create directory `build-b` and run: `cmake -Wno-dev -G Ninja -S <this repository> -B build-b -DCMAKE_TOOLCHAIN_FILE=toolchain-b.cmake` (or any Makefiles generator)
    * CMake output will include `Compiler version NOT found!` message
4. Remove `-Wno-dev` from commandline from point 3.
    * A lot of warnings will be reported, related to CMP0053
    * Visible snippets will indicate that `PREFIX` variable set in toolchain file was used as part of names of `#define`s in compiler detection code.