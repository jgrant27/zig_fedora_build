# Build Zig Lang on Fedora Linux

Instructions for building the [Zig language](https://ziglang.org) on [Fedora](https://getfedora.org) Linux.


Install all the pre-reqs for building Zig

```
|jgrant| mephisto in ~/build/
[master ✔] → sudo dnf install cmake clang clang-devel llvm llvm-devel lld lld-devel libstdc++-static libstdc++-devel glibc-static
```

Clone the Zig repo

```
|jgrant| mephisto in ~/build
 → git clone https://github.com/ziglang/zig.git
Cloning into 'zig'...
remote: Enumerating objects: 62, done.
remote: Counting objects: 100% (62/62), done.
remote: Compressing objects: 100% (49/49), done.
remote: Total 80781 (delta 23), reused 30 (delta 13), pack-reused 80719
Receiving objects: 100% (80781/80781), 70.41 MiB | 30.80 MiB/s, done.
Resolving deltas: 100% (57714/57714), done.
```

Change into the cloned repo dir

```
|jgrant| mephisto in ~/build
 → cd zig

|jgrant| mephisto in ~/build/zig
[master ✔] →
```

Create the cmake build directory, change into it and build
```
mkdir build
cd build
cmake ..
time make -j8 install
```

Add the `zig` binary to your path.
```
|jgrant| mephisto in ~/build/zig/build
[master ✔] → ln -s $HOME/build/zig/build/zig $HOME/bin/
```

Now when you run `zig` you should see something like the following output !

```
|jgrant| mephisto in ~
 → zig
Usage: zig [command] [options]

Commands:
  build                        build project from build.zig
  build-exe [source]           create executable from source or object files
  build-lib [source]           create library from source or object files
  build-obj [source]           create object from source or assembly
  builtin                      show the source code of @import("builtin")
  cc                           C compiler
  fmt                          parse files and render in canonical zig format
  id                           print the base64-encoded compiler id
  init-exe                     initialize a `zig build` application in the cwd
  init-lib                     initialize a `zig build` library in the cwd
  libc [paths_file]            Display native libc paths file or validate one
  run [source] [-- [args]]     create executable and run immediately
  translate-c [source]         convert c code to zig code
  targets                      list available compilation targets
  test [source]                create and run a test build
  version                      print version number and exit
  zen                          print zen of zig and exit

Compile Options:
  --c-source [options] [file]  compile C source code
  --cache-dir [path]           override the local cache directory
  --cache [auto|off|on]        build in cache, print output path to stdout
  --color [auto|off|on]        enable or disable colored error messages
  --disable-gen-h              do not generate a C header file (.h)
  --disable-valgrind           omit valgrind client requests in debug builds
  --eh-frame-hdr               enable C++ exception handling by passing --eh-frame-hdr to linker
  --enable-valgrind            include valgrind client requests release builds
  -fstack-check                enable stack probing in unsafe builds
  -fno-stack-check             disable stack probing in safe builds
  -fsanitize-c                 enable C undefined behavior detection in unsafe builds
  -fno-sanitize-c              disable C undefined behavior detection in safe builds
  --emit [asm|bin|llvm-ir]     (deprecated) emit a specific file format as compilation output
  -fPIC                        enable Position Independent Code
  -fno-PIC                     disable Position Independent Code
  -ftime-report                print timing diagnostics
  -fstack-report               print stack size diagnostics
  -fmem-report                 print memory usage diagnostics
  -fdump-analysis              write analysis.json file with type information
  -femit-docs                  create a docs/ dir with html documentation
  -fno-emit-docs               do not produce docs/ dir with html documentation
  -femit-bin                   (default) output machine code
  -fno-emit-bin                do not output machine code
  -femit-asm                   output .s (assembly code)
  -fno-emit-asm                (default) do not output .s (assembly code)
  -femit-llvm-ir               produce a .ll file with LLVM IR
  -fno-emit-llvm-ir            (default) do not produce a .ll file with LLVM IR
  --libc [file]                Provide a file which specifies libc paths
  --name [name]                override output name
  --output-dir [dir]           override output directory (defaults to cwd)
  --pkg-begin [name] [path]    make pkg available to import and push current pkg
  --pkg-end                    pop current pkg
  --main-pkg-path              set the directory of the root package
  --release-fast               build with optimizations on and safety off
  --release-safe               build with optimizations on and safety on
  --release-small              build with size optimizations on and safety off
  --single-threaded            source may assume it is only used single-threaded
  -dynamic                     create a shared library (.so; .dll; .dylib)
  --strip                      exclude debug symbols
  -target [name]               <arch>-<os>-<abi> see the targets command
  --verbose-tokenize           enable compiler debug output for tokenization
  --verbose-ast                enable compiler debug output for AST parsing
  --verbose-link               enable compiler debug output for linking
  --verbose-ir                 enable compiler debug output for Zig IR
  --verbose-llvm-ir            enable compiler debug output for LLVM IR
  --verbose-cimport            enable compiler debug output for C imports
  --verbose-cc                 enable compiler debug output for C compilation
  --verbose-llvm-cpu-features  enable compiler debug output for LLVM CPU features
  -dirafter [dir]              add directory to AFTER include search path
  -isystem [dir]               add directory to SYSTEM include search path
  -I[dir]                      add directory to include search path
  -mllvm [arg]                 (unsupported) forward an arg to LLVM's option processing
  --override-lib-dir [arg]     override path to Zig lib directory
  -ffunction-sections          places each function in a separate section
  -D[macro]=[value]            define C [macro] to [value] (1 if [value] omitted)
  -mcpu [cpu]                  specify target CPU and feature set
  -code-model [default|tiny|   set target code model
               small|kernel|
               medium|large]

Link Options:
  --bundle-compiler-rt         for static libraries, include compiler-rt symbols
  --dynamic-linker [path]      set the path to ld.so
  --each-lib-rpath             add rpath for each used dynamic library
  --library [lib]              link against lib
  --forbid-library [lib]       make it an error to link against lib
  --library-path [dir]         add a directory to the library search path
  --linker-script [path]       use a custom linker script
  --version-script [path]      provide a version .map file
  --object [obj]               add object file to build
  -L[dir]                      alias for --library-path
  -l[lib]                      alias for --library
  -rdynamic                    add all symbols to the dynamic symbol table
  -rpath [path]                add directory to the runtime library search path
  --subsystem [subsystem]      (windows) /SUBSYSTEM:<subsystem> to the linker
  -F[dir]                      (darwin) add search path for frameworks
  -framework [name]            (darwin) link against framework
  --ver-major [ver]            dynamic library semver major version
  --ver-minor [ver]            dynamic library semver minor version
  --ver-patch [ver]            dynamic library semver patch version

Test Options:
  --test-filter [text]         skip tests that do not match filter
  --test-name-prefix [text]    add prefix to all tests
  --test-cmd [arg]             specify test execution command one arg at a time
  --test-cmd-bin               appends test binary path to test cmd args
  --test-evented-io            runs the test in evented I/O mode
```
