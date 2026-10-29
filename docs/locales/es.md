| [KR 한국어](./ko.md) | [US English](../../README.md) | [JP 日本語](./ja.md) | [CN 简体中文](./zh-CN.md) | [ES Español](./es.md) |
| :---: | :---: | :---: | :---: | :---: |
| [FR Français](./fr.md) | [DE Deutsch](./de.md) | [RU Русский](./ru.md) | [SA العربية](./ar.md) | [IN हिन्दी](./hi.md) |
---

# Soren Lindqvist

`Programador de Sistemas` • `Motores de Almacenamiento` • `DSP de Audio en Tiempo Real` • `Estocolmo, Suecia`

Hola. Me dedico a construir sistemas de almacenamiento distribuido de ultra baja latencia y motores de procesamiento acústico en tiempo real. Mi trabajo diario se centra en la programación de sistemas con Rust y C++ moderno, operaciones de E/S con copia cero en el kernel de Linux a través de io_uring y máquinas de estados finitos deterministas.

Cuando no estoy analizando fallos de caché en CPU o diseñando registros de escritura anticipada (WAL), me encontrarás experimentando con sintetizadores analógicos modulares, preparando café etíope en V60 o pedaleando en bicicleta gravel por pistas nórdicas.

---

## 🛠️ Áreas de Especialización

- **Motores de Almacenamiento de Alto Rendimiento**: Diseño de almacenes clave-valor basados en LSM-Trees, registros de escritura anticipada (WAL) y asignadores de memoria libres de bloqueos (lock-free).
- **E/S de Kernel y Redes**: Explotación de pipelines asíncronos con `io_uring`, rutas de paquetes con omisión de kernel y observabilidad de latencia basada en eBPF.
- **Procesamiento Digital de Señales (DSP)**: Implementación de algoritmos de modelado físico acelerados con SIMD para simulación de propagación de ondas sonoras.
- **Confiabilidad Distribuida**: Validación de protocolos de consenso (Raft) y pruebas de concurrencia deterministas.

---

## 📂 Proyectos de Código Abierto Destacados

### 1. `aether-db`
> Motor de almacenamiento persistente embebido basado en LSM-Tree escrito en Rust con E/S de disco asíncrona directa mediante `io_uring`.
- **Foco**: Deserialización con copia cero, MemTable libre de bloqueos con skip-lists y registros de confirmación de solo adición.
- **Pila Tecnológica**: Rust, io_uring, Linux AIO, empaquetado de bits SIMD
- **Regla de Diseño**: Cero asignaciones dinámicas en el montón (heap) dentro de la ruta crítica de escritura.

### 2. `pulse-dsp`
> Motor acústico de modelado físico en tiempo real para síntesis de audio espacial y simulación de respuesta al impulso de salas.
- **Foco**: Resolución de la ecuación de onda multicanal a 96kHz / 24-bit con una latencia de búfer inferior a 1,8 ms.
- **Pila Tecnológica**: C++20, intrínsecos AVX-512 / NEON, CMake, PortAudio

### 3. `trace-tap`
> Sonda eBPF ligera para supervisar la saturación de búferes de sockets Linux y tiempos de respuesta en colas TCP del kernel.
- **Foco**: Observabilidad con sobrecarga mínima (<0,4% de penalización de CPU) para nodos de negociación de alta frecuencia y streaming.
- **Pila Tecnológica**: C, eBPF / libbpf, Zig, Linux Tracepoints

### 4. `nord-vibe`
> Orquestador de terminal en CLI que sincroniza paletas de color, ligaduras tipográficas y disposiciones entre Neovim, Tmux y Alacritty.
- **Pila Tecnológica**: Go, Unix Domain Sockets, TOML

---

## 💻 Pila Tecnológica y Entorno

### Lenguajes de Programación
| Nivel | Lenguajes | Contexto Principal |
| :--- | :--- | :--- |
| **Producción Diaria** | Rust, C++20, C | Motores de almacenamiento, núcleos DSP de audio, sondas eBPF |
| **Herramientas y Servicios** | Go, Python, Zig | Orquestación de compilaciones, canalizaciones de datos, suites de benchmark |
| **Shell y Automatización** | Fish, POSIX Shell, Bash | Aprovisionamiento de entornos, bancos de prueba en CI, ajuste de parámetros del kernel |

### Sistemas y Arquitectura
| Dominio | Tecnologías y Estándares |
| :--- | :--- |
| **Kernel y SO** | Linux (Arch / Debian), `io_uring`, `epoll`, eBPF, cgroups v2, hugepages |
| **Protocolos y RPC** | QUIC, gRPC, Protocol Buffers, FlatBuffers, Cap'n Proto, WebSocket |
| **Datos y Consenso** | Consenso Raft, LSM-Tree, WAL, arquitectura interna de RocksDB, SQLite, PostgreSQL |
| **Modelos de Concurrencia** | Búferes anulares lock-free, RCU (Read-Copy-Update), tuberías Actor, colas SPMC/MPSC |

### Espacio de Trabajo
```text
Sistema Operativo : Arch Linux (Kernel 6.x, conjunto zen)
Terminal          : Alacritty + Tmux
Editor            : Neovim (LSP nativo, Lua, Treesitter)
Shell             : Fish shell con indicador starship
Herramientas      : Cargo, CMake, Ninja, Make
Hardware          : AMD Ryzen 9 7950X, 64GB DDR5 ECC, PCIe 4.0 NVMe RAID-0
Audio             : RME Babyface Pro FS, Sintetizador modular Eurorack 48HP
```

---

## 📈 Filosofía de Ingeniería

1. **La exactitud prima sobre la astucia**: El código ultrarrápido que devuelve datos corruptos carece de valor. Demuestra invariantes con pruebas de propiedades (Property testing) y fuzzing continuo.
2. **Simpatía Mecánica (Mechanical Sympathy)**: Comprende las cachés de CPU, predictores de saltos, tablas de páginas y ancho de banda del bus de memoria. El hardware no es una abstracción flotante.
3. **Pruebas Deterministas**: La simulación de máquinas de estados con semilla reproducible expone condiciones de carrera concurrentes mucho antes que semanas de pruebas a ciegas en producción.
4. **Dependencias Mínimas**: Cada biblioteca o crate externo añade una deuda de mantenimiento. Confía en interfaces estándar probadas exhaustivamente.

---

## 📚 Lecturas e Investigaciones Actuales

- *Designing Data-Intensive Applications* por Martin Kleppmann (tercera relectura sobre estructuras internas de almacenamiento)
- Verificación formal de estructuras de datos lock-free mediante TLA+
- Implementación de algoritmos DSP de audio de bajo consumo sobre microcontroladores ARM Cortex-M7

---

## 📬 Contacto

- **GitHub Discussions**: Siéntete libre de abrir un hilo en cualquiera de mis repositorios.
- **Correo Electrónico**: `soren.lindqvist.dev [at] proton.me`
- **Huella Digital PGP**: `9B4F 3E21 78C6 A10D 5E42  F098 32D1 8A7B 64C2 11E9`
- **Ubicación**: Estocolmo, Suecia (UTC+1 / CET)

---
*Escrito por Soren Lindqvist • Última actualización: Octubre de 2026*
