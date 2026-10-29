| [KR 한국어](./ko.md) | [US English](../../README.md) | [JP 日本語](./ja.md) | [CN 简体中文](./zh-CN.md) | [ES Español](./es.md) |
| :---: | :---: | :---: | :---: | :---: |
| [FR Français](./fr.md) | [DE Deutsch](./de.md) | [RU Русский](./ru.md) | [SA العربية](./ar.md) | [IN हिन्दी](./hi.md) |
---

# 소렌 린드크비스트 (Soren Lindqvist)

`시스템 프로그래머` • `스토리지 엔진` • `실시간 오디오 DSP` • `스웨덴 스톡홀름`

안녕하세요. 지연 시간이 극도로 낮은 분산 스토리지 시스템과 실시간 오디오 연산 엔진을 만드는 엔지니어입니다. 일상에서는 Rust와 모던 C++ 기반의 시스템 프로그래밍, io_uring을 활용한 제로카피 리눅스 커널 I/O, 그리고 결정론적 유한 상태 머신(Finite-State Machine)을 주로 연구하고 구축합니다.

캐시 미스를 프로파일링하거나 WAL(Write-Ahead Log)을 설계하지 않을 때는 모듈러 아날로그 신디사이저 패칭을 실험하거나, 에티오피아 원두를 핸드드립(V60)으로 내리고, 북유럽의 자갈길을 달리는 그래블 바이크 라이딩을 즐깁니다.

---

## 🛠️ 주요 관심사 및 전문 분야

- **초고속 스토리지 엔진**: LSM-Tree 키-값 저장소, 로그 선행 기입(WAL), 락프리(Lock-free) 메모리 할당자 설계.
- **커널 I/O 및 고성능 네트워킹**: `io_uring` 비동기 I/O 파이프라인, 커널 바이패스 패킷 경로, eBPF 기반의 마이크로초 단위 지연 시간 관측.
- **디지털 신호 처리 (DSP)**: 음향 파동 방정식 시뮬레이션 및 공간 오디오 합성을 위한 SIMD 벡터화 알고리즘 구현.
- **분산 시스템 무결성**: 분산 합의 알고리즘(Raft) 검증 및 결정론적 동시성 무결성 테스트.

---

## 📂 대표 오픈소스 프로젝트

### 1. `aether-db`
> Rust로 작성된 임베디드 지속성 LSM-Tree 스토리지 엔진. 비동기 `io_uring` 디스크 I/O를 직접 결합.
- **핵심 목표**: 제로카피 역직렬화, 스킵리스트 기반 락프리 멤테이블(MemTable), 순차 덧붙이기 전용 커밋 로그.
- **기술 스택**: Rust, io_uring, Linux AIO, SIMD 비트 패킹
- **설계 철칙**: 임계 쓰기 경로(Critical Write Path)에서 동적 힙 메모리 할당 0건 보장.

### 2. `pulse-dsp`
> 공간 오디오 합성과 실내 잔향 시뮬레이션을 위한 실시간 물리 모델링 음향 엔진.
- **핵심 목표**: 96kHz / 24-bit 환경에서 1.8ms 미만의 버퍼 지연으로 다채널 파동 방정식 실시간 계산.
- **기술 스택**: C++20, AVX-512 / NEON 인트린식, CMake, PortAudio

### 3. `trace-tap`
> 리눅스 소켓 버퍼 팽창 및 커널 TCP 큐 턴어라운드 시간을 추적하는 초경량 eBPF 프로브.
- **핵심 목표**: 고빈도 거래 노드 및 미디어 스트리밍 서버를 위한 극저오버헤드(<0.4% CPU 점유) 관측성 제공.
- **기술 스택**: C, eBPF / libbpf, Zig, Linux Tracepoints

### 4. `nord-vibe`
> Neovim, Tmux, Alacritty 전반의 컬러 팔레트, 폰트 리가처, 터미널 레이아웃을 실시간 동기화하는 CLI 워크스페이스 오케스트레이터.
- **기술 스택**: Go, Unix Domain Sockets, TOML

---

## 💻 기술 스택 및 개발 환경

### 프로그래밍 언어
| 분류 | 언어 | 주 활용 맥락 |
| :--- | :--- | :--- |
| **주력 프로덕션** | Rust, C++20, C | 고성능 스토리지 엔진, 오디오 DSP 커널, eBPF 저수준 추적 |
| **도구 및 서비스** | Go, Python, Zig | 빌드 오케스트레이터, 데이터 파이프라인, 벤치마크 스위트 |
| **쉘 및 자동화** | Fish, POSIX Shell, Bash | 시스템 환경 부트스트래핑, CI 검증 리그, 커널 파라미터 튜닝 |

### 시스템 및 아키텍처
| 영역 | 기술 및 프로토콜 |
| :--- | :--- |
| **커널 및 OS** | Linux (Arch / Debian), `io_uring`, `epoll`, eBPF, cgroups v2, hugepages |
| **프로토콜 및 RPC** | QUIC, gRPC, Protocol Buffers, FlatBuffers, Cap'n Proto, WebSocket |
| **데이터 및 분산 합의** | Raft consensus, LSM-Tree, WAL, RocksDB 내부 구조, SQLite, PostgreSQL |
| **동시성 모델** | Lock-free 링 버퍼, RCU (Read-Copy-Update), 액터 파이프라인, SPMC/MPSC |

### 작업 환경
```text
운영체제       : Arch Linux (Kernel 6.x, zen 패치셋)
터미널         : Alacritty + Tmux
에디터         : Neovim (Native LSP, Lua, Treesitter)
쉘 환경        : Fish shell + Starship 프롬프트
빌드 도구      : Cargo, CMake, Ninja, Make
하드웨어 사양   : AMD Ryzen 9 7950X, 64GB DDR5 ECC, PCIe 4.0 NVMe RAID-0
오디오 장비    : RME Babyface Pro FS, 48HP 커스텀 유로랙 신디사이저
```

---

## 📈 엔지니어링 철학

1. **기교보다 정확성이 우선**: 아무리 빨라도 손상된 데이터를 반환하는 코드는 무가치합니다. 속성 기반 테스트(Property testing)와 퍼징으로 불변식을 먼저 입증합니다.
2. **기계적 공감(Mechanical Sympathy)**: CPU 캐시, 분기 예측기, 페이지 테이블, 메모리 버스 대역폭을 항상 의식합니다. 하드웨어는 결코 추상적인 블랙박스가 아닙니다.
3. **결정론적 검증**: 시드를 고정할 수 있는 상태 머신 시뮬레이션은 수 주간의 무작위 프로덕션 테스트보다 동시성 버그를 훨씬 빠르고 확실하게 잡아냅니다.
4. **의존성 최소화**: 외부 라이브러리나 크레이트를 하나 추가할 때마다 유지보수 부채가 늘어납니다. 충분히 검증된 표준 인터페이스와 자체 데이터 구조를 신뢰합니다.

---

## 📚 최근 읽고 있는 자료 및 탐구 주제

- 마틴 클레프만 저 *데이터 중심 애플리케이션 설계 (Designing Data-Intensive Applications)* (스토리지 엔진 내부 3회독)
- TLA+를 이용한 락프리 동시성 데이터 구조 정형 검증
- ARM Cortex-M7 마이크로컨트롤러 기반의 저전력 오디오 DSP 구현

---

## 📬 연락처

- **GitHub Discussions**: 제 저장소 이슈나 토론 탭을 언제든 이용해 주세요.
- **이메일**: `soren.lindqvist.dev [at] proton.me`
- **PGP 핑거프린트**: `9B4F 3E21 78C6 A10D 5E42  F098 32D1 8A7B 64C2 11E9`
- **위치**: 스웨덴 스톡홀름 (UTC+1 / CET)

---
*소렌 린드크비스트 작성 • 최종 업데이트: 2026년 10월*
