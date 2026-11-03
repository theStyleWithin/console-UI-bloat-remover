# console-UI-bloat-remover
its in the name a console UI bloat remover. object: removes unecessary bloat in a consoles UI. Handy especially for legacy consoles that still keep there storefront icons/buttons even after the company declares the console no longer profitable. storefronts, sign-in-link account prompts or buttons, dead/cancelled social features, news, subscriptions

┌─────────────────────────────────────┐
│     Console Bloat Remover           │
├─────────────────────────────────────┤
│                                     │
│  1. UI Cleanup                      │
│  2. Account & Online                │
│  3. Language Filters                │
│  4. Advanced                        │
│  5. Status & Logs                   │
│  6. About / Credits                 │
│                                     │
│  [Apply Changes]    [Revert All]    │
└─────────────────────────────────────┘

UI Cleanup
────────────────────────────
[ON]  Hide eShop / Storefront
[ON]  Hide Dead Social Features (Miiverse-style)
[OFF] Hide Notifications / News
[OFF] Remove Promo / Spotlight Banners
[ON]  Simplify Home Menu Layout

[Apply]  [Back]

Account & Online
────────────────────────────
[ON]  Disable Forced Account Sign-in
[ON]  Skip Account Linking Prompts
[OFF] Block Background Online Checks
[OFF] Disable Error Reporting / Telemetry

[Apply]  [Back]

Update Prompts
────────────────────────────
[ON]  Block System Update Prompts
[ON]  Block Game Update Prompts

Note: This only stops the nag screens.
It does not prevent manual updates.

[Apply]  [Back]

Language Filters
────────────────────────────
[OFF] Disable System Language Filters

Filter Strength:
( ) Off
(•) Moderate
( ) Aggressive

Note: Only affects system-level filters.
Some games have their own filters.

[Apply]  [Back]

Advanced
────────────────────────────
[ ] Enable Experimental Patches
[ ] Keep Backup of Original Files
[ ] Show Technical Details

Danger Zone:
[Restore Original System Behavior]

[Back]

Status & Logs
────────────────────────────
Active Features:
• eShop Hidden
• Account Prompts Disabled
• Language Filters: Off

Last Applied: 2026-11-02 19:24
Plugin Status: Running

[View Full Log]  [Back]

Design Notes

Keep each page focused on one category so it doesn’t feel overwhelming.
Use clear ON/OFF toggles instead of complicated settings.
Always have Apply and Back easily reachable.
Put the most commonly wanted options near the top.
Include a big Revert All option on the main screen for safety.

Phase 1 – Research & Feasibility (Per confirmed platform)

Map how the system menu, storefront, account system, and language filters work on each target
Identify existing homebrew, plugins, or patches that already touch these areas
Determine the cleanest technical approach (sysmodule, plugin, theme replacement, config edit, etc.)
Note any major blockers or high-risk areas

Phase 2 – Architecture & Design

Decide overall structure (one multi-platform tool vs separate tools per console)
Design the modular feature set and config system
Decide how users will enable/disable each feature
Plan safety / reversibility measures

Phase 3 – Prototype (First platform only)

Build a minimal working version on the highest-priority console you own
Focus first on the easiest wins (e.g. hiding store tiles or disabling one major nag)
Get basic language filter bypass working if feasible

Phase 4 – Expansion & Polish

Add remaining features on the first platform
Port the approach to the next confirmed console
Improve UI, documentation, and stability

Phase 5 – Release Prep

Write clear install/uninstall instructions
Add safety warnings
Prepare a public repo structure
