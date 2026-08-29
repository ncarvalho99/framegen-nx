# FrameGen NX

FrameGen NX is an experimental research project exploring system-level frame generation on the Nintendo Switch. The long-term goal is a single Ultrahand toggle that can enable frame interpolation for compatible games and emulators without requiring native engine support.

> [!WARNING]
> This project is in early development. There is no usable release yet, compatibility has not been established, and nothing here should currently be installed on a console.

## Intended design

FrameGen NX is planned as a system-wide framework with separate graphics adapters:

- **Vulkan/NVK adapter:** the first implementation target for compatible emulators and homebrew.
- **NVN/VI research adapter:** an experimental path for retail Switch titles. Universal compatibility is not proven.
- **Frame-generation backend:** color-frame interpolation with duplicate-frame detection, frame pacing, and automatic bypass when the GPU cannot meet its deadline.
- **Ultrahand control plane:** global toggle, per-title profiles, status, and recovery controls.

The initial performance target is **2x generation from 30 FPS to 60 FPS at 720p**. Generated frames improve visual motion but do not increase game simulation speed or input sampling rate.

## Current status

The project is currently in the architecture and prototype-bootstrap phase:

- Technical feasibility and reference implementations have been studied.
- Vulkan integration is considered the first practical milestone.
- Retail NVN interception remains experimental and must be validated capture-first.
- Tegra X1 GPU time, memory bandwidth, latency, thermals, and artifact quality still require measurement on hardware.
- No claim of support for every game is being made.

Internal architecture and validation notes are maintained locally during development and are intentionally excluded from the public repository.

## Lossless Scaling assets

This repository does **not** contain or distribute Lossless Scaling, `Lossless.dll`, extracted shaders, models, Steam files, or other proprietary assets.

An optional research backend may follow the user-supplied-file mechanism demonstrated by NetherSX2_nx and lsfg-vk. If developed, users would have to obtain Lossless Scaling legally and provide their own supported DLL. Any extraction would occur locally on the user's device. This approach remains subject to technical validation and legal review; supplying your own DLL does not itself grant redistribution or reverse-engineering rights.

An independently developed interpolation backend remains the preferred distributable path.

## Planned milestones

1. Bootstrap the build, test, and hardware-measurement infrastructure.
2. Implement an owned interpolation backend with replayable test vectors.
3. Prove 2x frame generation in a controlled Switch Vulkan sample.
4. Integrate and benchmark the Vulkan/NVK adapter without reducing real game FPS.
5. Build a fail-open, capture-only NVN probe across representative titles.
6. Attempt generated NVN presentation only after capture and fence ownership are proven safe.
7. Add the Ultrahand package, per-title profiles, watchdog, and instant safe-mode disable.

## Safety and compatibility

Frame generation competes with games for the Tegra X1 GPU. The implementation must automatically fall back to real frames when timing, temperature, memory pressure, synchronization, or compatibility checks fail. Per-title profiles and a denylist will remain necessary even if broad NVN support becomes possible.

This project is not affiliated with Nintendo, NVIDIA, Valve, or the developer of Lossless Scaling. It is intended for lawful homebrew research on user-owned hardware and software.

## Building and contributing

Build instructions and contribution requirements will be added with the first runnable prototype. Until then, the repository should be treated as pre-alpha research rather than end-user software.
