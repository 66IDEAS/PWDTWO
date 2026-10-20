# iPhone generator, accessibility, diagnostics and search

PWDTWO iPhone 0.4.3 (9) implements the three approved development slices and the duplicate-search correction from the user's screenshot. It is compiled and checked, but not installed on the physical phone: both iPhone targets still need the existing Apple App Group profile association. The installed phone app remains 0.3.0 (5).

## Generator

The entry editor opens a native Generator sheet. Password options include 8–128 characters and uppercase, lowercase, numbers and special-character groups. At least one group is required. English passphrases use 3–10 random words, no separator/hyphens/spaces, a random two-digit number and a special character. Defaults are a 24-character password with all groups, or five words. The existing shared cryptographic generator is reused.

Generate and Generate Again save each result to encrypted generator history before releasing it to the preview. Masking follows the device preference; Reveal and Copy are explicit actions. Use in Entry updates the protected draft, while saving the entry remains a separate editor action. Cancel leaves the entry's password unchanged, although successfully generated values remain in encrypted history. Successful options are remembered on this device, outside synced vault settings.

Sheet dismissal, changed editor, lock, session changes and repeated Use invalidate the choice. A generation whose result arrives after cancellation can retain its protected history but cannot overwrite the draft or release its value. Copy uses the common optional clipboard-expiry adapter.

## Accessibility and search

At accessibility text sizes, field/action rows stack vertically, value text wraps, and generator count controls give their labels full width. Copy/reveal controls have at least 44-point targets with field-specific accessibility labels. Detail reveals are independent per field and reset when leaving the screen or changing masking preferences; reveal controls disappear when masking is disabled. Entry rows identify their title, type and navigation purpose; decorative branding does not duplicate VoiceOver announcements. The editor has focused fields, Next/Done submission behavior and a keyboard Done action.

Search is now scoped to the native Search tab. Items and Settings no longer inherit the top “Search unlocked vaults” field; the bottom Search control remains and activates the native search input. This uses Apple's [tab search activation](https://developer.apple.com/documentation/swiftui/view/tabviewsearchactivation(_:)) and [native search interface](https://developer.apple.com/documentation/SwiftUI/Adding-a-search-interface-to-your-app).

Native simulator hosting checks verify that Settings contains no search field and that the Search tab's input accepts text. Snapshots cover Settings, Generator, Diagnostics and entry details at the largest Dynamic Type size. These checks support the implemented layout; they do not certify complete physical VoiceOver traversal, keyboard focus or accessibility across every screen.

## On-device diagnostics

Settings → Report a Problem opens a native diagnostic preview. Users can exclude build/OS information or recent events, inspect the complete JSON, save it through the Files exporter and attach it manually to a bug report. Nothing is uploaded or sent automatically. Clearing local history requires confirmation and does not remove already exported reports.

Events contain only a timestamp and one of seven fixed codes: session started, vault unlocked, unlock failed, vault locked, entry saved, generation protected or operation failed. The report adds a fixed format/application identifier and generation timestamp, plus optional numeric app version/build/OS fields. There is no arbitrary error-text logging path. Reports exclude vault contents, names, identifiers, accounts, websites, paths, clipboard, screenshots, passwords and keys. Unrecognized on-disk content is rejected and never forwarded into a report; an unavailable log can still produce a build/OS-only report.

The private `.diagnostics` directory is outside discoverable/synced vault payloads, excluded from OS backup and configured for complete iOS Data Protection. A serialized writer actor encodes and publishes off the UI actor; monotonically increasing revisions prevent an older queued write from undoing clearing. Retention is seven days at maintenance, at most 2,000 events and at most 10 MiB persisted data. Suspended or closed applications cannot promise deletion at an exact wall-clock deadline. The fixed internal `events.kdbx` filename is typed JSON used with the existing bounded private reader, not an encrypted vault. The public report is JSON. A verified GitHub issue URL is not configured in this repository, so no issue link is invented.

## Validation and delivery

The full iOS 26.2 suite passed 48 cases, with two separately driven interop fixtures skipped and no failures. After final UI-only refinements, all ten generator/diagnostics/native-interface cases passed again. Generator checks cover protected history, explicit use, cancel, persistence, invalid options, changed editors, lock and replay. Diagnostic checks cover the exact allowlisted schema, malformed-content exclusion, optional sections, retention/bounds, private permissions, backup exclusion and stale queued writes after clearing. Fixtures use fictional temporary vaults and no user clipboard, accounts or cloud files.

Final arm64 simulator and unsigned physical-device products compile against SDK 27 with minimum iOS 26, matching 0.4.3 (9) main/provider versions, the actual provider principal class and no XCTest runtime in deployable copies. Frozen source hashes match. [Evidence and final check counts](../dev/iphone/results/2026-10-14/polish/summary.json); [native screenshots](../dev/iphone/results/2026-10-14/polish/final-ui-screenshots/manifest.json).

Physical installation remains gated by the pending App Group signing setup. Physical UI/VoiceOver, Files export, hardware Data Protection/biometrics and iOS27 runtime acceptance remain open. Parent generator, diagnostics, accessibility and mobile/release tasks retain their wider unfinished scope; these checks are not an independent production security review.
