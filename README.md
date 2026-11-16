# ACP automatic approval verification

2026-11-16, Arch Linux, KDE host. All captured conversations use a dedicated test project and isolated OpenResearch storage, with no existing research transcript copied.

- `ask.png` / `auto-approve.png`: real OpenResearch server and browser, deterministic ACP E2E peer. The first request waits; opting in unblocks it; a server restart preserves the setting.
- `real-dsh-ask.png` / `real-dsh-auto-dark.png`: real DeepSeek Harness 0.2.2-rc.1 / DeepSeek V4.1 Flash. An outside-workspace write triggers a one-action permission request. The saved Auto-approve choice permits two separate explicit escalation retries. Both output files were independently checked for their expected contents.
- `native-permissions-zh.png` / `native-narrow.png`: the Linux desktop app using system WebKitGTK on a private Xvfb display, in Chinese, including the 900 × 700 window. The host user's desktop session and production app were kept running.

Validation accompanying the implementation:
- 883 frontend tests pass; typecheck, i18n and styles pass.
- All 4 ACP E2E flows pass: default Ask and opt-in while waiting, restart persistence and revocation; durable grants/mode switches/refusals; late permission cancellation after a prompt reply; revocation after deleting the launch configuration and reloading the saved chat.
- 366 targeted Rust harness/ACP/session-serialization tests pass, including opaque permission IDs, cancellation and the removed-launch policy boundary.
- Clippy and formatting pass.
- The complete local Rust CI-profile run covered 2175 tests: 2173 passed, one login test inherited SSH session variables, and one engine crash-boundary test exceeded the five-minute limit under concurrent build/load. Each passed when rerun separately; the login rerun cleared SSH_CONNECTION/SSH_CLIENT/SSH_TTY, and the crash-boundary test completed in 38.5 seconds. The PR's CI is the final platform check.

macOS and Windows desktop windows were not inspected locally. No new runtime dependency or media component is introduced by this feature.
