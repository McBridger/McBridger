# 🌉 McBridger Ecosystem

**Native continuity between macOS and Android.**
*Secure, local, and open-source.*

If you own a Mac and an Android device, you live in two disconnected worlds. The universal clipboard and seamless continuity features standard to the Apple ecosystem simply don't exist for you.

**McBridger fills this void.** It bridges the gap between incompatible platforms, creating a unified workspace where your devices communicate directly — natively and securely.

---

### ⚡️ The McBridger Advantage

While most cross-platform tools are sluggish web-wrappers or require constant internet access, McBridger stands out as a purpose-built, native solution:

*   **Truly Native Performance:**
    *   **macOS:** Built with Swift (SwiftUI + CoreBluetooth) for a lightweight footprint that lives in your Menu Bar.
    *   **Android:** Powered by React Native and Kotlin JSI for instant responsiveness.
*   **Direct & Local:** Uses Bluetooth Low Energy (BLE) for peer-to-peer connection. No cloud dependency — your data transfers directly between devices, even offline.
*   **Bidirectional Sync:** Copy text on your Mac and paste it on your Android — or vice versa. It works instantly, both ways.

### 🔒 Privacy & Security

We believe your data belongs to you. McBridger is architected to exclude third parties entirely.

*   **No Accounts Required:** Currently, authentication relies on a **6-word mnemonic phrase**. This allows devices to discover each other securely without a central server or registration.
*   **End-to-End Encryption:** All traffic is strictly encrypted with **AES-GCM**.
*   **Replay Protection:** Timestamp verification prevents session hijacking.

> *Note: We plan to introduce optional user accounts for identity management in the future, but the mnemonic-based "Direct Mode" will remain as a privacy-first standard.*

### 🚀 Roadmap

We are rolling out features incrementally. The current focus is on stability and clipboard sync, followed by:

1.  **File & Folder Exchange:** Enabling the seamless transfer of files and directories between connected devices.
2.  **Platform Expansion:** Bringing native support to Windows, Linux, and iOS to close the loop.
3.  **Mesh Networking (Long-term Goal):** Implementing multi-hop relay capabilities (e.g., Mac <-> Tablet <-> Phone) to extend range and connectivity resilience.

### 📂 Repository Structure

This repository acts as the central hub and documentation for the ecosystem.

*   **[McBridger for Mac](https://github.com/McBridger/mac)** – Source code for the macOS client.
*   **[McBridger Mobile](https://github.com/McBridger/mobile)** – Source code for the Android client.
*   **`@McBridger/`** – (Root) Releases, documentation, and coordination.

### 🛠 Tech Stack

Designed for minimal latency and maximum reliability:
*   **macOS:** SwiftUI, Combine, CoreBluetooth.
*   **Android:** React Native, Kotlin (Native Modules/JSI), Zustand.
*   **Protocol:** Custom BLE sync layer with robust error handling.

---
**[Security Protocol Deep-Dive](https://github.com/McBridger/mobile/blob/main/ENCRYPTION.md)**
