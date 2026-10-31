MIFAOGAMES — Stage 3 / native prototype (NOT A FINISHED BACKGROUND GAME SERVER)

New source files: android_native_reference/MifaServerCore.kt,
MifaServerService.kt, AndroidManifest.fragment.xml.

Implemented in source:
- independent UDP/JSON loop on port 7778, no dependency on Godot's frame loop;
- player registration with stable UUID + secret token, reconnect via UUID/token;
- online counter from authenticated heartbeats (30s timeout);
- persisted player records including HP, armor, inventory, position, and world JSON;
- save every 60s, stop and restart saves;
- notification buttons invoke real service commands.

NOT implemented:
- Godot ENet/RPC protocol compatibility: existing WiFiLobby clients use ENet port 24567
  and cannot connect to this native UDP/JSON prototype on port 7778;
- authoritative movement, inventory, damage, shots, loot, mutant simulation;
- actual migration from Net.gd / battle.gd to this server;
- complete Android Gradle plugin / APK build, lifecycle bridge, notification permission;
- real device testing under screen-off/Doze and OEM battery management;
- safe concurrent multi-threaded server state / crash-safe durable fsync;
- secure production authentication (tokens should be protected and rate-limited).

To make this a production server, either embed a compatible Godot headless engine in a
separate Android process/service (substantial native work) or migrate BOTH clients and
server to a newly designed protocol with validated authoritative commands.

The manifest is a FRAGMENT, not a standalone valid AndroidManifest.xml.
Foreground service types and permissions require Android version-specific review.
Android may still stop background processes under resource/battery constraints.

No claim of working APK, successful build, or physical-device testing is made.
