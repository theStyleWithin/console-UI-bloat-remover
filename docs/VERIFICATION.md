# Verification Log

Checked 2026-11-04 against the Luma3DS README and `sysmodules/loader/source/patcher.c` (master).

## Confirmed
| Claim | Evidence |
|---|---|
| Luma applies code patches (IPS, BPS, UPS) from `/luma/titles/<TID>/` | `patcher.c` `applyCodeIpsPatch`, `patcherApplyCodeBpsPatch`, `applyCodeUpsPatch` |
| Code patches and LayeredFS apply to **applets**, not only games (applet = title ID prefix `0x00040030`) | `patchCode()`: `if(isApp \|\| isApplet)` calls `patchLayeredFs` |
| HOME Menu is a patchable applet. Title IDs: USA `0004003000008F02`, JPN `0004003000008202`, EUR `0004003000009802`, KOR `000400300000A902`, CHN `000400300000A102`, TWN `000400300000B102` | `patchCode()` `isHomeMenu` |
| Sysmodule patches load from `/luma/sysmodules/<TID>.ips`, gated by the "load external FIRMs and modules" option | `patcher.c` |
| "Enable game patching" must be on for title patches/LayeredFS | Luma wiki, Optional features |
| Config menu: hold **Select** at boot. Chainloader menu: hold **Start**. Rosalina: **L+Down+Select** | Luma README |
| Game plugin (.3gx) loader merged in Luma v13.0 (PabloMK7 maintainer, Nanquitas original) | Luma README |
| Luma's own sysmodules cover only initial kernel-loaded processes | Luma README |

## Corrected from earlier draft
- Plugin loader is documented as **game plugins**. This is consistent with HOME Menu needing patches via `/luma/titles/` instead.
- `/luma/titles` patching uses IPS, BPS and UPS, not IPS only.

## Not yet verified (3dbrew returned HTTP 403 to automated fetch)
- Title IDs for the eShop, Miiverse (`olv`), software keyboard (`swkbd`), Mii Maker, and modules `act`, `nim`, `boss`, `news`, `frd`.
- Where the profanity filter lives (swkbd flag and word list, Mii name validation, friend/profile text).
- How HOME Menu builds its icon list and which layout files control tile visibility.
- Whether homebrew can read system title RomFS directly, or the user must dump via GodMode9.
- Exact scope of the .3gx plugin loader (appears to be game processes only; not confirmed from docs).
- Online-service end dates (eShop Mar 2023, online play Apr 2024, Miiverse Nov 2017) are from general knowledge, not checked this session.

Next step: get these from 3dbrew in a browser, or from dumps of a real console in Phase 1.
