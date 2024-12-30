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
cargo install cargo-make
```

## Init a new project

```bash
cargo leptos new --git https://github.com/tqq1994516/start-wasmcloud
```

## Compiling your project

### For release

Modify the `wasmcloud.toml` file, uncomment the line containing the comment `prod build` and comment out the line containing the comment `dev build`.

```bash
wash build
```

### For development

Modify the `wasmcloud.toml` file, uncomment the line containing the comment `dev build` and comment out the line containing the comment `prod build`.

```bash
wash build
```

### How to run the component?

This template can quickly run `leptos-wasi` as an application in the `wasmCloud` environment.

In order to enable the correct access to the front-end static resources, it's necessary to replace the value of `${PWD}` on line 38 in the `wadm.yaml` with the actual present working directory (pwd) value of the current project before running. Currently, I haven't found a good way to replace this value when generating the template. So, at this stage, it needs to be modified manually. For example: xxx.:

The directory of my project is located at `/root/demo`, so my wadm.yaml needs to be modified like this.

```yaml
        - type: link
          properties:
            target: blobstore-fs
            namespace: wasi
            package: blobstore
            interfaces: [blobstore]
            target_config:
              - name: root-directory
                properties:
                  root: '/root/demo/target/site'
```

#### Run application

```bash
wash app deploy ./wadm.yaml
```

#### Check the status of the app

```bash
wash app status {{project-name}}
```

#### Delete application

```bash
wash app deploy {{project-name}}
```

## Licensing

This template itself is released under the Unlicense. You should replace the LICENSE for your own application with an appropriate license if you plan to release it publicly.
