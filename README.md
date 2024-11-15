<picture>
    <source srcset="https://raw.githubusercontent.com/leptos-rs/leptos/main/docs/logos/Leptos_logo_Solid_White.svg" media="(prefers-color-scheme: dark)">
    <img src="https://raw.githubusercontent.com/leptos-rs/leptos/main/docs/logos/Leptos_logo_RGB.svg" alt="Leptos Logo">
</picture>

# Leptos WASI Starter Template

This is a template for use with the [Leptos](https://github.com/leptos-rs/leptos) web
framework and the [cargo-leptos](https://github.com/akesson/cargo-leptos) tool
using [leptos_wasi](https://github.com/leptos-rs/leptos_wasi).

## Prerequisites

```bash
cargo install cargo-leptos --locked
cargo install cargo-generate
```

## Init a new project

```bash
cargo leptos new --git https://github.com/leptos-rs/start-wasi
```

### How to serve static files?

You **MUST** write the `serve_static_files` function in
[`src/server.rs`](src/server.rs).

We make no assumptions about which world is available for your component.
It is not guaranteed that you will give filesystem access to your component.
That's why you need to explicitly write the logic to serve static files.

If you do want to use `wasi:filesystem`, then you can check the link
in the comments of the said function. In the future, we may add default
implementation in `leptos_wasi` to ease your life.

## Compiling your project

### For release

```bash
cargo leptos build --release
```

### For development

```bash
cargo leptos build
```

### How to run the component?

Well, by nature, WebAssembly give you the freedom to chose the runtime you want.

For now, we have only tested running the commponents with [Wasmtime](https://wasmtime.dev):

```
wasmtime serve {{component_outdir}}/wasm32-wasip2/debug/{{crate_name}}.wasm
```

Be sure to add the flags you need to provide the worlds your component depends on:

* `-Scli` for the CLI world,
* `--dir target/site/pkg` if you want, for example, to use `wasi:filesystem` to serve
  the static assets,
* `--env` if you want to pass environment variables,

## Licensing

This template itself is released under the Unlicense. You should replace the LICENSE for your own application with an appropriate license if you plan to release it publicly.
