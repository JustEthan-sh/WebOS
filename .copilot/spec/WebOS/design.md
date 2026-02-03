# Linux Web VM - Technical Design Document

## 1. System Architecture

### 1.1 Networking & Token-Based Security
The Go Proxy requires a shared secret to prevent Cross-Site WebSocket Hijacking (CSWSH).

- **Handshake:** The Proxy generates a 32-character token on startup. The user copies this into the Web VM settings.
- **Header Validation:** The browser client sends `Sec-WebSocket-Protocol: vmt-token-<token>`.
- **Traffic:** Raw Ethernet frames are encapsulated in binary WebSocket messages.

### 1.2 Distro Presets (TOML Engine)
We use a TOML configuration engine to map OS-specific needs to QEMU hardware targets.

```toml
# example: arch.vm.toml
[metadata]
name = "Arch Linux (Official)"
author = "Project Team"
is_official = true

[cpu]
model = "max"
cores = 2
flags = ["+ssse3", "+sse4.1", "+sse4.2"]

[display]
resolution = "1280x720"
driver = "virtio-vga"
```

### 1.3 Community Preset Sandboxing
- **Warning System:** Any TOML file where `metadata.is_official` is false triggers an M3 AlertDialog with a "Use at your own risk" message.
- **Argument Sanitization:** The VM Controller parses the TOML and only allows a strict whitelist of keys to be converted into QEMU arguments, preventing shell injection or unauthorized file access.

## 2. Implementation Logic

### 2.1 The Auto-Snapshot Lifecycle
- **Trigger:** `window.onbeforeunload`
- **Flow:** Stop VM -> Generate Migration Stream -> Write to OPFS (`/snapshots/auto.bin`) -> Close Tab.
- **Resume:** On app load, SvelteKit checks for `auto.bin` presence.

### 2.2 UI (Material 3 Expressive)
- **Theming:** Dynamic color palettes via `@material/material-color-utilities`.
- **Motion:** Emphasized easing for "Heavy" actions (Snapshotting, Booting).

## 3. Data Strategy
- **OPFS:** Primary storage for ISOs and Virtual Disks via `SyncAccessHandle`.
- **IndexedDB:** Metadata for presets, history, and snapshot descriptions.
- **Web Audio:** AudioWorklet for real-time PCM processing from the virtual AC97 device.