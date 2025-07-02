##Armory

**Created by Alan Reiner on 13 July, 2011**  
**Modernized for Python 3 & Fedora 42 - January 2025**

[Armory](https://github.com/etotheipi/BitcoinArmory) is a full-featured Bitcoin client, offering a dozen innovative features not found in any other client software! Manage multiple wallets (deterministic and watching-only), print paper backups that work forever, import or sweep private keys, and keep your savings in a computer that never touches the internet, while still being able to manage incoming payments, and create outgoing payments with the help of a USB key.

Multi-signature transactions are accommodated under-the-hood about 80%, and will be completed and integrated into the UI soon.

**Armory has no independent networking components built in.** Instead, it relies on on the Satoshi client to securely connect to peers, validate blockchain data, and broadcast transactions for us.  Although it was initially planned to cut the umbilical cord to the Satoshi client and implement independent networking, it has turned out to be an inconvenience worth having. Reimplementing all the networking code would be fraught with bugs, security holes, and possible blockchain forking.  The reliance on Bitcoin-Qt right now is actually making Armory more secure!

## 🚀 **Python 3 & Modern System Compatibility**

This fork has been comprehensively modernized for **Python 3** and **modern Linux distributions** (tested on Fedora 42). The modernization includes:

- ✅ **Python 3.7+ Compatibility**: All syntax, imports, and language features updated
- ✅ **PyQt5 Migration**: Complete GUI framework upgrade from PyQt4 → PyQt5  
- ✅ **Modern Build Tools**: Updated packaging, requirements, and build scripts
- ✅ **Fedora 42 Ready**: Tested and validated on modern Linux distributions

### **Key Modernization Changes:**
- All print statements converted to function calls
- Python 2/3 import compatibility (email, urllib2, etc.)
- Exception syntax updated (`except X, e:` → `except X as e:`)
- Signal/slot syntax modernized for PyQt5
- Build system updated (pyrcc4 → pyrcc5)
- Removed deprecated Python 2 constructs (xrange, L suffixes, etc.)

##Donations

##Building Armory From Source


## Installation Instructions

### Prerequisites

This modernized version requires:
- **Python 3.7+** with development headers
- **PyQt5** for GUI components
- **Bitcoin Core** (bitcoind) for blockchain operations
- **Modern Linux distribution** (tested on Fedora 42)

### Quick Installation

#### Fedora/RHEL/CentOS
```bash
# Install system dependencies
sudo dnf install -y python3-devel python3-pip gcc-c++ make swig \
    python3-qt5 python3-twisted cryptopp-devel leveldb-devel

# Clone and build
git clone https://github.com/grimmolf/bitcoinrmory-fedora.git
cd bitcoinrmory-fedora
make
```

#### Ubuntu/Debian
```bash
# Install system dependencies
sudo apt update
sudo apt install -y python3-dev python3-pip build-essential swig \
    python3-pyqt5 python3-twisted libcrypto++-dev libleveldb-dev

# Clone and build
git clone https://github.com/grimmolf/bitcoinrmory-fedora.git
cd bitcoinrmory-fedora
make
```

#### Arch Linux
```bash
# Install system dependencies
sudo pacman -S python python-pip gcc make swig python-pyqt5 \
    python-twisted crypto++ leveldb

# Clone and build
git clone https://github.com/grimmolf/bitcoinrmory-fedora.git
cd bitcoinrmory-fedora
make
```

### Detailed Installation Steps

1. **Install Bitcoin Core** (required dependency):
   ```bash
   # Download from https://bitcoin.org/en/download
   # Or install via package manager:
   sudo dnf install bitcoin-core  # Fedora
   sudo apt install bitcoind      # Ubuntu/Debian
   ```

2. **Clone the repository**:
   ```bash
   git clone https://github.com/grimmolf/bitcoinrmory-fedora.git
   cd bitcoinrmory-fedora
   ```

3. **Install Python dependencies**:
   ```bash
   pip3 install --user -r requirements.txt
   ```

4. **Build C++ components**:
   ```bash
   make clean
   make
   ```

5. **Run tests** (optional but recommended):
   ```bash
   make test
   ```

6. **Launch Armory**:
   ```bash
   python3 ArmoryQt.py
   ```

### Dependencies (Updated for Python 3)

**Core Dependencies:**
* **GNU Compiler Collection (g++)**
  - Fedora: `sudo dnf install gcc-c++`
  - Ubuntu: `sudo apt install build-essential`

* **Python 3.7+ with development headers**
  - Fedora: `sudo dnf install python3-devel`
  - Ubuntu: `sudo apt install python3-dev`

* **PyQt5** (replaces PyQt4)
  - Fedora: `sudo dnf install python3-qt5`
  - Ubuntu: `sudo apt install python3-pyqt5`

* **Python Twisted** (asynchronous networking)
  - Fedora: `sudo dnf install python3-twisted`
  - Ubuntu: `sudo apt install python3-twisted`

* **Crypto++** (cryptographic operations)
  - Fedora: `sudo dnf install cryptopp-devel`
  - Ubuntu: `sudo apt install libcrypto++-dev`

* **SWIG** (Python/C++ bindings)
  - Fedora: `sudo dnf install swig`
  - Ubuntu: `sudo apt install swig`

* **LevelDB** (blockchain database)
  - Fedora: `sudo dnf install leveldb-devel`
  - Ubuntu: `sudo apt install libleveldb-dev`

### Troubleshooting

**Build Issues:**
- Ensure all development packages are installed (`-devel` on Fedora, `-dev` on Ubuntu)
- For build errors, try: `make clean && make DEBUG=1`

**Runtime Issues:**
- Verify Bitcoin Core is installed and accessible
- Check Python path includes local installation: `export PYTHONPATH=$PWD:$PYTHONPATH`
- For GUI issues, ensure X11 forwarding is enabled for SSH sessions

**Python Import Errors:**
- This version requires Python 3.7+, will not work with Python 2.x
- Install missing packages with: `pip3 install <package-name>`  

##Sample Code

Armory contains over 25,000 lines of code, between the C++ and python libraries.  This can be very confusing for someone unfamiliar with the code (you).  Below I have attempted to illustrate the CONOPS (concept of operations) that the library was designed for, so you know how to use it in your own development activities.  There is a TON of sample code in the following:

* C++ -   [BlockUtilsTest.cpp](cppForSwig/BlockUtilsTest.cpp)
* Python -   [Unit Tests](pytest/), [sample_armory_code.py](extras/sample_armory_code.py)


##License

Distributed under the GNU Affero General Public License (AGPL v3)  
See [LICENSE file](LICENSE) or [here][License]

##Copyright

Copyright (C) 2011-2015, Armory Technologies, Inc.


[Armory Build Instructions]: https://bitcoinarmory.com/building-from-source
[Windows Crypto Download]: http://www.cryptopp.com/#download
[Windows SWIG Download]: http://www.swig.org/download.html
[Windows Python Download]: http://www.python.org/getit/
[Windows Twisted Download]: http://twistedmatrix.com/trac/wiki/Downloads
[Windows QT Download]: http://www.riverbankcomputing.co.uk/software/pyqt/download
[QT4 Reactor Download]: https://launchpad.net/qt4reactor
[Windows PyWin Download]: http://sourceforge.net/projects/pywin32/files/pywin32/
[Windows Py2Exe Download]:  http://www.py2exe.org/
[License]: http://www.gnu.org/licenses/agpl.html
[Donation Image]: https://chart.googleapis.com/chart?chs=250x250&cht=qr&chl=bitcoin:1ArmoryXcfq7TnCSuZa9fQjRYwJ4bkRKfv?&label=Armory+Donation
