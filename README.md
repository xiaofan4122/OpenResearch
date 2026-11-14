# AppImage system media runtime evidence

Upstream issue: https://github.com/alphaXiv/OpenResearch/issues/1032

All reports and images in this branch are synthetic. No private report or account data is included.

- before.png: original v0.2.25 package freezes while loading a local HTML video; its WebKit process exits.
- after.png: the revised small AppImage automatically selects Arch's system WebKit/GStreamer. Files -> media-report.html shows the decoded 160x90 frame. Restarting restores the preview successfully. No manual LD_LIBRARY_PATH was supplied. The test binary is a source-built v0.2.25 runtime, marked Dev.
- missing-light.png / missing-dark.png: with system WebKit and media plugins hidden in a private mount namespace, the app shows dependency installation instructions before starting the dashboard. Escape closes the dialog and the launch returns 1.
- media-report.html: the self-contained H.264/AAC report used in the real desktop flow.

The same built AppImage passes dashboard/media checks on Ubuntu 22.04, Ubuntu 24.04 and Debian 12 under Xvfb in containers. Ubuntu 22.04 additionally passes the bundled fallback after removing system WebKit, and shows the dependency dialog after removing media plugins. Native SDK paths and bundled fallback paths are checked in /proc. The media check validates AudioContext creation and a decoded green pixel, not full audio playback or subtitle support.

With the same existing desktop executable, baseline package: 99,985,912 bytes; revised package: 99,990,008 bytes (4,096 bytes extra). No GStreamer media plugins or FFmpeg codec dependencies are added to the image. Missing system dependencies still take disk space when installed through the distribution.

Local verification: 45 script tests; 10 shell-environment and 7 process Rust tests; cargo fmt and clippy; actionlint and offline zizmor. The runtime package reused a v0.2.25 executable; Rust environment changes are tested from the PR source. ARM64 desktop runtime execution, macOS/Windows windows, full playback and subtitles are outside this local runtime matrix.

Assisted-by: Codex
