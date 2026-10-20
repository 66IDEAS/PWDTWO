# PWDTWO macOS autonomous batch — 2026-10-10

Status: offline batch implemented and validated; the full application is not complete. This document describes the current offline development slice; it does not approve production cryptography, cloud sync or browser extensions. Earlier validation entries are historical and retain their original limitations.

## Implemented in this batch

- Cross-vault Move: encrypted intent in the source, durable destination receipt/copies before source Trash, restart/resume without duplicates, and Keep Originals. Changed originals or destination copies block finalization. Ordinary Copy also preserves the richer supported schema.
- Dated complete entry history: review masked fields, notes, custom fields and files; restore as a new version; explicitly clear history. No automatic pruning.
- Password/passphrase generation: shared Rust OS randomness, unbiased selection, all requested character categories guaranteed, 7,776-word EFF English list with retained attribution. Used values publish to encrypted per-vault history before insertion into an unsaved editor.
- Encrypted device-only drafts: per-vault random key inside encrypted metadata, AES-GCM sidecars with owner binding, private files, restart recovery, changed-base review and Keep as New Entry. Drafts never become active credentials or enter backups. Corrupt or detected stale sidecars are retained rather than overwritten.
- Identities/documents, optional masked custom fields and file attachments. Default attachment limit 1 MB, configurable per vault; lowering it retains existing files. Attachment removal is retained in prior versions. Native export warns that the resulting file is unencrypted.
- Nested folders, empty folders, tags/filtering, subtree rename, whole-tree Trash with an explicit warning, collision-safe tree restoration, and explicit per-vault Empty Trash.
- Current CSV import from Google Password Manager, 1Password, LastPass and Apple Passwords: review before publication, exact duplicate/possible-match Skip defaults, Keep Both/Update Existing, complete quoted/Unicode/multiline parsing, sensitive extra columns, preserved existing fields absent from narrow exports, and counts after publication. The source is untouched. CSV cannot recover data omitted by the source application.
- Migration exports: login-only CSV with a plaintext warning; standard password-protected KDBX with current records/custom fields/binaries and optional history/Trash. The user chooses a separate export password. No PWDTWO recovery key, local drafts, generator history or transfer receipts enter the standard migration container.
- Sanitized on-device diagnostic review and user-selected JSON export. No telemetry or automatic upload.
- Recovery keys can be deliberately saved to a private plaintext file or sent to the native print dialog after explicit warnings; acknowledgement remains the user’s responsibility. The shared private file writer is tested; physical printing/recovery-key GUI export was not exercised.
- Vault name/icon/accent inside encryption; opening a supported PWDTWO file as an independent local copy; explicitly confirmed deletion of one local file, its draft and targeted biometric enrollment. Other vaults/manual exports are retained.

## Practical limits

This uses the controlled experimental KDBX fork and experimental envelope, not the final production domain model. Identities use flexible custom fields; structured schemas/passkeys are still outstanding. Attachments/history are inline and can duplicate bytes; the development envelope is bounded at 8 MiB/1,000 entries and the encrypted file at 32 MiB. Attachment settings are currently bounded at 8 MB. These are evaluation bounds, not approved product limits. Oversized/unknown data fails rather than silently truncating.

A supported PWDTWO file opens as an independent copy; there is no in-place external-file ownership/cloud connection. Standard KeePass import is not implemented. Standard KDBX migration export has independent-reader evidence for fields/history/binaries; it does not promise roundtrip semantics for every competing client.

Private local publication uses revision checks and local advisory locks where applicable. They do not provide atomic compare-and-swap against non-cooperating writers, provider transactions or a power-loss proof. Draft preservation failures may retain an earlier edit; the UI reports that the latest preservation was not confirmed.

## Still outstanding

Independent engineering work remains: production schema/memory/format hardening; cloud adapters and conflict UI; designated-device scheduled single-backup behavior; Safari/Chrome/native-app autofill; TOTP/passkeys/security analysis; deliberate sharing; richer import formats; Sparkle integration and release tooling. These are not implemented by the offline batch above.

External evidence/configuration is also needed: real Google OAuth registration and account/provider testing; iCloud multi-device validation; real Safari/Chrome extension installation and platform ceremonies; supported macOS 26 runtime; additional hardware/biometric lifecycle tests; Developer ID/notarization/release credentials; public release/appcast signing and hosting. Existing single-vault Touch ID user confirmation remains valid; automated tests use controlled biometric adapters and make no new sensor claim.

D02–D05 production decisions/reviews remain open. A working development app and successful regression suite do not close those gates. Parent-task completion stays 3/96 across the entire four-platform project, not a macOS completion percentage.

## Build and verification

See `dev/macos-preview/README.md` for command-line signed/local builds. Current app: `dev/macos-preview/build/PWDTWO Local Vault.app`. Consolidated validation and artifact/source fingerprints are recorded in `dev/experiments/foundation/results/macos-batch-summary.json` with all passing checks and remaining limitations. Tests use private disposable fictional fixtures; user vaults, settings and Keychain are not modified.

## Subsequent cloud/autofill integration

The [cloud/autofill handover](cloud-autofill-handover-2026-10-10.md) records the later native provider-folder sync and entitled browser/system integration candidate. Its narrower implementation and validation supersede the corresponding earlier missing-component statements; live installed/provider and production gates remain open.
