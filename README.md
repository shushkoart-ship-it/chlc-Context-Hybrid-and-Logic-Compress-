```markdown
# CHLC — Context Hybrid and Logical Compress

**Analyze. Adapt. Compress.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.6+](https://img.shields.io/badge/python-3.6+-blue.svg)](https://www.python.org/)
[![PyPI version](https://badge.fury.io/py/chlc.svg)](https://badge.fury.io/py/chlc)

CHLC is a **smart compression library** that doesn't just compress data — it **understands** it. It analyzes the content (text, binary, structured data), selects the optimal combination of algorithms, and applies them in a hybrid chain. The result is better compression, especially for text and structured data.

---

## ✨ Why CHLC?

| Feature | Description |
|---------|-------------|
| 🧠 **Context-Aware** | Detects file type (text, JSON, binary, etc.) and chooses strategy |
| 🧩 **Hybrid Chains** | Combines RLE, Delta, Dictionary, and more |
| 🛡️ **Integrity** | CRC32 checksum in every `.chlc` file |
| 📊 **Error Codes** | 4-character codes for precise debugging |
| 📦 **Pure Python** | No external dependencies |

---

## 🔧 Installation

```bash
pip install chlc
```

Or from source:

```bash
git clone https://github.com/YOUR_USERNAME/chlc.git
cd chlc
pip install -e .
```

---

🚀 Quick Start

Compress a file

```python
import chlc

chlc.compress_file('document.txt')  # → document.chlc
```

Decompress a file

```python
import chlc

chlc.decompress_file('document.chlc')  # → document_restored.txt
```

Work with bytes (in memory)

```python
import chlc

data = b"Hello world" * 100

compressed = chlc.compress(data)
original = chlc.decompress(compressed)

assert data == original  # True
```

---

📦 File Format: .chlc

Every CHLC file contains:

```
┌─────────────────────────────────────────┐
│ Magic: "CHLC" (4 bytes)                 │
│ Version: 0x01 (1 byte)                  │
│ Steps count (1 byte)                    │
│ Original size (4 bytes)                 │
│ Compressed size (4 bytes)               │
│ CRC32 checksum (4 bytes)                │
│ Algorithm chain (N bytes)               │
├─────────────────────────────────────────┤
│ Compressed data                         │
└─────────────────────────────────────────┘
```

---

🧪 Supported Algorithms

Algorithm Code Description
RLE 0x01 Run-Length Encoding for repetitive bytes
Delta 0x02 Stores differences between adjacent values
Dictionary 0x03 Replaces frequent words with short codes
Spaces 0x04 Removes extra whitespace and newlines
(more coming) — —

---

❗ Error Codes

Every error has a 4-character code for precise debugging:

Code Description
F001 File is not a CHLC archive
F002 Header is corrupted
V001 Unsupported format version
D001 CRC32 mismatch (file corrupted)
D002 Data truncated
A001 Unknown algorithm in the chain
A002 RLE data is invalid
S001 Insufficient memory
S002 Permission denied
S003 File not found

Usage

```python
import chlc

try:
    chlc.decompress_file('broken.chlc')
except chlc.CHLCError as e:
    print(e)  # [D001] CRC32 mismatch (file corrupted)
```

---

🧠 How It Works

```
Input File
    ↓
[1] Context Analysis → What type is this? (text, binary, JSON, ...)
    ↓
[2] Algorithm Selection → Choose the best chain
    ↓
[3] Hybrid Compression → Apply algorithms in sequence
    ↓
[4] Save .chlc → Add header + CRC32
```

Decompression applies the reverse chain automatically.

---

📊 Performance

File Type Original CHLC Compressed Ratio
war_and_peace.txt 3.2 MB ~1.1 MB ~65%
config.json 45 KB ~12 KB ~73%
source_code.py 128 KB ~40 KB ~68%

(Numbers depend on content and algorithm chain.)

---

🤝 Contributing

Contributions are welcome! Here's how:

1. Fork the repo
2. Create a feature branch (git checkout -b feature/amazing)
3. Commit changes (git commit -m 'Add amazing feature')
4. Push to branch (git push origin feature/amazing)
5. Open a Pull Request

---

📝 License

MIT License — see LICENSE for details.

TL;DR: Use it freely, modify it, sell it, but keep the copyright notice.

---

🌟 Support

If you like this project, please ⭐ star it on GitHub!

---

📬 Contact

· Author: am1s3
· Email: shushko.art@gmail.com
