MIFAOGAMES Stage 6 — server core integration groundwork

Added server-owned movement integration (fixed 20Hz), armor-first damage, item add/consume with validation, UUID-based state snapshots on disconnect and every 60 seconds.

IMPORTANT: Existing battle.gd and net.gd RPC actions are NOT yet routed into these methods. Existing client protocol remains untouched. Identity authentication is NOT wired into the Join RPC. Therefore this is NOT a finished authoritative multiplayer server.

Android Kotlin UDP/JSON prototype remains incompatible with Godot ENet. No Foreground Service is built into APK, and no background-screen-off testing was performed.

To finish: add client auth RPC and secure persistent token storage, refactor battle actions to authoritative server commands, embed a compatible Godot headless runtime or implement the complete Godot ENet protocol in native server, package service in Android Gradle build and test on hardware.
