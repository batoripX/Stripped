# Stripped

Stripped Also known as Stripped 1 is a lightweight, zero-dependency, 64-bit native game engine built from first principles using modern C++20. Designed exclusively for developers, advanced modders, and power users, the framework rejects third-party middleware and runtime web abstractions in favor of a monolithic, data-oriented architecture compiled via LLVM-MinGW and `libc++`.

## Technical Architecture & Design Constraints

* **Monolithic Compilation & Security:** Statically links all engine modules into a single executable. Fully optimized using Link-Time Optimization (`-flto`), which flattens the execution layout and strips all binary symbol tables. This layout creates an un-patchable assembly footprint that natively neutralizes conventional memory-scanning and binary-patching cheat tools.
* **Zero-Dependency Pipeline:** Relies strictly on the C++ Standard Library (`std::` and STL). Implements Slang for high-performance shader compilation directly to SPIR-V, driving a clean Vulkan 1.4 compute and rendering pipeline.
* **Dynamic Virtual Memory Management:** Completely eliminates hardcoded structural layouts, array sizes, and static offsets. Memory spaces are mapped dynamically at runtime using Win32 kernel virtual allocation (`MapViewOfFile`), preventing automated tools from anchoring onto fixed memory addresses.
* **Symmetric Interface Sandboxing:** Modding logic runs directly within the main engine execution loop for $0\text{ms}$ latency, utilizing pure abstract C-style interfaces (Vtables) to blind external code to internal data structures. Every transaction is authenticated via a high-entropy runtime session token (Magic Cookie) to instantly drop unauthorized or anonymous function hooks.
* **Hardware Exhaustion Handling:** Features a deterministic eviction pipeline for runtime assets to optimize physical VRAM boundaries. If memory allocation hits definitive physical hardware limits, the engine executes a graceful, controlled shutdown and writes detailed system architecture failure diagnostics directly to disk.

## Licensing & Distribution
Stripped is fully open-source software distributed under the **GNU GPL v3** license. The project enforces complete transparency of source code while legally shielding the engine from proprietary or closed-source rebranding.
