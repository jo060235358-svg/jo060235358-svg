| [KR 한국어](./ko.md) | [US English](../../README.md) | [JP 日本語](./ja.md) | [CN 简体中文](./zh-CN.md) | [ES Español](./es.md) |
| :---: | :---: | :---: | :---: | :---: |
| [FR Français](./fr.md) | [DE Deutsch](./de.md) | [RU Русский](./ru.md) | [SA العربية](./ar.md) | [IN हिन्दी](./hi.md) |
---

# Soren Lindqvist

`Programador de Sistemas` • `Motores de Armazenamento` • `DSP de Áudio em Tempo Real` • `Estocolmo, Suécia`

Olá. Meu trabalho é voltado à criação de sistemas de armazenamento distribuído de baixíssima latência e motores computacionais acústicos em tempo real. Minha rotina envolve programação de sistemas em Rust e C++ moderno, operações de I/O de cópia zero no kernel Linux via io_uring e máquinas de estados finitos determinísticas.

Quando não estou investigando perdas de cache (cache misses) ou projetando logs de escrita antecipada (WAL), você pode me encontrar experimentando sintetizadores modulares analógicos, preparando café etíope filtrado na V60 ou pedalando em estradas de terra pela Escandinávia.

---

## 🛠️ Áreas de Especialidade

- **Motores de Armazenamento de Alto Desempenho**: Arquitetura de bancos chave-valor baseados em LSM-Tree, logs de transações (WAL) e alocadores de memória lock-free.
- **I/O de Kernel e Redes**: Exploração de pipelines assíncronos com `io_uring`, caminhos de pacotes com desvio de kernel (kernel-bypass) e observabilidade via eBPF.
- **Processamento Digital de Sinais (DSP)**: Implementação de modelos físicos acústicos com aceleração vetorial SIMD para espacialização sonora.
- **Confiabilidade de Sistemas Distribuídos**: Verificação de protocolos de consenso (Raft) e testes de concorrência determinísticos.

---

## 📂 Projetos Open-Source em Destaque

### 1. `aether-db`
> Motor de armazenamento persistente embarcado baseado em LSM-Tree, desenvolvido em Rust com E/S assíncrona direta via `io_uring`.
- **Foco**: Deserialização com cópia zero, MemTable lock-free com skip-lists e log de commit estritamente sequencial (append-only).
- **Stack**: Rust, io_uring, Linux AIO, empacotamento de bits SIMD
- **Regra de Ouro**: Zero alocações dinâmicas na heap no caminho crítico de gravação.

### 2. `pulse-dsp`
> Motor acústico de modelagem física em tempo real para síntese de áudio espacial e simulação de resposta ao impulso de salas.
- **Foco**: Solução de equações de onda multicanal a 96kHz / 24-bit com latência de buffer inferior a 1,8 ms.
- **Stack**: C++20, intrínsecos AVX-512 / NEON, CMake, PortAudio

### 3. `trace-tap`
> Sonda eBPF minimalista para monitoramento de saturação de buffers de sockets Linux e tempo de trânsito em filas TCP no kernel.
- **Foco**: Sobrecarga mínima (<0,4% de penalidade de CPU) para nós de negociação de alta frequência e streaming.
- **Stack**: C, eBPF / libbpf, Zig, pontos de rastreamento do Linux

### 4. `nord-vibe`
> Ferramenta CLI para sincronização em tempo real de paletas de cores, ligaduras tipográficas e painéis entre Neovim, Tmux e Alacritty.
- **Stack**: Go, Unix Domain Sockets, TOML

---

## 💻 Stack Tecnológica e Ambiente

### Linguagens de Programação
| Nível | Linguagens | Contexto Principal |
| :--- | :--- | :--- |
| **Produção Diária** | Rust, C++20, C | Motores de armazenamento, kernels de DSP de áudio, sondas eBPF |
| **Ferramentas e Serviços** | Go, Python, Zig | Orquestração de compilação, pipelines de dados, baterias de benchmark |
| **Shell e Automação** | Fish, POSIX Shell, Bash | Inicialização de ambientes, esteiras de teste em CI, ajustes de kernel |

### Sistemas e Arquitetura
| Domínio | Tecnologias e Padrões |
| :--- | :--- |
| **Kernel e SO** | Linux (Arch / Debian), `io_uring`, `epoll`, eBPF, cgroups v2, hugepages |
| **Protocolos e RPC** | QUIC, gRPC, Protocol Buffers, FlatBuffers, Cap'n Proto, WebSocket |
| **Armazenamento e Consenso** | Consenso Raft, LSM-Tree, WAL, arquitetura interna do RocksDB, SQLite, PostgreSQL |
| **Modelos de Concorrência** | Buffers circulares lock-free, RCU (Read-Copy-Update), pipelines de Atores, SPMC/MPSC |

### Ambiente de Trabalho
```text
Sistema Operacional : Arch Linux (Kernel 6.x, patchset zen)
Emulador de Terminal: Alacritty + Tmux
Editor de Código    : Neovim (LSP nativo, Lua, Treesitter)
Shell               : Fish shell com prompt starship
Ferramentas de Build: Cargo, CMake, Ninja, Make
Configuração de HW  : AMD Ryzen 9 7950X, 64GB DDR5 ECC, PCIe 4.0 NVMe RAID-0
Equipamento de Áudio: RME Babyface Pro FS, sintetizador modular Eurorack 48HP
```

---

## 📈 Filosofia de Engenharia

1. **Correção Antes da Esperteza**: Código extremamente veloz que corrompe dados é inútil. Demonstre invariantes com testes baseados em propriedades (Property testing) e fuzzing contínuo.
2. **Empatia com a Máquina (Mechanical Sympathy)**: Entenda o funcionamento de caches de CPU, preditores de desvio, tabelas de página e largura de banda de memória. Hardware não é uma abstração etérea.
3. **Testes Determinísticos**: A simulação de autômatos com sementes reprodutíveis desmascara condições de corrida muito antes de semanas de testes cegos em produção.
4. **Dependências Mínimas**: Cada biblioteca de terceiros agregada representa uma dívida técnica futura. Dê preferência a interfaces padronizadas e amplamente testadas.

---

## 📚 Leituras e Tópicos de Estudo Atuais

- *Designing Data-Intensive Applications* de Martin Kleppmann (3ª leitura, focada nos pormenores de motores de armazenamento)
- Verificação formal de estruturas de dados sem travas (lock-free) com TLA+
- Implementação de algoritmos de DSP de áudio de baixo consumo em microcontroladores ARM Cortex-M7

---

## 📬 Contato

- **GitHub Discussions**: Sinta-se à vontade para abrir discussões em meus repositórios.
- **E-mail**: `soren.lindqvist.dev [at] proton.me`
- **Impressão Digital PGP**: `9B4F 3E21 78C6 A10D 5E42  F098 32D1 8A7B 64C2 11E9`
- **Localização**: Estocolmo, Suécia (UTC+1 / CET)

---
*Escrito por Soren Lindqvist • Última atualização: Outubro de 2026*
