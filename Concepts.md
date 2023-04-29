## Learnings from Rust 

- Better ways to speed up the compile time for rust 
    - Faster Linking is an way to increase the speed of linking phase (time taken by by the system software to combine multiple objects thrown by the compiler or an assembler ). could use zld in Macos and lld for windows.
        Cargo.toml needs to be change if you are using any of these linkers 
        # On Windows
        ```
        cargo install -f cargo-binutils
        rustup component add llvm-tools-preview
        ```
        Add the following to your Cargo.toml
        ```
        [target.x86_64-pc-windows-msvc]
        rustflags = ["-C", "link-arg=-fuse-ld=lld"]
        [target.x86_64-pc-windows-gnu]
        rustflags = ["-C", "link-arg=-fuse-ld=lld"]
        ```
        # On Linux:
        # - Ubuntu, 
        ```
        sudo apt-get install lld clang
        ```
        # - Arch, 
        ```
        sudo pacman -S lld clang
        ```
        Add the following to your Cargo.toml
        ```
        [target.x86_64-unknown-linux-gnu]
        rustflags = ["-C", "linker=clang", "-C", "link-arg=-fuse-ld=lld"]
        ```
        # On MacOS,
         ```
         brew install michaeleisel/zld/zld
        ```
        Add the following to your Cargo.toml
        ```
        [target.x86_64-apple-darwin]
        rustflags = ["-C", "link-arg=-fuse-ld=/usr/local/bin/zld"]
        [target.aarch64-apple-darwin]
        rustflags = ["-C", "link-arg=-fuse-ld=/usr/local/bin/zld"]
        ```
    - Could also use watcher like cargo-watch

    - Testing command :
    ```
    cargo test
    ```
    does a unit test for the rust project with the written test cases.
    
    ```
    cargo tarpaulin --ignore-tests
    ```
    computes code coverage for the project(i.e, collects data weather the part of project has been ovelooked or beeen not tested)
    - Linting can be done using a package like clippy

    - Security Vulnarabilities 
    ```
    cargo audit
    ```
    -