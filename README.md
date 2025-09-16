# Simple TCP Port Scanner

[![License: MIT](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Python](https://img.shields.io/badge/python-3.7%2B-blue.svg)](https://www.python.org/)

---

## Project Overview

A compact, easy-to-read Python utility that checks a target host (domain or IPv4 address) for open TCP ports from a curated list of common service ports. This tool is built with the Python standard library (`socket`) and is intended for educational use, quick local diagnostics, and light-weight testing in development environments.

## Key Features

* Resolves hostnames to IPv4 addresses and gracefully handles DNS errors.
* Scans a configurable list of common TCP ports (FTP, SSH, HTTP, HTTPS, DNS, SMTP, etc.).
* Uses `connect_ex()` with a short timeout to determine reachability, avoiding unhandled exceptions on failed connections.
* Simple command-line interface with clear, colored-friendly status output (OPEN/CLOSED).
* Minimal dependencies — works with the Python standard library only.

---

## Table of Contents

* [Installation](#installation)
* [Usage](#usage)
* [Example Output](#example-output)
* [Configuration](#configuration)
* [Limitations](#limitations)
* [Security & Legal](#security--legal)
* [Roadmap](#roadmap)
* [Contributing](#contributing)
* [License](#license)

---

## Installation

1. Ensure Python 3.7 or newer is installed on your system.
2. Clone this repository or copy the `port_scanner.py` file into your project directory.
3. (Optional) Create and activate a virtual environment:

```bash
python3 -m venv venv
# macOS / Linux
source venv/bin/activate
# Windows
venv\Scripts\activate
```

No external packages are required.

---

## Usage

Run the scanner interactively from the command line:

```bash
python3 port_scanner.py
Enter target IP or domain: example.com
```

The script will resolve the hostname (if necessary) and attempt to connect to each port in the scanner's port list. Ports that accept a TCP connection are reported as `OPEN`; ports that do not are reported as `CLOSED`.

---

## Example Output

```
Enter target IP or domain: localhost

🔍 Scanning target: localhost (127.0.0.1)

❌ Port 20 is CLOSED
❌ Port 21 is CLOSED
✅ Port 22 is OPEN
❌ Port 23 is CLOSED
❌ Port 25 is CLOSED
❌ Port 53 is CLOSED
✅ Port 80 is OPEN
❌ Port 110 is CLOSED
❌ Port 143 is CLOSED
❌ Port 443 is CLOSED
❌ Port 8080 is CLOSED
```

---

## Configuration

You can modify the `common_ports` list in `port_scanner.py` to add or remove ports. Typical ports included by default:

```python
common_ports = [20, 21, 22, 23, 25, 53, 80, 110, 143, 443, 8080]
```

For production or advanced use, consider accepting ports or ranges via command-line arguments and adding concurrency (see Roadmap).

---

## Limitations

* IPv4 only — the script uses `socket.AF_INET` and `socket.gethostbyname()`.
* Small, fixed port list — not a full-range scanner.
* `connect_ex()` does not reliably distinguish between `closed` and `filtered` (firewalled) ports.
* Single-threaded — scanning a large number of ports will be slow.
* No banner grabbing or service fingerprinting — the script only tests for TCP connection acceptance.

---

## Security & Legal

Network scanning can be considered intrusive. Only scan machines and networks that you own or have explicit authorization to test. Unauthorized scans may violate local laws or acceptable-use policies. Use this tool responsibly and ethically.

---

## Roadmap (Suggested Enhancements)

* Add IPv6 support using `socket.getaddrinfo()`.
* Accept port ranges and custom lists via `argparse`.
* Implement concurrency with `concurrent.futures.ThreadPoolExecutor` or `asyncio`.
* Add banner grabbing after successful connections to identify running services.
* Provide machine-readable output formats (JSON, CSV) for automation.
* Add unit tests and CI checks.

---

## Contributing

Contributions are welcome. If you’d like to contribute:

1. Fork the repository.
2. Create a topic branch 
3. Commit your changes and push to your fork.
4. Open a pull request describing your changes.

Please follow a clear commit history and include tests for new functionality where appropriate.

---

## Author

Ganesh R Kuppasta=https://www.linkedin.com/in/ganesh-kuppasta-0677392ab/

---

## License

This project is licensed under the MIT License — see the `LICENSE` file for details.
