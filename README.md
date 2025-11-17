<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/banner/banner.dark.svg">
    <source media="(prefers-color-scheme: light)" srcset="assets/banner/banner.light.svg">
    <img alt="CELLSIGINT banner" src="assets/banner/banner.light.svg" width="900">
  </picture>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/version-5.0.0-00ff00?style=for-the-badge&labelColor=000000" alt="v5.0.0"/>
  <img src="https://img.shields.io/badge/rust-1.75+-ff6600?style=for-the-badge&logo=rust&labelColor=000000" alt="Rust"/>
  <img src="https://img.shields.io/badge/license-EINIX-blue?style=for-the-badge&labelColor=000000" alt="EINIX"/>
  <img src="https://img.shields.io/badge/PRs-welcome-00ffff?style=for-the-badge&labelColor=000000" alt="PRs Welcome"/>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/GSM-2G-yellow?style=flat-square&labelColor=1a1a1a" alt="GSM"/>
  <img src="https://img.shields.io/badge/EDGE-2.5G-orange?style=flat-square&labelColor=1a1a1a" alt="EDGE"/>
  <img src="https://img.shields.io/badge/UMTS-3G-blue?style=flat-square&labelColor=1a1a1a" alt="UMTS"/>
  <img src="https://img.shields.io/badge/LTE-4G-green?style=flat-square&labelColor=1a1a1a" alt="LTE"/>
  <img src="https://img.shields.io/badge/NR-5G-red?style=flat-square&labelColor=1a1a1a" alt="5G NR"/>
  <img src="https://img.shields.io/badge/FR2-mmWave-purple?style=flat-square&labelColor=1a1a1a" alt="mmWave"/>
</p>

<p align="center">
  <b>🔥 From RF to IMSI in microseconds: military-grade cellular SIGINT powered by Rust, rainbow tables, and machine learning. 🔥</b><br/>
  <sub>From 2G GSM to 5G mmWave • Rainbow Table Attacks • ML Classification • Distributed Operations</sub>
</p>

<p align="center">
  <a href="#-quick-start">Quick Start</a> •
  <a href="#-features">Features</a> •
  <a href="#-architecture">Architecture</a> •
  <a href="#-hardware">Hardware</a> •
  <a href="#-documentation">Docs</a>
</p>

---

<div align="center">

### 🎯 **One Tool. Every Generation. Complete Visibility.**

</div>

```
┌────────────────────────────────────────────────────────────────────────────────────┐
│                                                                                    │
│   ┌─────────┐     ┌─────────┐     ┌─────────┐     ┌─────────┐     ┌─────────┐      │
│   │  2G/GSM │───▶│  3G/UMTS│───▶│  4G/LTE │───▶│ 5G FR1  │───▶│ 5G FR2  │      │
│   │ 850-1900│     │ 700-2100│     │ 450-5925│     │ Sub-6GHz│     │ mmWave  │      │
│   └────┬────┘     └────┬────┘     └────┬────┘     └────┬────┘     └────┬────┘      │
│        │               │               │               │               │           │
│        ▼               ▼               ▼               ▼               ▼           │
│   ┌──────────────────────────────────────────────────────────────────────┐         │
│   │                    CELLULAR SIGNAL HUNT v5.0                         │         │
│   │  ════════════════════════════════════════════════════════════════    │         │
│   │  [■■■■■■■■■■] IMSI Capture    [■■■■■■■■■■] GUTI Extraction           │         │
│   │  [■■■■■■■■■■] Rainbow Tables  [■■■■■■■■■■] ML Classification         │         │
│   │  [■■■■■■■■■■] SS7 Analysis    [■■■■■■■■■■] WebRTC Mesh               │         │
│   └──────────────────────────────────────────────────────────────────────┘         │
│                                                                                    │
└────────────────────────────────────────────────────────────────────────────────────┘
```

---

## ⚡ Quick Start

```bash
# Clone the beast
git clone https://github.com/QuantGenAIPhr34kW1z/cellsigint-core.git cellsigint
cd cellsigint

# Build with all the power
cargo build --release --all-features

# Simulation mode (no hardware needed)
./target/release/gsm-scanner --simulate -vv

# Real capture with RTL-SDR
sudo ./target/release/gsm-scanner -B gsm900 -g 40

# LTE cell hunting
sudo ./target/release/gsm-scanner --mode lte --band 7

# 5G NR FR2 mmWave (requires wideband SDR)
sudo ./target/release/gsm-scanner --mode nr --band n257 --fr2
```

---

## 🚀 Features

<table>
<tr>
<td width="50%">

---

## 🏗️ Architecture

```
                          ┌─────────────────────────────────────┐
                          │         SIGNAL HUNT CORE            │
                          │═════════════════════════════════════│
                          │                                     │
    ┌──────────────┐      │   ┌─────────┐   ┌─────────┐         │      ┌──────────────┐
    │   RTL-SDR    │──────│─▶│ Capture │─▶│ Demod   │         │      │   Database   │
    │   HackRF     │      │   │ Engine  │   │ GMSK/   │         │──────│   SQLite     │
    │   USRP B210  │      │   │         │   │ OFDM    │         │      │   TimeSeries │
    │   LimeSDR    │      │   └────┬────┘   └────┬────┘         │      └──────────────┘
    │   RX-888     │      │        │             │              │
    └──────────────┘      │        ▼             ▼              │      ┌──────────────┐
                          │  ┌─────────────────────┐            │      │   WebRTC     │
                          │  │   Protocol Stack    │            │──────│   P2P Mesh   │
                          │  │   ───────────────── │            │      │   Signaling  │
                          │  │   L1 → L2 → L3      │            │      └──────────────┘
                          │  │   PHY  MAC  RRC/NAS │            │
                          │  └──────────┬──────────┘            │      ┌──────────────┐
                          │             │                       │      │   ML Engine  │
                          │             ▼                       │──────│   TensorFlow │
                          │  ┌─────────────────────┐            │      │   PyTorch    │
                          │  │  Identity Extractor │            │      └──────────────┘
                          │  │  ═════════════════  │            │
                          │  │  IMSI GUTI 5G-GUTI  │            │      ┌──────────────┐
                          │  │  MSISDN IMEI TMSI   │            │      │   Rainbow    │
                          │  └─────────────────────┘            │──────│   Tables     │
                          │                                     │      │   2TB A5/1   │
                          └─────────────────────────────────────┘      └──────────────┘
```

---

## 📊 Protocol Support Matrix

|      Protocol      | Capture | Decode |  Extract  |    Attack    |    Status    |
| :-----------------: | :-----: | :----: | :--------: | :----------: | :-----------: |
|    **GSM**    |   ✅   |   ✅   |  ✅ IMSI  |   ✅ A5/1   | 🟢 Production |
| **GPRS/EDGE** |   ✅   |   ✅   |  ✅ TLLI  |    ✅ GEA    | 🟢 Production |
|   **UMTS**   |   ✅   |   ✅   |  ✅ IMSI  | ⚠️ Limited |    🟡 Beta    |
|    **LTE**    |   ✅   |   ✅   |  ✅ GUTI  |      ❌      | 🟢 Production |
| **5G NR FR1** |   ✅   |   ✅   | ✅ 5G-GUTI |      ❌      | 🟢 Production |
| **5G NR FR2** |   ✅   |   ✅   | ✅ 5G-GUTI |      ❌      |    🟡 Beta    |
|  **SS7/MAP**  |   ✅   |   ✅   | ✅ MSISDN |     N/A     | 🟢 Production |
|   **GTP-C**   |   ✅   |   ✅   |   ✅ APN   |     N/A     | 🟢 Production |

---

## 🔧 Hardware Compatibility

<table>
<tr>
<th>Device</th>
<th>BW</th>
<th>Freq Range</th>
<th>GSM</th>
<th>LTE</th>
<th>5G FR1</th>
<th>5G FR2</th>
<th>TX</th>
</tr>
<tr>
<td><b>RTL-SDR v4</b></td>
<td>2.4MHz</td>
<td>24-1766 MHz</td>
<td>✅</td>
<td>❌</td>
<td>❌</td>
<td>❌</td>
<td>❌</td>
</tr>
<tr>
<td><b>HackRF One</b></td>
<td>20MHz</td>
<td>1-6000 MHz</td>
<td>✅</td>
<td>✅</td>
<td>⚠️</td>
<td>❌</td>
<td>✅</td>
</tr>
<tr>
<td><b>USRP B210</b></td>
<td>56MHz</td>
<td>70-6000 MHz</td>
<td>✅</td>
<td>✅</td>
<td>✅</td>
<td>❌</td>
<td>✅</td>
</tr>
<tr>
<td><b>LimeSDR</b></td>
<td>61MHz</td>
<td>100kHz-3.8GHz</td>
<td>✅</td>
<td>✅</td>
<td>✅</td>
<td>❌</td>
<td>✅</td>
</tr>
<tr>
<td><b>USRP X310 + UBX-160</b></td>
<td>160MHz</td>
<td>10MHz-6GHz</td>
<td>✅</td>
<td>✅</td>
<td>✅</td>
<td>❌</td>
<td>✅</td>
</tr>
<tr>
<td><b>Sivers IMA EVK</b></td>
<td>400MHz</td>
<td>24-30 GHz</td>
<td>❌</td>
<td>❌</td>
<td>❌</td>
<td>✅</td>
<td>✅</td>
</tr>
</table>

---

## 📈 Performance

```
╔══════════════════════════════════════════════════════════════════════════════════╗
║                           BENCHMARK RESULTS                                      ║
╠══════════════════════════════════════════════════════════════════════════════════╣
║                                                                                  ║
║   Sample Processing Rate                                                         ║
║   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━             ║
║   RTL-SDR (2.4 MSps)    ████████████████████████████████████████  100%           ║
║   HackRF (20 MSps)      ████████████████████████████████████████  100%           ║
║   USRP B210 (56 MSps)   ████████████████████████████████████████  100%           ║
║   LimeSDR (61 MSps)     ████████████████████████████████████████  100%           ║
║                                                                                  ║
║   Identity Extraction Latency                                                    ║
║   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━             ║
║   IMSI (GSM)            < 50ms  ████                                             ║
║   GUTI (LTE)            < 100ms ████████                                         ║
║   5G-GUTI (NR)          < 200ms ████████████████                                 ║
║                                                                                  ║
║   A5/1 Rainbow Table Lookup                                                      ║
║   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━             ║
║   Average lookup time   < 2 seconds                                              ║
║   Success rate          > 90% (with full tables)                                 ║
║   Table size            2TB (full keyspace coverage)                             ║
║                                                                                  ║
╚══════════════════════════════════════════════════════════════════════════════════╝
```

---

## 🧪 ML Signal Classification

```python
# Supported signal types for classification

SIGNAL_TYPES = {
    # 2G
    "GSM_FCCH", "GSM_SCH", "GSM_BCCH", "GSM_TCH", "GSM_RACH", "GSM_SDCCH",
    "EDGE_PDTCH",

    # 3G
    "UMTS_PSCH", "UMTS_SSCH", "UMTS_CPICH", "UMTS_DPCH",

    # 4G
    "LTE_PSS", "LTE_SSS", "LTE_PBCH", "LTE_PDSCH", "LTE_PDCCH",
    "LTE_PUSCH", "LTE_PRACH",

    # 5G
    "NR_PSS", "NR_SSS", "NR_PBCH", "NR_PDSCH", "NR_SSB",

    # Other
    "WIFI_802.11a/b/g/n/ac/ax", "BLUETOOTH", "BLE", "ZIGBEE",
    "LORA", "SIGFOX", "NOISE"
}

# Modulation types for AMR
MODULATIONS = [
    "BPSK", "QPSK", "8PSK", "16QAM", "64QAM", "256QAM",
    "GMSK", "GFSK", "MSK", "OFDM", "DSSS", "CSS"
]
```

---

## 🌐 Distributed Deployment

```
                    ┌─────────────────────────────────────────┐
                    │            WEBRTC MESH                  │
                    │     NAT Traversal • DTLS • SCTP         │
                    └─────────────────────────────────────────┘
                                        │
           ┌────────────────────────────┼────────────────────────────┐
           │                            │                            │
           ▼                            ▼                            ▼
    ┌──────────────┐              ┌──────────────┐              ┌──────────────┐
    │   NODE #1    │◀──────────▶│   NODE #2    │◀──────────▶│   NODE #3    │
    │  ──────────  │              │  ──────────  │              │  ──────────  │
    │  RTL-SDR     │              │  HackRF      │              │  USRP B210   │
    │  GSM 900     │              │  LTE B7      │              │  5G n78      │
    │  GPS: Fixed  │              │  GPS: RTK    │              │  GPS: RTK    │
    │              │              │              │              │              │
    │  📍 51.5°N   │              │  📍 51.6°N   │              │  📍 51.4°N   │
    │     0.1°W    │              │     0.2°W    │              │     0.0°E    │
    └──────────────┘              └──────────────┘              └──────────────┘
           │                            │                            │
           └────────────────────────────┼────────────────────────────┘
                                        │
                                        ▼
                          ┌─────────────────────────┐
                          │    TRIANGULATION        │
                          │    ━━━━━━━━━━━━━        │
                          │    Cell: 234-15-1234    │
                          │    Est. Location:       │
                          │    51.52°N, 0.08°W      │
                          │    Accuracy: ±50m       │
                          │    Confidence: 94%      │
                          └─────────────────────────┘
```

---

## 📁 Project Structure

```
cellular-signal-hunt/
├── src/
│   ├── main.rs              # Entry point & CLI
│   │
│   ├── # ═══ PHASE: GSM CORE ═══
│   ├── sdr.rs               # RTL-SDR abstraction
│   ├── signal.rs            # DSP, FFT, burst detection
│   ├── sync.rs              # TSC, FCCH, SCH, timing
│   ├── channel.rs           # Viterbi, interleaving, CRC
│   ├── l2.rs                # LAPDm Layer 2
│   ├── logical_channel.rs   # BCCH, CCCH, SDCCH, TCH
│   ├── extractor.rs         # L3 parsing, IMSI, SMS
│   ├── storage.rs           # SQLite backend
│   ├── tui.rs               # Terminal dashboard
│   ├── scanner.rs           # ARFCN scanner
│   ├── web.rs               # REST API + WebSocket
│   ├── hopping.rs           # Frequency hopping
│   ├── gprs.rs              # GPRS/EDGE 8PSK
│   ├── multi_sdr.rs         # Multi-device sync
│   │
│   ├── # ═══ PHASE: WIDEBAND ═══
│   ├── soapy.rs             # SoapySDR abstraction
│   ├── wideband.rs          # HackRF, USRP, LimeSDR
│   ├── lte.rs               # LTE PHY (PSS/SSS/PBCH)
│   ├── lte_decoder.rs       # NAS/RRC protocols
│   ├── lte_tui.rs           # LTE dashboard
│   │
│   ├── # ═══ PHASE: 5G & ML ═══
│   ├── nr.rs                # 5G NR FR1
│   ├── cipher.rs            # A5/1, A5/2 analysis
│   ├── ml.rs                # Signal classification
│   ├── distributed.rs       # Multi-node coordination
│   │
│   ├── # ═══ PHASE: PROTOCOLS ═══
│   ├── um_layer.rs          # GSM air interface
│   ├── auth.rs              # Auth interception
│   ├── ss7.rs               # SS7/MAP parsing
│   ├── gtpc.rs              # GTP-C decoder
│   │
│   └── # ═══ PHASE: ADVANCED ═══
│       ├── rainbow.rs       # A5/1 rainbow tables
│       ├── ml_dataset.rs    # ML training data
│       ├── webrtc_coord.rs  # WebRTC P2P mesh
│       └── nr_fr2.rs        # 5G mmWave
│
├── Cargo.toml               # Dependencies
├── README.md                # You are here
├── SECURITY.md              # Security considerations
└── LICENSE                  # EINIX License
```

---

## 📊 Statistics

<div align="center">

|         Metric         |  Value  |
| :---------------------: | :-----: |
| **Lines of Code** | ~18,500 |
|    **Modules**    |   31   |
|   **Protocols**   |   15+   |
| **Signal Types** |   35+   |
|  **SDR Devices**  |   8+   |
|   **Features**   |   50+   |

</div>

---

## ⚠️ Legal Disclaimer

```
╔══════════════════════════════════════════════════════════════════════════════════╗
║                                                                                  ║
║   ██╗    ██╗ █████╗ ██████╗ ███╗  ██╗██╗███╗  ██╗ ██████╗                        ║
║   ██║    ██║██╔══██╗██╔══██╗████╗ ██║██║████╗ ██║██╔════╝                        ║
║   ██║ █╗ ██║███████║██████╔╝██╔██╗██║██║██╔██╗██║██║  ███╗                       ║
║   ██║███╗██║██╔══██║██╔══██╗██║╚████║██║██║╚████║██║   ██║                       ║
║   ╚███╔███╔╝██║  ██║██║  ██║██║ ╚███║██║██║ ╚███║╚██████╔╝                       ║
║    ╚══╝╚══╝ ╚═╝  ╚═╝╚═╝  ╚═╝╚═╝  ╚══╝╚═╝╚═╝  ╚══╝ ╚═════╝                        ║
║                                                                                  ║
║   This software is provided for:                                                 ║
║   • Authorized security research and penetration testing                         ║
║   • Educational purposes in controlled lab environments                          ║
║   • Private network testing with explicit permission                             ║
║   • Academic research on cellular protocol security                              ║
║                                                                                  ║
║   Unauthorized interception of cellular communications is ILLEGAL in most        ║
║   jurisdictions and may result in severe criminal penalties.                     ║
║                                                                                  ║
║   THE AUTHORS ASSUME NO LIABILITY FOR MISUSE OF THIS SOFTWARE.                   ║
║   By using this software, you agree to comply with all applicable laws.          ║
║                                                                                  ║
╚══════════════════════════════════════════════════════════════════════════════════╝
```

---

## 📚 Documentation

|           Document           | Description                                        |
| :--------------------------: | :------------------------------------------------- |
|   [SECURITY.md](SECURITY.md)   | Security considerations and responsible disclosure |
|      [API.md](docs/API.md)      | REST API and WebSocket documentation               |
| [HARDWARE.md](docs/HARDWARE.md) | Detailed hardware setup guides                     |

---

## 📖 References

<details>
<summary><b>3GPP Specifications</b></summary>

- TS 04.08 - GSM Mobile Radio Interface Layer 3
- TS 05.02 - GSM Multiplexing and Multiple Access
- TS 05.03 - GSM Channel Coding
- TS 03.20 - GSM Security Functions (A5 Cipher)
- TS 29.002 - SS7 MAP Protocol
- TS 29.060 - GTP-C Protocol
- TS 36.211 - LTE Physical Channels
- TS 36.331 - LTE RRC Protocol
- TS 24.301 - LTE NAS Protocol
- TS 38.104 - NR Base Station Radio
- TS 38.211 - NR Physical Channels
- TS 38.101-2 - NR UE Radio (FR2)

</details>

<details>
<summary><b>Security Research</b></summary>

- Biryukov, Shamir, Wagner: "Real Time Cryptanalysis of A5/1"
- Nohl, Paget: "GSM: SRSLY?" (CCC 2009)
- Golde, Redon, Seifert: "Let Me Answer That For You" (USENIX 2013)
- Rupprecht et al.: "Breaking LTE on Layer Two" (IEEE S&P 2019)

</details>

---

**Built with 🦀 Rust • Powered by 📡 SDR • For 🔬 Science**

© EINIX SA All rights reserved.

</div>
