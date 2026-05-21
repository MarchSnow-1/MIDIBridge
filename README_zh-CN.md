<div align="center">

# MIDIBridge

**通过网络将 MIDI 信号实时传输到任意设备**

[![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20macOS%20%7C%20Linux-blue?style=for-the-badge)](https://github.com/MarchSnow-1/midibridge)
[![Golang](https://img.shields.io/badge/Golang-1.26%2B-green?style=for-the-badge)](https://go.dev)
[![GitHub Repo stars](https://img.shields.io/github/stars/MarchSnow-1/midibridge?style=for-the-badge)](https://github.com/MarchSnow-1/midibridge)
[![License](https://img.shields.io/badge/License-MIT-orange?style=for-the-badge)](LICENSE)

[**English**](README.md) | [**简体中文**](README_zh-CN.md)

</div>

---

## 简介

MIDIBridge 是一套轻量开源工具，可将 MIDI 信号通过互联网实时传输到任意机器

无需额外硬件，不限物理距离，即插即用

```
MIDI 键盘 ──USB──▶ 服务端 ──WebSocket──▶ 客户端 ──虚拟 MIDI──▶ DAW / 其他软件
```

## 仓库结构

| 组件 | 仓库 | 说明 |
|------|------|------|
| **服务端** | [midibridge-server](https://github.com/MarchSnow-1/midibridge-server) | 读取 USB MIDI 输入并通过 WebSocket 广播 |
| **客户端** | [midibridge-client](https://github.com/MarchSnow-1/midibridge-client) | 接收信号并注入虚拟 MIDI 端口供 DAW 使用 |

## 功能特性

| 特性 | 说明 |
|------|------|
| 🔌 零配置配对 | 设一次密码，客户端自动连接 |
| 👥 多客户端 | 一个服务端同时广播到多台客户端 |
| 🔄 热插拔恢复 | 随时插拔键盘，服务端自动重新识别 |
| 🎯 指定设备 | 配置目标 MIDI 设备名称，未就绪时自动重试 |
| 🔒 密码保护 | bcrypt 哈希存储，支持远程在线修改 |
| ♻️ 断线重连 | 指数退避 + 随机抖动，防止同时重连冲击服务端 |

## 快速开始

### 服务端

从 [MIDIBridge-Server Releases](https://github.com/MarchSnow-1/midibridge-server/releases) 下载对应平台的二进制，解压后直接运行

> 首次启动后，通过 HTTP API 修改默认密码<br>
> 具体操作方式请参考服务端仓库 README.md

### 客户端

从 [MIDIBridge-Client Releases](https://github.com/MarchSnow-1/midibridge-client/releases) 下载对应平台的二进制，解压后直接运行：

```bash
./midibridge-client
```

> 启动前编辑 `data/config.json`，填入服务端 IP 与密码

> [!IMPORTANT]
> **Windows 用户注意**：由于底层驱动限制，需先安装 [loopMIDI](https://www.tobias-erichsen.de/software/loopmidi.html) 并在其中创建一个与配置文件中 `virtualPortName` 同名的虚拟端口，客户端才能正常注入 MIDI 信号

## 许可证

[MIT](LICENSE) — 自由使用、修改、分发