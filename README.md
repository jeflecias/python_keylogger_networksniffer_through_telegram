# Python Keylogger & Network Sniffer via Telegram

A proof-of-concept Python script that simultaneously captures system keystrokes and monitors local network traffic, exfiltrating the logged data to a Telegram bot for real-time monitoring.

## Features

- **Keylogging:** Captures keystrokes globally using `pynput` and buffers them to reduce API calls.
- **Network Sniffing:** Uses `pyshark` to capture and inspect live network packets, identifying TCP/HTTP traffic details.
- **Telegram Exfiltration:** Sends captured data streams directly to a specified Telegram Chat ID using the Telegram Bot API.

## Requirements

- Python 3.x
- `pynput`
- `requests`
- `pyshark`
- [Wireshark](https://www.wireshark.org/) / `tshark` installed on the host system.

## Setup & Usage

1. **Install dependencies:**
   ```bash
   pip install pynput requests pyshark
   ```

2. **Configure Telegram Bot:**
   - Create a new bot using [BotFather](https://core.telegram.org/bots#botfather) on Telegram.
   - Obtain your Bot Token.
   - Obtain your Chat ID.

3. **Configure the Script:**
   - Open `keylogger.py`.
   - Replace `INSERT BOT TOKEN HERE` with your Telegram Bot Token.
   - Replace `INSERT CHAT ID HERE` with your Telegram Chat ID.
   - Ensure the `interface` variable in `pyshark.LiveCapture(interface='Wi-Fi')` matches your system's active network interface (e.g., `'eth0'`, `'wlan0'`, or `'Ethernet'`).

4. **Run the Script:**
   ```bash
   python keylogger.py
   ```

## Known Limitations

- **Network Sniffer API Rate Limits:** The script currently sends a Telegram message for *every* captured packet matching the criteria. This will quickly exceed Telegram's rate limits (HTTP 429). In a real-world scenario, network logs must be heavily buffered or filtered to specific, low-volume events.
- **Synchronous I/O:** The use of `requests.post` inside the packet processing loop blocks execution, which may lead to dropped network packets during capture.

## ⚠️ Legal & Ethical Disclaimer

**For Educational and Authorized Testing Purposes Only.**

This tool is provided strictly for educational purposes, security research, and authorized network monitoring. 
- **Do not** use this script on any system, network, or device that you do not own or have explicit, written permission to monitor.
- Unauthorized interception of network traffic or logging keystrokes without user consent is illegal in most jurisdictions.
- The author and contributors assume no liability and are not responsible for any misuse, damage, or legal consequences caused by this software. Use responsibly.
