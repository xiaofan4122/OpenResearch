# HTML media preview regression evidence

Upstream issue: https://github.com/alphaXiv/OpenResearch/issues/1032

Environment: Arch Linux x86_64, a real OpenResearch GTK/WebKit desktop window on an Xvfb display, 1280x820. Both runs use fresh application data and the same synthetic local project. No private report or user data is included.

Open the project, select Files, then open media-report.html.

- before.png: original v0.2.25 AppImage. The preview is frozen at video loading after WebKit exits. The server health endpoint still returns 200. The log reports a missing GStreamer autoaudiosink element followed by GLib NULL-instance diagnostics.
- after.png: source-built v0.2.25 desktop repackaged with the media-dependency fix. The video frame is decoded at 160x90. The source-built runtime is marked Dev in the window.
- media-report.html: self-contained synthetic H.264/AAC video and Web Audio reproducer used for the desktop screenshots.

The separate package smoke test additionally masks host WebKit/GStreamer and validates a green canvas pixel and AudioContext initialization. These screenshots alone do not establish full audio playback or subtitle support.

Assisted-by: Codex
