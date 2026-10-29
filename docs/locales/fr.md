| [KR 한국어](./ko.md) | [US English](../../README.md) | [JP 日本語](./ja.md) | [CN 简体中文](./zh-CN.md) | [ES Español](./es.md) |
| :---: | :---: | :---: | :---: | :---: |
| [FR Français](./fr.md) | [DE Deutsch](./de.md) | [RU Русский](./ru.md) | [SA العربية](./ar.md) | [IN हिन्दी](./hi.md) |
---

# Soren Lindqvist

`Programmeur Systèmes` • `Moteurs de Stockage` • `DSP Audio Temps Réel` • `Stockholm, Suède`

Bonjour. Je conçois des systèmes de stockage distribué à très faible latence et des moteurs de calcul acoustique en temps réel. Mon quotidien s'articule autour de la programmation système en Rust et C++ moderne, des entrées/sorties Linux sans copie via io_uring et de la modélisation par machines d'états finis déterministes.

Lorsque je ne suis pas occupé à profiler les défauts de cache CPU ou à concevoir des journaux de transactions (WAL), vous me trouverez en train d'expérimenter sur des synthétiseurs modulaires analogiques, de préparer du café éthiopien en V60 ou d'arpenter les chemins de gravel scandinaves à vélo.

---

## 🛠️ Domaines d'Expertise

- **Moteurs de Stockage Haute Performance** : Conception de magasins clé-valeur de type LSM-Tree, journaux de réécriture anticipée (WAL) et allocateurs de mémoire sans verrou (lock-free).
- **Entrées/Sorties Noyau & Réseau** : Exploitation des pipelines asynchrones `io_uring`, chemins réseau à contournement du noyau (kernel-bypass) et observabilité de latence basée sur eBPF.
- **Traitement Numérique du Signal (DSP)** : Implémentation d'algorithmes de modélisation physique accélérés par SIMD pour la simulation de propagation d'ondes acoustiques.
- **Fiabilité des Systèmes Distribués** : Validation formelle du protocole de consensus Raft et tests de concurrence déterministes.

---

## 📂 Projets Open-Source Majeurs

### 1. `aether-db`
> Moteur de stockage persistant intégré basé sur un LSM-Tree, écrit en Rust avec E/S disque asynchrones directes via `io_uring`.
- **Points Clés** : Désérialisation sans copie, table mémoire (MemTable) sans verrou à base de skip-lists, journal de validation en ajout pur.
- **Technologies** : Rust, io_uring, Linux AIO, compactage de bits SIMD
- **Règle Fondamentale** : Aucune allocation dynamique sur le tas (heap) sur le chemin critique d'écriture.

### 2. `pulse-dsp`
> Moteur acoustique de modélisation physique en temps réel pour la synthèse audio spatiale et la simulation de réponse impulsionnelle de pièces.
- **Points Clés** : Résolution de l'équation d'onde multicanale à 96kHz / 24-bit avec une latence de tampon inférieure à 1,8 ms.
- **Technologies** : C++20, intrinsèques AVX-512 / NEON, CMake, PortAudio

### 3. `trace-tap`
> Sonde eBPF ultra-légère mesurant la saturation des tampons de sockets Linux et les temps de transit dans les files d'attente TCP du noyau.
- **Points Clés** : Observabilité à très faible coût (<0,4% de charge processeur) pour les nœuds de trading haute fréquence et de streaming.
- **Technologies** : C, eBPF / libbpf, Zig, Linux Tracepoints

### 4. `nord-vibe`
> Utilitaire d'environnement de travail CLI synchronisant les palettes de couleurs, ligatures et dispositions entre Neovim, Tmux et Alacritty.
- **Technologies** : Go, Unix Domain Sockets, TOML

---

## 💻 Environnement et Technologies

### Langages de Programmation
| Niveau | Langages | Contexte d'Usage |
| :--- | :--- | :--- |
| **Production Quotidienne** | Rust, C++20, C | Moteurs de stockage, cœurs de calcul DSP audio, sondes eBPF |
| **Outils & Services** | Go, Python, Zig | Outils de compilation sur mesure, pipelines de données, bancs de test |
| **Shell & Scripting système** | Fish, POSIX Shell, Bash | Initialisation d'environnements, bancs d'essai CI, paramétrage noyau |

### Systèmes & Architecture
| Domaine | Technologies & Standards |
| :--- | :--- |
| **Noyau & Système** | Linux (Arch / Debian), `io_uring`, `epoll`, eBPF, cgroups v2, hugepages |
| **Protocoles & RPC** | QUIC, gRPC, Protocol Buffers, FlatBuffers, Cap'n Proto, WebSocket |
| **Données & Consensus** | Consensus Raft, LSM-Tree, WAL, architecture interne de RocksDB, SQLite, PostgreSQL |
| **Modèles de Concurrence** | Tampons circulaires lock-free, RCU (Read-Copy-Update), modèles Acteur, files SPMC/MPSC |

### Poste de Travail
```text
Système d'exploitation : Arch Linux (Noyau 6.x, patchset zen)
Émulateur de terminal  : Alacritty + Tmux
Éditeur de code        : Neovim (LSP natif, Lua, Treesitter)
Interpréteur shell     : Fish shell avec prompt starship
Outils de compilation  : Cargo, CMake, Ninja, Make
Machine principale     : AMD Ryzen 9 7950X, 64GB DDR5 ECC, PCIe 4.0 NVMe RAID-0
Équipement audio       : RME Babyface Pro FS, synthétiseur modulaire Eurorack 48HP
```

---

## 📈 Philosophie d'Ingénierie

1. **L'exactitude prime sur l'ingéniosité** : Un code rapide qui corrompt les données est inutile. Prouvez systématiquement les invariants avec des tests basés sur les propriétés (Property testing) et le fuzzing.
2. **Sympathie Mécanique (Mechanical Sympathy)** : Gardez toujours à l'esprit les caches processeur, les prédicteurs de branchement, les tables des pages et la bande passante mémoire. Le matériel n'est pas une fiction abstraite.
3. **Tests Déterministes** : Une simulation avec machines d'états reproductibles met en lumière les situations de concurrence critique bien plus vite que des semaines de tests en production.
4. **Parcimonie des Dépendances** : Chaque bibliothèque tierce introduite est une dette de maintenance future. Privilégiez les interfaces standard éprouvées.

---

## 📚 Lectures et Recherches du Moment

- *Designing Data-Intensive Applications* de Martin Kleppmann (3e relecture, axée sur les mécanismes de bas niveau des moteurs de stockage)
- Vérification formelle des structures de données sans verrou avec TLA+
- Implémentation d'algorithmes DSP audio basse consommation sur microcontrôleurs ARM Cortex-M7

---

## 📬 Me Contacter

- **GitHub Discussions** : N'hésitez pas à ouvrir un sujet sur mes dépôts.
- **Courriel** : `soren.lindqvist.dev [at] proton.me`
- **Empreinte PGP** : `9B4F 3E21 78C6 A10D 5E42  F098 32D1 8A7B 64C2 11E9`
- **Localisation** : Stockholm, Suède (UTC+1 / CET)

---
*Rédigé par Soren Lindqvist • Dernière mise à jour : Octobre 2026*
