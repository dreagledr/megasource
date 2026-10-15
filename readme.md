Adapting LÖVE to suit Emscripten

LÖVE's megasource, clone LÖVE into the *libs* folder.

## emscripten-fetch

This fork is based on [Davidobot/megasource@emscripten](https://github.com/Davidobot/megasource/tree/emscripten).
The `emscripten-fetch` branch (the default one) tracks
[dreagledr/love](https://github.com/dreagledr/love) on branch `emscripten-fetch`
as the `libs/love` submodule — that is the LÖVE tree that carries the **emfetch**
HTTP module.

Clone it recursively so the submodule comes along:

```
git clone --recursive https://github.com/dreagledr/megasource.git
```

## Building

Pinned toolchain: [emsdk](https://github.com/emscripten-core/emsdk) **2.0.0** and
**Ninja** (newer Emscripten versions removed `getMemory`, which the tooling needs).

```sh
./emsdk install 2.0.0
./emsdk activate 2.0.0
source ./emsdk_env.sh

emcmake cmake . -B build/release -G Ninja -DLOVE_JIT=0 -DCMAKE_BUILD_TYPE=Release
cmake --build build/release
```

Add `-DLOVEJS_COMPAT=1` for the compatibility target (no pthreads). The resulting
`build/release/love/love.js`, `love.wasm` and `love.worker.js` are the engine
binaries consumed by [love.js](https://github.com/dreagledr/love.js).

## Related repositories

* [dreagledr/love](https://github.com/dreagledr/love) — the engine, branch
  `emscripten-fetch`.
* [dreagledr/love.js](https://github.com/dreagledr/love.js) — the web tooling,
  prebuilt engine binaries and a runnable
  [fetch demo](https://github.com/dreagledr/love.js/tree/master/sample).
