| [KR 한국어](./docs/locales/ko.md) | [US English](./README.md) | [JP 日本語](./docs/locales/ja.md) | [CN 简体中文](./docs/locales/zh-CN.md) | [ES Español](./docs/locales/es.md) |
| :---: | :---: | :---: | :---: | :---: |
| [FR Français](./docs/locales/fr.md) | [DE Deutsch](./docs/locales/de.md) | [RU Русский](./docs/locales/ru.md) | [SA العربية](./docs/locales/ar.md) | [IN हिन्दी](./docs/locales/hi.md) |

---

# Soren Lindqvist

`Systems Programmer` • `Storage Engines` • `Real-time Audio DSP` • `Stockholm, Sweden`

Hi there. I build low-latency distributed storage systems and real-time audio computation tools. My daily work revolves around systems programming in Rust and modern C++, zero-copy Linux kernel I/O via `io_uring`, and deterministic finite-state machines.

When I am not profiling cache misses or designing write-ahead logs, you can find me experimenting with modular analog synthesizers, roasting small-batch Ethiopian coffee, or riding gravel bikes across northern Scandinavian trails.

---

## 🛠️ What I Do

- **High-Throughput Storage Engines**: Designing LSM-tree key-value stores, write-ahead logs (WAL), and lock-free memory allocators.
- **Kernel I/O & Networking**: Exploring `io_uring`, kernel-bypass packet paths, and eBPF-based latency observability.
- **Digital Signal Processing (DSP)**: Implementing SIMD-accelerated physical modeling algorithms for acoustic wave propagation.
- **Reliability & Formal Models**: Validating distributed consensus protocols (Raft) and deterministic concurrency testing.

---

## 📂 Featured Open-Source Projects

### 1. `aether-db`
> An embedded, persistent LSM-Tree storage engine written in Rust with direct asynchronous `io_uring` disk I/O.
- **Focus**: Zero-copy deserialization, lock-free memtable using skip-lists, and append-only commit logs.
- **Tech Stack**: Rust, io_uring, Linux AIO, SIMD bit-packing
- **Design Rule**: Zero dynamic heap allocations in the critical write path.

### 2. `pulse-dsp`
> Real-time physical modeling acoustic engine for spatial audio synthesis and room impulse simulation.
- **Focus**: Multi-channel wave equation solver running at 96kHz / 24-bit with under 1.8ms buffer latency.
- **Tech Stack**: C++20, AVX-512 / NEON intrinsics, CMake, PortAudio

### 3. `trace-tap`
> Minimalist eBPF probe for tracking Linux socket buffer bloat and kernel TCP queue turnaround times.
- **Focus**: Ultra-low overhead (<0.4% CPU penalty) observability for high-frequency trading and streaming nodes.
- **Tech Stack**: C, eBPF / libbpf, Zig, Linux Tracepoints

### 4. `nord-vibe`
> CLI workspace tool that synchronizes color schemes, font ligatures, and layouts across Neovim, Tmux, and Alacritty.
- **Tech Stack**: Go, Unix Domain Sockets, TOML

---

## 💻 Technical Stack & Environment

### Programming Languages
| Tier | Languages | Primary Context |
| :--- | :--- | :--- |
| **Daily Production** | Rust, C++20, C | High-throughput storage engines, audio DSP kernels, eBPF |
| **Tooling & Services** | Go, Python, Zig | Custom build tooling, data pipelines, benchmark suites |
| **Scripting & Systems Tooling** | Fish, POSIX Shell, Bash | System bootstrapping, test rigs, kernel parameter tuning |

### Systems & Architecture
| Domain | Technologies & Standards |
| :--- | :--- |
| **Kernel & OS** | Linux (Arch / Debian), `io_uring`, `epoll`, eBPF, cgroups v2, hugepages |
| **Protocols & RPC** | QUIC, gRPC, Protocol Buffers, FlatBuffers, Cap'n Proto, WebSocket |
| **Data & Consensus** | Raft consensus, LSM-Tree, WAL, RocksDB internals, SQLite, PostgreSQL |
| **Concurrency Models** | Lock-free ring buffers, RCU (Read-Copy-Update), Actor pipelines, SPMC/MPSC |

### Daily Workspace
```text
Host OS        : Arch Linux (Kernel 6.x, zen patchset)
Terminal       : Alacritty + Tmux
Editor         : Neovim (Native LSP, Lua, Treesitter)
Shell          : Fish shell with starship prompt
Build Tools    : Cargo, CMake, Ninja, Make
Hardware Rig   : AMD Ryzen 9 7950X, 64GB DDR5 ECC, PCIe 4.0 NVMe RAID-0
Audio Work     : RME Babyface Pro FS, Custom 48HP Eurorack modular synth
```

---

## 📈 Engineering Philosophy

1. **Correctness Before Cleverness**: Fast code that returns corrupted data is useless. Prove invariants with property tests and fuzzing first.
2. **Mechanical Sympathy**: Understand CPU caches, branch predictors, page tables, and memory bus bandwidth. The hardware is not an abstract theory.
3. **Deterministic Testing**: Random simulation with seedable state machines exposes concurrency race conditions faster than weeks of production testing.
4. **Minimal Dependencies**: Every third-party crate or library added is a maintenance tax. Rely on well-tested standard interfaces whenever possible.

---

## 📚 Currently Reading & Exploring

- *Designing Data-Intensive Applications* by Martin Kleppmann (storage engine internals)
- Formal verification of lock-free data structures using TLA+
- Low-power audio DSP on ARM Cortex-M7 microcontrollers

---

## 📬 Get in Touch

- **GitHub Discussions**: Feel free to open a topic on any of my repositories.
- **Email**: `soren.lindqvist.dev@proton.me`
- **PGP Fingerprint**: `9B4F 3E21 78C6 A10D 5E42  F098 32D1 8A7B 64C2 11E9`
- **Location**: Stockholm, Sweden (UTC+1 / CET)

---
*Maintained by Soren Lindqvist • Systems & Audio DSP*
