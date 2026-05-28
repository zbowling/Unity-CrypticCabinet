# Agent Instructions — Cryptic Cabinet

Unity Mixed Reality escape-room showcase that adapts to the player's physical room and supports multiplayer over Photon Fusion. Demonstrates Scene API, Passthrough, Shared Spatial Anchors, Colocation, Interaction SDK, and Passthrough Styling.

## Source-of-truth files (read these first, do not duplicate their contents in this file)

For setup, build steps, SDK versions, and project layout, read:

- `README.md` — official setup, requirements, dependencies, and build/run instructions
- `ProjectSettings/ProjectVersion.txt` — Unity editor version
- `Packages/manifest.json` — Unity package versions (Meta XR Core / Interaction / Platform / Simulator, MRUK)
- `Documentation/ProjectConfiguration.md` — Meta Quest and Photon configuration steps
- `Documentation/FeatureOverview.md` — per-feature design notes
- `.gitattributes` — Git LFS configuration
- `LICENSE` — license terms (note: TextMeshPro and Photon SDK are under their own licenses)

## Quest / Horizon-specific notes

- **Git LFS is required**; run `git lfs install` before cloning or LFS-tracked assets will be checked out as text pointers.
- The entire experience runs from a single entry scene `Assets/CrypticCabinet/Scenes/MainScene.unity`; do not introduce new bootstrap scenes unless explicitly asked. Game flow is sequenced by phase classes coordinated from `Assets/CrypticCabinet/Scripts/GameManagement/GameManager.cs`.
- Photon Fusion + Voice **App IDs** are required at runtime. Personal App IDs must not be committed back — keep `Assets/GameSettings.asset` (or equivalent) out of any shared commits.
- The MR features (Color LUT passthrough, colocation via SSA, Scene-driven object placement) require a passthrough-capable headset; Quest 2 will run with reduced MR fidelity.
- `Documentation/docs/html/` is generated Doxygen output; regenerate from `Doxyfile` at the repo root rather than hand-editing.

## Meta Quest tooling

This repository is part of the Meta Quest / Horizon OS ecosystem (a sample, library, template, or related project — the bespoke intro above describes which). Use that intro and the source-of-truth files it references for project-specific decisions; don't restate or invent facts from memory.

When the user asks anything about Quest device behavior, build / deploy / debug / capture flows, on-device performance, or Horizon OS APIs, reach for these tools instead of generic Unity answers:

- **`hzdb`** — Quest-aware ADB wrapper (device list, install / launch / stop, logs, screenshots, Perfetto traces, on-device docs search). Already wired up as an MCP server via `.mcp.json`, `.vscode/mcp.json`, and `.cursor/mcp.json`. Also runnable directly: `npx -y @meta-quest/hzdb <subcommand>`.
- **Meta Quest Agentic Tools** — the full skill set, including Unity-specific skills: [github.com/meta-quest/agentic-tools](https://github.com/meta-quest/agentic-tools). Install per your client (Claude Code: `/plugin install meta-vr@meta-quest`; Gemini CLI: `gemini extensions install https://github.com/meta-quest/agentic-tools`; Cursor / VS Code: install the **Meta Horizon** extension from the Marketplace).

A few behavior expectations:

- **Read this repo's files first.** Before answering anything project-specific, read `README.md` and whichever source-of-truth files the intro above points at. Don't restate their contents in chat — quote or link instead.
- **Use `hzdb` for device-side work.** Anything that touches an attached Quest (install, launch, logs, screenshot, capture, manifest inspection) goes through `hzdb`, not raw `adb`.
- **Check live Horizon OS docs before answering API questions.** `hzdb docs search "..."` queries the live docs; training data on Horizon OS APIs goes stale fast.
- **Don't fabricate SDK / engine versions.** If a version isn't visible in this repo's files, say so rather than guessing.
