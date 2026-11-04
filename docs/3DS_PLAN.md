# 3DS Plan: Console UI Bloat Remover

Target platform: **Nintendo 3DS family on Luma3DS (Boot9Strap CFW)**.
See `VERIFICATION.md` for which claims below are confirmed and which are still open.

## Why 3DS
- Firmware is frozen (final 11.17), so byte-pattern patches target one known version per model and region.
- Server side is dead (eShop purchases ended Mar 2023, online play Apr 2024, Miiverse Nov 2017), so the bloat is plainly bloat and ban risk is low.
- Luma3DS can patch system applets (including HOME Menu) at load time from the SD card, with no NAND writes.

## Architecture: patch-pack manager
1. **Manager app (.3dsx)**: UI follows the README mockup. Detects model, region and firmware, picks applicable patches, writes the Luma tree to the SD card.
2. **Patch definitions (data files)**: target title ID, file or code region, byte signature, replacement, supported firmware and regions, expected hash of the original, risk level. No hardcoded offsets.
3. **Revert manifest**: every created file is logged; "Revert All" deletes exactly those files.
4. **Originals**: do not ship Nintendo assets. Ship diffs and signatures only; users supply their own dumps (GodMode9 script, or in-app if filesystem access allows).
5. **Optional sysmodule (later)**: only for dynamic behavior static patches cannot do (e.g. filtering the title list HOME Menu sees). Experimental tier.

Output locations (confirmed from Luma source): `/luma/titles/<TID>/code.ips|.bps|.ups`, `/luma/titles/<TID>/romfs/`, and `/luma/sysmodules/<TID>.ips` for sysmodules.

## Phases
1. **Research**: dump HOME Menu, software keyboard, `act`, `nim`, `news`; map where each bloat item lives. Exit: feature / module / patch-method table.
2. **Dev setup and safety**: NAND backup via GodMode9, manifest and revert engine, signature matcher. Exit: a no-op patch applies and reverts cleanly.
3. **Prototype**: hide the eShop tile on one model and region. Exit: works on real hardware and reverts.
4. **Feature expansion**: social features, account prompts, notifications, update nags, language filter.
5. **Coverage**: other models and regions, UI polish.
6. **Release**: docs, install/uninstall instructions, compatibility matrix.

## Technical challenges
**UI removal**
- Icons come from the installed title list; options are layout edits, code patches, or list filtering. Uninstalling titles is a NAND change and is avoided.
- HOME Menu layouts (BCLYT/BCLIM) are fragile; hiding a tile can break grid spacing or navigation.
- Per-model and per-region module bytes differ; every patch needs per-variant signatures and hash checks.
- Account/sign-in prompts likely originate in several places (`act`, settings, applets).

**Language filter**
- Likely several call sites: software keyboard profanity flag/word list, Mii name validation, friend/profile text (to be confirmed in Phase 1).
- Prefer making the check always pass over emptying the word list.
- Game-level filters are out of scope.
- Moderate mode idea: allow words in local-only fields, keep the filter on anything shared.

## References
3dbrew.org, Luma3DS (source and wiki), GodMode9, devkitPro (devkitARM, libctru, citro2d), CTRPluginFramework, Anemone3DS and the theme scene, Pretendo Network (consider a compatibility mode), Nintendo Homebrew Discord, GBAtemp, 3ds.hacks.guide.

## Config
`/3ds/bloat-remover/config.toml`: one boolean per feature plus `filter_mode = "off" | "moderate" | "aggressive"`. Each toggle shows "supported on your model and firmware" before it can be applied. Dry run before apply. Pretendo-compatible mode leaves online features alone.

## Risks
- **Bricking**: low if no NAND is touched. A bad system-module patch can bootloop, so the SD-card revert path is essential. Take a NAND backup first.
- **Instability**: wrong-byte matches can crash applets; hash checks and per-variant signatures mitigate.
- **Bans**: mostly moot with Nintendo servers off; relevant only with revival services such as Pretendo.
- **Legal**: do not distribute Nintendo files; distribute diffs and signatures. Not legal advice.
- **Scope creep**: dynamic service filtering stays out of the first release.
