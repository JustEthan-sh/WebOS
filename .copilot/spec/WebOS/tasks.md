# Linux Web VM - Implementation Roadmap

## Phase 1: Engine & Secure Proxy (Weeks 1-5)
- [ ] TSK-101: Build qemu-wasm with libslirp and SharedArrayBuffer.
- [ ] TSK-102: Develop the Go Proxy with Token-based auth middleware.
- [ ] TSK-103: Implement the binary WebSocket client with secret-header support.
- [ ] TSK-104: Build the AudioWorklet for low-latency sound.

## Phase 2: M3 UI & Config Engine (Weeks 6-10)
- [ ] TSK-201: Scaffold SvelteKit with material-web components.
- [ ] TSK-202: Implement the TOML Parser and configuration mapper.
- [ ] TSK-203: Build the "Preset Library" UI (Official vs. Community tabs).
- [ ] TSK-204: Implement the "Security Warning" dialog for community presets.

## Phase 3: Lifecycle & Persistence (Weeks 11-16)
- [ ] TSK-301: Implement beforeunload auto-snapshot logic.
- [ ] TSK-302: Develop the Snapshot Import/Export utility (.vmsnap).
- [ ] TSK-303: Implement navigator.storage.persist() and quota UI.

## Phase 4: Optimization & Distros (Weeks 17-22)
- [ ] TSK-401: Implement OPFS SyncAccessHandle for virtual disk I/O.
- [ ] TSK-402: Create and test TOML presets for Arch, Ubuntu, and Zorin.
- [ ] TSK-403: Implement "Memory Ballooning" logic in the VM Controller.

## Phase 5: Testing & Release (Weeks 23-26)
- [ ] TSK-501: Benchmarking networking speed through the authenticated Proxy.
- [ ] TSK-502: Final UI polish for "Expressive" motion transitions.
- [ ] TSK-503: Release Go Proxy binaries for all platforms.