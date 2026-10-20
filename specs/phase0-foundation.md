# Phase 0 — engineering baseline and threat model

Recorded 2026-10-09. This document closes specific planning work; it does not declare the cryptographic protocol, experimental KDBX fork, cloud concurrency or biometric integrations production-ready. The authoritative feature scope remains in specifications.md, architecture.md and ux.md.

## Product/build matrix (T002)

| Product | Implementation | Initial runtime baseline | Identifier selected for configuration |
| --- | --- | --- | --- |
| PWDTWO for Mac | Swift 6, SwiftUI with AppKit; direct macOS target | macOS 26/27; arm64 only throughout the bundle | `com.sixtysixideas.pwdtwo.mac` |
| PWDTWO for iPhone | Separate Swift 6 / SwiftUI target with UIKit adapters | iOS 26/27; physical arm64, appropriate Apple-silicon simulator builds | `com.66ideas.pwdtwo.iphone` |
| PWDTWO for iPad | Separate Swift 6 / SwiftUI target with UIKit adapters | iPadOS 26/27; physical arm64, appropriate Apple-silicon simulator builds | `com.sixtysixideas.pwdtwo.ipad` |
| PWDTWO for Android | Kotlin / Jetpack Compose with native Android adapters | Recorded Android 16/17 baseline, min API 36; validate compile/target SDK before implementation | `com.sixtysixideas.pwdtwo` |

The identifiers are repository configuration decisions, not registered developer resources or store listings. Credential/Safari extension identifiers will be children of their owning product; entitlements, groups and provisioning must be validated before registration/distribution. Android physical-release ABI starts with `arm64-v8a`; `x86_64` is for emulator validation, not Intel Mac distribution. Any need for additional physical Android ABIs requires measured target-device evidence before release.

The shared core remains Rust, compiled separately for each native target. UniFFI remains a candidate, not an adopted dependency. The Mac preview does not link a vault core and must not establish a competing Swift storage implementation. Browser DOM automation may use TypeScript/JavaScript; user-facing application/credential chooser views remain native.

The supported OS window rolls only after stable major releases. Keep Safari tied to supported Apple OS versions, and test current/previous stable Chrome on Mac and Android. Confirm the matrix at release time; do not set an upper OS installation cap or infer compatibility from compilation alone. Newer native API use must preserve the previous supported generation’s behavior.

### Available command-line environment

- Measured Mac: Apple silicon, macOS 27.0.1, Xcode 26.6 (17F113), macOS SDK 26.5, Swift 6.3.3.
- Swift’s reported default target is newer than the deployment baseline; the preview explicitly sets `arm64-apple-macosx26.0` and checks Mach-O metadata.
- Rust/Cargo 1.92.0 are installed. Apple Mac/iOS targets are available; Android Rust targets and an Android SDK were not found in the inspected standard configuration. Do not claim Android build validation.
- CoreSimulator was inaccessible inside the command sandbox. No mobile simulator was booted or validated. Xcode GUI use is unnecessary for the Mac build.
- Production toolchain and dependency versions must be pinned after the binding/format gates; no speculative package update or SDK installation is performed here.

## Threat model and boundaries (T004)

### Assets and actors

Protect vault contents (including notes, URLs, identities, device names, history, Trash, generated values and attachments), passwords, recovery secrets, derived keys, passkey private keys, authenticator seeds, pending edits and local drafts. Provider refresh/access tokens and release-signing keys are separate protected assets. A cloud file’s presence/size and access timing may be observable to its provider; encryption does not hide all traffic metadata.

Assume an attacker may obtain encrypted files and old backups, submit malformed files, tamper with or replay provider data, trigger hostile web pages/iframes/navigation, send forged or replayed IPC requests, or possess stale shared credentials. Devices may crash, run out of storage, lose authorization or remain offline through concurrent password changes and migration. A legitimate shared-vault participant can read/copy/export every decrypted record and retain it indefinitely.

An unlocked compromised OS, malicious privileged process or person possessing valid vault credentials can defeat application confidentiality. Do not claim to repair such compromise, erase copies remotely, or revoke remembered plaintext. Physical-device security, provider account MFA and user-controlled secret storage remain separate responsibilities. These limits do not justify weakening the lock boundary in a healthy supported OS.

### Keys and authority

| Material / authority | Required boundary |
| --- | --- |
| Vault password | Per vault; processed locally through the reviewed KDF; never given to the provider, diagnostics or unrelated vaults. New-password length policy does not alter existing password bytes. |
| Recovery secret | Independent per vault and held by the user; no vendor/trusted-contact escrow. Recovery requires an available corresponding encrypted file and replaces both credentials. Normal password change retains the recovery secret. |
| Recovery public metadata / wrapped material | Authenticated and bound to vault identity, protocol version and credential generation. Public header fields must never disclose usable plaintext unlock material. Unauthenticated fields cannot authorize destructive changes. Exact construction remains D03 work. |
| Device-local unlock keys | Bound to platform biometric-only access and enrollment state; not released by device PIN/login fallback. A biometric result is not a substitute for reviewing actual Keychain/Keystore access policy. |
| Shared application session | Coordinates visibility and activity across separately protected vaults; it is not one common password/key. No included vault contents become visible until all included authorization requirements pass. |
| Provider tokens and permissions | Authorize encrypted-file operations only; do not decrypt vaults. Cloud owner/writer distinctions do not implement PWDTWO owner/editor/viewer roles. |
| Transfer password | New random bearer secret for one independent snapshot; communicated separately from its file. No expiry, single-use or named-recipient identity claim. |
| Release-signing secrets | Outside the public repository and vault runtime. Valid artifact/update signatures are required but do not validate vault cryptography. |

### Required controls and verification obligations

1. **File boundary:** authenticate before trusting contents; bound parser, XML/decompression and KDF work, reject inconsistent identity/generation metadata, and preserve a usable previous revision through interrupted replacement. Fuzz and adversarial-input checks are separate from happy-path round trips.
2. **Local derived data:** protect drafts, staged changes, search indexes and preview temporary files with the appropriate vault boundary. Exclude secret fields from ordinary search. Lock immediately invalidates every native content surface and credential grant; preserving a draft may not delay lock.
3. **Authentication:** only deliberate app/autofill activity extends the shared session. Device lock, manual lock and timeout revoke all open access together, including late callbacks. Mandatory re-entry after credential change and biometric enrollment invalidation survive process boundaries and restart. Optional periodic re-entry is off by default.
4. **Browser/application boundary:** verify native callers and browser sender context, bind each fill grant to the specific destination/document/fields/session, and reject replay or navigation reuse. Exact saved hosts only; explicit mismatch confirmation cannot override passkey RP binding or native application association. Login auto-submit remains off by default, and card/identity submission is always manual.
5. **Cloud boundary:** treat downloaded bytes and provider timestamps as untrusted inputs. Preserve concurrent encrypted versions and local pending edits before reconciliation. A read followed by unconditional upload is not atomic concurrency control. Real provider probes must validate the final publication/deletion/handover protocol; a local file lock cannot supply cross-device ordering.
6. **Credential generations:** after learning of an authenticated change, require the new password before exposing the affected vault. Preserve independently encrypted branches and require explicit unlock/credential choice if changes conflict. Old backups/offline copies remain protected by their original credentials; rotation does not retroactively erase access.
7. **Deletion/migration/backup:** distinguish confirmed deletion from denied access or transient absence. Never recreate a retired cloud file automatically. Verify destination before deleting source; preserve newer source revisions and track retryable cleanup. Backups are opt-in, one replaceable file and one designated writer, with fencing of stale/in-flight writers and preserved old backup on replacement failure.
8. **Shared-content boundary:** equal shared-vault access includes recovery. Protect unrelated private vaults and deliver replacement shared credentials securely. Independent transfers serialize only confirmed current content and optional selected notes/attachments, never history or source unlocking secrets.
9. **Privacy and diagnostics:** allowlist technical fields before logging; no vault/account identifiers, personal paths, raw responses, memory dumps or automatic uploads. Manual preview/export is explicit. Clipboard clearing is off by default and may clear only the owned, still-current copy when enabled. Masking is presentation, not authentication; disabling it does not disable lock or search exclusions.
10. **Dependencies and release:** use maintained primitives through reviewed libraries. Preserve third-party licences; original MIT licensing does not relicense vendored code. Test supported native APIs/versions on actual platforms, verify release/update signatures and notarization, and review data migration/recovery before publication.

### Decision gates still open

**2026-10-10 follow-up:** [Foundation implementation results](phase0-foundation-results.md) add a runnable bounded recovery candidate, Swift integration, UniFFI comparison, shared-session checks and provider harnesses. Recovery encoding and API candidates now exist; their production approval and the live gates below remain open. Earlier counts describe their original experiment, not the current complete suite.

- **D02:** [additional mutation review](../dev/experiments/kdbx-mutation-review/README.md) reproduced two history/reference defects and verified isolated fixes with 20 active checks; the original fork is unchanged. The controlled KDBX fork is still the leading candidate. Review its history mutation/attachment reference behavior, deletion/custom icon APIs, unknown-data preservation and maintenance strategy before production adoption.
- **D03:** the documented public-key recovery-block construction remains a candidate. Final cryptographic library, reviewed KDF limits, recovery encoding and atomic generation transition remain unresolved; no new primitives are introduced by the preview.
- **D04:** actual Drive/iCloud concurrency and multi-device deletion/backup fencing evidence is required. Local simulation results do not close this gate. No existing user cloud files should be used as experimental fixtures.
- **D05:** shared bindings/secret lifetime and real multi-vault biometric unlocking need validation. A user’s physical biometric interaction is unavoidable for the biometric proof; browser/OS enablement and provisioning are separate from command-line compilation.
- **D01:** provider sharing and secure shared-credential delivery remain engineering work; no application backend, emergency access or enrollment service is implied.

## Preview/production separation

`dev/macos-preview` is an in-memory UX implementation for T012. Its sample lock is a visibility state, not an authentication mechanism; its generated phrases use an explicitly illustrative small list. No samples, Swift preview persistence assumptions or demonstration credentials may be used as production vault defaults. The approved Rust core and its review gates remain authoritative for real vault operations.
