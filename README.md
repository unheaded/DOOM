# DOOM

> Fork of [id-Software/DOOM](https://github.com/id-Software/DOOM) — reference source for the [Unheaded Protocol Computer (UPC)](https://github.com/unheaded/unheaded)

This is id Software's original DOOM source code (released 1997 under GPL-2.0), preserved as reference material for the Unheaded project. The source is unmodified — all UPC integration work lives in the companion [doomgeneric](https://github.com/unheaded/doomgeneric) repository.

## Why This Fork Exists

The Unheaded Protocol Computer runs DOOM compiled to MBC bytecode inside eBPF/XDP programs. The compilation pipeline starts here:

```
This repo (original C source)
    │
    ▼  doomgeneric platform layer + libc stubs
    │
doomgeneric repo (portable DOOM + UPC integration)
    │
    ▼  riscv64-unknown-elf-gcc -march=rv32i
    │
doom.elf (RISC-V 32-bit ELF)
    │
    ▼  rv32i_to_mbc (Rust translator)
    │
doom.mbc → loaded into BPF maps → executed by XDP programs
```

This fork preserves the original source as the canonical reference. See [doomgeneric](https://github.com/unheaded/doomgeneric) for the actual UPC integration, build pipeline, and running DOOM over IPv6.

## Directory Structure

| Directory | Contents |
|:---|:---|
| `linuxdoom-1.10/` | The DOOM engine — renderer, game logic, networking, sound |
| `sndserv/` | Sound server (separate process, IPC to game) |
| `sersrc/` | Serial/modem driver for multiplayer |
| `ipx/` | IPX network driver for multiplayer |

## Original Documentation

The original release notes from id Software are in [README.TXT](README.TXT).

## Related Repositories

- **[unheaded/doomgeneric](https://github.com/unheaded/doomgeneric)** — portable DOOM engine + UPC integration (Go, eBPF, MBC bytecode, browser viewer)
- **[unheaded/unheaded](https://github.com/unheaded/unheaded)** — the Unheaded Protocol — full protocol stack and compute platform

## License

GPL-2.0 — see [LICENSE.TXT](LICENSE.TXT)

## Credits

- **id Software** / **John Carmack** — original DOOM engine (1993, GPL release 1997)
- **[Unheaded](https://github.com/unheaded)** — UPC adaptation
