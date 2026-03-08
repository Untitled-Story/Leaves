# Repository Guidelines

## Project Structure & Module Organization
- `leaves-api/` contains API patches on top of Paper/Spigot/Bukkit.
- `leaves-server/` contains server implementation patches on top of Paper/CraftBukkit.
- `patches/` holds generated patch files (source of truth for PRs).
- Reference sources may be present but gitignored; it's OK to consult them for comparison and integration.
- `docs/` contains contributor and project documentation.
- `build/` and `build-data/` hold build outputs and generated metadata.
- Tests live under `leaves-api/src/test/java/` and `leaves-server/src/test/java/`.

## Build, Test, and Development Commands
- `./gradlew applyPatches`: materialize patched source trees in `leaves-api/` and `leaves-server/`.
- `./gradlew createMojmapLeavesclipJar`: build the server jar; output goes to `build/libs/`.
- `./gradlew rebuildPatches`: convert your local commits into patch files in `patches/`.
- `./gradlew test`: run the full test suite (JUnit 5).
- `./gradlew :leaves-api:test` or `./gradlew :leaves-server:test`: run module-scoped tests.

JDK 21+ is required; Gradle toolchains can download it automatically if missing.

## Coding Style & Naming Conventions
- Java code uses 4-space indentation and K&R-style braces in existing sources; follow the surrounding style.
- Prefer existing naming patterns and package structure; avoid introducing new top-level packages without discussion.
- No project-wide auto-formatter is enforced; keep changes minimal and consistent with nearby code.

## Testing Guidelines
- Tests are JUnit 5 (Jupiter). Place new tests next to the module they cover.
- Name tests descriptively (e.g., `FeatureBehaviorTest`) and keep fixtures minimal.
- Run module tests locally before `rebuildPatches` when touching that module.

## Commit & Pull Request Guidelines
- Recent commits use short, imperative summaries such as `chore: Update ...`, `fix ...`, or `Update ...`.
- Use `type: summary` for routine changes; `[ci skip]` is used for doc-only updates when appropriate.
- PRs should describe the problem, the patch impact, and testing performed. Link related issues and include reproduction steps when relevant.

## Patch Workflow Notes
- Work inside `leaves-api/` and/or `leaves-server/` after `applyPatches`.
- Your commits become patches via `rebuildPatches`; only commits after the Paper base are treated as Leaves patches.
