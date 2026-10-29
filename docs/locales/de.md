| [KR 한국어](./ko.md) | [US English](../../README.md) | [JP 日本語](./ja.md) | [CN 简体中文](./zh-CN.md) | [ES Español](./es.md) |
| :---: | :---: | :---: | :---: | :---: |
| [FR Français](./fr.md) | [DE Deutsch](./de.md) | [RU Русский](./ru.md) | [SA العربية](./ar.md) | [IN हिन्दी](./hi.md) |
---

# Soren Lindqvist

`Systemprogrammierer` • `Speicher-Engines` • `Echtzeit-Audio-DSP` • `Stockholm, Schweden`

Hallo. Ich entwickle verteilte Speichersysteme mit minimaler Latenz und echtzeitfähige Akustikberechnungs-Engines. Meine tägliche Arbeit dreht sich um hardwarenahe Systemprogrammierung in Rust und modernem C++, Zero-Copy Linux-Kernel-I/O mittels io_uring sowie deterministische endliche Zustandsautomaten.

Wenn ich nicht gerade Cache-Misses analysiere oder Write-Ahead-Logs entwerfe, experimentiere ich mit modularen analogen Synthesizern, brühe äthiopischen Filterkaffee per Hand auf (V60) oder fahre mit dem Gravelbike über skandinavische Schotterpisten.

---

## 🛠️ Schwerpunkte und Kernkompetenzen

- **Hochdurchsatz-Speicher-Engines**: Entwurf von LSM-Tree-Schlüssel-Wert-Speichern, Write-Ahead-Logs (WAL) und sperrenfreien (lock-free) Speicherallokatoren.
- **Kernel-I/O & Hochleistungsnetzwerke**: Erforschung von `io_uring`-Pipelines, Kernel-Bypass-Datenpfaden und eBPF-basierter Latenzobservierbarkeit.
- **Digitale Signalverarbeitung (DSP)**: Implementierung SIMD-vektorisierter physikalischer Modellierungsalgorithmen zur Simulation akustischer Wellenausbreitung.
- **Zuverlässigkeit in verteilten Systemen**: Validierung von Konsensprotokollen (Raft) und deterministische Nebenläufigkeitstests.

---

## 📂 Ausgewählte Open-Source-Projekte

### 1. `aether-db`
> Eine eingebettete, persistente LSM-Tree-Speicher-Engine in Rust mit direkter asynchroner `io_uring`-Datenträger-I/O.
- **Schwerpunkte**: Zero-Copy-Deserialisierung, sperrenfreie MemTable auf Skip-List-Basis und reines Anhänge-Commit-Log.
- **Technologie-Stack**: Rust, io_uring, Linux AIO, SIMD-Bit-Packing
- **Design-Leitlinie**: Null dynamische Heap-Allokationen im kritischen Schreibpfad.

### 2. `pulse-dsp`
> Akustik-Engine zur Echtzeit-Physikmodellierung für Raumklangsynthese und Raumimpulsantwort-Simulation.
- **Schwerpunkte**: Mehrkanalige Wellengleichungsberechnung bei 96kHz / 24-Bit mit weniger als 1,8 ms Pufferlatenz.
- **Technologie-Stack**: C++20, AVX-512 / NEON Intrinsics, CMake, PortAudio

### 3. `trace-tap`
> Schlanke eBPF-Sonde zur Überwachung von Pufferüberläufen in Linux-Sockets und Kernel-TCP-Warteschlangenlaufzeiten.
- **Schwerpunkte**: Minimale Ausführungslast (<0,4% CPU-Overhead) für Hochfrequenzhandels- und Streaming-Knoten.
- **Technologie-Stack**: C, eBPF / libbpf, Zig, Linux Tracepoints

### 4. `nord-vibe`
> CLI-Arbeitsplatz-Manager, der Farbpaletten, Schriftligaturen und Layouts synchron über Neovim, Tmux und Alacritty hinweg verwaltet.
- **Technologie-Stack**: Go, Unix Domain Sockets, TOML

---

## 💻 Technologiestack und Entwicklungsumgebung

### Programmiersprachen
| Ebene | Sprachen | Haupteinsatzbereich |
| :--- | :--- | :--- |
| **Tägliche Produktion** | Rust, C++20, C | Speicher-Engines, Audio-DSP-Kerne, eBPF-Systemanalysen |
| **Werkzeuge & Dienste** | Go, Python, Zig | Build-Automatisierung, Datenpipelines, Benchmark-Suiten |
| **Shell & Skripte** | Fish, POSIX Shell, Bash | System-Bootstrapping, CI-Prüfstände, Kernel-Parameter-Tuning |

### Systeme & Architektur
| Bereich | Technologien & Standards |
| :--- | :--- |
| **Kernel & Betriebssystem** | Linux (Arch / Debian), `io_uring`, `epoll`, eBPF, cgroups v2, hugepages |
| **Protokolle & RPC** | QUIC, gRPC, Protocol Buffers, FlatBuffers, Cap'n Proto, WebSocket |
| **Daten & Konsens** | Raft-Konsens, LSM-Tree, WAL, RocksDB-Interna, SQLite, PostgreSQL |
| **Nebenläufigkeitsmodelle** | Lock-free Ringpuffer, RCU (Read-Copy-Update), Actor-Pipelines, SPMC/MPSC |

### Arbeitsplatz-Setup
```text
Betriebssystem : Arch Linux (Kernel 6.x, zen patchset)
Terminal       : Alacritty + Tmux
Editor         : Neovim (Native LSP, Lua, Treesitter)
Shell          : Fish shell mit starship prompt
Build-Systeme  : Cargo, CMake, Ninja, Make
Hardware       : AMD Ryzen 9 7950X, 64GB DDR5 ECC, PCIe 4.0 NVMe RAID-0
Audio-Setup    : RME Babyface Pro FS, 48HP Eurorack Modularsynthesizer
```

---

## 📈 Ingenieursphilosophie

1. **Korrektheit vor Raffinesse**: Schneller Code, der korrumpierte Daten liefert, ist wertlos. Invarianten müssen stets zuerst durch eigenschaftsbasiertes Testen (Property testing) und Fuzzing bewiesen werden.
2. **Mechanische Sympathie (Mechanical Sympathy)**: Verstehe CPU-Caches, Sprungvorhersagen, Seitentabellen und Speicherbandbreiten. Hardware ist kein abstraktes Gedankenspiel.
3. **Deterministisches Testen**: Zustandsmaschinensimulationen mit festem Zufallssamen decken Nebenläufigkeitsfehler verlässlicher auf als wochenlange Blindtests im Produktivbetrieb.
4. **Minimale Abhängigkeiten**: Jede hinzugefügte Bibliothek ist eine künftige Wartungslast. Setze nach Möglichkeit auf ausgiebig erprobte Standardschnittstellen.

---

## 📚 Aktuelle Lektüre & Forschungsthemen

- *Designing Data-Intensive Applications* von Martin Kleppmann (3. Durchgang mit Fokus auf interne Speicherarchitekturen)
- Formale Verifikation sperrenfreier Datenstrukturen mit TLA+
- Implementierung energiesparender Audio-DSP-Algorithmen auf ARM Cortex-M7 Mikrocontrollern

---

## 📬 Kontakt

- **GitHub Discussions**: Eröffne gerne eine Diskussion in einem meiner Repositories.
- **E-Mail**: `soren.lindqvist.dev [at] proton.me`
- **PGP-Fingerabdruck**: `9B4F 3E21 78C6 A10D 5E42  F098 32D1 8A7B 64C2 11E9`
- **Standort**: Stockholm, Schweden (UTC+1 / CET)

---
*Verfasst von Soren Lindqvist • Zuletzt aktualisiert: Oktober 2026*
