# Awesome REA [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of resources for REA (Reverse Engineer Anything), the open-source MCP server and CLI that lets AI coding agents reverse engineer native binaries, Electron and JavaScript apps, .NET assemblies, Android APKs, firmware, network captures, and live app behavior.

REA connects agents such as Claude Code, Codex, Cursor, and Gemini CLI to reverse-engineering tools like Ghidra, Hopper, IDA, JADX, and Frida through the Model Context Protocol (MCP). Analysis runs on your own machine, and every finding comes with the evidence and limitations behind it.

```bash
npx rea-agents@latest setup
```

This list is community-maintained and not affiliated with the REA project. Contributions welcome, see [CONTRIBUTING.md](CONTRIBUTING.md).

> **Legal note.** REA is for lawful research and analysis of software you own or are authorized to examine. Commercial engines (IDA Pro, Hopper, JEB) require your own license.

## Contents

- [Official](#official)
- [Getting Started](#getting-started)
- [Guides](#guides)
- [Showcases and Case Studies](#showcases-and-case-studies)
- [Documentation by Target](#documentation-by-target)
  - [Native Binaries](#native-binaries)
  - [JavaScript, Electron, and Web](#javascript-electron-and-web)
  - [Mobile and Managed Code](#mobile-and-managed-code)
  - [Firmware, Hardware, and Runtime](#firmware-hardware-and-runtime)
- [Integrations and Agent Setup](#integrations-and-agent-setup)
- [Architecture and Internals](#architecture-and-internals)
- [Articles and Tutorials](#articles-and-tutorials)
- [Reviews and Critical Takes](#reviews-and-critical-takes)
- [Community](#community)
- [Translations](#translations)
- [Related Tools](#related-tools)
- [Related Awesome Lists](#related-awesome-lists)

## Official

- [morluto/rea](https://github.com/morluto/rea) - Source repository. MIT licensed, written in TypeScript.
- [rea.tools](https://rea.tools/) - Official website with guides, showcases, blog, and FAQ in 20 languages.
- [rea-agents on npm](https://www.npmjs.com/package/rea-agents) - The published package behind `npx rea-agents` and the `rea` CLI.
- [Releases](https://github.com/morluto/rea/releases) - Versioned release notes.
- [Changelog](https://github.com/morluto/rea/blob/main/CHANGELOG.md) - Full change history.
- [Roadmap](https://github.com/morluto/rea/blob/main/docs/roadmap.md) - Planned work and direction.
- [FAQ](https://rea.tools/faq/) - Common questions, including what data reaches your model provider.

## Getting Started

- [Get started](https://rea.tools/get-started/) - Step-by-step setup for Windows, macOS, and Linux, including the curl installer.
- [Installation docs](https://github.com/morluto/rea/blob/main/docs/installation.md) - Node.js requirements, engine detection, and per-target prerequisites.
- [Your first investigation](https://rea.tools/first-investigation/) - A guided walk through a small Notes app, end to end.
- [Dinosaur speed lab](https://rea.tools/examples/dino-lab/) - Interactive example: find what controls the speed of the Chrome dinosaur game.
- [CLI reference](https://github.com/morluto/rea/blob/main/docs/cli.md) - Every `rea` command, including `rea doctor`, `rea update`, and the analysis subcommands.
- [New to RE with AI? What to reverse engineer first, and how to ask](https://github.com/morluto/rea/discussions/2412) - Community beginner ladder from a program you wrote yourself up to malware in a VM.

## Guides

- [Recover a sound-pan calculation](https://rea.tools/guides/native/) - Native binaries. Inspect instructions, follow a caller, read constants, and check the recovered C.
- [Follow a CSV export](https://rea.tools/guides/javascript/) - JavaScript and Electron. Trace one feature across renderer, preload, IPC, and main process.
- [Observe a click](https://rea.tools/guides/browser/) - Browser behavior. Capture a request and find the code that turns the response into a download.
- [Native investigation](https://github.com/morluto/rea/blob/main/docs/native-investigation.md) - The full native workflow the agent follows.
- [JavaScript application workflows](https://github.com/morluto/rea/blob/main/docs/javascript-application-workflows.md) - Module graphs, artifact reconstruction, and runtime reconciliation.

## Showcases and Case Studies

- [How an authenticator generates a login code](https://rea.tools/showcase/aegis/) - Android APK. Finds the six-digit TOTP calculation in Aegis and explains the 30-second rotation.
- [Solve a CTF flag checker](https://rea.tools/showcase/ctf/) - Native binary. Turns a DownUnderCTF checker into equations and verifies the flag.
- [DX-Ball's sound-pan calculation](https://rea.tools/showcase/dx-ball/) - 1996 Windows game. Recovers a C function that passes 3,205 original x86 test cases.
- [How Notion copies text and HTML](https://rea.tools/showcase/notion/) - Electron. Traces the clipboard bridge from renderer through preload and IPC to the main process.
- [How TH04 aims a ring of bullets](https://rea.tools/showcase/th04/) - PC-98 DOS executable. Matches a 16-bit angle helper to readable C++ and compares against historical compiler output.
- [All showcases](https://rea.tools/showcase/) - Index with evidence pages for each case.

## Documentation by Target

### Native Binaries

- [Ghidra provider](https://github.com/morluto/rea/blob/main/docs/ghidra-provider.md) - Free engine path. Needs a JDK 21 or newer.
- [IDA provider](https://github.com/morluto/rea/blob/main/docs/ida-provider.md) - Using an existing IDA Pro install.
- [Go binaries](https://github.com/morluto/rea/blob/main/docs/go-binaries.md) - Symbol recovery and runtime structures in Go executables.
- [Rust binaries](https://github.com/morluto/rea/blob/main/docs/rust-binaries.md) - Working with Rust mangling and panics.
- [Raw binary](https://github.com/morluto/rea/blob/main/docs/raw-binary.md) - Headerless images and unknown formats.
- [WebAssembly artifacts](https://github.com/morluto/rea/blob/main/docs/wasm-artifacts.md) - Inspecting WebAssembly modules.
- [EVM bytecode](https://github.com/morluto/rea/blob/main/docs/evm-bytecode.md) - Smart contract bytecode analysis.
- [Recorded crashes](https://github.com/morluto/rea/blob/main/docs/recorded-crashes.md) - Reading Linux crash recordings.
- [Binary diagnostics](https://github.com/morluto/rea/blob/main/docs/binary-diagnostics.md) - Offline ELF layout and format checks.
- Ghidra platform notes: [DOS](https://github.com/morluto/rea/blob/main/docs/ghidra-dos.md), [MIPS](https://github.com/morluto/rea/blob/main/docs/ghidra-mips.md), [PowerPC](https://github.com/morluto/rea/blob/main/docs/ghidra-ppc.md), [PSP](https://github.com/morluto/rea/blob/main/docs/ghidra-psp.md), [RISC-V](https://github.com/morluto/rea/blob/main/docs/ghidra-riscv.md), [.NET NativeAOT](https://github.com/morluto/rea/blob/main/docs/ghidra-nativeaot.md), [Windows](https://github.com/morluto/rea/blob/main/docs/windows-ghidra-p0.md).

### JavaScript, Electron, and Web

- [JavaScript application graph](https://github.com/morluto/rea/blob/main/docs/javascript-application-graph.md) - Modules, imports, and Electron boundaries as JSON.
- [JavaScript recovery](https://github.com/morluto/rea/blob/main/docs/javascript-recovery.md) - Deminifying and recovering readable source.
- [JavaScript artifact reconstruction](https://github.com/morluto/rea/blob/main/docs/javascript-artifact-reconstruction.md) - Rebuilding bundles into modules.
- [JavaScript runtime observation](https://github.com/morluto/rea/blob/main/docs/javascript-runtime-observation.md) - Watching code execute in a Chrome-family browser.
- [Electron observation](https://github.com/morluto/rea/blob/main/docs/electron-observation.md) - Attaching to packaged Electron apps.
- [Electron fuses](https://github.com/morluto/rea/blob/main/docs/electron-fuses.md) - What Electron fuses allow and block.
- [Browser observation](https://github.com/morluto/rea/blob/main/docs/browser-observation.md) - Capturing live website behavior.
- [Website module trace](https://github.com/morluto/rea/blob/main/docs/website-module-trace.md) - Following a feature through a site's scripts.
- [Website script export](https://github.com/morluto/rea/blob/main/docs/website-script-export.md) - Pulling scripts out of a live page.
- [Web network captures](https://github.com/morluto/rea/blob/main/docs/web-network-captures.md) - HAR and SAZ files.
- [Packet captures](https://github.com/morluto/rea/blob/main/docs/packet-captures.md) and [PCAP analysis](https://github.com/morluto/rea/blob/main/docs/pcap-analysis.md) - Network-level evidence.

### Mobile and Managed Code

- [Android analysis](https://github.com/morluto/rea/blob/main/docs/android-analysis.md) - APKs via JADX. Needs a JDK.
- [ADB device analysis](https://github.com/morluto/rea/blob/main/docs/adb-device-analysis.md) - Working against a connected Android device.
- [Apktool resource analysis](https://github.com/morluto/rea/blob/main/docs/apktool-resource-analysis.md) - Resources, manifests, and layouts.
- [Apple application analysis](https://github.com/morluto/rea/blob/main/docs/apple-application-analysis.md) - macOS and iOS app bundles.
- [Flutter analysis](https://github.com/morluto/rea/blob/main/docs/flutter-analysis.md) - Dart snapshots in Flutter apps.
- [HarmonyOS analysis](https://github.com/morluto/rea/blob/main/docs/harmony-analysis.md) - HarmonyOS packages.
- [Managed code analysis](https://github.com/morluto/rea/blob/main/docs/managed-code-analysis.md) - .NET assemblies without a native engine.
- [JEB analysis](https://github.com/morluto/rea/blob/main/docs/jeb-analysis.md) - Using existing JEB projects.

### Firmware, Hardware, and Runtime

- [Firmware analysis](https://github.com/morluto/rea/blob/main/docs/firmware-analysis.md) - Embedded images.
- [Signal recordings](https://github.com/morluto/rea/blob/main/docs/signal-recordings.md) - Logic-analyzer captures.
- [Process capture](https://github.com/morluto/rea/blob/main/docs/process-capture.md) - Observing a running process.
- [Frida instrumentation](https://github.com/morluto/rea/blob/main/docs/frida-instrumentation.md) - Dynamic hooks with Frida.
- [SQLite databases](https://github.com/morluto/rea/blob/main/docs/sqlite-databases.md) - Inspecting app data stores.

## Integrations and Agent Setup

- [Client configuration](https://github.com/morluto/rea/blob/main/docs/client-configuration.md) - Manual MCP registration for any agent with local MCP support.
- [Client verification](https://github.com/morluto/rea/blob/main/docs/client-verification.md) - Confirm your agent sees the REA tools.
- [MCP contracts](https://github.com/morluto/rea/blob/main/docs/mcp-contracts.md) - Tool inputs, outputs, and guarantees.
- [MCP prompts](https://github.com/morluto/rea/blob/main/docs/mcp-prompts.md) - Prompt templates REA exposes to agents.
- [morluto/rea on skills.sh](https://www.skills.sh/morluto/rea) - Install the bundled skills with `npx skills add morluto/rea`.
- [REA as a DSH plugin](https://www.dshplugin.store/plugin/morluto/rea) - Plugin store listing.
- [Reverse Engineer Anything skill on TypingMind](https://www.typingmind.com/skills/morluto-reverse-engineer-anything) - Skill packaging for other LLM frontends.
- [A 32K local model drove REA over MCP](https://github.com/morluto/rea/discussions/3098) - Running REA with a small local model, 3 of 3 tasks with 10 tools.

## Architecture and Internals

- [Docs index](https://github.com/morluto/rea/blob/main/docs/index.md) - Entry point to all reference docs.
- [Tool design](https://github.com/morluto/rea/blob/main/docs/tool-design.md) - Principles behind REA's MCP tool surface.
- [Reverse engineering tools](https://github.com/morluto/rea/blob/main/docs/reverse-engineering-tools.md) - Engines REA can drive and how they are detected.
- [Reconstruction readiness](https://github.com/morluto/rea/blob/main/docs/reconstruction-readiness.md), [coverage](https://github.com/morluto/rea/blob/main/docs/reconstruction-coverage.md), and [obligation ledgers](https://github.com/morluto/rea/blob/main/docs/reconstruction-obligation-ledgers.md) - How REA tracks what a reconstruction still owes.
- [Testing](https://github.com/morluto/rea/blob/main/docs/testing.md) - Test layout and how to run the suite.
- [Migration to 6.2](https://github.com/morluto/rea/blob/main/docs/migration-6.2.md) - Breaking changes in the 6.x line.
- [Contributing](https://github.com/morluto/rea/blob/main/CONTRIBUTING.md) - How to contribute to REA itself.
- [Security policy](https://github.com/morluto/rea/blob/main/SECURITY.md) - Reporting vulnerabilities in REA.
- [Does reverse engineering need a bigger model?](https://rea.tools/blog/reverse-engineering-models/) - Official blog, October 2026. Specialized versus general models, with compiler-feedback learning.
- [The industrial revolution in reverse engineering](https://rea.tools/blog/touhou-reconstruction/) - Official blog, October 2026. Reconstructing TH04, TH08, and TH095 with agents and verification.

## Articles and Tutorials

- [Reverse Engineering with AI: Trace Electron and Native Apps](https://www.sitepoint.com/reverse-engineering-with-ai-rea-electron-tracing/) - SitePoint. Install, run `rea doctor`, and trace a feature from UI into native code.
- [REA explained for AI coding agents](https://dev.to/daviddeng/rea-explained-for-ai-coding-agents-5g6j) - DEV Community. Walkthrough with advice to pin versions.
- [REA: Let Your AI Agent Reverse Engineer the App Features You Wish You Had](https://dev.to/arshtechpro/rea-let-your-ai-agent-reverse-engineer-the-app-features-you-wish-you-had-3en7) - DEV Community.
- [REA: Teaching AI Agents to Reverse Engineer Binaries Through MCP](https://starlog.is/articles/ai-agents/morluto-rea) - Starlog. Architecture-focused overview.
- [REA: Reverse Engineer Anything With AI Agents](https://www.kunalganglani.com/blog/rea-reverse-engineer-anything-agents) - Kunal Ganglani. Overview and setup.
- [What is REA (Reverse Engineer Anything)?](https://apidog.com/blog/what-is-rea-reverse-engineer-anything/) - Apidog. Covers the star surge and the FAQ note on what reaches your model provider.
- [REA Reverse Engineer Anything GitHub: Free Quick Start](https://agentos.guide/rea-reverse-engineer-anything-github) - AgentOS guide.
- [How to Reverse Engineer Anything](https://howtorea.com/) - Independent companion handbook, not affiliated with the project.
- [REA v6.4.0 verified on Windows 11 with Claude Code and Codex CLI](https://wikidocs.net/451131) - Korean. Hands-on verification notes.
- [REA 讓 AI Agent 協助拆解軟體運作](https://www.inside.com.tw/article/42615-rea-reverse-engineer-anything-open-source-mcp-ai-agent-github) - Traditional Chinese. INSIDE coverage.
- [REA GitHub Erfolg](https://www.all-ai.de/news/news26top/rea-github-erfolg) - German. all-ai.de coverage.

## Reviews and Critical Takes

- [rea: reverse engineering tools for agents](https://gittested.com/reviews/morluto-rea/) - GitTested. Tested 6.2.0 and found plain shell tools matched it on small programs. Verdict: adopt with care.
- [Reverse Engineer Anything MCP: hands-on](https://www.mindstudio.ai/blog/reverse-engineer-anything-mcp/) - MindStudio. Rebuilt parts of macOS Preview with and without REA and compared.
- [REA: Reverse Engineer Anything](https://www.eigent.ai/blog/rea-reverse-engineer-anything) - Eigent. Argues the tool mostly wires existing RE tools together.
- [Reverse Engineer Anything GitHub repo](https://www.geeky-gadgets.com/reverse-engineer-anything-github-repo/) - Geeky Gadgets. Raises IP and DRM concerns.

## Community

- [Discord](https://discord.gg/GkcryMnJDM) - Official server.
- [@reatools on X](https://x.com/reatools) - Official account.
- [GitHub Discussions](https://github.com/morluto/rea/discussions) - Q&A, show and tell, ideas.
- [Reverse Engineering 101 with REA + Ghidra](https://github.com/morluto/rea/discussions/3791) - Community learning resource.
- [Reverse Engineering toolkit](https://github.com/morluto/rea/discussions/3845) - Community-shared toolkit.
- [Contributors](https://rea.tools/contributors/) - People behind the project.

## Translations

Official README translations in the repo: [简体中文](https://github.com/morluto/rea/blob/main/docs/readme/README_zh.md), [繁體中文](https://github.com/morluto/rea/blob/main/docs/readme/README_zh-TW.md), [日本語](https://github.com/morluto/rea/blob/main/docs/readme/README_ja.md), [한국어](https://github.com/morluto/rea/blob/main/docs/readme/README_ko.md), [Deutsch](https://github.com/morluto/rea/blob/main/docs/readme/README_de.md), [Español](https://github.com/morluto/rea/blob/main/docs/readme/README_es.md), [Français](https://github.com/morluto/rea/blob/main/docs/readme/README_fr.md), [Português (Brasil)](https://github.com/morluto/rea/blob/main/docs/readme/README_pt-BR.md), [Русский](https://github.com/morluto/rea/blob/main/docs/readme/README_ru.md), [Italiano](https://github.com/morluto/rea/blob/main/docs/readme/README_it.md), [Polski](https://github.com/morluto/rea/blob/main/docs/readme/README_pl.md), [Türkçe](https://github.com/morluto/rea/blob/main/docs/readme/README_tr.md), [Українська](https://github.com/morluto/rea/blob/main/docs/readme/README_uk.md), [Tiếng Việt](https://github.com/morluto/rea/blob/main/docs/readme/README_vi.md), [ไทย](https://github.com/morluto/rea/blob/main/docs/readme/README_th.md), [Bahasa Indonesia](https://github.com/morluto/rea/blob/main/docs/readme/README_id.md), [العربية](https://github.com/morluto/rea/blob/main/docs/readme/README_ar.md), [فارسی](https://github.com/morluto/rea/blob/main/docs/readme/README_fa.md), [Ελληνικά](https://github.com/morluto/rea/blob/main/docs/readme/README_el.md).

## Related Tools

Engines and runtimes REA drives or complements.

- [Ghidra](https://github.com/NationalSecurityAgency/ghidra) - Free software reverse engineering suite from the NSA. REA's default native engine.
- [Hopper](https://www.hopperapp.com/) - macOS and Linux disassembler. REA setup can install it with approval.
- [IDA Pro](https://hex-rays.com/ida-pro) - Commercial disassembler and decompiler.
- [JADX](https://github.com/skylot/jadx) - Dex to Java decompiler used for Android targets.
- [Frida](https://github.com/frida/frida) - Dynamic instrumentation toolkit used for runtime hooks.
- [Model Context Protocol](https://modelcontextprotocol.io/) - The protocol REA speaks to agents.

## Related Awesome Lists

- [awesome](https://github.com/sindresorhus/awesome) - The root list.
- [awesome-reversing](https://github.com/tylerha97/awesome-reversing) - General reverse engineering resources.
- [awesome-mcp-servers](https://github.com/punkpeye/awesome-mcp-servers) - Other MCP servers.

