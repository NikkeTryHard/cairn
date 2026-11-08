# RackMaw

Rust source for the RackMaw-Champion-Ctl3 ScrabbleBot configuration. The bot estimates tile value with sampled future racks, paces bids against a fitted market model, and searches word partitions for cashing and the final dump. It is derived from Karthik Subramanian's MIT-licensed Vickrey-Scrabblebot; the original license and attribution are retained.

## Hackathon build

Install stable Rust, clone this repository, and run from its root:

```sh
cargo build --release --locked -p vickrey-bot
```

The executable is `target/release/vickrey`. The release profile uses optimization level 3, thin LTO, and one code-generation unit. The dictionary is included in the source build. The files in `config/` are the fixed Champion-Ctl3 strategy and market parameters. This bot does not use a neural network, Python, CUDA, or model compilation.

## Run

Use a bot credential issued by the ScrabbleBot server, stored outside the repository:

```sh
./target/release/vickrey --token-file /absolute/path/to/bot.token run
```

Run from the repository root so the supplied configuration is loaded. Do not run two processes with the same bot credential. `run` joins casual games and registers for available tournaments; add `--no-tournaments` for casual-only operation. For connection and account status, run `./target/release/vickrey status`.
