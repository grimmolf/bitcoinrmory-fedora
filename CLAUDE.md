# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Core Architecture

Bitcoin Armory is a full-featured Bitcoin wallet client written in Python with C++ performance-critical components. It operates as a light client that depends on Bitcoin Core for blockchain data and network connectivity.

### Key Components

- **ArmoryQt.py**: Main GUI application entry point (PyQt4-based)
- **armoryd.py**: JSON-RPC daemon for headless/programmatic access  
- **armoryengine/**: Core Python business logic modules
- **cppForSwig/**: High-performance C++ blockchain operations
- **BDM (Block Data Manager)**: Central component managing blockchain data and wallet operations
- **SDM (Satoshi Daemon Manager)**: Manages Bitcoin Core integration and communication

### Architecture Pattern
```
GUI/RPC Layer → Python Business Logic → SWIG Bindings → C++ Core → LevelDB Storage
                                                      ↑
                                              Bitcoin Core (via RPC)
```

## Build and Development Commands

### Building the Application
```bash
# Build all components (C++ and Python)
make

# Build with debug symbols
make DEBUG=1

# Build test tools
make all-test-tools

# Clean build artifacts
make clean
```

### Testing
```bash
# Run all tests (C++ and Python)
make test

# Run C++ unit tests only
make gtest

# Run Python unit tests only  
make pytest
# or directly:
python -m unittest discover
```

### C++ Development
The C++ code in `cppForSwig/` uses:
- **SWIG** for Python bindings
- **LevelDB** for blockchain storage  
- **Crypto++** for cryptographic operations
- Custom Makefile build system

### Dependencies
Core dependencies include:
- **Python 2.6/2.7** with development headers
- **PyQt4** for GUI
- **Twisted** for networking (RPC server)
- **SWIG** for C++ bindings
- **Crypto++** development libraries
- **g++** compiler with C++11 support

## Key Development Notes

### Bitcoin Core Integration
Armory requires a running Bitcoin Core instance. The SDM component:
- Manages bitcoind process lifecycle
- Handles RPC communication for blockchain data
- Monitors synchronization status
- Can auto-download and configure Bitcoin Core

### Wallet Architecture
- **Deterministic wallets** with hierarchical key generation
- **Multi-mode support**: Full, watching-only, and observing wallets
- **Advanced encryption** with key stretching (KDF)
- **Fragmented backup system** for enhanced security
- **Multi-signature support** (M-of-N schemes)

### Threading Model
- **Main thread**: GUI and user interactions
- **BDM thread**: Blockchain operations and database access
- **Network thread**: Bitcoin Core communication
- **Injection system** for cross-thread communication

### File Structure
- `armoryengine/` - Core wallet and blockchain logic
- `ui/` - GUI dialog and frame components  
- `pytest/` - Python unit tests
- `cppForSwig/` - C++ blockchain database and utilities
- `cppForSwig/gtest/` - C++ unit tests
- `img/` - GUI icons and resources

### Testing Strategy
- **C++ tests**: Google Test framework in `cppForSwig/gtest/`
- **Python tests**: unittest discovery in `pytest/`
- **Integration tests**: Full blockchain operations with test data
- Test data includes sample blockchain files in `cppForSwig/reorgTest/`

### Installation and Packaging
- **Linux**: Makefile with install target, debian packaging in `dpkgfiles/`
- **OSX**: Build scripts in `osxbuild/`
- **Windows**: py2exe setup for standalone executable

This codebase prioritizes security, performance, and Bitcoin protocol compliance. The hybrid Python/C++ architecture provides flexibility for GUI development while maintaining performance for blockchain operations.