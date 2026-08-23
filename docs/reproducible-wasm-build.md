# Reproducible WASM build

## Toolchain pins

Record exact versions in CI and locally:

- Emscripten / wasi-sdk version (or Docker image digest)
- CMake / Ninja versions
- Dependency lockfile commit

## Suggested steps

```bash
# example — adjust to this repo's scripts
git submodule update --init --recursive
cmake -S . -B build -DCMAKE_TOOLCHAIN_FILE=$WASI_SDK/share/cmake/wasi-sdk.cmake
cmake --build build
sha256sum build/*.wasm
```

## Verification

Two clean checkouts on the same pinned toolchain should produce identical `.wasm` SHA-256 digests.
If they differ, check timestamps embedded in the binary, randomized symbol order, and absolute paths in DWARF.
