<div align="center">

# MIDIBridge

**Stream MIDI signals to any device over the Internet in real time**

[![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20macOS%20%7C%20Linux-blue?style=for-the-badge)](https://github.com/MarchSnow-1/midibridge)
[![Golang](https://img.shields.io/badge/Golang-1.26%2B-green?style=for-the-badge)](https://go.dev)
[![GitHub Repo stars](https://img.shields.io/github/stars/MarchSnow-1/midibridge?style=for-the-badge)](https://github.com/MarchSnow-1/midibridge)
[![License](https://img.shields.io/badge/License-MIT-orange?style=for-the-badge)](LICENSE)

[**English**](README.md) | [**简体中文**](README_zh-CN.md)

</div>

---

## Overview

MIDIBridge is a lightweight, open-source toolset that streams MIDI signals to any machine over the Internet in real time.

No extra hardware. No distance limit. Just plug in and play.

```
MIDI Keyboard ──USB──▶ Server ──WebSocket──▶ Client ──Virtual MIDI──▶ DAW / Other Software
```

## Repositories

| Component | Repo | Description |
|-----------|------|-------------|
| **Server** | [midibridge-server](https://github.com/MarchSnow-1/midibridge-server) | Reads USB MIDI input and broadcasts over WebSocket |
| **Client** | [midibridge-client](https://github.com/MarchSnow-1/midibridge-client) | Receives signals and injects them into a virtual MIDI port for use by DAWs |

## Features

| Feature | Description |
|---------|-------------|
| 🔌 Zero-config pairing | Set password once — client auto-connects |
| 👥 Multi-client | One server broadcasts to multiple clients simultaneously |
| 🔄 Hot-plug recovery | Unplug and replug the keyboard anytime — server auto-detects |
| 🎯 Device targeting | Configure target MIDI device name — auto-retries until ready |
| 🔒 Password-protected | bcrypt-hashed storage with remote online update |
| ♻️ Auto-reconnect | Exponential backoff with random jitter to avoid connection storms |

## Quick Start

### Server

Download the binary for your platform from [MIDIBridge-Server Releases](https://github.com/MarchSnow-1/midibridge-server/releases), extract and run

> Change the default password via the HTTP API after first launch.<br>
> See the server repository README.md for detailed instructions.

### Client

Download the binary for your platform from [MIDIBridge-Client Releases](https://github.com/MarchSnow-1/midibridge-client/releases), extract and run:

```bash
./midibridge-client
```

> Edit `data/config.json` with your server IP and password before starting.

> [!IMPORTANT]
> **Windows users**: Due to driver limitations, install [loopMIDI](https://www.tobias-erichsen.de/software/loopmidi.html) first and create a virtual port with the same name as `virtualPortName` in your config file — otherwise the client cannot inject MIDI signals.

## License

[MIT](LICENSE) — Use, modify, and distribute freely.
