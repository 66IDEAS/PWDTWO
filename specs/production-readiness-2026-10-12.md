# Production-readiness implementation — 2026-10-12

The user authorised the next security/storage, sync-failure and backup/recovery development batch after the installed Mac/iPhone fictional iCloud round trip. This document records the resulting development slices; it does not approve PWDTWO for sole-copy storage of real credentials.

## Storage and dependency boundary

Local vault lifecycles pin their private directory before asynchronous operations. ABI 2 passes that directory's device/inode identity to the core. Native reads and Rust lock/read/stage/publish/cleanup use pinned descriptors and refuse redirected directories, replaced staging files, ownership/permission changes, links and special files. Cleanup removes only the originally owned stage. Existing conditional replacement, create-only publication, cancellation, interruption and durability reporting remain enforced.

The complete workspace lockfile passes pinned cargo-audit 0.22.2 without ignores. Unused upstream rustfmt/test-with development tools caused the original findings; removing those manifest sections reproducibly prunes their obsolete dependencies without changing the app's cryptographic dependency versions. Owned dependency custom-data strings/buffers wipe on replacement/drop, and the regression checks that ownership boundary. This does not guarantee erasure of serializer allocations, temporary formatting strings, Swift strings, framework copies, registers or OS memory.

Source fingerprints and automated results: [security checks](../dev/security/results/2026-10-12/summary.json), [advisory report](../dev/security/results/2026-10-12/dependency-audit.json).

## Password and recovery changes during sync

Each changed vault retains previous password components inside its authenticated encrypted custom metadata. They let a newly authorised current password read retained older sync ancestors. A previous password value cannot open a vault protected by a different new value. Choosing the same value does not revoke knowledge of it; the app still requires fresh password entry when it learns of a higher authenticated generation. Previous recovery private keys are not retained; ordinary password changes preserve the selected recovery authority, while forgotten-password recovery replaces it.

A device that cannot authenticate a retained revision pauses before outgoing writes and asks for that revision's password. Correct authentication must verify container identity, app owner and the authenticated recovery authority. Equivalent choices deduplicate by generation, authority and component, rather than generation alone. All unresolved ciphertext and pending offline edits stay intact. After authentication, the normal entry conflict review also identifies the verified password/recovery protection to keep. A newer known generation cannot be bypassed by selecting an older generation. Concurrent changes at the same generation provide explicit verified choices; generation numbers are not a distributed total order.

Reconciliation retains the selected protection generation and merges read-key histories. It conservatively refuses incompatible unknown custom metadata rather than silently discarding operation receipts or keys. A combined head authenticated directly by a device's already authorised component can supply read history for other retained ancestors. Authorisations are ephemeral and cleared by the shared app lock. Biometric material for an affected vault is retired only after authentication, immediately before credential publication; it must be enabled again afterward. Ordinary content merges never count as password entry. Selecting current protection from a biometric-only session does not authorise new biometric enrollment.

Interrupted upload after durable local reconciliation preserves the resulting ciphertext and parent set. Reopening with the selected password reads retained ancestors and retries transfer. Revisions arriving during review invalidate confirmation before overwriting local data. The evaluated history is bounded to 256 retained components; hitting this limit fails closed. Independent protocol/memory review, a production lifecycle for retained keys and complete unsupported-metadata handling remain open.

## Optional single scheduled backup

Backup is disabled until the user enables it. Settings accept a frequency of 1–3650 days. One device's opaque local identity is designated in encrypted per-vault settings; another device can explicitly take over without the former device's approval. Frequency and the last authenticated completion time remain when changing writers. The first enabled schedule is due immediately, and overdue execution resumes when the designated app is running, unlocked and can access/reconcile the provider.

Cloud vaults use exactly one `PWDTWO-backup.pwdtwo` beside their immutable encrypted revisions. It contains the complete KDBX vault bytes, not a separate record export. Local-only vaults use one `PWDTWO-<owner>-backup.pwdtwo` in a user-selected bookmarked folder. Manual exports stay separate, user-managed files. The schedule and completion receipt synchronize inside the vault. Separate restored vaults start with no inherited schedule or provider binding.

Before writing, a cloud writer reconciles the current assignment and stops on another writer, unresolved credential/entry/settings review or missing revisions. Publication rechecks the locally visible provider set and pinned local vault bytes. The file is staged, byte-verified, synced and atomically replaces the previous backup; failure before replacement preserves that prior file. Cancellation and ownership checks protect staged publication and cleanup. Staged bytes are checked again at the final gate to reject same-inode modification. Provider checks run outside the short cancellation/publication mutex; a bounded regression confirms that locking does not wait for a blocked provider validation. Completion is recorded only after successful publication. A failed receipt save leaves the usable backup and may cause a later safe retry.

This is coordination against **locally visible** provider state. iCloud/Drive can delay the new assignment to a former writer; OS file coordination is not a remote compare-and-swap. Physical cloud writer-handover/conflict/corruption tests and platform scheduling validation remain required. There is no claim that a suspended/locked/terminated iPhone executes a scheduled backup in the background. Cloud-vault deletion/explicit backup deletion integration remains a separate task.

## iPhone backup and restoration

Settings → Backup & restore exports an authenticated saved vault through the native Files exporter. It includes saved entries, history, attachments, folders, Trash and generated values; device-only drafts remain excluded. Existing backups keep their original credentials after live password changes.

The native Files importer authenticates and reviews a backup before creating a separate vault. It preserves existing vaults and the source backup, remaps restored entry identities and does not inherit cloud/schedule ownership. The user can supply the backup's password, or its recovery key with a new restored-vault password; recovery requires acknowledgement that the replacement recovery key was saved. Shared lock/background clears the review and input fields. These code paths do not replace a current vault silently.

## Evidence and remaining production gates

The prior installed 0.4.2 Mac/0.2.2 iPhone automatic iCloud round trip remains evidence only for that earlier build and the dedicated fictional fixture. No real password/recovery change or backup-setting change was performed to prove this new protocol.

Current validation/deployment results are recorded in `dev/security/results/2026-10-12/`. A development package passing signing checks is not notarized production distribution. Remaining gates include independent cryptographic/security review; complete memory/key and stable schema/migration adoption; actual device protection/biometric and changed-credential/backup cloud ceremonies; safe revision compaction beyond the current development limits; direct mobile Google Drive integration; iPhone Safari/app autofill; and release signing/notarization/updater and delivery. Android and separate iPad application work remain separate phases.

## Installed development updates

Mac **0.5.0 (500)** is installed and launched at the existing checkout app path. Strict current-Mac/nested signature checks pass. The previous app package is retained under ignored `production-readiness-previous/`. A scoped GUI smoke check opens the unchanged fictional seven-record sync vault, including the user's `123` note; the native backup sheet shows scheduling off. Original included-vault selection is restored and the app is left locked. Personal vault contents were not opened for this check.

iPhone **0.3.0 (5)** is installed without uninstalling the existing application; `devicectl` verifies the installed version. Strict signed identity/profile/device coverage passes. Launch is deferred because the physical phone is locked; CoreDevice's exact failure is `Locked`. Unlock and open PWDTWO when convenient. The existing vault password and recovery keys were not changed, and no schedule was enabled.

[Combined evidence and remaining gates](../dev/security/results/2026-10-12/readiness-summary.json), [final native checks and fingerprints](../dev/security/results/2026-10-12/native-readiness.json), [Mac installation](../dev/security/results/2026-10-12/mac-installation.json), [iPhone installation](../dev/security/results/2026-10-12/iphone-installation.json). The original live iCloud round trip remains previous-build evidence; actual changed-credential/backup cloud delivery is still unverified.
