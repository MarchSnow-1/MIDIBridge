<div align="center">

# MIDIBridge

**Stream MIDI signals to any device over the Internet in real time**

[![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20macOS%2013%2B%20%7C%20Linux%20%7C%20Android-blue?style=for-the-badge)](https://github.com/MarchSnow-1/midibridge)
[![Golang](https://img.shields.io/badge/Golang-1.27.3%2B-green?style=for-the-badge)](https://go.dev)
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
| **Android** | [midibridge-android](https://github.com/MarchSnow-1/midibridge-android) | Run MIDIBridge Server on your Android device |

## Features

| Feature | Description |
|---------|-------------|
| 🔌 Zero-config pairing | Set password once — client auto-connects |
| 👥 Multi-client | One server broadcasts to multiple clients simultaneously |
| 🔄 Hot-plug recovery | Unplug and replug the keyboard anytime — server auto-detects |
| 🎯 Device targeting | Configure target MIDI device name — auto-retries until ready |
| 🔒 Password-protected | bcrypt-hashed storage with remote online update |
| ♻️ Auto-reconnect | Exponential backoff with random jitter to avoid connection storms |
| 🔗 External integration | Local programs can read the live MIDI stream directly over TCP — no virtual MIDI port required |

## Quick Start

### Server

Download the binary for your platform from [MIDIBridge-Server Releases](https://github.com/MarchSnow-1/midibridge-server/releases), extract and run

> Change the default password via the HTTP API after first launch.<br>
> See the server repository README.md for detailed instructions.

### Android

Run MIDIBridge Server on your Android device

Download the APK from [MIDIBridge-Android Releases](https://github.com/MarchSnow-1/midibridge-android/releases) and install it on your phone.

> See [MIDIBridge-Android README](https://github.com/MarchSnow-1/midibridge-android) for details.

### Client

Download the binary for your platform from [MIDIBridge-Client Releases](https://github.com/MarchSnow-1/midibridge-client/releases), extract and run:

```bash
./midibridge-client
```

> Edit `data/config.json` with your server IP and password before starting.

> [!IMPORTANT]
> **Windows users**: Due to driver limitations, install [loopMIDI](https://www.tobias-erichsen.de/software/loopmidi.html) first and create a virtual port with the same name as `virtualPortName` in your config file — otherwise the client cannot inject MIDI signals.

#### External integration (optional)

Besides injecting into a virtual MIDI port, the client can also publish the same MIDI stream over a local TCP loopback socket, so other programs on the same machine can read it directly

```bash
./midibridge-client -ipc-listen 127.0.0.1:9003
```

This is **off by default** and does not change the normal virtual-MIDI-port workflow. The interface is read-only and unauthenticated, so it is intended for programs running on the same machine.

See `docs/PROTOCOL.md` in the client repository for the protocol specification and copy-paste-ready examples.

## License

[MIT](LICENSE) — Use, modify, and distribute freely.
