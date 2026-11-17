# OpenResearch Linux media evidence

Synthetic report/clip screenshots for alphaXiv/OpenResearch#1033. No private research content or credentials are included.

- media-working.png: actual AppImage HTML preview; Web Audio and decoded video/canvas, private Arch native Wayland session.
- media-disabled.png: same preview after a hung media plugin; static HTML and installation guidance remain visible. The fixture reports missing AudioContext as expected with media disabled.
- install-light.png: expandable package commands and keyboard-focused download link.
- install-dark-zh.png: Chinese, dark appearance, 900 × 700 window and keyboard-focused download link.

After syncing main, the rebuilt package again passed all 21 native-window scenarios. SHA256: aac09762ecd31eb6dad9a3f4b486756b7c1214c47e2e7d5b183f5122ffc878d8 (100,039,160 bytes). Runtime/UI source matches the main-synced PR; head 8c928ad also includes the Ubuntu runner SDK setup correction. Media screenshots above were refreshed from that package. The two installation screenshots use the unchanged media component from the preceding native inspection.
