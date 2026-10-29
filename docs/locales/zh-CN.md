| [KR 한국어](./ko.md) | [US English](../../README.md) | [JP 日本語](./ja.md) | [CN 简体中文](./zh-CN.md) | [ES Español](./es.md) |
| :---: | :---: | :---: | :---: | :---: |
| [FR Français](./fr.md) | [DE Deutsch](./de.md) | [RU Русский](./ru.md) | [SA العربية](./ar.md) | [IN हिन्दी](./hi.md) |
---

# 索伦·林德奎斯特 (Soren Lindqvist)

`系统程序员` • `存储引擎` • `实时音频数字信号处理 (DSP)` • `瑞典斯德哥尔摩`

你好。我是一名专注于超低延迟分布式存储系统与实时音频计算引擎的系统软件工程师。我的日常工作围绕 Rust 与现代 C++ 系统级编程、基于 io_uring 的零拷贝 Linux 内核 I/O，以及确定性有限状态机（FSM）构建展开。

如果不处于性能调优、分析 CPU 缓存未命中或设计预写式日志（WAL）的状态，你通常能在模块化模拟合成器调试现场、手冲埃塞俄比亚咖啡台前，或者北欧碎石路骑行的旅途中找到我。

---

## 🛠️ 核心专业领域

- **高吞吐量存储引擎**：LSM 树键值存储、预写式日志（WAL）与无锁（Lock-free）内存分配器架构设计。
- **内核 I/O 与高性能网络**：深入探索 `io_uring` 异步管道、内核旁路数据通路，以及基于 eBPF 的微秒级延迟可观测性。
- **数字信号处理 (DSP)**：实现用于声学声波模拟与空间音频合成的 SIMD 向量化算法。
- **分布式可靠性验证**：Raft 一致性协议工程化验证与确定性并发时序测试。

---

## 📂 代表性开源项目

### 1. `aether-db`
> 基于 Rust 实现的高性能嵌入式持久化 LSM-Tree 存储引擎，直接集成异步 `io_uring` 磁盘 I/O。
- **重点特性**：零拷贝反序列化、跳表实现的无锁内存表（MemTable）、纯追加式提交日志。
- **技术栈**：Rust, io_uring, Linux AIO, SIMD 位打包
- **设计守则**：在关键写入路径（Critical Write Path）上保持零动态堆内存分配。

### 2. `pulse-dsp`
> 用于空间音频合成与室内脉冲响应模拟的实时物理声学引擎。
- **重点特性**：支持 96kHz / 24-bit 采样，在 1.8ms 以下缓冲延迟内实时计算多声道声波方程。
- **技术栈**：C++20, AVX-512 / NEON 向量指令集, CMake, PortAudio

### 3. `trace-tap`
> 监测 Linux 套接字缓冲区膨胀与内核 TCP 队列流转时间的超轻量级 eBPF 探测器。
- **重点特性**：专为高频交易系统与媒体流分发节点设计的极低开销（CPU 损耗 <0.4%）可观测性工具。
- **技术栈**：C, eBPF / libbpf, Zig, Linux Tracepoints

### 4. `nord-vibe`
> 用于在 Neovim、Tmux 和 Alacritty 之间实时同步调色板、字体连字与工作区布局的 CLI 管理套件。
- **技术栈**：Go, Unix Domain Sockets, TOML

---

## 💻 技术储备与开发环境

### 编程语言
| 层级 | 语言 | 主要应用场景 |
| :--- | :--- | :--- |
| **日常核心** | Rust, C++20, C | 高吞吐量存储引擎、音频 DSP 计算核心、eBPF 系统探针 |
| **工具与服务** | Go, Python, Zig | 自定义构建工具、数据流水线、性能基准测试套件 |
| **脚本与自动化** | Fish, POSIX Shell, Bash | 环境自动化初始化、CI 验证平台、内核参数动态微调 |

### 核心系统与架构
| 领域 | 技术与协议标准 |
| :--- | :--- |
| **内核与操作系统** | Linux (Arch / Debian), `io_uring`, `epoll`, eBPF, cgroups v2, hugepages |
| **协议与远程调用** | QUIC, gRPC, Protocol Buffers, FlatBuffers, Cap'n Proto, WebSocket |
| **存储与分布式共识** | Raft 共识算法, LSM-Tree, WAL, RocksDB 内部原理, SQLite, PostgreSQL |
| **高并发模型** | 无锁环形缓冲区 (Ring Buffer), RCU 机制, Actor 并发流水线, SPMC/MPSC 队列 |

### 个人工作台
```text
操作系统       : Arch Linux (Linux 6.x 内核, zen 补丁集)
终端环境       : Alacritty + Tmux
代码编辑器     : Neovim (原生 LSP, Lua 配置, Treesitter)
命令行交互     : Fish shell 搭配 Starship 提示符
构建工具链     : Cargo, CMake, Ninja, Make
硬件配置       : AMD Ryzen 9 7950X, 64GB DDR5 ECC, PCIe 4.0 NVMe RAID-0
音频工作台     : RME Babyface Pro FS, 48HP 定制 Eurorack 模块合成器
```

---

## 📈 工程实践哲学

1. **准确性重于奇技淫巧**：任何返回损坏数据的所谓高性能代码都毫无价值。始终优先使用基于属性的测试（Property testing）与模糊测试（Fuzzing）证明不变量。
2. **机械同理心（Mechanical Sympathy）**：深入理解 CPU 缓存层次、分支预测、内存分页与总线吞吐能力。硬件从不是不可捉摸的抽象产物。
3. **确定性测试**：可设定随机种子的状态机仿真环境，能比生产环境中数周的盲目随机测试更早捕获复杂并发竞态缺陷。
4. **克制引入依赖**：每新增一个第三方库或 crate，都是对未来维护成本的透支。在绝大多数情况下优先依托经过充分考验的标准接口。

---

## 📚 近期研读与探索方向

- Martin Kleppmann 著《设计数据密集型应用》（深入存储引擎实现细节，第 3 遍重读）
- 运用 TLA+ 对无锁并发数据结构进行严格的形式化验证
- 基于 ARM Cortex-M7 微控制器的低功耗音频 DSP 算法移植

---

## 📬 交流与联系

- **GitHub Discussions**：欢迎在我的任一代码仓库中开启议题与技术探讨。
- **电子邮箱**：`soren.lindqvist.dev [at] proton.me`
- **PGP 指纹**：`9B4F 3E21 78C6 A10D 5E42  F098 32D1 8A7B 64C2 11E9`
- **地理坐标**：瑞典斯德哥尔摩 (UTC+1 / CET)

---
*作者：索伦·林德奎斯特 • 最近更新：2026年10月*
