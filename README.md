# Building of intgemm fallback module

Clone and get submodules.

```
cd intgemm
patch -p 1 < ../patch-intgemm.diff
cd ..
```

```
mkdir build
cd build
emcmake cmake ..
emmake make
```

Inspect wasm file using `wasm2wat intgemm_fallback.wasm`. There shall no be imports except memory, and no elements for table.

TODOs to hack around shadow stack:
- when instantiated via `WebAssembly.Instance`, provide a main memory
- when main module instantiated, allocate memory using main module and call `staveRestore` to the end of allocated block.
