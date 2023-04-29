## Learnings from Rust 

- Better ways to speed up the compile time for rust 
    - Faster Linking is an way to increase the speed of linking phase (time taken by by the system software to combine multiple objects thrown by the compiler or an assembler ). could use zld in Macos and lld for windows.
        Cargo.toml needs to be change if you are using any of these linkers 
        # On Windows
        ```
        cargo install -f cargo-binutils
        rustup component add llvm-tools-preview
        ```
        [target.x86_64-pc-windows-msvc]
        rustflags = ["-C", "link-arg=-fuse-ld=lld"]
        [target.x86_64-pc-windows-gnu]
        rustflags = ["-C", "link-arg=-fuse-ld=lld"]
        
        # On Linux:
        # - Ubuntu, 
        ```
        sudo apt-get install lld clang
        ```
        # - Arch, 
        ```
        sudo pacman -S lld clang
        ```
        [target.x86_64-unknown-linux-gnu]
        rustflags = ["-C", "linker=clang", "-C", "link-arg=-fuse-ld=lld"]

        # On MacOS,
         ```
         brew install michaeleisel/zld/zld
         ```
        [target.x86_64-apple-darwin]
        rustflags = ["-C", "link-arg=-fuse-ld=/usr/local/bin/zld"]
        [target.aarch64-apple-darwin]
        rustflags = ["-C", "link-arg=-fuse-ld=/usr/local/bin/zld"]
    - 