# Phase 0 foundation results — 2026-10-10

The four independent engineering workstreams have runnable candidates and recorded local evidence. They advance the foundation without connecting personal user vaults to the Mac preview; the optional signed prototype now uses encrypted sample entries. D02–D05 remain open for the specific checks below; this report does not approve production cryptography or cloud synchronization.

The earlier unattended turn stopped at a tool-permission wait. After the application restart, existing artifacts were recovered, missing dependencies fetched, and the local suites completed. No personal cloud account or protected Keychain item was accessed.

**Later user-present follow-up, 2026-10-10:** Real biometric-only authentication now passes in the native Touch ID test bundle. The first protected-item attempt stopped at creation with missing-entitlement error -34018; cleanup passed. A native automatic-signing Xcode target and profile-aware command-line builder are prepared, and the target builds successfully with signing disabled. A matching provisioning profile is still required for the two protected-key reads. [Touch ID evidence and procedure](../dev/experiments/biometric-session/README.md). Earlier unattended results retain their original scope.

**Provisioned follow-up completed, 2026-10-10:** After the user installed Xcode 27.0 and signed in, automatic signing registered this Mac and supplied a matching development profile. The active Keychain test passes: one biometric-only authorization reads both independent protected keys, no additional prompts are permitted, reads before authentication and after context invalidation are denied, and both test items are deleted. This closes the tested Mac protected-key retrieval/reuse portion; it does not yet connect the materials to vault decryption or establish enrolment/extension/lifecycle behavior. [Recorded active result](../dev/experiments/biometric-session/results/active-run.json).

## Outcomes

| Workstream | Implemented and verified | Remaining boundary |
| --- | --- | --- |
| Vault format and recovery — T005/T006 | Isolated KDBX candidate includes the two additional history/reference repairs, parser/resource guards, explicit raw-key API, versioned recovery encoding, authenticated generation binding, password change and replacement recovery. | Production format/dependency adoption, complete schema preservation, cryptographic review, calibrated resource policy, durable rotation and memory-lifetime work. |
| Swift–Rust integration — T009 | Swift actor invokes real Rust create/open/change/recover operations through ticket-checked C ABI; lock/cancellation rejects stale results. UniFFI Swift comparison also runs; Kotlin source generates. | Final API decision, Kotlin/Android compilation/runtime, Apple mobile linking/runtime, extension memory tests and packaging/licensing review. |
| Shared biometric session — T010 | Provisioned two-key and two-vault Touch ID passed; all-or-none opening rejects missing/bad materials and stale/cancelled callbacks. The prototype now loads encrypted sample envelopes. | Enrollment changes, OS lock events, extension behavior and production key/draft lifecycle. |
| Cloud preparation — T007/T008 | Drive request/failure/ownership tests and a disposable live capability harness; native file-coordination harness with synthetic revision/conflict evidence. | Live Drive races, two-Mac iCloud ordering/conflicts, deletion versus permissions, backup-writer fencing, retirement and migration. |

## Reproducible evidence

The [foundation runner and contract](../dev/experiments/foundation/README.md) and [binding comparison](../dev/experiments/binding-comparison/README.md) contain commands and limitations. The complete foundation run used the optional independent Python reader. Logs are local synthetic evidence, with no secret values.

| Verification | Result |
| --- | --- |
| Rust storage/recovery/boundary regressions | Latest suite: 46 unit checks and eight process/transaction checks passed; two independent-reader checks and the subprocess helper are opt-in/skipped in the parent invocation. |
| Independent KDBX reader | Both opt-in fixture/reopen tests passed separately, including PyKeePass read/write between them. This exercises the inherited fixture, not every new schema or recovery representation. |
| Isolated candidate hardening | Three passed: decompression ceiling, unknown XML rejection, and depth/DTD rejection. |
| C bridge and Swift actor | Release library and Swift 6 warnings-as-errors build passed; synthetic create, disk round-trip, lock/reopen, password change, retained recovery, replacement recovery and old-key rejection passed. |
| Shared session | Eleven checks passed with injected providers; zero protected reads or biometric prompts. |
| Google Drive | Twelve offline checks passed; no live request. |
| macOS file coordination | Local synthetic read/replace/read passed; no ubiquitous item used. |
| UniFFI 0.32.2 | Swift compilation and four behavioral checks passed; Swift/Kotlin generated. Kotlin not compiled. |
| Rust Apple mobile targets | `cargo check` passed for `aarch64-apple-ios` and `aarch64-apple-ios-sim`; no linked mobile application or device run. |
| Static checks | Own candidate library passes Clippy with warnings as errors; unrelated upstream lints are outside this claim. |

Final reports: [foundation](../dev/experiments/foundation/results/run-all.json), [bindings](../dev/experiments/binding-comparison/results/run-all.json). Report hashes identify the tested implementation sources. Preparation separately records the generated candidate's Rust source hashes. No full upstream regression suite, fuzzing campaign, independent security audit or all-platform validation is implied.

One `/usr/bin/time -l` run of the release Rust / native Swift workflow measured **1.40 seconds wall time, 85,164,032 bytes maximum resident set size (about 81 MiB), and 79,250,080 bytes peak footprint**. The workflow uses small synthetic data with the evaluation creation profile of 64 MiB Argon2id, three passes and one lane. It performs several operations; this is not a per-unlock benchmark, a worst-case bound or an extension budget. [Raw resource measurement](../dev/experiments/foundation/results/swift-core-resources.log).

## Design conclusions and limits

The controlled KDBX fork remains a viable candidate for the narrowly tested format. Fail-closed handling is preferable to silently dropping unsupported XML, but deliberately rejects some external files. The next schema evaluation must cover every required PWDTWO record, nested custom data and unknown-field behavior. The original evaluated vendor sources remain unchanged; all additional changes live in an isolated generated copy and reproducible patches.

The recovery candidate meets the tested policy: ordinary password changes retain the recovery key; recovery replaces both credentials; old credentials still unlock their old file copies. Neither a public generation counter nor a valid old file proves freshness. Persistent anti-rollback state and crash-safe publication remain protocol work. The current 8 MiB file ceiling and KDF settings are experimental, not changes to accepted attachment limits or production defaults.

Generation tickets work across the Swift/C/Rust boundary and prevent late results from reopening a locked context. Secret wrappers erase allocations they own, but upstream database/key buffers and language/framework copies need further work. Cancelling a ticket does not stop already-running crypto; a process-wide KDF scheduling budget remains required. The original material-only state machine remains separately tested; the later shared-vault session also decrypts/authenticates every selected file and sample envelope before publication.

UniFFI is worth carrying forward for ordinary domain APIs because it generates Swift/Kotlin bindings and typed errors. Its borrowed synchronous byte input has a scoped Swift pointer lifetime, while owned byte transfers make serialization copies. Keep secret ownership and cancellation semantics explicit regardless of binding. Select the final API only after the Kotlin/device/extension checks; the comparison does not run the full vault protocol through UniFFI.

The provider harnesses are ready for deliberate disposable-account/device experiments. Their [procedures](../dev/experiments/foundation/cloud/README.md) identify expected outcomes and failure cases. Local coordination and HTTP response classification do not prove a distributed protocol. No extra backup history, application backend or scope reduction has been introduced.

## Next sequence

1. Continue independent format/schema, memory-lifetime and durable-write review; settle the production profile from evidence.
2. The protected multi-vault Touch ID experiment passed. Continue separate enrolment and OS lifecycle validation; do not treat the sample-key proof as production/extension acceptance.
3. Use a dedicated Drive test account and two Macs with a dedicated iCloud folder to capture live provider evidence. Keep backup handover, deletion, retirement and migration open until their scenarios pass.
4. Close the relevant architecture decisions and integrate the reviewed core with the native Mac application. The current GUI remains a clearly labelled sample-data preview in the meantime.


## Mac Touch ID now opens actual encrypted fixtures — 2026-10-10

The native preview now has an optional development-signed Touch ID mode. Its adapter retrieves both independent per-vault password components using one biometric-only context and additional Keychain interaction forbidden. The shared session reads each disposable KDBX file, decrypts through the Rust candidate and verifies its authenticated root identity before publishing both vaults together. Wrong/missing credentials, corruption, cancellation or either opening failure expose neither vault. Each attempt owns fresh core handles; shared lock synchronously destroys them so a queued operation or late commit cannot restore access.

The actual GUI reached the sample interface with authenticated two-vault status, and clicking Lock Preview immediately hid all entries. A separate final-build preparation/quit report confirms protected-item and encrypted-file cleanup. The final native locked screen was visually inspected. [Integration evidence](../dev/experiments/biometric-session/results/preview-integration.json), [cleanup report](../dev/experiments/biometric-session/results/preview-cleanup.json).

Regression evidence: 41 Rust checks, three dependency-hardening checks, eleven injected material-session checks, eight additional real-decryption scenarios and 32 preview model checks pass. Clippy, native Swift/release builds, local file/Drive checks and iOS Rust target checks also pass in the current suite. The two opt-in independent-reader checks were not included in this invocation; their earlier results remain historical evidence. Matching profile/app/Keychain-group isolation and strict Apple Development signature verification pass.

This integration deliberately leaves fictional interface entries and drafts in memory. The encrypted fixtures carry root identities, not the GUI records, and are deleted at normal exit. It does not close production encrypted CRUD, recovery/enrollment UI, OS lock behavior, extension authorization, macOS 26 runtime or D02–D05 security/design review. Forced termination can leave only this run's disposable artifacts; no broad Keychain cleanup is performed.

The final signed preview also produced a [local active-session report](../dev/experiments/biometric-session/results/preview-active-session.json) with `actualEncryptedVaultsOpened: 2` and authenticated expected identities. This report is distinct from the separate quit/cleanup run. Settings now explicitly describes the temporary encrypted fixtures, protected keys and optional credential-free local report.


## Encrypted sample entries and local publication — 2026-10-10

The candidate now persists authenticated encrypted revisions with same-directory staging, readback validation, file flush, base-revision recheck and atomic local rename. Local cooperating processes use a per-vault advisory lock. A core-generation guard serializes publication with lock/cancel. A failed final directory sync is reported as published with unconfirmed durability, rather than falsely promising unchanged live bytes. A trusted authenticated base revision and container UUID prevent stale saves and accidental cross-vault replacement during rotation/recovery. No additional retained automatic backup was added.

Eight process/storage tests pass, including abrupt exits at eight boundaries, competing subprocess writers, a genuine file-limit write failure, failed/cancelled writes, stale/duplicate creation, path/security checks, corrupt-live/orphan handling and the post-publication failure classification. The native persistence workflow also passes create, rotation, recovery, reopen and rejection cases. These are process-interruption checks on this Mac's local filesystem, not physical power-cut or cloud-provider evidence.

The optional native GUI now stores fictional login/card/note records, long notes, folder/tag strings, stars and Trash flags in a strict experimental encrypted envelope. Save/star/Trash/Undo operations publish on disk before changing the visible model; Save Changes navigation/close waits for publication. The integration harness uses real encryption/files/transactions with an injected provider and proves disk reload after shared locking, new notes, state toggles and stale-write preservation of both external bytes and unsaved drafts. All 38 model checks pass. Unknown/future fields or versions and owner changes fail closed; other supported KDBX custom metadata is preserved.

The latest full foundation suite passes 46 Rust unit checks, eight transaction tests, three dependency-hardening checks, eleven material-session checks, eight multi-vault scenarios, native persistence and record/model workflows, Clippy, release/native builds, local file/Drive checks and iOS Rust type checks. Its source hashes identify the current tested core. The two opt-in external-reader cases were not repeated in this invocation, and the experimental preview envelope is not an interoperability claim. Signed and unprotected preview builds are checked separately.

Parent production gates remain open. The envelope covers only the sample UI and is not the reviewed full PWDTWO schema. Fixture files and protected keys are deleted on normal exit; unsaved drafts/generator history remain in memory. Full history/attachments/conflicts, descriptor-relative filesystem hardening, physical power-loss durability, calibrated memory policy, production setup/recovery, OS lifecycle, supported-old-OS runtime and provider tests remain pending. [Local contract](../dev/experiments/foundation/README.md#local-encrypted-transactions--2026-10-10), [current suite](../dev/experiments/foundation/results/run-all.json), [preview procedure](../dev/macos-preview/README.md).


## Native persistent local-vault experiment — 2026-10-10

The separate `PWDTWO Local Vault.app` now provides native password-based setup/opening and offline recovery for one retained local test vault. Creation/recovery are staged until explicit acknowledgement of the new recovery key; publication uses the existing authenticated revision/CAS writer. Recovery preserves entries while replacing both credentials. Quitting preserves the encrypted file, and a fresh process/controller reopens saved entries by password. Cancelling unconfirmed creation/recovery publishes nothing. Native setup layout was inspected without creating a user vault.

The native lifecycle and controller/model harnesses use disposable directories and check actual encryption/reopening, mandatory acknowledgement, wrong-password/key failure, old-secret rejection, new recovery-key verification, retained records, cancellation, stale writers, generation retirement, permissions, no-follow reads and backup exclusion. Model checks increase to 41. The isolated persistent build does not enroll biometric items, change either existing preview mode or close any production parent gate.

[Procedure and explicit limits](../dev/macos-preview/README.md#experimental-persistent-local-vault), [curated evidence](../dev/experiments/foundation/results/local-lifecycle-summary.json). The full production schema, encrypted draft/generated-history storage, multiple vaults, persistent Touch ID/password-change UI, provider/OS/old-OS validation and the D02–D05 reviews remain open.


## Persistent local Touch ID adapter — 2026-10-10

The persistent development app now has password-authorized opt-in enrollment in native Security & Unlocking settings and a Touch ID action on the locked screen. Its separately provisioned app/Keychain group retains an owned current-enrollment/device-only component across normal quits. Every biometric opening still authenticates the retained encrypted file. Recovery retires the old enrollment; external credential replacement rejects/removes a stale component; password opening remains available.

Controlled-adapter encrypted-file integration, the existing password/recovery controller workflow, 41 model checks and updated local lifecycle checks pass. A separately provisioned prompt-free synthetic probe passes protected item creation, attribute detection, unauthenticated-read denial and exact-item cleanup. Local app signature/isolated entitlements and both previous UI configurations compile/verify as applicable. This slice did not rerun the full Rust/provider suite or request a fingerprint; actual persistent GUI enrollment/unlock awaits the user. [Curated targeted evidence](../dev/experiments/foundation/results/persistent-touch-id-summary.json).


## Multiple persistent local vaults — 2026-10-10

The native development app can add independently protected local vaults through a focused setup sheet, keeping the existing personal file and enrollment. Additional files use canonical UUID owners supported by the strict experimental envelope. Session opening collects separate passwords and/or one grouped protected-key authorization, authenticates every included member, then publishes all records together. Exclusion preserves the file/key; unavailable registrations stay visible for an explicit user decision rather than being silently dropped. Recovery targets one member and does not expose a partial included session.

45 model checks and the real-encryption multi-vault/controller workflows pass, covering independent saves, cancellation, wrong last password, mixed/grouped authorization, restart membership, unavailable files, owner-scoped drafts and targeted recovery. The complete foundation runner passes 47 unit + eight transaction checks and the existing native/platform/offline workflows. Production D02–D05 gates remain open. Names are retained only inside encrypted files; extra unopened vaults have opaque labels after restart, and the evaluation is bounded to 16 members. The user confirmed the prior single-vault Touch ID feature works; that is not new multi-vault hardware evidence.


## Ordinary local password-change UI — 2026-10-10

A native selected-vault sheet now connects the existing shared-core password-change operation to persistent local vaults. Current-password entry is mandatory after Touch ID opening; ordinary changes preserve the recovery key and supported payload. Targeted enrollment retirement precedes revision-guarded publication, without changing other vaults. Wrong credentials/cancel retain the current session; stale or unconfirmed publication requires shared reopening.

51 model checks, the new real-encryption credential-change workflow, existing persistent/multiple-vault/biometric harnesses and the full foundation runner pass. Isolated native Settings/File routes, layout, empty-form gate and cancellation were inspected; no user-present credential-change or sensor outcome is claimed. [Current-source evidence](../dev/experiments/foundation/results/password-change-summary.json). Parent production tasks/gates remain open.


## Local device-preference/clipboard adapter — 2026-10-10

The persistent Mac app retains four non-secret device preferences (masking, shared timeout, optional clipboard clearing and delay), keeping accepted defaults and bounded local scope. One clipboard adapter routes explicit sensitive/recovery Copy buttons, tracks the app's ownership token without reading/retaining clipboard plaintext, preserves later copies, continues maintenance while locked and performs opted-in quit cleanup.

58 model/26 settings-clipboard checks, prior local encryption/controller/authentication regressions, both sample native compiles, final signing and fixed empty-folder native Settings inspection pass. UI-test launch/isolation and initial empty-catalog errors are recorded in tasks E33/E34 with regression guards. No new Rust/provider/sensor claim or production adoption is made. [Current-source evidence](../dev/experiments/foundation/results/device-preferences-summary.json).


## Manual encrypted backup export — 2026-10-10

The Mac development app now reviews one open vault's saved-item/Trash scope and exports its authenticated encrypted file through a native save dialog. Copies retain the original generation's password/recovery protection, include all currently supported saved contents and exclude unsaved drafts and biometric material. This manual action adds no automatic backups. The existing pending-edit gate applies before export.

61 model/26 device checks and the targeted real-encryption backup harness pass with prior local/controller/controlled-biometric/multiple-vault/password-change regressions. Backup checks cover byte identity, current-password/original-key reopening, Trash, credential-generation independence, live-file/alias/link rejection, cancellation, injected publication failures and destination races. The full foundation runner was not rerun after the Swift snapshot addition; Rust was unchanged. Restore UI, full-schema packaging, scheduler/provider coordination and D02–D05 production gates remain open. Existing-destination revision checking plus an advisory lock does not establish atomic CAS against non-cooperating external writers.

Isolated native checks verify both entry routes, per-vault targeting, cancellation, the corrected single-extension filename and a successful encrypted save matching the fixture source at mode 0600. Published Apple Development signature verification passes. [Curated current-source evidence](../dev/experiments/foundation/results/manual-backup-export-summary.json).


## Separate local restoration — 2026-10-10

A captured backup can be authenticated and reviewed before creating a separate local vault. Password restoration keeps its existing credentials; recovery requires a chosen password and acknowledged replacement key. Application owner/entry identities are reassigned through an explicit core copy operation that requires every supported field to remain unchanged. Existing vaults and the user-managed source remain intact; the copy has no provider binding or inherited biometric item. Locked included groups remain locked until all members authenticate; an empty catalog can open the restored vault directly.

Security locking/cancellation retires the review and core work, including timeout maintenance for a review started while locked. Create-only publication on Apple targets excludes an external creation at the final gate. Complete production schema/date packaging, whole-vault replacement, selective copying, provider identity design and D02–D05 gates remain open.


67 model/26 device checks, restoration/export and prior local regressions pass. The complete foundation runner passes 48 Rust unit + nine transaction checks, required lint/release/native/offline/iOS-target checks; all 26 foundation hashes match. Both earlier native variants compile and the published development signature verifies. Isolated native testing verifies both restore entry routes, captured-file review, immediate contents, untouched source/originals and fresh grouped reopening. [Curated current-source evidence](../dev/experiments/foundation/results/backup-restoration-summary.json). Parent production tasks remain open.


## Selected-entry local copying — 2026-10-10

The Mac development app can review and copy active entries from one unlocked vault into another, with an existing destination folder or top level. Originals and existing destination entries remain intact; new IDs and destination protection make each copy independent. Supported fields, notes, tags and favorites survive. A typed core plan authenticates both containers and publishes copies with an encrypted operation receipt in one destination transaction. Same-operation replay is a no-op; conflicting plans, stale files and invalid identities are rejected. Receipt retention survives ordinary edits/removal and is explicitly bounded.

71 model/26 device checks, real-encryption copy/export/restore and prior local regressions pass. The complete foundation runner passes 49 Rust unit and nine transaction checks, required lint/release/native/offline/iOS-target checks; all 26 source hashes match. Both prior native variants compile; published development signing verifies. Isolated native icon/File/context-menu routes, cancellation, bulk selection, folder review, immediate contents and fresh-process reopening pass. Source bytes remain unchanged; independent destination copies preserve all current fields. [Curated evidence](../dev/experiments/foundation/results/cross-vault-copy-summary.json).

This completes an experimental copy slice only. Parent completion stays 3/96. Move, interrupted-operation resume UI, complete history/attachment/organization schema, provider integration and D02–D05 production reviews remain open. Existing-file advisory/revision checks do not provide atomic CAS against non-cooperating external writers.
