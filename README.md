<h1 align="center">PySentry</h1>

<p align="center">
  <i>"A simple, educational Endpoint Detection & Response (EDR) tool — where Python meets Cyber Defense."</i>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.x-blue?logo=python" alt="Python Badge">
  <img src="https://img.shields.io/badge/psutil-Library-green" alt="psutil Badge">
  <img src="https://img.shields.io/badge/Platform-Windows-blueviolet" alt="Platform Badge">
  <img src="https://img.shields.io/badge/License-MIT-lightgrey" alt="License Badge">
</p>

---

## About The Project

**PySentry** is a lightweight educational Endpoint Detection & Response (EDR) system written entirely in Python. It was built to demonstrate defensive cybersecurity principles for a college technology exhibition.

*It's not a real antivirus — but it thinks like one.*

PySentry operates on a Zero Trust model: it assumes every unknown process or registry entry could be suspicious until proven safe. It includes two primary modules:
- **Active Network Scan**: monitors all running processes that maintain active internet connections.
- **Persistence Scan**: examines Windows Registry "Run" keys for unauthorized startup entries.

---

## Features

- **Unknown process detection**: flags processes not listed in the pre-defined safe list (`KNOWN_GOOD_PATHS`).
- **Process impersonation detection**: checks for legitimate process names (like `svchost.exe`) running from untrusted directories.
- **Suspicious port heuristics**: identifies processes using non-standard network ports (other than 80/443).
- **Registry persistence scan**: detects unauthorized programs in the Windows "Run" key.
- **Active response**: prompts the user for permission to terminate suspicious processes in real time.

---

## Getting Started

### Prerequisites
- Python 3.x
- `psutil` library

```bash
pip install psutil
```

### Installation

```bash
git clone https://github.com/D-Majumder/PySentry.git
cd PySentry
```

### Usage

This script must be run as Administrator for full functionality (open PowerShell or CMD via "Run as Administrator").

```bash
python py_sentry.py
```

The main menu will appear — choose from:
```
Option 1: Network Scan
Option 2: Persistence Scan
Option 3: Full System Audit
```

---

## Tuning Required

PySentry is intentionally strict — it will flag legitimate software (like Steam, Discord, or even your antivirus). To fine-tune:

1. Run Option 3 (Full System Audit).
2. Review the "SUSPICIOUS" alerts.
3. Open `py_sentry.py` and add safe entries to:
   ```python
   KNOWN_GOOD_PATHS = []       # For network scan
   KNOWN_SAFE_STARTUPS = []    # For persistence scan
   ```
4. Save and re-run the scan — the report should now be cleaner and more accurate.

---

## How to Demo This Project

### Demo 1: The "Unknown Attacker"

Run PySentry in Terminal 1 (as Admin):
```bash
python py_sentry.py
```
In Terminal 2, simulate a "malicious" connection:
```bash
python -c "import socket, time; s=socket.socket(); s.connect(('google.com', 80)); time.sleep(300)"
```
In Terminal 1, select Option 1 (Network Scan) — PySentry flags `python.exe` as UNKNOWN. Press `y` to block the threat; the process terminates instantly.

### Demo 2: The "Impersonator" (Advanced)

Copy `python.exe` from your installation folder to Downloads, rename it to `svchost.exe`, and run it as a fake "system process":
```bash
cd C:\Users\YourName\Downloads
.\svchost.exe -c "import socket, time; s=socket.socket(); s.connect(('google.com', 80)); time.sleep(300)"
```
In PySentry, choose Option 1 (Network Scan) — it detects "svchost.exe running from Downloads" as a HIGH-SEVERITY ALERT.

---

## Project Philosophy

PySentry helps beginners understand:
- How EDR tools monitor system behavior.
- How heuristics and process analysis can detect intrusions.
- Why whitelisting and zero trust matter in security.

---

## Disclaimer

This project is for educational purposes only. It is not a professional antivirus and should not be used for real-world protection. Use responsibly and only in controlled environments.

---

## Built With

- Python
- psutil
- Windows OS Registry APIs

---

## Author

<p align="center">
  <a href="mailto:dhrubamajumder@proton.me" target="_blank">
    <img src="https://img.shields.io/badge/Email-Dhruba%20Majumder-blue?logo=gmail" alt="Email Badge">
  </a>
  <a href="https://www.linkedin.com/in/iamdhrubamajumder/" target="_blank">
    <img src="https://img.shields.io/badge/LinkedIn-Dhruba%20Majumder-blue?logo=linkedin" alt="LinkedIn Badge">
  </a>
  <a href="https://github.com/D-Majumder" target="_blank">
    <img src="https://img.shields.io/badge/GitHub-D--Majumder-black?logo=github" alt="GitHub Badge">
  </a>
</p>
