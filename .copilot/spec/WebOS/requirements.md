# Linux Web VM - Requirements Specification

This document captures the functional and non-functional requirements for the Linux Web VM project using the EARS (Easy Approach to Requirements Syntax) notation.

## 1. Document Overview
A browser-native virtual machine platform capable of booting x86_64 Linux ISOs with full hardware emulation, persistent storage, and secure virtualized networking via an authenticated Go proxy.

## 2. Functional Requirements

### 2.1 Virtual Machine Core (x86_64)
- **REQ-CORE-001 (Ubiquitous):** The system shall emulate a full x86_64 CPU architecture using the qemu-wasm engine.
- **REQ-CORE-002 (Event-Driven):** When a user selects a Linux ISO, the system shall mount the image as a virtual CD-ROM device.
- **REQ-CORE-003 (State-Driven):** While the guest OS is playing sound, the system shall stream audio buffers via an AudioWorklet.

### 2.2 Distro Presets & Community Sharing (TOML)
- **REQ-OPT-001 (Ubiquitous):** The system shall store optimization presets for common distributions in TOML format (e.g., arch.vm.toml).
- **REQ-OPT-002 (Event-Driven):** When a user imports a "Community Preset," the system shall display a Material 3 "High-Emphasis Warning" regarding the security risks of third-party configurations.
- **REQ-OPT-003 (Event-Driven):** The system shall allow users to export their custom TOML configurations for community sharing.

### 2.3 Networking & Proxy Security (Go)
- **REQ-NET-001 (Ubiquitous):** The system shall provide a standalone, downloadable Go-based proxy server for host networking.
- **REQ-NET-002 (Event-Driven):** When the browser connects to the Go proxy, it must provide a Shared Secret Token; otherwise, the proxy shall reject the connection.

### 2.4 Persistence & Snapshots
- **REQ-STO-001 (State-Driven):** While the browser tab is closing, the system shall automatically generate a "Resume Snapshot" in the dedicated auto slot.
- **REQ-STO-002 (Event-Driven):** When a user triggers "Export Snapshot," the system shall package the state and disk metadata into a portable .vmsnap file.

## 3. User Stories

### 3.1 The "Custom Experience" User
**Story:** As a power user, I want to import a community-made 'Gentoo-Optimized' preset so I don't have to manually tune CPU flags.

**Acceptance Criteria:**
- System displays a prominent safety warning before applying the preset.
- Invalid TOML syntax is caught and reported to the user.

### 3.2 The "Secure Admin"
**Story:** As a sysadmin, I want my proxy to require a token so my local network isn't exposed to other websites.

**Acceptance Criteria:**
- Proxy requires an `X-VM-Token` header for all WebSocket upgrades.

## 4. Non-Functional Requirements
- **Security:** Community presets must be sanitized to prevent injection of malicious emulator arguments.
- **Usability:** The Material 3 Expressive UI must maintain a clear distinction between "Official" and "Community" content.