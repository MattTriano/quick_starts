# Up and running with rust
 
A brief description of what this project does.

## Installation

Ensure you have Rust installed:

If `rustc --version` returns a version number for Rust, proceed to the next section. Otherwise, you can install `rust` via this command. I went with the default installation.

```console
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Then `source` that new installation via

```console
source "$HOME/.cargo/env"
```

Run these commands to check that `rust` and its package manager, `cargo`.

```console
rustc --version
cargo --version
```

## Usage

1. Make a project

```console
cargo new project_name
cd project_name
```

You'll have a project with this structure.

```console
project_name/
  ├── Cargo.toml
  └── src/
      └── main.rs
```

`Cargo.toml` is for dependencies and project metadata.
`/src/main.rs` is the entrypoint for the program.

2. Build the project:
```bash
cargo build
```

3. Run the project:
```bash
cargo run
```

4. Run tests:
```bash
cargo test
```

The configured basic project doesn't have any tests, but you would put tests in a `.rs` file in the `project_name/tests/` dir.

```rust
use project_name;

#[test]
fn test_something() {
    assert!(some logic);
}
```

## Development

- Source code is in `src/`
- Tests are in `tests/`
- Dependencies are listed in `Cargo.toml`

