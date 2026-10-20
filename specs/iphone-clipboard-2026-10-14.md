# iPhone optional clipboard expiry

PWDTWO iPhone 0.4.1 (7) implements the iPhone development slice of T031/T039/T079. Clearing is **off by default**, independently configured on this device under Settings → Clipboard. When enabled, the delay is 15, 30, 60 or 120 seconds; 60 seconds is the initial choice. Unsupported stored/runtime delays fall back to 60. Preferences never enter a vault, sync revision or App Group.

All explicit application Copy buttons use one native adapter. Passwords, generated values, recovery keys, card numbers/security codes and sensitive custom fields receive expiry when enabled. Usernames and non-sensitive fields do not. Copies preserve the exact value and remain local to this iPhone. Locked sessions refuse ordinary copies; pending creation/recovery may copy only the current displayed recovery key through a separate entry point.

The adapter uses [Apple's UIPasteboard item expiry](https://developer.apple.com/documentation/uikit/uipasteboard) with the local-only option. The OS owns removal of the copied item, including while the app is suspended. PWDTWO keeps no extra plaintext copy or timer, never reads the general clipboard, and never performs a delayed blanket clear. Later items have their own identity, including a new copy of identical text. Preference changes apply to future copies; a previously assigned expiry remains attached to its original item.

This feature controls the app's explicit Copy buttons. Native text selection/system Copy menus are OS-owned and do not pass through the application adapter. Expiry cannot remove already-pasted text or independently saved clipboard history. Physical-device timing/background behavior remains to be verified; the implementation does not promise exact scheduling on every OS/device.

## Verification

Fourteen focused iOS 26.2 simulator cases passed: six clipboard checks and eight existing session regressions. The new cases cover defaults, all supported delays/fallback, exact values, secret/non-secret scope, preference persistence/device locality/invalid values, locked-copy refusal, pending recovery-key authorization, native expiry after releasing the adapter, and preserving later different/identical copies. Native checks use fresh app-private named pasteboards with fictional text only; they do not read or change the user's general clipboard. The unchanged controller regressions cover grouped unlock, recovery, encrypted drafts, CRUD/history/Trash, generation, cancellation and inactivity/storage protection.

Final device compilation and frozen-input hashes are recorded in [results](../dev/iphone/results/2026-10-14/clipboard/summary.json). This change does not modify vault contents, passwords, biometric enrollment, cloud bindings or the existing physical installation. Installation of the current app with its AutoFill extension still requires the pending Apple App Group profile association for both targets.
