# PWDTWO — Development task list

Created 2026-10-09 from the accepted functional, architecture and UX documents using the 66-fetch-tasks workflow. This is a planning artifact. The user approved the phase plan on 2026-10-09; it is now the implementation baseline. Approval selects the sequence and scope, not release dates or completion of technical gates. No application development or publication is performed by this document.

All accepted scope is retained. The approved release phases below overlay the existing dependency/work-area groupings; task IDs and source references remain stable. Mac is the first running application for feedback; iPhone, iPad and Android remain separate required products. 3 of 96 development tasks are complete; 93 remain pending. Existing experiments are evidence, not completed production features.

## Approved development phases

**Status: approved by the user on 2026-10-09.** The goal is a useful running Mac application first, then dependable Mac sync/autofill, then access from the separate iPhone, iPad and Android applications. Advanced credentials, sharing and health tools follow that cross-device foundation. Every accepted feature remains assigned; later delivery does not remove it from scope. No dates are estimated before the unresolved technical gates are measured.

| Phase | Usable outcome | Main scope | Exit condition |
| --- | --- | --- | --- |
| **P0 — Foundation and interactive Mac preview** | A native Mac interface to try with sample data; documented production design decisions. | Build/repository baseline, format and recovery selection, real provider experiments, shared-core bindings, Mac authentication probes; interactive Liquid Glass navigation, search, editing and generator preview. | Sample-data UI runs; D02/D03 and shared-core boundaries have reviewed outcomes, D04 has a provider-backed design, and real Mac biometric behavior is established. UI feedback can begin before the other experiments finish. |
| **MVP — Offline Mac vault** | A usable dedicated Mac development build with durable local vaults. | Multiple independently protected vaults; shared unlock/lock session, Touch ID and recovery; logins, cards, identities, notes and attachments; search, password/passphrase generation and retained history; folders/tags/favorites, entry history, Trash and cross-vault copy/move; manual encrypted backup/restore; imports from all four agreed sources; local diagnostics and native Settings. | Local CRUD, recovery, lock/draft handling, imports and backup restoration pass on both supported Mac generations. Relevant security, accessibility and preservation reviews pass. No cloud or browser completion is implied. |
| **R1 — Release 1: Mac for everyday use** | The first planned public Mac release, with sync and autofill. | Both Google Drive and iCloud Drive; conflicts, credential-change handling, device status, local/cloud deletion and provider migration; the optional single scheduled backup with designated writer; Safari/Chrome login filling and save/update, compatible Mac app autofill; CSV/KDBX migration exports; sync/backup notifications; Sparkle and notarized GitHub download linked from 66ideas.com. | Real multi-Mac/provider fault cases preserve data, installed browser integrations pass, backups survive handover/failure, and the scoped signed/notarized release passes its checks. |
| **R2 — Release 2: iPhone and iPad** | Two separate native Apple mobile apps using the same vaults. | Dedicated Liquid Glass iPhone tabs and adaptive iPad layouts; released vault features, offline use, recovery/biometrics, both providers, backup/restore, attachments and diagnostics; Safari and compatible-app login autofill/save flows, native setup guidance and App Store preparation. | Mac↔iPhone↔iPad sync and recovery work on both supported OS generations, with real biometric/extension and background-execution tests. Each product passes its own store/release checks. |
| **R3 — Release 3: Android** | A dedicated native Android app, completing the initial four-platform goal. | Kotlin/Compose with Material 3, phone/tablet adaptation; parity with released vault workflows, offline access, Google Drive, recovery/biometrics, Chrome and compatible-app login autofill/save flows, backup scheduling and Google Play preparation. | Actual Apple↔Android Drive synchronization, native autofill and backup-device handover work on both supported Android generations. Local-only behavior and release/update preservation pass. |
| **R4 — Release 4: advanced capabilities across the apps** | The remaining agreed feature set on supported native surfaces. | Passkey creation/use/sync and supported transfers; QR/manual authenticator setup and code filling; weak/reused-password health and opt-in free HIBP checks; equal-access shared vaults with secure credential delivery; encrypted independent copies; reviewed card/identity autofill. Extend every app, extension, migration/backup path and relevant notification category. | Actual cross-platform ceremonies, sharing/recovery, full-content round trips and the remaining UX requirements pass. Unsupported platform transfer/fill routes are stated explicitly; final integrated security, compatibility and release review is complete. |

### Why this sequence

- P0 provides something tangible to use early, without waiting for the full vault engine or mobile apps. The existing feasibility window is not this interactive preview.
- The MVP includes recovery, retained history/Trash and manual encrypted backup/restore from the start. Scheduled backups remain a later opt-in feature; they are not a substitute for a manual recovery path.
- R1 proves the shared storage protocol and browser boundaries on Mac before bringing more device types into the synchronization matrix. Both providers remain required, one provider per vault.
- R2 and R3 deliver the principal cross-device benefit ahead of advanced features. The iPhone and iPad remain distinct products, not ports used to replace the Mac app.
- R4 groups the more complex native credential and sharing work on top of tested device/cloud foundations. Early feasibility probes still happen in P0 or before dependent work, so unsupported assumptions are discovered ahead of implementation.

Liquid Glass, platform conventions, accessibility, clear offline state and the eight accepted delightful touches apply from the first relevant UI. Security, testing, performance and diagnostics are continuous work, not a final cleanup phase. All phases preserve the MIT licence, no application-operated backend direction, on-device diagnostics, current/previous OS support and accepted privacy/default settings.

### Task allocation and split-task rules

Each of the 96 existing tasks has an **Approved delivery** line below. A task assigned to several phases is an umbrella task: implement and verify only the explicitly described phase/platform slice, leaving its parent checkbox open until all slices and original acceptance criteria are complete. Phase labels do not replace the source requirements.

For planning and evidence, identify slices as `T054/MVP`, `T079/R2`, etc. Do not mark a slice complete merely because a later feature is hidden. For each slice, record implemented behavior, applicable prerequisite slices and validation evidence. Existing `Depends on` lists describe full-task closure; the following explicit splits define which prerequisites apply to earlier deliverables. A prior-phase implementation may provide a required shared component without the entire cross-platform parent being finished.

| Tasks | Approved slice and prerequisite treatment |
| --- | --- |
| T007–T010 | P0 proves the real provider protocol on Mac, shared bindings/target viability and Mac biometric unlocking. R1 completes installed Mac login integrations. R2/R3 validate the corresponding mobile secure-storage, provider and credential surfaces before enabling them. R4 validates passkeys, card/identity authorization and sharing capabilities before those ship. Keep failed capability probes visible. |
| T011, T013–T014 | Settle MVP bounds and all schema/versioning requirements early. Defer detailed advanced-feature behavior to R4 while ensuring earlier clients preserve or safely reject unsupported data. The approved D02/D03/D04/core-boundary decisions still precede production core implementation. |
| T018–T019, T032 | MVP implements and verifies Mac secure storage, shared-session locking and local-only backup exclusion. R2 implements and verifies iPhone/iPad adapters; R3 does Android. Shared session policy and per-vault protection never become optional to accelerate a phase. |
| T023–T026, T041 | MVP includes native attachment handling and complete history/Trash for the record types it exposes. T041/MVP has no dependency on the later T030 authenticator UI; R4 adds that code presentation and passkey/history/index cases. Preserve all supported fields and referenced bytes at every stage. |
| T034–T035, T042–T043 | MVP provides local creation/opening/settings and verifies that slice; cloud choices are connected and verified in R1, with advanced settings in R4. T043/MVP requires the MVP slices of T034–T042, not later OTP/cloud features. Unimplemented operations are not presented as working. |
| T051 | MVP provides local-only deletion and removal of local unlock/draft/index data after T026, T032 and native vault management; it does not depend on cloud adapters. R1 adds remote deletion, confirmed-deletion discovery, backup retirement and pending-cleanup handling after T045–T050. |
| T053–T054 | T054/MVP implements manual encrypted export and local separate-vault restore after T017, T027 and the reviewed backup packaging/storage design. It does not depend on the cloud scheduler in T053. R1 adds the complete T053 scheduler/handover and T054 cloud file selection/replacement coordination. Original backup credentials, validation and full-content preservation remain mandatory in both slices. |
| T055–T056 | MVP history/Trash UI depends on local T024–T026 and T039, not T049 sync review. MVP copy/move UI follows T027/T038; selective recovery also uses T054/MVP. R1 adds concurrent sync/conflict presentation. |
| T057–T058 | All four agreed Mac import sources are in MVP using their then-supported export routes. Preview and report fields/types not yet supported; never silently claim a complete migration. R1 adds the two migration-export formats. R4 extends coverage for newly supported content where the external formats permit it. |
| T062–T063, T067–T070 | R1 provides destination-bound login grants, trusted IPC, both browsers, Mac application fill and optional onboarding. T070/R1 does not await passkeys. R4 adds OTP/card/identity fills and passkeys, after T030/T061 and the relevant real-platform capability probes. |
| T074 | R1 enables only the implemented conflict/sync/backup categories after T049/T050/T053; it does not await T072 leak checks. R2/R3 add native mobile notifications, and R4 adds the leak category after T072. All payloads stay generic with per-device controls. |
| T079–T080 | R2 runs these tasks for iPhone/iPad after T076/T077 and Apple prerequisite slices; it does not depend on T078 or Android validation. R3 runs the Android slice after T078. T080 initially connects released sync/storage/backup workflows; its T059/T060 sharing dependency applies to the R4 sharing slice only. |
| T081–T082 | R2/R3 implement password login filling/capture for their native supported browser/app surfaces after T062 and the respective platform T079 slice. T030 and reviewed card/identity flows are prerequisites of their R4 enhancements, not the earlier password-only integration. |
| T083–T084 | T083 is the R4 passkey work. T084/R2 and T084/R3 implement all already-released features in the respective native UI and depend on those features/platform adapters only. Advanced health, sharing, OTP/card fills and passkeys depend on T030/T059–T061/T067/T071–T073/T083 in T084/R4. Mac-only external import/export remains Mac-only in every phase. |
| T085 | R2/R3 validate their native sync and backup scheduling before release after the corresponding T080/T084 slices. Leak-check scheduling and advanced notification behavior enter R4 after T072 and their native UI; do not hold ordinary mobile sync validation until then. |
| T086–T090 | Run relevant accessibility, performance, security, preservation and UX checks for every deliverable: synthetic-preview UX in P0, offline Mac checks in MVP, Mac cloud/browser checks in R1, Apple mobile in R2, Android in R3 and integrated advanced features in R4. Their broad dependencies apply only when those components are included; R4 closes the full checklist. This does not waive security review of any earlier released code. |
| T091–T096 | R1 includes Sparkle and the Mac portions of security/end-to-end/UX checks, documentation and readiness before T092 Mac publication preparation. R2 independently prepares the two Apple mobile products through T093; R3 prepares Android through T094. Their scoped readiness checks do not await another platform’s store artifact. R4 updates every release path and completes overall readiness; each earlier release requires its own complete scoped checks. |

### Phase completion records

| Phase | Required review evidence before completion |
| --- | --- |
| P0 | Running sample-data Mac preview; recorded gate decisions and remaining platform-specific probes. No real-vault security claims based on the preview. |
| MVP | Successful local save/restart, lock/draft/recovery and backup restoration on supported Macs; imported-content results; reviewed production crypto/persistence and native UX. Treat as a development build, not an automatic public launch. |
| R1 | Actual provider race/recovery tests, browser/native-app login tests, single-backup handover tests, all Mac release-scope reviews, verified updater and notarized artifacts. |
| R2 | Separate iPhone/iPad native behavior and physical-device security checks; live Mac/Apple-mobile sync, offline, autofill and background tests; platform-specific release preparation. |
| R3 | Real Apple/Android Drive interoperability and native Android security/autofill tests, supported-device performance and Google Play preparation. |
| R4 | Advanced native credential/transfer/sharing tests, full preservation and UX coverage, closed remaining task slices and integrated release/security evidence. |

Track the approved slices as actionable work items while retaining the parent IDs and traceability. Public source/release preparation is included; recording this approval does not publish software, sign in to providers or complete implementation work. Phase assignments may be revised from running-app feedback and measured technical results without silently dropping features.

## Source requirements and traceability

`F01–F47` refer to the original numbered functional stories in [specifications.md](specifications.md); `A01–A46` to [architecture.md](architecture.md); `UX01–UX50` to [ux.md](ux.md); `C1–C4` to [constitution.md](constitution.md). These prefixes disambiguate existing IDs without renumbering their source documents. `D01–D05` are the architecture gates. Titles below are copied from the sources.

Every mapped task inherits the complete acceptance criteria and constraints of its cited sources; its completion outcome below supplements rather than replaces them. Functional Common behavior, the architecture’s detailed decisions and the UX accessibility/review guidance apply across tasks. The register provides coverage, not evidence that a requirement has been implemented.

### Technical requirements

| Source ID | Requirement | Development tasks |
| --- | --- | --- |
| [A01](architecture.md#1-explore-operation-without-an-application-operated-backend) | Explore operation without an application-operated backend. | [T001](#t001), [T004](#t004), [T044](#t044), [T060](#t060) |
| [A02](architecture.md#2-persist-and-process-vault-data-on-the-device) | Persist and process vault data on the device. | [T008](#t008), [T013](#t013), [T014](#t014), [T015](#t015), [T021](#t021), [T022](#t022), [T029](#t029), [T030](#t030), [T032](#t032), [T037](#t037), [T043](#t043), [T047](#t047), [T050](#t050), [T087](#t087) |
| [A03](architecture.md#3-use-separate-storage-provider-adapters) | Use separate storage-provider adapters. | [T007](#t007), [T008](#t008), [T035](#t035), [T044](#t044), [T045](#t045), [T046](#t046), [T047](#t047), [T050](#t050), [T080](#t080), [T085](#t085) |
| [A04](architecture.md#4-isolate-vault-keys-and-recovery-paths) | Isolate vault keys and recovery paths. | [T004](#t004), [T006](#t006), [T010](#t010), [T016](#t016), [T017](#t017), [T018](#t018), [T019](#t019), [T036](#t036), [T048](#t048), [T079](#t079), [T088](#t088) |
| [A05](architecture.md#5-preserve-concurrent-changes-durably) | Preserve concurrent changes durably. | [T007](#t007), [T008](#t008), [T014](#t014), [T015](#t015), [T023](#t023), [T025](#t025), [T026](#t026), [T027](#t027), [T047](#t047), [T048](#t048), [T049](#t049), [T055](#t055), [T056](#t056), [T087](#t087), [T089](#t089) |
| [A06](architecture.md#6-separate-vault-logic-from-platform-integrations) | Separate vault logic from platform integrations. | [T004](#t004), [T009](#t009), [T010](#t010), [T013](#t013), [T019](#t019), [T043](#t043), [T062](#t062), [T063](#t063), [T068](#t068), [T079](#t079), [T081](#t081), [T082](#t082), [T088](#t088) |
| [A07](architecture.md#7-treat-kdbx-as-a-conditional-format-choice) | Treat KDBX as a conditional format choice. | [T005](#t005), [T006](#t006), [T014](#t014), [T015](#t015), [T058](#t058), [T087](#t087), [T088](#t088), [T089](#t089), [T095](#t095) |
| [A08](architecture.md#8-make-backups-independent-of-synchronization-history) | Make backups independent of synchronization history. | [T007](#t007), [T008](#t008), [T027](#t027), [T031](#t031), [T053](#t053), [T054](#t054), [T056](#t056), [T080](#t080), [T085](#t085), [T089](#t089) |
| [A09](architecture.md#9-evaluate-provider-based-sharing-of-separate-encrypted-containers) | Evaluate provider-based sharing of separate encrypted containers. | [T004](#t004), [T007](#t007), [T045](#t045), [T046](#t046), [T059](#t059), [T060](#t060), [T080](#t080), [T088](#t088) |
| [A10](architecture.md#10-transfer-encrypted-individual-copies-without-expiring-links) | Transfer encrypted individual copies without expiring links. | [T004](#t004), [T059](#t059), [T088](#t088) |
| [A11](architecture.md#11-exclude-trusted-contact-emergency-access) | Exclude trusted-contact emergency access. | [T001](#t001), [T060](#t060) |
| [A12](architecture.md#12-use-provider-authorization-and-local-vault-unlocking-for-device-setup) | Use provider authorization and local vault unlocking for device setup. | [T001](#t001), [T004](#t004), [T017](#t017), [T034](#t034), [T035](#t035), [T044](#t044), [T060](#t060) |
| [A13](architecture.md#13-build-four-separate-native-applications) | Build four separate native applications. | [T002](#t002), [T009](#t009), [T033](#t033), [T076](#t076), [T077](#t077), [T078](#t078), [T093](#t093), [T094](#t094) |
| [A14](architecture.md#14-recommend-swift-for-each-apple-application) | Recommend Swift for each Apple application. | [T002](#t002), [T033](#t033), [T064](#t064), [T068](#t068), [T076](#t076), [T077](#t077), [T081](#t081), [T093](#t093) |
| [A15](architecture.md#15-recommend-kotlin-for-the-android-application) | Recommend Kotlin for the Android application. | [T002](#t002), [T078](#t078), [T082](#t082), [T094](#t094) |
| [A16](architecture.md#16-share-one-native-vault-library-across-four-separate-applications) | Share one native vault library across four separate applications. | [T003](#t003), [T005](#t005), [T009](#t009), [T013](#t013), [T087](#t087), [T088](#t088) |
| [A17](architecture.md#17-keep-browser-automation-separate-from-native-application-views) | Keep browser automation separate from native application views. | [T010](#t010), [T062](#t062), [T063](#t063), [T064](#t064), [T065](#t065), [T066](#t066), [T067](#t067), [T069](#t069), [T070](#t070), [T081](#t081), [T082](#t082), [T088](#t088) |
| [A18](architecture.md#18-support-the-current-and-previous-major-os-generations) | Support the current and previous major OS generations. | [T002](#t002), [T076](#t076), [T077](#t077), [T078](#t078), [T089](#t089), [T092](#t092), [T093](#t093), [T094](#t094), [T096](#t096) |
| [A19](architecture.md#19-support-apple-silicon-exclusively-on-macos) | Support Apple silicon exclusively on macOS. | [T002](#t002), [T033](#t033), [T092](#t092) |
| [A20](architecture.md#20-distribute-the-notarized-mac-application-through-github-and-66ideascom) | Distribute the notarized Mac application through GitHub and 66ideas.com. | [T001](#t001), [T091](#t091), [T092](#t092), [T095](#t095), [T096](#t096) |
| [A21](architecture.md#21-publish-the-application-source-under-the-mit-licence) | Publish the application source under the MIT licence. | [T001](#t001), [T003](#t003), [T075](#t075), [T092](#t092), [T093](#t093), [T094](#t094), [T095](#t095), [T096](#t096) |
| [A22](architecture.md#22-distribute-mobile-applications-through-the-platform-stores) | Distribute mobile applications through the platform stores. | [T002](#t002), [T076](#t076), [T077](#t077), [T078](#t078), [T093](#t093), [T094](#t094), [T095](#t095), [T096](#t096) |
| [A23](architecture.md#23-bind-each-synchronized-vault-to-one-cloud-provider) | Bind each synchronized vault to one cloud provider. | [T007](#t007), [T008](#t008), [T044](#t044), [T045](#t045), [T046](#t046), [T052](#t052), [T080](#t080), [T089](#t089) |
| [A24](architecture.md#24-use-sparkle-for-built-in-macos-updates-following-md22) | Use Sparkle for built-in macOS updates, following MD22. | [T091](#t091), [T092](#t092), [T095](#t095) |
| [A25](architecture.md#25-use-pwdtwo-as-the-application-name) | Use PWDTWO as the application name. | [T002](#t002), [T003](#t003), [T033](#t033), [T042](#t042), [T092](#t092), [T093](#t093), [T094](#t094), [T095](#t095) |
| [A26](architecture.md#26-support-local-only-vault-storage) | Support local-only vault storage. | [T015](#t015), [T032](#t032), [T034](#t034), [T051](#t051), [T052](#t052), [T079](#t079), [T080](#t080) |
| [A27](architecture.md#27-migrate-vaults-between-local-and-cloud-storage) | Migrate vaults between local and cloud storage. | [T007](#t007), [T008](#t008), [T052](#t052), [T080](#t080), [T089](#t089) |
| [A28](architecture.md#28-keep-diagnostics-on-device-with-deliberate-support-exports) | Keep diagnostics on-device with deliberate support exports. | [T075](#t075), [T095](#t095) |
| [A29](architecture.md#29-keep-attachments-within-the-complete-local-vault) | Keep attachments within the complete local vault. | [T005](#t005), [T014](#t014), [T015](#t015), [T023](#t023), [T041](#t041), [T080](#t080), [T087](#t087) |
| [A30](architecture.md#30-resolve-import-duplicates-without-silent-replacement) | Resolve import duplicates without silent replacement. | [T011](#t011), [T057](#t057), [T058](#t058) |
| [A31](architecture.md#31-match-website-credentials-to-explicitly-approved-hosts) | Match website credentials to explicitly approved hosts. | [T011](#t011), [T062](#t062), [T064](#t064), [T065](#t065), [T081](#t081), [T082](#t082), [T088](#t088) |
| [A32](architecture.md#32-generate-passwords-and-english-passphrases-locally) | Generate passwords and English passphrases locally. | [T011](#t011), [T028](#t028), [T031](#t031), [T040](#t040) |
| [A33](architecture.md#33-make-leaked-password-checks-opt-in-through-hibp) | Make leaked-password checks opt-in through HIBP. | [T011](#t011), [T031](#t031), [T072](#t072), [T085](#t085) |
| [A34](architecture.md#34-organize-each-vault-with-nested-folders-and-multiple-tags) | Organize each vault with nested folders and multiple tags. | [T008](#t008), [T014](#t014), [T024](#t024), [T026](#t026), [T047](#t047), [T055](#t055) |
| [A35](architecture.md#35-make-password-clipboard-clearing-optional) | Make password clipboard clearing optional. | [T011](#t011), [T031](#t031), [T039](#t039), [T079](#t079) |
| [A36](architecture.md#36-keep-system-notification-content-generic) | Keep system notification content generic. | [T031](#t031), [T074](#t074), [T085](#t085) |
| [A37](architecture.md#37-separate-synchronized-vault-settings-from-device-preferences) | Separate synchronized vault settings from device preferences. | [T008](#t008), [T014](#t014), [T023](#t023), [T031](#t031), [T042](#t042), [T047](#t047), [T053](#t053), [T072](#t072), [T074](#t074) |
| [A38](architecture.md#38-preserve-optional-card-and-identity-fields-across-native-clients) | Preserve optional card and identity fields across native clients. | [T010](#t010), [T011](#t011), [T014](#t014), [T022](#t022), [T041](#t041), [T062](#t062), [T067](#t067), [T081](#t081), [T082](#t082) |
| [A39](architecture.md#39-make-sensitive-value-masking-configurable) | Make sensitive-value masking configurable. | [T022](#t022), [T031](#t031), [T039](#t039) |
| [A40](architecture.md#40-scope-password-health-exceptions-to-specific-findings) | Scope password-health exceptions to specific findings. | [T008](#t008), [T014](#t014), [T047](#t047), [T071](#t071), [T073](#t073) |
| [A41](architecture.md#41-preserve-passkey-lifecycle-and-sharing-semantics) | Preserve passkey lifecycle and sharing semantics. | [T005](#t005), [T010](#t010), [T014](#t014), [T026](#t026), [T061](#t061), [T069](#t069), [T083](#t083), [T088](#t088) |
| [A42](architecture.md#42-keep-minimal-encrypted-device-status-records) | Keep minimal encrypted device-status records. | [T008](#t008), [T014](#t014), [T047](#t047), [T050](#t050) |
| [A43](architecture.md#43-preserve-unsaved-edits-as-encrypted-local-drafts) | Preserve unsaved edits as encrypted local drafts. | [T020](#t020), [T038](#t038), [T079](#t079) |
| [A44](architecture.md#44-separate-local-vault-removal-from-cloud-file-deletion) | Separate local vault removal from cloud-file deletion. | [T007](#t007), [T008](#t008), [T051](#t051), [T053](#t053) |
| [A45](architecture.md#45-reauthorize-biometric-unlocking-after-enrollment-changes) | Reauthorize biometric unlocking after enrollment changes. | [T006](#t006), [T010](#t010), [T018](#t018), [T019](#t019), [T079](#t079), [T088](#t088) |
| [A46](architecture.md#46-apply-a-length-based-policy-to-newly-chosen-vault-passwords) | Apply a length-based policy to newly chosen vault passwords. | [T006](#t006), [T011](#t011), [T016](#t016), [T017](#t017), [T034](#t034) |

### Architecture gates

| Source ID | Requirement | Development tasks |
| --- | --- | --- |
| [D01](architecture.md#decisions-required-before-core-development) | Service responsibilities for sharing and device setup. | [T004](#t004), [T007](#t007), [T059](#t059), [T060](#t060), [T096](#t096) |
| [D02](architecture.md#decisions-required-before-core-development) | Native vault format and compatibility. | [T005](#t005), [T013](#t013), [T088](#t088), [T096](#t096) |
| [D03](architecture.md#decisions-required-before-core-development) | Encryption, recovery, and key lifecycle. | [T004](#t004), [T006](#t006), [T013](#t013), [T048](#t048), [T088](#t088), [T096](#t096) |
| [D04](architecture.md#decisions-required-before-core-development) | Synchronization, deletion, and provider migration. | [T007](#t007), [T008](#t008), [T013](#t013), [T044](#t044), [T048](#t048), [T052](#t052), [T088](#t088), [T096](#t096) |
| [D05](architecture.md#decisions-required-before-core-development) | Shared core and platform integration boundaries. | [T004](#t004), [T009](#t009), [T010](#t010), [T013](#t013), [T018](#t018), [T063](#t063), [T088](#t088), [T096](#t096) |

### Functional requirements

| Source ID | Requirement | Development tasks |
| --- | --- | --- |
| [F01](specifications.md#1-access-the-password-manager-on-supported-devices) | Access the password manager on supported devices. | [T002](#t002), [T012](#t012), [T033](#t033), [T043](#t043), [T076](#t076), [T077](#t077), [T078](#t078), [T089](#t089), [T092](#t092), [T093](#t093), [T094](#t094), [T096](#t096) |
| [F02](specifications.md#2-search-for-passwords) | Search for passwords. | [T021](#t021), [T037](#t037), [T043](#t043), [T087](#t087) |
| [F03](specifications.md#3-save-login-entries) | Save login entries. | [T014](#t014), [T015](#t015), [T022](#t022), [T038](#t038), [T043](#t043), [T084](#t084) |
| [F04](specifications.md#4-autofill-credentials-from-the-browser) | Autofill credentials from the browser. | [T010](#t010), [T031](#t031), [T062](#t062), [T063](#t063), [T064](#t064), [T065](#t065), [T070](#t070), [T081](#t081), [T082](#t082), [T089](#t089) |
| [F05](specifications.md#5-synchronize-credentials-across-devices) | Synchronize credentials across devices. | [T007](#t007), [T008](#t008), [T044](#t044), [T045](#t045), [T046](#t046), [T047](#t047), [T080](#t080), [T085](#t085), [T089](#t089) |
| [F06](specifications.md#6-generate-passwords) | Generate passwords. | [T011](#t011), [T028](#t028), [T031](#t031), [T040](#t040), [T043](#t043), [T066](#t066), [T084](#t084) |
| [F07](specifications.md#7-use-the-password-manager-offline) | Use the password manager offline. | [T015](#t015), [T032](#t032), [T033](#t033), [T043](#t043), [T047](#t047), [T079](#t079), [T080](#t080), [T087](#t087), [T089](#t089) |
| [F08](specifications.md#8-autofill-credentials-in-mobile-applications) | Autofill credentials in mobile applications. | [T010](#t010), [T062](#t062), [T081](#t081), [T082](#t082) |
| [F09](specifications.md#9-unlock-with-a-master-password-or-optional-biometrics) | Unlock with a master password or optional biometrics. | [T004](#t004), [T006](#t006), [T010](#t010), [T011](#t011), [T016](#t016), [T017](#t017), [T018](#t018), [T019](#t019), [T031](#t031), [T034](#t034), [T035](#t035), [T042](#t042), [T043](#t043), [T063](#t063), [T079](#t079), [T088](#t088) |
| [F10](specifications.md#10-recover-access-using-a-recovery-key) | Recover access using a recovery key. | [T004](#t004), [T006](#t006), [T008](#t008), [T016](#t016), [T017](#t017), [T018](#t018), [T034](#t034), [T036](#t036), [T043](#t043), [T048](#t048), [T054](#t054), [T060](#t060), [T079](#t079), [T084](#t084), [T088](#t088), [T089](#t089), [T095](#t095) |
| [F11](specifications.md#11-lock-the-vault-automatically) | Lock the vault automatically. | [T010](#t010), [T011](#t011), [T019](#t019), [T031](#t031), [T042](#t042), [T043](#t043), [T063](#t063), [T079](#t079) |
| [F12](specifications.md#12-resolve-conflicting-changes-without-losing-either-version) | Resolve conflicting changes without losing either version. | [T008](#t008), [T047](#t047), [T048](#t048), [T049](#t049), [T074](#t074), [T084](#t084), [T089](#t089) |
| [F13](specifications.md#13-import-existing-passwords) | Import existing passwords. | [T011](#t011), [T057](#t057), [T089](#t089), [T095](#t095) |
| [F14](specifications.md#14-capture-and-update-logins-from-websites) | Capture and update logins from websites. | [T066](#t066), [T081](#t081), [T082](#t082) |
| [F15](specifications.md#15-recover-generated-passwords-from-interrupted-workflows) | Recover generated passwords from interrupted workflows. | [T008](#t008), [T014](#t014), [T029](#t029), [T040](#t040), [T047](#t047), [T066](#t066), [T084](#t084) |
| [F16](specifications.md#16-view-copy-and-edit-credentials-manually) | View, copy, and edit credentials manually. | [T020](#t020), [T022](#t022), [T031](#t031), [T038](#t038), [T039](#t039), [T042](#t042), [T043](#t043), [T079](#t079), [T084](#t084) |
| [F17](specifications.md#17-delete-and-restore-entries) | Delete and restore entries. | [T008](#t008), [T024](#t024), [T026](#t026), [T047](#t047), [T055](#t055), [T084](#t084), [T089](#t089) |
| [F18](specifications.md#18-inspect-and-restore-previous-versions) | Inspect and restore previous versions. | [T005](#t005), [T008](#t008), [T014](#t014), [T023](#t023), [T025](#t025), [T047](#t047), [T055](#t055), [T084](#t084), [T087](#t087), [T089](#t089) |
| [F19](specifications.md#19-choose-accounts-and-match-websites-correctly) | Choose accounts and match websites correctly. | [T011](#t011), [T062](#t062), [T064](#t064), [T065](#t065), [T066](#t066), [T081](#t081), [T082](#t082), [T088](#t088) |
| [F20](specifications.md#20-export-vault-data) | Export vault data. | [T011](#t011), [T058](#t058), [T089](#t089), [T095](#t095) |
| [F21](specifications.md#21-create-and-restore-encrypted-backups) | Create and restore encrypted backups. | [T007](#t007), [T008](#t008), [T011](#t011), [T027](#t027), [T031](#t031), [T042](#t042), [T051](#t051), [T053](#t053), [T054](#t054), [T056](#t056), [T074](#t074), [T080](#t080), [T084](#t084), [T085](#t085), [T089](#t089), [T095](#t095) |
| [F22](specifications.md#22-set-up-a-vault-and-connect-additional-devices) | Set up a vault and connect additional devices. | [T017](#t017), [T034](#t034), [T035](#t035), [T044](#t044), [T070](#t070), [T080](#t080) |
| [F23](specifications.md#23-view-known-device-activity-and-understand-access-controls) | View known device activity and understand access controls. | [T008](#t008), [T050](#t050), [T060](#t060), [T080](#t080), [T095](#t095) |
| [F24](specifications.md#24-see-synchronization-status) | See synchronization status. | [T050](#t050), [T074](#t074), [T080](#t080) |
| [F25](specifications.md#25-create-synchronize-use-and-transfer-passkeys) | Create, synchronize, use, and transfer passkeys. | [T005](#t005), [T010](#t010), [T014](#t014), [T026](#t026), [T058](#t058), [T059](#t059), [T061](#t061), [T069](#t069), [T083](#t083), [T088](#t088), [T089](#t089), [T095](#t095) |
| [F26](specifications.md#26-generate-and-fill-authenticator-codes) | Generate and fill authenticator codes. | [T011](#t011), [T014](#t014), [T030](#t030), [T041](#t041), [T067](#t067), [T081](#t081), [T082](#t082), [T084](#t084) |
| [F27](specifications.md#27-review-password-health) | Review password health. | [T011](#t011), [T071](#t071), [T073](#t073), [T084](#t084) |
| [F28](specifications.md#28-check-passwords-against-known-leaks) | Check passwords against known leaks. | [T011](#t011), [T031](#t031), [T042](#t042), [T072](#t072), [T073](#t073), [T074](#t074), [T084](#t084), [T085](#t085) |
| [F29](specifications.md#29-organize-entries-with-favorites-folders-and-tags) | Organize entries with favorites, folders, and tags. | [T008](#t008), [T014](#t014), [T024](#t024), [T026](#t026), [T037](#t037), [T047](#t047), [T055](#t055), [T084](#t084) |
| [F30](specifications.md#30-store-secure-notes-and-custom-fields) | Store secure notes and custom fields. | [T014](#t014), [T022](#t022), [T038](#t038), [T041](#t041), [T084](#t084) |
| [F31](specifications.md#31-pwdtwo-managed-new-device-verification--removed-from-scope) | PWDTWO-managed new-device verification — removed from scope. **Withdrawn — no feature implementation.** | [T001](#t001) |
| [F32](specifications.md#32-lock-manually-and-change-the-master-password) | Lock manually and change the master password. | [T004](#t004), [T006](#t006), [T008](#t008), [T017](#t017), [T018](#t018), [T019](#t019), [T036](#t036), [T048](#t048), [T079](#t079), [T088](#t088), [T089](#t089) |
| [F33](specifications.md#33-autofill-in-mac-applications) | Autofill in Mac applications. | [T010](#t010), [T062](#t062), [T068](#t068), [T070](#t070) |
| [F34](specifications.md#34-generate-memorable-passphrases) | Generate memorable passphrases. | [T011](#t011), [T028](#t028), [T029](#t029), [T040](#t040), [T084](#t084) |
| [F35](specifications.md#35-share-entries-and-vaults-with-other-people) | Share entries and vaults with other people. | [T004](#t004), [T007](#t007), [T045](#t045), [T046](#t046), [T048](#t048), [T059](#t059), [T060](#t060), [T061](#t061), [T069](#t069), [T080](#t080), [T083](#t083), [T084](#t084), [T088](#t088), [T089](#t089), [T095](#t095) |
| [F36](specifications.md#36-send-an-encrypted-copy-of-an-item) | Send an encrypted copy of an item. | [T004](#t004), [T011](#t011), [T059](#t059), [T060](#t060), [T061](#t061), [T069](#t069), [T080](#t080), [T083](#t083), [T084](#t084), [T088](#t088), [T089](#t089), [T095](#t095) |
| [F37](specifications.md#37-trusted-contact-emergency-access--removed-from-scope) | Trusted-contact emergency access — removed from scope. **Withdrawn — no feature implementation.** | [T001](#t001) |
| [F38](specifications.md#38-store-and-fill-payment-cards-and-identity-information) | Store and fill payment cards and identity information. | [T010](#t010), [T014](#t014), [T022](#t022), [T038](#t038), [T039](#t039), [T041](#t041), [T062](#t062), [T067](#t067), [T081](#t081), [T082](#t082), [T084](#t084) |
| [F39](specifications.md#39-store-documents-and-attachments) | Store documents and attachments. | [T005](#t005), [T011](#t011), [T014](#t014), [T015](#t015), [T023](#t023), [T031](#t031), [T041](#t041), [T042](#t042), [T080](#t080), [T084](#t084), [T087](#t087), [T089](#t089) |
| [F40](specifications.md#40-manage-multiple-independently-protected-vaults) | Manage multiple independently protected vaults. | [T004](#t004), [T008](#t008), [T014](#t014), [T017](#t017), [T019](#t019), [T021](#t021), [T027](#t027), [T032](#t032), [T034](#t034), [T035](#t035), [T037](#t037), [T042](#t042), [T043](#t043), [T051](#t051), [T054](#t054), [T056](#t056), [T079](#t079), [T080](#t080), [T084](#t084), [T089](#t089) |
| [F41](specifications.md#41-synchronize-vault-files-through-icloud-drive-and-google-drive) | Synchronize vault files through iCloud Drive and Google Drive. | [T007](#t007), [T008](#t008), [T035](#t035), [T044](#t044), [T045](#t045), [T046](#t046), [T047](#t047), [T080](#t080), [T085](#t085), [T089](#t089), [T095](#t095) |
| [F42](specifications.md#42-prefer-portable-keepass-compatible-vault-files-where-feasible) | Prefer portable KeePass-compatible vault files where feasible. | [T004](#t004), [T005](#t005), [T006](#t006), [T014](#t014), [T015](#t015), [T058](#t058), [T088](#t088), [T089](#t089), [T095](#t095) |
| [F43](specifications.md#43-add-long-notes-to-every-password-and-credit-card) | Add long notes to every password and credit card. | [T011](#t011), [T014](#t014), [T022](#t022), [T038](#t038), [T041](#t041), [T058](#t058), [T084](#t084), [T087](#t087) |
| [F44](specifications.md#44-update-the-mac-application-from-within-pwdtwo) | Update the Mac application from within PWDTWO. | [T042](#t042), [T091](#t091), [T092](#t092), [T095](#t095) |
| [F45](specifications.md#45-keep-a-vault-local-without-cloud-synchronization) | Keep a vault local without cloud synchronization. | [T015](#t015), [T032](#t032), [T034](#t034), [T043](#t043), [T051](#t051), [T079](#t079), [T080](#t080), [T089](#t089), [T095](#t095) |
| [F46](specifications.md#46-change-an-existing-vaults-storage-mode-or-cloud-provider) | Change an existing vault's storage mode or cloud provider. | [T007](#t007), [T008](#t008), [T052](#t052), [T080](#t080), [T089](#t089), [T095](#t095) |
| [F47](specifications.md#47-share-on-device-diagnostics-in-a-bug-report) | Share on-device diagnostics in a bug report. | [T011](#t011), [T075](#t075), [T084](#t084), [T095](#t095) |

### UX requirements

| Source ID | Requirement | Development tasks |
| --- | --- | --- |
| [UX01](ux.md#1-feel-at-home-on-each-platform) | Feel at home on each platform. | [T002](#t002), [T012](#t012), [T033](#t033), [T076](#t076), [T077](#t077), [T078](#t078), [T086](#t086), [T090](#t090) |
| [UX02](ux.md#2-adopt-liquid-glass-on-apple-platforms) | Adopt Liquid Glass on Apple platforms. | [T002](#t002), [T012](#t012), [T033](#t033), [T076](#t076), [T077](#t077), [T086](#t086), [T090](#t090) |
| [UX03](ux.md#3-follow-established-platform-conventions) | Follow established platform conventions. | [T002](#t002), [T012](#t012), [T033](#t033), [T076](#t076), [T077](#t077), [T078](#t078), [T086](#t086), [T090](#t090) |
| [UX04](ux.md#4-make-everyday-use-delightful) | Make everyday use delightful. | [T012](#t012), [T043](#t043), [T084](#t084), [T086](#t086), [T090](#t090) |
| [UX05](ux.md#5-give-each-vault-a-recognizable-identity) | Give each vault a recognizable identity. | [T012](#t012), [T024](#t024), [T034](#t034), [T037](#t037), [T084](#t084), [T086](#t086), [T090](#t090) |
| [UX06](ux.md#6-make-successful-actions-feel-satisfying) | Make successful actions feel satisfying. | [T012](#t012), [T038](#t038), [T039](#t039), [T084](#t084), [T086](#t086), [T090](#t090) |
| [UX07](ux.md#7-make-the-password-generator-enjoyable-and-readable) | Make the password generator enjoyable and readable. | [T028](#t028), [T040](#t040), [T084](#t084), [T086](#t086), [T090](#t090) |
| [UX08](ux.md#8-make-search-and-quick-actions-feel-effortless) | Make search and quick actions feel effortless. | [T012](#t012), [T021](#t021), [T037](#t037), [T068](#t068), [T076](#t076), [T077](#t077), [T078](#t078), [T086](#t086), [T090](#t090) |
| [UX09](ux.md#9-give-each-entry-type-a-pleasing-useful-presentation) | Give each entry type a pleasing, useful presentation. | [T012](#t012), [T038](#t038), [T039](#t039), [T041](#t041), [T084](#t084), [T086](#t086), [T090](#t090) |
| [UX10](ux.md#10-make-offline-and-synchronization-states-reassuring) | Make offline and synchronization states reassuring. | [T012](#t012), [T043](#t043), [T050](#t050), [T084](#t084), [T086](#t086), [T090](#t090) |
| [UX11](ux.md#11-give-the-first-launch-a-warm-focused-welcome) | Give the first launch a warm, focused welcome. | [T012](#t012), [T034](#t034), [T057](#t057), [T084](#t084), [T086](#t086), [T090](#t090) |
| [UX12](ux.md#12-make-reversible-actions-forgiving) | Make reversible actions forgiving. | [T012](#t012), [T024](#t024), [T026](#t026), [T055](#t055), [T084](#t084), [T086](#t086), [T090](#t090) |
| [UX13](ux.md#13-use-a-three-column-mac-main-window) | Use a three-column Mac main window. | [T012](#t012), [T033](#t033), [T037](#t037), [T086](#t086), [T090](#t090) |
| [UX14](ux.md#14-place-mac-search-in-the-top-toolbar) | Place Mac search in the top toolbar. | [T012](#t012), [T021](#t021), [T037](#t037), [T086](#t086), [T090](#t090) |
| [UX15](ux.md#15-separate-reading-and-editing-within-the-mac-detail-pane) | Separate reading and editing within the Mac detail pane. | [T012](#t012), [T038](#t038), [T039](#t039), [T086](#t086), [T090](#t090) |
| [UX16](ux.md#16-create-mac-entries-from-the-toolbar) | Create Mac entries from the toolbar. | [T012](#t012), [T038](#t038), [T086](#t086), [T090](#t090) |
| [UX17](ux.md#17-confirm-navigation-away-from-unsaved-mac-edits) | Confirm navigation away from unsaved Mac edits. | [T012](#t012), [T020](#t020), [T038](#t038), [T086](#t086), [T090](#t090) |
| [UX18](ux.md#18-present-a-focused-mac-locked-screen) | Present a focused Mac locked screen. | [T012](#t012), [T043](#t043), [T086](#t086), [T090](#t090) |
| [UX19](ux.md#19-use-items-search-and-settings-tabs-on-iphone) | Use Items, Search and Settings tabs on iPhone. | [T076](#t076), [T086](#t086), [T090](#t090) |
| [UX20](ux.md#20-adapt-the-ipad-layout-to-the-available-window-width) | Adapt the iPad layout to the available window width. | [T077](#t077), [T086](#t086), [T090](#t090) |
| [UX21](ux.md#21-use-material-3-navigation-adapted-to-the-window-size) | Use Material 3 navigation adapted to the window size. | [T078](#t078), [T086](#t086), [T090](#t090) |
| [UX22](ux.md#22-create-and-edit-entries-in-an-appropriately-sized-native-form) | Create and edit entries in an appropriately sized native form. | [T020](#t020), [T076](#t076), [T077](#t077), [T078](#t078), [T084](#t084), [T086](#t086), [T090](#t090) |
| [UX23](ux.md#23-keep-ipad-search-close-to-the-entry-list) | Keep iPad search close to the entry list. | [T021](#t021), [T077](#t077), [T086](#t086), [T090](#t090) |
| [UX24](ux.md#24-offer-biometrics-automatically-when-deliberately-opening-the-locked-app) | Offer biometrics automatically when deliberately opening the locked app. | [T076](#t076), [T077](#t077), [T078](#t078), [T086](#t086), [T090](#t090) |
| [UX25](ux.md#25-use-clear-recognizable-entry-rows-across-platforms) | Use clear, recognizable entry rows across platforms. | [T012](#t012), [T021](#t021), [T037](#t037), [T038](#t038), [T076](#t076), [T077](#t077), [T078](#t078), [T086](#t086), [T090](#t090) |
| [UX26](ux.md#26-keep-entry-details-clearly-organized-across-platforms) | Keep entry details clearly organized across platforms. | [T012](#t012), [T038](#t038), [T039](#t039), [T041](#t041), [T076](#t076), [T077](#t077), [T078](#t078), [T086](#t086), [T090](#t090) |
| [UX27](ux.md#27-generate-a-password-or-passphrase-from-the-entry-editor) | Generate a password or passphrase from the entry editor. | [T012](#t012), [T040](#t040), [T084](#t084), [T086](#t086), [T090](#t090) |
| [UX28](ux.md#28-present-a-compact-login-autofill-chooser-in-mac-browsers) | Present a compact login autofill chooser in Mac browsers. | [T064](#t064), [T065](#t065), [T090](#t090) |
| [UX29](ux.md#29-offer-a-compact-browser-prompt-to-save-or-update-a-login) | Offer a compact browser prompt to save or update a login. | [T066](#t066), [T081](#t081), [T082](#t082), [T090](#t090) |
| [UX30](ux.md#30-guide-vault-creation-through-focused-steps) | Guide vault creation through focused steps. | [T034](#t034), [T084](#t084), [T090](#t090) |
| [UX31](ux.md#31-guide-opening-an-existing-vault-from-its-storage-location) | Guide opening an existing vault from its storage location. | [T035](#t035), [T084](#t084), [T090](#t090) |
| [UX32](ux.md#32-present-recovery-as-a-dedicated-guided-flow) | Present recovery as a dedicated guided flow. | [T036](#t036), [T084](#t084), [T090](#t090) |
| [UX33](ux.md#33-organize-settings-by-purpose-and-make-preference-scope-clear) | Organize Settings by purpose and make preference scope clear. | [T012](#t012), [T031](#t031), [T042](#t042), [T076](#t076), [T077](#t077), [T078](#t078), [T086](#t086), [T090](#t090) |
| [UX34](ux.md#34-make-conflicting-entry-versions-easy-to-compare-and-resolve) | Make conflicting entry versions easy to compare and resolve. | [T049](#t049), [T084](#t084), [T090](#t090) |
| [UX35](ux.md#35-preview-dated-history-versions-before-restoring) | Preview dated history versions before restoring. | [T025](#t025), [T055](#t055), [T084](#t084), [T090](#t090) |
| [UX36](ux.md#36-make-trash-accessible-and-restoration-straightforward) | Make Trash accessible and restoration straightforward. | [T026](#t026), [T055](#t055), [T084](#t084), [T090](#t090) |
| [UX37](ux.md#37-present-each-vaults-backup-settings-on-one-clear-screen) | Present each vault's backup settings on one clear screen. | [T042](#t042), [T053](#t053), [T054](#t054), [T084](#t084), [T090](#t090) |
| [UX38](ux.md#38-preview-a-backup-before-choosing-how-to-restore-it) | Preview a backup before choosing how to restore it. | [T054](#t054), [T084](#t084), [T090](#t090) |
| [UX39](ux.md#39-make-the-destination-and-effect-of-copying-or-moving-clear) | Make the destination and effect of copying or moving clear. | [T027](#t027), [T056](#t056), [T084](#t084), [T090](#t090) |
| [UX40](ux.md#40-preview-imports-and-review-possible-duplicates-before-applying-them) | Preview imports and review possible duplicates before applying them. | [T057](#t057), [T090](#t090) |
| [UX41](ux.md#41-make-export-scope-format-and-protection-explicit) | Make export scope, format and protection explicit. | [T058](#t058), [T090](#t090) |
| [UX42](ux.md#42-present-actionable-password-health-findings-with-clear-scope) | Present actionable password-health findings with clear scope. | [T071](#t071), [T072](#t072), [T073](#t073), [T084](#t084), [T090](#t090) |
| [UX43](ux.md#43-make-authenticator-codes-easy-to-read-and-copy) | Make authenticator codes easy to read and copy. | [T030](#t030), [T041](#t041), [T067](#t067), [T081](#t081), [T082](#t082), [T084](#t084), [T090](#t090) |
| [UX44](ux.md#44-identify-passkeys-clearly-and-use-native-sign-in-flows) | Identify passkeys clearly and use native sign-in flows. | [T061](#t061), [T069](#t069), [T083](#t083), [T084](#t084), [T090](#t090) |
| [UX45](ux.md#45-review-the-destination-and-fields-before-filling-cards-or-identities) | Review the destination and fields before filling cards or identities. | [T067](#t067), [T081](#t081), [T082](#t082), [T084](#t084), [T090](#t090) |
| [UX46](ux.md#46-preview-an-independent-copy-and-separate-its-file-from-its-transfer-password) | Preview an independent copy and separate its file from its transfer password. | [T059](#t059), [T084](#t084), [T090](#t090) |
| [UX47](ux.md#47-distinguish-shared-file-access-from-shared-vault-credentials) | Distinguish shared file access from shared vault credentials. | [T042](#t042), [T060](#t060), [T084](#t084), [T090](#t090) |
| [UX48](ux.md#48-let-users-review-a-diagnostic-report-before-sharing-it) | Let users review a diagnostic report before sharing it. | [T042](#t042), [T075](#t075), [T084](#t084), [T090](#t090) |
| [UX49](ux.md#49-add-and-inspect-attachments-through-native-controls) | Add and inspect attachments through native controls. | [T023](#t023), [T041](#t041), [T077](#t077), [T084](#t084), [T090](#t090) |
| [UX50](ux.md#50-offer-optional-platform-specific-autofill-onboarding) | Offer optional, platform-specific autofill onboarding. | [T042](#t042), [T070](#t070), [T081](#t081), [T082](#t082), [T090](#t090) |

### Project constraints

| Source ID | Requirement | Development tasks |
| --- | --- | --- |
| [C1](constitution.md#1-open-source-under-the-mit-licence) | Open source under the MIT licence. | [T003](#t003), [T088](#t088), [T092](#t092), [T093](#t093), [T094](#t094), [T095](#t095), [T096](#t096) |
| [C2](constitution.md#2-public-source-and-private-release-credentials) | Public source and private release credentials. | [T001](#t001), [T003](#t003), [T088](#t088), [T091](#t091), [T092](#t092), [T093](#t093), [T094](#t094), [T095](#t095), [T096](#t096) |
| [C3](constitution.md#3-on-device-diagnostics-and-deliberate-sharing) | On-device diagnostics and deliberate sharing. | [T003](#t003), [T004](#t004), [T075](#t075), [T088](#t088), [T091](#t091), [T093](#t093), [T094](#t094), [T095](#t095), [T096](#t096) |
| [C4](constitution.md#4-owner-controlled-recovery) | Owner-controlled recovery. | [T001](#t001), [T004](#t004), [T006](#t006), [T016](#t016), [T017](#t017), [T036](#t036), [T088](#t088), [T095](#t095), [T096](#t096) |

### Accepted research additions

The accepted R01–R12 register in [recommendations.md](recommendations.md#specification-mapping) is covered through its functional mappings:

| Research ID | Functional coverage |
| --- | --- |
| R01 | F14, F15 |
| R02 | F16–F18 |
| R03 | F16, F19 |
| R04 | F20, F21 |
| R05 | F22–F24 |
| R06 | F25 |
| R07 | F26 |
| R08 | F27, F28 |
| R09 | F29, F30 |
| R10 | F22, F23; F31 withdrawn |
| R11 | F33, F34 |
| R12 | F35, F36, F38, F39; F37 withdrawn |

## Existing feasibility evidence and open gates

The [Mac evaluation](../dev/experiments/mac-validation/README.md) reports 18 default storage/recovery tests plus two independent-reader checks, 23 sync-model tests, 11 native test groups and 10 host-protocol tests. These results are recorded evidence; this task-list preparation did not rerun them. The original unmodified recovery baseline still has its documented failures.

The native window and extension executables are feasibility scaffolding. The cloud model assumes atomic conditional writes; authentication was injected; actual browser ceremonies, Keychain-backed shared unlocking and live provider guarantees remain unproven. The controlled KDBX fork is not yet a production dependency.

| Gate | Backlog closure work | What it blocks |
| --- | --- | --- |
| D01 | T004, T007, T059, T060 | Shared credential delivery and provider sharing claims; product scope is already resolved. |
| D02 | T005 | Production storage/format adoption. |
| D03 | T004, T006 | Production encryption/recovery assumptions; integrated review follows in T088. |
| D04 | T007, T008 | Production reconciliation, backup fencing, retirement and migration protocol adoption. |
| D05 | T009, T010 | Native core boundary and each platform’s real biometric/credential integration claims. |

T012 may proceed with clearly marked synthetic data after the build baseline. It must not be presented as a working secure password manager. Gate-dependent production tasks begin only after their relevant evidence and decisions exist. Platform gates may close independently, Mac first. No new backend, format substitution or scope reduction is implicit in a failed experiment.

## Ordered development backlog

`Depends on` lists prerequisites for full-task closure; the phase plan explicitly scopes earlier platform/feature slices. Shared UI outcomes are implemented separately in each native app; they do not imply shared HTML views. Mac delivery is integrated in T033–T075; the corresponding mobile experiences and adapters are completed in T076–T085. Independent work may proceed once its own prerequisites are met. Platform-specific verification runs as each platform becomes available.

### Baseline, decisions and feasibility gates

<a id="t001"></a>

- [x] **T001 — Reconcile the accepted requirements baseline**
  - Completed 2026-10-09: reconciled source hosting and shared inactivity semantics in the authoritative specifications/constitution; preserved withdrawn scope and historical experiments.
  - Approved delivery: P0 — baseline, threat model and reviewed format/recovery decisions.
  - Sources: [F31](specifications.md#31-pwdtwo-managed-new-device-verification--removed-from-scope), [F37](specifications.md#37-trusted-contact-emergency-access--removed-from-scope), [A01](architecture.md#1-explore-operation-without-an-application-operated-backend), [A11](architecture.md#11-exclude-trusted-contact-emergency-access), [A12](architecture.md#12-use-provider-authorization-and-local-vault-unlocking-for-device-setup), [A20](architecture.md#20-distribute-the-notarized-mac-application-through-github-and-66ideascom), [A21](architecture.md#21-publish-the-application-source-under-the-mit-licence), [C2](constitution.md#2-public-source-and-private-release-credentials), [C4](constitution.md#4-owner-controlled-recovery).
  - Depends on: None.
  - Complete when: Correct the stale independent-vault-timer note in the functional open-details section to the confirmed app-wide session, and the constitution’s undecided-source-host statement to the selected GitHub destination. Preserve historical experiment results and conditional decisions. Keep withdrawn F31/F37 recorded but excluded; also exclude emergency access, expiring links, internal sharing roles, paid breach monitoring and a PWDTWO enrollment service. Do not imply the public repository already exists.

<a id="t002"></a>

- [ ] **T002 — Define the native target and support matrix**
  - Approved delivery: P0 — baseline, threat model and reviewed format/recovery decisions.
  - Sources: [F01](specifications.md#1-access-the-password-manager-on-supported-devices), [A13](architecture.md#13-build-four-separate-native-applications), [A14](architecture.md#14-recommend-swift-for-each-apple-application), [A15](architecture.md#15-recommend-kotlin-for-the-android-application), [A18](architecture.md#18-support-the-current-and-previous-major-os-generations), [A19](architecture.md#19-support-apple-silicon-exclusively-on-macos), [A22](architecture.md#22-distribute-mobile-applications-through-the-platform-stores), [A25](architecture.md#25-use-pwdtwo-as-the-application-name), [UX01](ux.md#1-feel-at-home-on-each-platform), [UX02](ux.md#2-adopt-liquid-glass-on-apple-platforms), [UX03](ux.md#3-follow-established-platform-conventions).
  - Depends on: [T001](#t001).
  - Complete when: Specify four distinct products and identifiers: Swift/SwiftUI plus AppKit for macOS, separate Swift/SwiftUI plus UIKit iPhone and iPad targets, and Kotlin/Compose Android. Record toolchains, Android ABIs, extension targets and rolling current/previous stable OS/browser tests. Start from the recorded Apple 26/27 and Android 16/17 baseline, verifying current SDK/store constraints when implementing. Mac and all bundled components are arm64 only; no Catalyst, web application views or shared UI runtime.

<a id="t003"></a>

- [ ] **T003 — Prepare the development and contributor foundation**
  - Approved delivery: P0 — baseline, threat model and reviewed format/recovery decisions.
  - Sources: [A16](architecture.md#16-share-one-native-vault-library-across-four-separate-applications), [A21](architecture.md#21-publish-the-application-source-under-the-mit-licence), [A25](architecture.md#25-use-pwdtwo-as-the-application-name), [C1](constitution.md#1-open-source-under-the-mit-licence), [C2](constitution.md#2-public-source-and-private-release-credentials), [C3](constitution.md#3-on-device-diagnostics-and-deliberate-sharing).
  - Depends on: [T002](#t002).
  - Complete when: Define production layout under dev/ separately from experiments; configure command-line builds, dependency pinning, relevant CI checks, synthetic fixtures, configuration examples and secret exclusions. Retain MIT/66IDEAS notices and audit third-party obligations, including any MPL-covered bindings. Document local builds without official signing credentials. Do not publish or commit real vaults, credentials or diagnostic secrets.

<a id="t004"></a>

- [x] **T004 — Document the threat model and security boundaries**
  - Completed 2026-10-09: [threat model and security boundaries](phase0-foundation.md#threat-model-and-boundaries-t004) document assets, attackers, key ownership, failure behavior and unresolved protocol gates.
  - Approved delivery: P0 — baseline, threat model and reviewed format/recovery decisions.
  - Sources: [F09](specifications.md#9-unlock-with-a-master-password-or-optional-biometrics), [F10](specifications.md#10-recover-access-using-a-recovery-key), [F32](specifications.md#32-lock-manually-and-change-the-master-password), [F35](specifications.md#35-share-entries-and-vaults-with-other-people), [F36](specifications.md#36-send-an-encrypted-copy-of-an-item), [F40](specifications.md#40-manage-multiple-independently-protected-vaults), [F42](specifications.md#42-prefer-portable-keepass-compatible-vault-files-where-feasible), [A01](architecture.md#1-explore-operation-without-an-application-operated-backend), [A04](architecture.md#4-isolate-vault-keys-and-recovery-paths), [A06](architecture.md#6-separate-vault-logic-from-platform-integrations), [A09](architecture.md#9-evaluate-provider-based-sharing-of-separate-encrypted-containers), [A10](architecture.md#10-transfer-encrypted-individual-copies-without-expiring-links), [A12](architecture.md#12-use-provider-authorization-and-local-vault-unlocking-for-device-setup), [C3](constitution.md#3-on-device-diagnostics-and-deliberate-sharing), [C4](constitution.md#4-owner-controlled-recovery), [D01](architecture.md#decisions-required-before-core-development), [D03](architecture.md#decisions-required-before-core-development), [D05](architecture.md#decisions-required-before-core-development).
  - Depends on: [T001](#t001).
  - Complete when: Describe password/offline attacks, malicious or stale cloud data, compromised browser callers, untrusted files, cross-vault access and secret lifetime. Define key ownership, authenticated metadata, per-vault separation, provider authorization versus decryption, shared-session boundaries and recovery/rotation limits. Retain the no-backend direction without assuming cloud accounts provide decryption authority; use maintained cryptographic constructions and explicit failure behavior.

<a id="t005"></a>

- [ ] **T005 — Close D02: select and document the vault format**
  - [x] 2026-10-10 candidate slice: reproduce isolated mutation repairs, add parser/resource guards and unknown-XML rejection, and rerun storage/independent-reader checks. [Evidence and remaining limits](phase0-foundation-results.md). Production selection remains open.
  - Approved delivery: P0 — baseline, threat model and reviewed format/recovery decisions.
  - Sources: [F18](specifications.md#18-inspect-and-restore-previous-versions), [F25](specifications.md#25-create-synchronize-use-and-transfer-passkeys), [F39](specifications.md#39-store-documents-and-attachments), [F42](specifications.md#42-prefer-portable-keepass-compatible-vault-files-where-feasible), [A07](architecture.md#7-treat-kdbx-as-a-conditional-format-choice), [A16](architecture.md#16-share-one-native-vault-library-across-four-separate-applications), [A29](architecture.md#29-keep-attachments-within-the-complete-local-vault), [A41](architecture.md#41-preserve-passkey-lifecycle-and-sharing-semantics), [D02](architecture.md#decisions-required-before-core-development).
  - Depends on: [T003](#t003), [T004](#t004).
  - Complete when: Evaluate the controlled KDBX fork against all required fields, custom metadata, passkeys, conflicts, history, Trash and embedded attachments. Review its four fixes, snapshot semantics, mutation APIs, licensing, maintenance and performance. Define versioning, unknown-field handling and narrowly tested external-reader/export guarantees. Record the final dependency/format decision; do not silently switch formats or reduce accepted features if KDBX has a major limitation.

<a id="t006"></a>

- [ ] **T006 — Close D03: validate the recovery and key protocol**
  - [x] 2026-10-10 candidate slice: implement versioned printable recovery keys, explicit raw-component API, authenticated identity/generation checks, rotation and replacement recovery; test corruption, swapped keys and old-copy behavior. [Protocol contract](../dev/experiments/foundation/README.md). Production review, durable transactions and secret-lifetime work remain open.
  - Approved delivery: P0 — baseline, threat model and reviewed format/recovery decisions.
  - Sources: [F09](specifications.md#9-unlock-with-a-master-password-or-optional-biometrics), [F10](specifications.md#10-recover-access-using-a-recovery-key), [F32](specifications.md#32-lock-manually-and-change-the-master-password), [F42](specifications.md#42-prefer-portable-keepass-compatible-vault-files-where-feasible), [A04](architecture.md#4-isolate-vault-keys-and-recovery-paths), [A07](architecture.md#7-treat-kdbx-as-a-conditional-format-choice), [A45](architecture.md#45-reauthorize-biometric-unlocking-after-enrollment-changes), [A46](architecture.md#46-apply-a-length-based-policy-to-newly-chosen-vault-passwords), [C4](constitution.md#4-owner-controlled-recovery), [D03](architecture.md#decisions-required-before-core-development).
  - Depends on: [T004](#t004), [T005](#t005).
  - Complete when: Specify and review KDF/encryption choices and resource bounds, recovery-key representation and bootstrap, authenticated identity/generation binding, secure raw-key APIs, rotation transactions and secret disposal. Exercise wrong/swapped/tampered keys, interrupted changes, ordinary change without the recovery private key, replacement recovery, old backups and stale external edits. Record reviewed production parameters; prototype test constants and weak KDF settings are not production defaults.

<a id="t007"></a>

- [ ] **T007 — Validate real cloud concurrency and scheduling capabilities**
  - [x] 2026-10-10 preparation slice: twelve offline Drive checks and local native file-coordination probe pass; disposable live race/conflict harnesses and [device procedures](../dev/experiments/foundation/cloud/README.md) are ready. No live provider claim; actual concurrency/scheduling remains open.
  - Approved delivery: P0 — real Mac/provider protocol evidence and design; R2/R3 — mobile execution validation; R4 — shared-participant cases.
  - Sources: [F05](specifications.md#5-synchronize-credentials-across-devices), [F21](specifications.md#21-create-and-restore-encrypted-backups), [F35](specifications.md#35-share-entries-and-vaults-with-other-people), [F41](specifications.md#41-synchronize-vault-files-through-icloud-drive-and-google-drive), [F46](specifications.md#46-change-an-existing-vaults-storage-mode-or-cloud-provider), [A03](architecture.md#3-use-separate-storage-provider-adapters), [A05](architecture.md#5-preserve-concurrent-changes-durably), [A08](architecture.md#8-make-backups-independent-of-synchronization-history), [A09](architecture.md#9-evaluate-provider-based-sharing-of-separate-encrypted-containers), [A23](architecture.md#23-bind-each-synchronized-vault-to-one-cloud-provider), [A27](architecture.md#27-migrate-vaults-between-local-and-cloud-storage), [A44](architecture.md#44-separate-local-vault-removal-from-cloud-file-deletion), [D01](architecture.md#decisions-required-before-core-development), [D04](architecture.md#decisions-required-before-core-development).
  - Depends on: [T004](#t004).
  - Complete when: Use disposable test data to validate Google Drive stale-write preconditions/resumable uploads and actual iCloud multi-device conflict/version behavior. Test deleted files, permission loss, backup-writer handover and in-flight writes. Establish supported native authorization, sharing and scheduling behavior. Local locks and the existing mock CAS provider are not evidence of cross-device guarantees. If needed, evaluate retained encrypted revisions with an explicit lifecycle distinct from the single user backup; do not adopt an unvalidated protocol.

<a id="t008"></a>

- [ ] **T008 — Close D04: specify synchronization, retirement and migration protocols**
  - Approved delivery: P0 — real Mac/provider protocol evidence and design; R2/R3 — mobile execution validation; R4 — shared-participant cases.
  - Sources: [F05](specifications.md#5-synchronize-credentials-across-devices), [F10](specifications.md#10-recover-access-using-a-recovery-key), [F12](specifications.md#12-resolve-conflicting-changes-without-losing-either-version), [F15](specifications.md#15-recover-generated-passwords-from-interrupted-workflows), [F17](specifications.md#17-delete-and-restore-entries), [F18](specifications.md#18-inspect-and-restore-previous-versions), [F21](specifications.md#21-create-and-restore-encrypted-backups), [F23](specifications.md#23-view-known-device-activity-and-understand-access-controls), [F29](specifications.md#29-organize-entries-with-favorites-folders-and-tags), [F32](specifications.md#32-lock-manually-and-change-the-master-password), [F40](specifications.md#40-manage-multiple-independently-protected-vaults), [F41](specifications.md#41-synchronize-vault-files-through-icloud-drive-and-google-drive), [F46](specifications.md#46-change-an-existing-vaults-storage-mode-or-cloud-provider), [A02](architecture.md#2-persist-and-process-vault-data-on-the-device), [A03](architecture.md#3-use-separate-storage-provider-adapters), [A05](architecture.md#5-preserve-concurrent-changes-durably), [A08](architecture.md#8-make-backups-independent-of-synchronization-history), [A23](architecture.md#23-bind-each-synchronized-vault-to-one-cloud-provider), [A27](architecture.md#27-migrate-vaults-between-local-and-cloud-storage), [A34](architecture.md#34-organize-each-vault-with-nested-folders-and-multiple-tags), [A37](architecture.md#37-separate-synchronized-vault-settings-from-device-preferences), [A40](architecture.md#40-scope-password-health-exceptions-to-specific-findings), [A42](architecture.md#42-keep-minimal-encrypted-device-status-records), [A44](architecture.md#44-separate-local-vault-removal-from-cloud-file-deletion), [D04](architecture.md#decisions-required-before-core-development).
  - Depends on: [T005](#t005), [T006](#t006), [T007](#t007).
  - Complete when: Define operation identities, revisions, authenticated generations, conflict resolution, rollback handling and crash-safe publication. Cover concurrent credential changes, clearing history/generator history/Trash, folder changes, settings, health exceptions and device records. Specify backup assignment fencing, confirmed deletion versus unavailability, stale-client retirement, migration discovery/rebinding and late edits. Demonstrate preservation under the actual provider contracts before adopting them.

<a id="t009"></a>

- [ ] **T009 — Close D05 core boundary: validate Rust bindings and packaging**
  - [x] 2026-10-10 Mac candidate slice: end-to-end Swift/C/Rust vault workflow, stale/cancellation checks, UniFFI Swift comparison and Kotlin generation pass; Apple mobile Rust targets type-check. [Binding assessment](../dev/experiments/binding-comparison/README.md). Kotlin runtime, mobile linking, extension budgets and final selection remain open.
  - Approved delivery: P0 — shared API, target/binding probes and packaging decision; R2/R3 — integration validation on mobile targets.
  - Sources: [A06](architecture.md#6-separate-vault-logic-from-platform-integrations), [A13](architecture.md#13-build-four-separate-native-applications), [A16](architecture.md#16-share-one-native-vault-library-across-four-separate-applications), [D05](architecture.md#decisions-required-before-core-development).
  - Depends on: [T003](#t003), [T004](#t004).
  - Complete when: Evaluate UniFFI versus the experimental C ABI and record the final Swift/Kotlin API and ownership model. Build a small fixture for every target family and extension environment. Validate error handling, cancellation, concurrency, secret copying/lifetime and extension memory limits. Define adapters for secure storage, files, provider access, authentication and lifecycle; share semantics through Rust while retaining four native UIs.

<a id="t010"></a>

- [ ] **T010 — Close D05 platform gate: test real authentication and autofill**
  - [x] 2026-10-10 provisioned Mac Keychain slice: one biometric-only authorization reads two independently protected disposable keys with no additional prompts permitted. Before-authentication and invalidated-context reads are denied; both contents match and cleanup passes. Native app signing/profile verified under Xcode 27. [Active evidence](../dev/experiments/biometric-session/README.md). Full vault decryption, enrolment changes, OS lifecycle and extension/autofill work remain open.
  - [x] 2026-10-10 user-present Touch ID slice: real biometric-only policy authentication passes in the native test bundle. Protected reads remain open: the ad-hoc CLI hit -34018 before item creation; prepared a native automatic-signing target and profile-aware build. [Result and signing procedure](../dev/experiments/biometric-session/README.md).
  - [x] 2026-10-10 independent session slice: compile native biometric/Keychain adapter and pass eleven all-or-none shared-session checks with injected providers. [Evidence](phase0-foundation-results.md). No Touch ID prompt or protected read occurred; real hardware, complete vault opening and autofill gates remain open.
  - Approved delivery: P0 — actual Mac biometric/session evidence; R1 — installed Mac login integrations; R2/R3 — native mobile gates; R4 — advanced credential/fill gates.
  - Sources: [F04](specifications.md#4-autofill-credentials-from-the-browser), [F08](specifications.md#8-autofill-credentials-in-mobile-applications), [F09](specifications.md#9-unlock-with-a-master-password-or-optional-biometrics), [F11](specifications.md#11-lock-the-vault-automatically), [F25](specifications.md#25-create-synchronize-use-and-transfer-passkeys), [F33](specifications.md#33-autofill-in-mac-applications), [F38](specifications.md#38-store-and-fill-payment-cards-and-identity-information), [A04](architecture.md#4-isolate-vault-keys-and-recovery-paths), [A06](architecture.md#6-separate-vault-logic-from-platform-integrations), [A17](architecture.md#17-keep-browser-automation-separate-from-native-application-views), [A38](architecture.md#38-preserve-optional-card-and-identity-fields-across-native-clients), [A41](architecture.md#41-preserve-passkey-lifecycle-and-sharing-semantics), [A45](architecture.md#45-reauthorize-biometric-unlocking-after-enrollment-changes), [D05](architecture.md#decisions-required-before-core-development).
  - Depends on: [T002](#t002), [T004](#t004), [T009](#t009).
  - Complete when: Validate entitled Mac credential/Safari extensions, Chrome-launched native messaging, actual Keychain/Touch ID access and OS lock events. Prove one biometric interaction can securely unlock multiple independently protected eligible vaults without device-credential fallback. Probe mobile equivalents, passkey ceremonies and reliable destination/field information for card/identity fills. Record supported surfaces and unresolved limitations; injected authentication, SDK objects and ad-hoc signing alone do not close this gate. Mac evidence may close its platform portion first.

<a id="t011"></a>

- [ ] **T011 — Specify remaining feature bounds and file contracts**
  - Approved delivery: P0 — MVP and architecture-critical contracts; R1 — sync/browser/export details; R4 — advanced-feature bounds.
  - Sources: [F06](specifications.md#6-generate-passwords), [F09](specifications.md#9-unlock-with-a-master-password-or-optional-biometrics), [F11](specifications.md#11-lock-the-vault-automatically), [F13](specifications.md#13-import-existing-passwords), [F19](specifications.md#19-choose-accounts-and-match-websites-correctly), [F20](specifications.md#20-export-vault-data), [F21](specifications.md#21-create-and-restore-encrypted-backups), [F26](specifications.md#26-generate-and-fill-authenticator-codes), [F27](specifications.md#27-review-password-health), [F28](specifications.md#28-check-passwords-against-known-leaks), [F34](specifications.md#34-generate-memorable-passphrases), [F36](specifications.md#36-send-an-encrypted-copy-of-an-item), [F39](specifications.md#39-store-documents-and-attachments), [F43](specifications.md#43-add-long-notes-to-every-password-and-credit-card), [F47](specifications.md#47-share-on-device-diagnostics-in-a-bug-report), [A30](architecture.md#30-resolve-import-duplicates-without-silent-replacement), [A31](architecture.md#31-match-website-credentials-to-explicitly-approved-hosts), [A32](architecture.md#32-generate-passwords-and-english-passphrases-locally), [A33](architecture.md#33-make-leaked-password-checks-opt-in-through-hibp), [A35](architecture.md#35-make-password-clipboard-clearing-optional), [A38](architecture.md#38-preserve-optional-card-and-identity-fields-across-native-clients), [A46](architecture.md#46-apply-a-length-based-policy-to-newly-chosen-vault-passwords).
  - Depends on: [T002](#t002), [T004](#t004).
  - Complete when: Document engineering choices for generator ranges/wordlist/suffixes, Unicode password length, timeout and schedule choices, clipboard delay, TOTP variants, health scoring, duplicate matching, notes/attachment/vault bounds and native preview limits. Define import schemas, CSV/KDBX export profiles, backup/report packaging, encrypted transfer negotiation and browser URL/frame rules. Preserve all agreed defaults. Resolve material capability or security tradeoffs explicitly before their dependent feature; routine bounds need not restart UX elicitation.

### First running Mac experience — synthetic data permitted before core gates

<a id="t012"></a>

- [x] **T012 — Build a usable native Mac UI for early hands-on review**
  - Completed 2026-10-09: [native Mac preview](../dev/macos-preview/README.md) built and launched with supplied PWDTWO branding. [Validation](../dev/macos-preview/VALIDATION.md): 28 model checks, seven inspected native captures, native menu dispatch and unsaved-close interception. Uses only synthetic in-memory data.
  - Approved delivery: P0 — interactive Mac preview with synthetic data and early UX feedback.
  - Sources: [F01](specifications.md#1-access-the-password-manager-on-supported-devices), [UX01](ux.md#1-feel-at-home-on-each-platform), [UX02](ux.md#2-adopt-liquid-glass-on-apple-platforms), [UX03](ux.md#3-follow-established-platform-conventions), [UX04](ux.md#4-make-everyday-use-delightful), [UX05](ux.md#5-give-each-vault-a-recognizable-identity), [UX06](ux.md#6-make-successful-actions-feel-satisfying), [UX08](ux.md#8-make-search-and-quick-actions-feel-effortless), [UX09](ux.md#9-give-each-entry-type-a-pleasing-useful-presentation), [UX10](ux.md#10-make-offline-and-synchronization-states-reassuring), [UX11](ux.md#11-give-the-first-launch-a-warm-focused-welcome), [UX12](ux.md#12-make-reversible-actions-forgiving), [UX13](ux.md#13-use-a-three-column-mac-main-window), [UX14](ux.md#14-place-mac-search-in-the-top-toolbar), [UX15](ux.md#15-separate-reading-and-editing-within-the-mac-detail-pane), [UX16](ux.md#16-create-mac-entries-from-the-toolbar), [UX17](ux.md#17-confirm-navigation-away-from-unsaved-mac-edits), [UX18](ux.md#18-present-a-focused-mac-locked-screen), [UX25](ux.md#25-use-clear-recognizable-entry-rows-across-platforms), [UX26](ux.md#26-keep-entry-details-clearly-organized-across-platforms), [UX27](ux.md#27-generate-a-password-or-passphrase-from-the-entry-editor), [UX33](ux.md#33-organize-settings-by-purpose-and-make-preference-scope-clear).
  - Depends on: [T002](#t002), [T003](#t003).
  - Complete when: Create an interactive Mac build with Liquid Glass navigation, three resizable columns, toolbar search/⌘F, New Item/⌘N, native read/edit forms, Save/Cancel, Settings/⌘, and a locked screen. Use clearly identified synthetic in-memory data until the production core gates close; exercise selection, filtering, item creation, generator presentation and unsaved-navigation choices. Launch via command-line tools for feedback. This build must not claim to protect real passwords or complete security/sync functionality.

### Shared native vault foundation

<a id="t013"></a>

- [ ] **T013 — Implement the reviewed Rust core and native interfaces**
  - Approved delivery: MVP — reviewed shared core and versioned model; R4 — advanced credential/sharing behaviors and full model coverage.
  - Sources: [A02](architecture.md#2-persist-and-process-vault-data-on-the-device), [A06](architecture.md#6-separate-vault-logic-from-platform-integrations), [A16](architecture.md#16-share-one-native-vault-library-across-four-separate-applications), [D02](architecture.md#decisions-required-before-core-development), [D03](architecture.md#decisions-required-before-core-development), [D04](architecture.md#decisions-required-before-core-development), [D05](architecture.md#decisions-required-before-core-development).
  - Depends on: [T005](#t005), [T006](#t006), [T008](#t008), [T009](#t009).
  - Complete when: Create production modules and Swift/Kotlin bindings from the reviewed decisions, including typed errors, cancellation and secret ownership. Keep UI and provider/OS calls behind adapters. Use common synthetic compatibility fixtures; do not copy the experimental storage fork or sync simulator into production without the recorded adoption decisions.

<a id="t014"></a>

- [ ] **T014 — Implement the versioned vault data model**
  - Approved delivery: MVP — reviewed shared core and versioned model; R4 — advanced credential/sharing behaviors and full model coverage.
  - Sources: [F03](specifications.md#3-save-login-entries), [F15](specifications.md#15-recover-generated-passwords-from-interrupted-workflows), [F18](specifications.md#18-inspect-and-restore-previous-versions), [F25](specifications.md#25-create-synchronize-use-and-transfer-passkeys), [F26](specifications.md#26-generate-and-fill-authenticator-codes), [F29](specifications.md#29-organize-entries-with-favorites-folders-and-tags), [F30](specifications.md#30-store-secure-notes-and-custom-fields), [F38](specifications.md#38-store-and-fill-payment-cards-and-identity-information), [F39](specifications.md#39-store-documents-and-attachments), [F40](specifications.md#40-manage-multiple-independently-protected-vaults), [F42](specifications.md#42-prefer-portable-keepass-compatible-vault-files-where-feasible), [F43](specifications.md#43-add-long-notes-to-every-password-and-credit-card), [A02](architecture.md#2-persist-and-process-vault-data-on-the-device), [A05](architecture.md#5-preserve-concurrent-changes-durably), [A07](architecture.md#7-treat-kdbx-as-a-conditional-format-choice), [A29](architecture.md#29-keep-attachments-within-the-complete-local-vault), [A34](architecture.md#34-organize-each-vault-with-nested-folders-and-multiple-tags), [A37](architecture.md#37-separate-synchronized-vault-settings-from-device-preferences), [A38](architecture.md#38-preserve-optional-card-and-identity-fields-across-native-clients), [A40](architecture.md#40-scope-password-health-exceptions-to-specific-findings), [A41](architecture.md#41-preserve-passkey-lifecycle-and-sharing-semantics), [A42](architecture.md#42-keep-minimal-encrypted-device-status-records).
  - Depends on: [T013](#t013).
  - Complete when: Model independent vault identities; logins, cards, identities, notes, documents, typed custom fields, passkeys and authenticators; nested folders/tags; full historical versions and attachment references; Trash, conflicts, generator records, device status and scoped settings. Preserve unknown supported metadata through all clients and reject incompatible destructive writes with an explanation.

<a id="t015"></a>

- [ ] **T015 — Implement authenticated, crash-safe local persistence**
  - Approved delivery: MVP — production local storage, password protection and recovery; verify the same core on each later platform.
  - Sources: [F03](specifications.md#3-save-login-entries), [F07](specifications.md#7-use-the-password-manager-offline), [F39](specifications.md#39-store-documents-and-attachments), [F42](specifications.md#42-prefer-portable-keepass-compatible-vault-files-where-feasible), [F45](specifications.md#45-keep-a-vault-local-without-cloud-synchronization), [A02](architecture.md#2-persist-and-process-vault-data-on-the-device), [A05](architecture.md#5-preserve-concurrent-changes-durably), [A07](architecture.md#7-treat-kdbx-as-a-conditional-format-choice), [A26](architecture.md#26-support-local-only-vault-storage), [A29](architecture.md#29-keep-attachments-within-the-complete-local-vault).
  - Depends on: [T014](#t014).
  - Complete when: Persist complete encrypted vaults and pending operations with staged writes, validation, atomic replacement where supported and recoverable interrupted transactions. Preserve the last usable revision on disk-full/corruption/cancel failures and distinguish durable local save from sync. Bound headers, KDF requests, decompression and parsing; keep derived sensitive data within its vault protection boundary.

<a id="t016"></a>

- [ ] **T016 — Implement password policy, key derivation and secret handling**
  - Approved delivery: MVP — production local storage, password protection and recovery; verify the same core on each later platform.
  - Sources: [F09](specifications.md#9-unlock-with-a-master-password-or-optional-biometrics), [F10](specifications.md#10-recover-access-using-a-recovery-key), [A04](architecture.md#4-isolate-vault-keys-and-recovery-paths), [A46](architecture.md#46-apply-a-length-based-policy-to-newly-chosen-vault-passwords), [C4](constitution.md#4-owner-controlled-recovery).
  - Depends on: [T006](#t006), [T013](#t013), [T015](#t015).
  - Complete when: Apply the reviewed cryptographic parameters and secret lifecycle. Require at least 15 characters for newly chosen passwords with spaces/long passphrases and local strength feedback; continue opening existing shorter passwords. Use consistent Unicode/encoding rules without silent normalization or truncation. Minimize secret copies across bindings and never log credentials.

<a id="t017"></a>

- [ ] **T017 — Implement per-vault creation, password changes and recovery**
  - Approved delivery: MVP — production local storage, password protection and recovery; verify the same core on each later platform.
  - Sources: [F09](specifications.md#9-unlock-with-a-master-password-or-optional-biometrics), [F10](specifications.md#10-recover-access-using-a-recovery-key), [F22](specifications.md#22-set-up-a-vault-and-connect-additional-devices), [F32](specifications.md#32-lock-manually-and-change-the-master-password), [F40](specifications.md#40-manage-multiple-independently-protected-vaults), [A04](architecture.md#4-isolate-vault-keys-and-recovery-paths), [A12](architecture.md#12-use-provider-authorization-and-local-vault-unlocking-for-device-setup), [A46](architecture.md#46-apply-a-length-based-policy-to-newly-chosen-vault-passwords), [C4](constitution.md#4-owner-controlled-recovery).
  - Depends on: [T016](#t016).
  - Complete when: Generate independent credentials per vault. Require the current password for ordinary changes even during biometric sessions, preserving the recovery key. Recovery works from a local available file without the old password, replaces both credentials and requires confirmation the new key was saved. Support save/print recovery information with vault identification. Validate old/new credential combinations and interrupted transitions; keep old-copy limitations explicit.

<a id="t018"></a>

- [ ] **T018 — Implement platform-protected biometric unlock material**
  - Approved delivery: MVP — Mac; R2 — iPhone/iPad; R3 — Android. Each native security/session adapter must pass before use.
  - Sources: [F09](specifications.md#9-unlock-with-a-master-password-or-optional-biometrics), [F10](specifications.md#10-recover-access-using-a-recovery-key), [F32](specifications.md#32-lock-manually-and-change-the-master-password), [A04](architecture.md#4-isolate-vault-keys-and-recovery-paths), [A45](architecture.md#45-reauthorize-biometric-unlocking-after-enrollment-changes), [D05](architecture.md#decisions-required-before-core-development).
  - Depends on: [T010](#t010), [T016](#t016), [T017](#t017).
  - Complete when: Implement Apple Keychain and Android Keystore adapters with biometric-only access, enrollment-change invalidation and no PIN/device-login fallback. Require vault passwords to re-enable affected biometric access or after learned credential changes. Support offline unlocking and optional periodic password re-entry, off by default. Prove the controls on each supported platform before enabling its adapter.

<a id="t019"></a>

- [ ] **T019 — Implement the shared application unlock and lock session**
  - Approved delivery: MVP — Mac; R2 — iPhone/iPad; R3 — Android. Each native security/session adapter must pass before use.
  - Sources: [F09](specifications.md#9-unlock-with-a-master-password-or-optional-biometrics), [F11](specifications.md#11-lock-the-vault-automatically), [F32](specifications.md#32-lock-manually-and-change-the-master-password), [F40](specifications.md#40-manage-multiple-independently-protected-vaults), [A04](architecture.md#4-isolate-vault-keys-and-recovery-paths), [A06](architecture.md#6-separate-vault-logic-from-platform-integrations), [A45](architecture.md#45-reauthorize-biometric-unlocking-after-enrollment-changes).
  - Depends on: [T018](#t018).
  - Complete when: Restore included vaults together after one eligible biometric interaction plus any required per-vault passwords; allow excluding a vault. Expose none until all remaining included vaults are authorized. Use one five-minute-default device-local inactivity timer reset only by PWDTWO interaction or deliberate autofill. Manual/device/timeout lock all vaults immediately, invalidating views, indexes, extension grants and late authentication callbacks.

<a id="t020"></a>

- [ ] **T020 — Implement encrypted local editor drafts**
  - Approved delivery: MVP — core operations and Mac integration; R2/R3 — corresponding native mobile integration.
  - Sources: [F16](specifications.md#16-view-copy-and-edit-credentials-manually), [A43](architecture.md#43-preserve-unsaved-edits-as-encrypted-local-drafts), [UX17](ux.md#17-confirm-navigation-away-from-unsaved-mac-edits), [UX22](ux.md#22-create-and-edit-entries-in-an-appropriately-sized-native-form).
  - Depends on: [T015](#t015), [T019](#t019).
  - Complete when: Persist authenticated drafts during editing so locks never wait on a final save. Resume/discard only after the associated vault unlocks; keep drafts out of sync and active autofill. Handle persistence failure, changed/deleted base entries, app termination and draft cleanup without falsely reporting a save or leaking plaintext.

<a id="t021"></a>

- [ ] **T021 — Implement scoped browsing and search**
  - Approved delivery: MVP — core operations and Mac integration; R2/R3 — corresponding native mobile integration.
  - Sources: [F02](specifications.md#2-search-for-passwords), [F40](specifications.md#40-manage-multiple-independently-protected-vaults), [A02](architecture.md#2-persist-and-process-vault-data-on-the-device), [UX08](ux.md#8-make-search-and-quick-actions-feel-effortless), [UX14](ux.md#14-place-mac-search-in-the-top-toolbar), [UX23](ux.md#23-keep-ipad-search-close-to-the-entry-list), [UX25](ux.md#25-use-clear-recognizable-entry-rows-across-platforms).
  - Depends on: [T014](#t014), [T019](#t019).
  - Complete when: Search titles, usernames, websites, tags and notes across unlocked vaults by default with a one-vault filter and source labels. Exclude passwords, OTP secrets and hidden custom fields. Support combined browsing by item type/favorite/folder/tag. Invalidate results and previews immediately on lock; no separately accessible plaintext aggregate index.

<a id="t022"></a>

- [ ] **T022 — Implement entry editing and rich record preservation**
  - Approved delivery: MVP — core operations and Mac integration; R2/R3 — corresponding native mobile integration.
  - Sources: [F03](specifications.md#3-save-login-entries), [F16](specifications.md#16-view-copy-and-edit-credentials-manually), [F30](specifications.md#30-store-secure-notes-and-custom-fields), [F38](specifications.md#38-store-and-fill-payment-cards-and-identity-information), [F43](specifications.md#43-add-long-notes-to-every-password-and-credit-card), [A02](architecture.md#2-persist-and-process-vault-data-on-the-device), [A38](architecture.md#38-preserve-optional-card-and-identity-fields-across-native-clients), [A39](architecture.md#39-make-sensitive-value-masking-configurable).
  - Depends on: [T014](#t014), [T015](#t015), [T020](#t020).
  - Complete when: Provide typed create/read/update operations for logins, secure notes, all optional card/identity fields and custom fields. Preserve incomplete records, multiline notes and line breaks without truncation; open links only by deliberate native actions. Save/cancel and validation must work offline and feed history/conflict handling.

<a id="t023"></a>

- [ ] **T023 — Implement embedded attachments and document records**
  - Approved delivery: MVP — local record/attachment/organization/history/Trash/copy behavior; R1 — synchronized operation paths; R4 — advanced record coverage.
  - Sources: [F18](specifications.md#18-inspect-and-restore-previous-versions), [F39](specifications.md#39-store-documents-and-attachments), [A05](architecture.md#5-preserve-concurrent-changes-durably), [A29](architecture.md#29-keep-attachments-within-the-complete-local-vault), [A37](architecture.md#37-separate-synchronized-vault-settings-from-device-preferences), [UX49](ux.md#49-add-and-inspect-attachments-through-native-controls).
  - Depends on: [T014](#t014), [T015](#t015), [T022](#t022).
  - Complete when: Embed any allowed file type in the complete encrypted vault. Default the per-vault configurable limit to 1,000,000 original bytes, reject oversized additions clearly and retain existing files after limit reductions. Preserve all references from current/history/Trash/conflicts; reclaim only unreferenced content. Validate full offline availability without loading every attachment into credential processes.

<a id="t024"></a>

- [ ] **T024 — Implement folders, tags and favorites**
  - Approved delivery: MVP — local record/attachment/organization/history/Trash/copy behavior; R1 — synchronized operation paths; R4 — advanced record coverage.
  - Sources: [F17](specifications.md#17-delete-and-restore-entries), [F29](specifications.md#29-organize-entries-with-favorites-folders-and-tags), [A34](architecture.md#34-organize-each-vault-with-nested-folders-and-multiple-tags), [UX05](ux.md#5-give-each-vault-a-recognizable-identity), [UX12](ux.md#12-make-reversible-actions-forgiving).
  - Depends on: [T014](#t014), [T022](#t022).
  - Complete when: Provide nested folders, one folder per entry, multiple tags and favorites. Confirm recursive folder deletion and retain its full subtree in Trash. Restore to the original parent or root, disambiguating a separate Name (restored) on collision; never merge/overwrite existing content. Tag removal leaves entries intact and concurrent hierarchy changes retain recoverable identities.

<a id="t025"></a>

- [ ] **T025 — Implement complete entry history**
  - Approved delivery: MVP — local record/attachment/organization/history/Trash/copy behavior; R1 — synchronized operation paths; R4 — advanced record coverage.
  - Sources: [F18](specifications.md#18-inspect-and-restore-previous-versions), [A05](architecture.md#5-preserve-concurrent-changes-durably), [UX35](ux.md#35-preview-dated-history-versions-before-restoring).
  - Depends on: [T022](#t022), [T023](#t023).
  - Complete when: Retain every editable field and historical attachment indefinitely until explicit history clearing. List dated versions, restore as a new current change while preserving the previous current version, and preserve unresolved conflicts separately. Include synchronized clear operations and safe attachment-reference retention.

<a id="t026"></a>

- [ ] **T026 — Implement Trash and recoverable deletion**
  - Approved delivery: MVP — local record/attachment/organization/history/Trash/copy behavior; R1 — synchronized operation paths; R4 — advanced record coverage.
  - Sources: [F17](specifications.md#17-delete-and-restore-entries), [F25](specifications.md#25-create-synchronize-use-and-transfer-passkeys), [F29](specifications.md#29-organize-entries-with-favorites-folders-and-tags), [A05](architecture.md#5-preserve-concurrent-changes-durably), [A34](architecture.md#34-organize-each-vault-with-nested-folders-and-multiple-tags), [A41](architecture.md#41-preserve-passkey-lifecycle-and-sharing-semantics), [UX12](ux.md#12-make-reversible-actions-forgiving), [UX36](ux.md#36-make-trash-accessible-and-restoration-straightforward).
  - Depends on: [T023](#t023), [T024](#t024), [T025](#t025).
  - Complete when: Keep deleted entries/folder trees until explicit Empty Trash; exclude them from search/autofill/passkey use. Restore duplicate matches as separate items and flag review; retain complete contents/history. Confirm permanent deletion, preserve concurrent offline edits for resolution and distinguish deletion metadata from recoverable Trash. Provide eligible Undo under the unlock boundary.

<a id="t027"></a>

- [ ] **T027 — Implement durable cross-vault copy and move**
  - Approved delivery: MVP — local record/attachment/organization/history/Trash/copy behavior; R1 — synchronized operation paths; R4 — advanced record coverage.
  - Sources: [F21](specifications.md#21-create-and-restore-encrypted-backups), [F40](specifications.md#40-manage-multiple-independently-protected-vaults), [A05](architecture.md#5-preserve-concurrent-changes-durably), [A08](architecture.md#8-make-backups-independent-of-synchronization-history), [UX39](ux.md#39-make-the-destination-and-effect-of-copying-or-moving-clear).
  - Depends on: [T023](#t023), [T025](#t025), [T026](#t026).
  - Complete when: Require both vaults unlocked. Copy full supported content, notes, attachments and history into an independent destination identity protected by that vault. Move commits destination before sending source to Trash. Record recoverable operation identity so interruption/retry never loses the original or unnecessarily duplicates the destination.

<a id="t028"></a>

- [ ] **T028 — Implement the local password and passphrase generators**
  - Approved delivery: MVP — offline generators and protected local history; R1 — synchronized history; R2/R3 — native mobile presentation.
  - Sources: [F06](specifications.md#6-generate-passwords), [F34](specifications.md#34-generate-memorable-passphrases), [A32](architecture.md#32-generate-passwords-and-english-passphrases-locally), [UX07](ux.md#7-make-the-password-generator-enjoyable-and-readable).
  - Depends on: [T011](#t011), [T013](#t013).
  - Complete when: Use a cryptographically secure random source and unbiased independent choices. Default passwords to 24 characters with all four categories; default passphrases to six capitalized English words joined without separators plus a random number and symbol. Vet/license the bundled wordlist, support agreed adjustable controls and reject invalid configurations; test actual output rather than display-length strength assumptions.

<a id="t029"></a>

- [ ] **T029 — Implement protected generator history**
  - Approved delivery: MVP — offline generators and protected local history; R1 — synchronized history; R2/R3 — native mobile presentation.
  - Sources: [F15](specifications.md#15-recover-generated-passwords-from-interrupted-workflows), [F34](specifications.md#34-generate-memorable-passphrases), [A02](architecture.md#2-persist-and-process-vault-data-on-the-device).
  - Depends on: [T015](#t015), [T028](#t028).
  - Complete when: Before releasing a generated value for use, retain it in the chosen unlocked vault with time and website where available. Support reveal/copy/save after unlock, offline restart survival and sync. Keep values until explicit clear, with the reviewed concurrent clear/generation semantics; keep generation preferences separate from vault history.

<a id="t030"></a>

- [ ] **T030 — Implement authenticator storage and code generation**
  - Approved delivery: R4 — authenticator configuration, generation and native copy/fill integration.
  - Sources: [F26](specifications.md#26-generate-and-fill-authenticator-codes), [A02](architecture.md#2-persist-and-process-vault-data-on-the-device), [UX43](ux.md#43-make-authenticator-codes-easy-to-read-and-copy).
  - Depends on: [T011](#t011), [T014](#t014), [T016](#t016).
  - Complete when: Parse supported QR/manual TOTP configurations, identify service/account for review and reject malformed or unsupported parameters. Generate offline codes and validity countdowns from the same shared implementation, preserving leading zeros. Support copy/fill through authorized adapters; do not claim syntax validation verifies the secret with the service.

<a id="t031"></a>

- [ ] **T031 — Implement settings scope and defaults**
  - Approved delivery: MVP — scoped settings foundation and applicable defaults; R1–R4 — controls for features as they become available.
  - Sources: [F04](specifications.md#4-autofill-credentials-from-the-browser), [F06](specifications.md#6-generate-passwords), [F09](specifications.md#9-unlock-with-a-master-password-or-optional-biometrics), [F11](specifications.md#11-lock-the-vault-automatically), [F16](specifications.md#16-view-copy-and-edit-credentials-manually), [F21](specifications.md#21-create-and-restore-encrypted-backups), [F28](specifications.md#28-check-passwords-against-known-leaks), [F39](specifications.md#39-store-documents-and-attachments), [A08](architecture.md#8-make-backups-independent-of-synchronization-history), [A32](architecture.md#32-generate-passwords-and-english-passphrases-locally), [A33](architecture.md#33-make-leaked-password-checks-opt-in-through-hibp), [A35](architecture.md#35-make-password-clipboard-clearing-optional), [A36](architecture.md#36-keep-system-notification-content-generic), [A37](architecture.md#37-separate-synchronized-vault-settings-from-device-preferences), [A39](architecture.md#39-make-sensitive-value-masking-configurable), [UX33](ux.md#33-organize-settings-by-purpose-and-make-preference-scope-clear).
  - Depends on: [T014](#t014).
  - Complete when: Keep backup configuration and attachment limits with the vault; keep masking, notifications, clipboard clearing, auto-submit, generator preferences, inactivity/periodic re-entry and leak-check consent/schedule on each device. Backups, clipboard clearing, auto-submit, periodic re-entry and leak checks start off; masking starts on. Apply device preferences consistently to integrations, without transferring network consent across devices.

<a id="t032"></a>

- [ ] **T032 — Implement local-only storage and backup exclusions**
  - Approved delivery: MVP — Mac local-only storage/exclusion; R2 — Apple mobile; R3 — Android.
  - Sources: [F07](specifications.md#7-use-the-password-manager-offline), [F40](specifications.md#40-manage-multiple-independently-protected-vaults), [F45](specifications.md#45-keep-a-vault-local-without-cloud-synchronization), [A02](architecture.md#2-persist-and-process-vault-data-on-the-device), [A26](architecture.md#26-support-local-only-vault-storage).
  - Depends on: [T015](#t015), [T019](#t019), [T031](#t031).
  - Complete when: Create/open local vaults without provider sign-in or upload work, coexisting with cloud vaults. Keep app-managed files outside synced locations and verify platform backup exclusions for vaults and derived sensitive files. Closing preserves files; explicit exports/backups remain available. Test reconnecting does not silently upload local-only data.

### Mac application connected to the production core

<a id="t033"></a>

- [ ] **T033 — Connect the dedicated Mac application to the reviewed core**
  - Approved delivery: MVP — native Mac application connected to the reviewed production core.
  - Sources: [F01](specifications.md#1-access-the-password-manager-on-supported-devices), [F07](specifications.md#7-use-the-password-manager-offline), [A13](architecture.md#13-build-four-separate-native-applications), [A14](architecture.md#14-recommend-swift-for-each-apple-application), [A19](architecture.md#19-support-apple-silicon-exclusively-on-macos), [A25](architecture.md#25-use-pwdtwo-as-the-application-name), [UX01](ux.md#1-feel-at-home-on-each-platform), [UX02](ux.md#2-adopt-liquid-glass-on-apple-platforms), [UX03](ux.md#3-follow-established-platform-conventions), [UX13](ux.md#13-use-a-three-column-mac-main-window).
  - Depends on: [T012](#t012), [T019](#t019), [T021](#t021), [T022](#t022), [T032](#t032).
  - Complete when: Replace fixture behavior with native core-backed state and durable local operations. Keep SwiftUI/AppKit, arm64-only bundles and the three-column window. Establish native menus, focus, commands, lifecycle and useful loading/empty/failure states; ensure app termination/restart preserves data and pending work.

<a id="t034"></a>

- [ ] **T034 — Implement first launch and new-vault setup**
  - Approved delivery: MVP — local setup/opening; R1 — complete cloud setup/opening; R2/R3 reuse the flows in native mobile interfaces.
  - Sources: [F09](specifications.md#9-unlock-with-a-master-password-or-optional-biometrics), [F10](specifications.md#10-recover-access-using-a-recovery-key), [F22](specifications.md#22-set-up-a-vault-and-connect-additional-devices), [F40](specifications.md#40-manage-multiple-independently-protected-vaults), [F45](specifications.md#45-keep-a-vault-local-without-cloud-synchronization), [A12](architecture.md#12-use-provider-authorization-and-local-vault-unlocking-for-device-setup), [A26](architecture.md#26-support-local-only-vault-storage), [A46](architecture.md#46-apply-a-length-based-policy-to-newly-chosen-vault-passwords), [UX05](ux.md#5-give-each-vault-a-recognizable-identity), [UX11](ux.md#11-give-the-first-launch-a-warm-focused-welcome), [UX30](ux.md#30-guide-vault-creation-through-focused-steps).
  - Depends on: [T017](#t017), [T018](#t018), [T031](#t031), [T033](#t033).
  - Complete when: Provide Create/Open and Mac Import entry points. Guide name/icon/color, supported storage, password confirmation, recovery save confirmation and optional biometrics with Back/Continue. Keep local-only creation working independently; connect cloud choices only when their validated adapters are ready, with honest availability states.

<a id="t035"></a>

- [ ] **T035 — Implement opening existing vaults**
  - Approved delivery: MVP — local setup/opening; R1 — complete cloud setup/opening; R2/R3 reuse the flows in native mobile interfaces.
  - Sources: [F09](specifications.md#9-unlock-with-a-master-password-or-optional-biometrics), [F22](specifications.md#22-set-up-a-vault-and-connect-additional-devices), [F40](specifications.md#40-manage-multiple-independently-protected-vaults), [F41](specifications.md#41-synchronize-vault-files-through-icloud-drive-and-google-drive), [A03](architecture.md#3-use-separate-storage-provider-adapters), [A12](architecture.md#12-use-provider-authorization-and-local-vault-unlocking-for-device-setup), [UX31](ux.md#31-guide-opening-an-existing-vault-from-its-storage-location).
  - Depends on: [T019](#t019), [T032](#t032), [T033](#t033).
  - Complete when: Use native file selection and a complete local download when needed; separate provider sign-in from vault unlocking. Show progress, request the vault password, link Forgot password to recovery and offer optional local biometrics after success. Handle incompatible/corrupt files without replacing a usable local copy; connect provider locations through T045/T046.

<a id="t036"></a>

- [ ] **T036 — Implement native recovery and password-change flows**
  - Approved delivery: MVP — complete Mac workflow; later integrations reuse its shared-core semantics.
  - Sources: [F10](specifications.md#10-recover-access-using-a-recovery-key), [F32](specifications.md#32-lock-manually-and-change-the-master-password), [A04](architecture.md#4-isolate-vault-keys-and-recovery-paths), [C4](constitution.md#4-owner-controlled-recovery), [UX32](ux.md#32-present-recovery-as-a-dedicated-guided-flow).
  - Depends on: [T017](#t017), [T019](#t019), [T033](#t033).
  - Complete when: Identify the selected vault, validate its recovery key, collect/confirm the new password, require replacement-key save confirmation and open only after success. Explain replacement and old-copy limits. Provide ordinary change with current-password verification and unchanged recovery key. Show interrupted/failure outcomes without claiming completion.

<a id="t037"></a>

- [ ] **T037 — Implement Mac browsing, search and vault identity**
  - Approved delivery: MVP — complete Mac workflow; later integrations reuse its shared-core semantics.
  - Sources: [F02](specifications.md#2-search-for-passwords), [F29](specifications.md#29-organize-entries-with-favorites-folders-and-tags), [F40](specifications.md#40-manage-multiple-independently-protected-vaults), [A02](architecture.md#2-persist-and-process-vault-data-on-the-device), [UX05](ux.md#5-give-each-vault-a-recognizable-identity), [UX08](ux.md#8-make-search-and-quick-actions-feel-effortless), [UX13](ux.md#13-use-a-three-column-mac-main-window), [UX14](ux.md#14-place-mac-search-in-the-top-toolbar), [UX25](ux.md#25-use-clear-recognizable-entry-rows-across-platforms).
  - Depends on: [T021](#t021), [T024](#t024), [T033](#t033).
  - Complete when: Wire toolbar search/⌘F, combined unlocked-vault scope, one-vault filtering, folders/tags/categories/favorites and labeled native rows. Preserve selection and useful keyboard/context-menu actions with discoverable alternatives. Show honest empty/no-result states and immediately remove locked content.

<a id="t038"></a>

- [ ] **T038 — Implement Mac read, create and edit workflows**
  - Approved delivery: MVP — complete Mac workflow; later integrations reuse its shared-core semantics.
  - Sources: [F03](specifications.md#3-save-login-entries), [F16](specifications.md#16-view-copy-and-edit-credentials-manually), [F30](specifications.md#30-store-secure-notes-and-custom-fields), [F38](specifications.md#38-store-and-fill-payment-cards-and-identity-information), [F43](specifications.md#43-add-long-notes-to-every-password-and-credit-card), [A43](architecture.md#43-preserve-unsaved-edits-as-encrypted-local-drafts), [UX06](ux.md#6-make-successful-actions-feel-satisfying), [UX09](ux.md#9-give-each-entry-type-a-pleasing-useful-presentation), [UX15](ux.md#15-separate-reading-and-editing-within-the-mac-detail-pane), [UX16](ux.md#16-create-mac-entries-from-the-toolbar), [UX17](ux.md#17-confirm-navigation-away-from-unsaved-mac-edits), [UX25](ux.md#25-use-clear-recognizable-entry-rows-across-platforms), [UX26](ux.md#26-keep-entry-details-clearly-organized-across-platforms).
  - Depends on: [T020](#t020), [T022](#t022), [T033](#t033).
  - Complete when: Provide read details with Copy/Reveal, Edit in the same pane, toolbar New Item/⌘N, type selection and prominent destination vault. Save/Cancel remain explicit. Navigation/close offers Save Changes, Discard Changes or Keep Editing; continue only after save success. Lock bypasses that dialog immediately and later offers the protected draft.

<a id="t039"></a>

- [ ] **T039 — Implement masking, reveal and safe clipboard actions**
  - Approved delivery: MVP — complete Mac workflow; later integrations reuse its shared-core semantics.
  - Sources: [F16](specifications.md#16-view-copy-and-edit-credentials-manually), [F38](specifications.md#38-store-and-fill-payment-cards-and-identity-information), [A35](architecture.md#35-make-password-clipboard-clearing-optional), [A39](architecture.md#39-make-sensitive-value-masking-configurable), [UX06](ux.md#6-make-successful-actions-feel-satisfying), [UX09](ux.md#9-give-each-entry-type-a-pleasing-useful-presentation), [UX15](ux.md#15-separate-reading-and-editing-within-the-mac-detail-pane), [UX26](ux.md#26-keep-entry-details-clearly-organized-across-platforms).
  - Depends on: [T019](#t019), [T031](#t031), [T038](#t038).
  - Complete when: Mask passwords/CVV/sensitive fields and card numbers except last four by default, with a device setting to show full values in unlocked views. Reset temporary reveal on navigation/lock. Give secret-free Copied feedback. Optional clipboard clearing tracks the actual owned copy/change identity and preserves later clipboard content; expose validated delay choices and scheduling limits.

<a id="t040"></a>

- [ ] **T040 — Implement the native generator and retained-history UI**
  - Approved delivery: MVP — complete Mac workflow; later integrations reuse its shared-core semantics.
  - Sources: [F06](specifications.md#6-generate-passwords), [F15](specifications.md#15-recover-generated-passwords-from-interrupted-workflows), [F34](specifications.md#34-generate-memorable-passphrases), [A32](architecture.md#32-generate-passwords-and-english-passphrases-locally), [UX07](ux.md#7-make-the-password-generator-enjoyable-and-readable), [UX27](ux.md#27-generate-a-password-or-passphrase-from-the-entry-editor).
  - Depends on: [T028](#t028), [T029](#t029), [T031](#t031), [T038](#t038).
  - Complete when: Use a Mac popover beside the password field with Password/Passphrase, options, exact preview and Generate Again. Visually distinguish passphrase segments without changing copied bytes or delaying use. Use in Entry retains history then updates only the editor; Save remains separate and Cancel leaves the field unchanged. Provide protected history retrieval and explicit clear.

<a id="t041"></a>

- [ ] **T041 — Implement notes, cards, identities, codes and attachment views**
  - Approved delivery: MVP — notes, cards, identities and native attachment previews; R4 — authenticator code presentation.
  - Sources: [F26](specifications.md#26-generate-and-fill-authenticator-codes), [F30](specifications.md#30-store-secure-notes-and-custom-fields), [F38](specifications.md#38-store-and-fill-payment-cards-and-identity-information), [F39](specifications.md#39-store-documents-and-attachments), [F43](specifications.md#43-add-long-notes-to-every-password-and-credit-card), [A29](architecture.md#29-keep-attachments-within-the-complete-local-vault), [A38](architecture.md#38-preserve-optional-card-and-identity-fields-across-native-clients), [UX09](ux.md#9-give-each-entry-type-a-pleasing-useful-presentation), [UX26](ux.md#26-keep-entry-details-clearly-organized-across-platforms), [UX43](ux.md#43-make-authenticator-codes-easy-to-read-and-copy), [UX49](ux.md#49-add-and-inspect-attachments-through-native-controls).
  - Depends on: [T023](#t023), [T030](#t030), [T038](#t038), [T039](#t039).
  - Complete when: Render the accepted optional fields and comfortable multiline notes with native controls. Show grouped TOTP/countdown plus Copy Code, with exact clipboard values. Support attachment type/name/size, picker and Mac drag/drop, bounded native image/PDF/text previews and deliberate Export/Open With. Clean up preview plaintext and hide it on lock; never fetch note links automatically.

<a id="t042"></a>

- [ ] **T042 — Implement native Mac Settings and vault management**
  - Approved delivery: MVP — Mac Settings foundation; R1/R4 — all controls for the features introduced in those releases.
  - Sources: [F09](specifications.md#9-unlock-with-a-master-password-or-optional-biometrics), [F11](specifications.md#11-lock-the-vault-automatically), [F16](specifications.md#16-view-copy-and-edit-credentials-manually), [F21](specifications.md#21-create-and-restore-encrypted-backups), [F28](specifications.md#28-check-passwords-against-known-leaks), [F39](specifications.md#39-store-documents-and-attachments), [F40](specifications.md#40-manage-multiple-independently-protected-vaults), [F44](specifications.md#44-update-the-mac-application-from-within-pwdtwo), [A25](architecture.md#25-use-pwdtwo-as-the-application-name), [A37](architecture.md#37-separate-synchronized-vault-settings-from-device-preferences), [UX33](ux.md#33-organize-settings-by-purpose-and-make-preference-scope-clear), [UX37](ux.md#37-present-each-vaults-backup-settings-on-one-clear-screen), [UX47](ux.md#47-distinguish-shared-file-access-from-shared-vault-credentials), [UX48](ux.md#48-let-users-review-a-diagnostic-report-before-sharing-it), [UX50](ux.md#50-offer-optional-platform-specific-autofill-onboarding).
  - Depends on: [T031](#t031), [T033](#t033).
  - Complete when: Provide the separate Settings window/⌘, and the six agreed groups with device/vault scope labels. Expose per-vault management and controls as their implementations land; present unavailable provider/integration states truthfully. Keep privacy-sensitive opt-ins and shared settings distinct and connect backup, sharing, diagnostics and autofill onboarding to their dedicated tasks.

<a id="t043"></a>

- [ ] **T043 — Verify the first usable Mac vault build**
  - Approved delivery: MVP — scoped offline Mac verification; R1 — rerun with cloud/browser features; later Mac releases retain regression coverage.
  - Sources: [F01](specifications.md#1-access-the-password-manager-on-supported-devices), [F02](specifications.md#2-search-for-passwords), [F03](specifications.md#3-save-login-entries), [F06](specifications.md#6-generate-passwords), [F07](specifications.md#7-use-the-password-manager-offline), [F09](specifications.md#9-unlock-with-a-master-password-or-optional-biometrics), [F10](specifications.md#10-recover-access-using-a-recovery-key), [F11](specifications.md#11-lock-the-vault-automatically), [F16](specifications.md#16-view-copy-and-edit-credentials-manually), [F40](specifications.md#40-manage-multiple-independently-protected-vaults), [F45](specifications.md#45-keep-a-vault-local-without-cloud-synchronization), [A02](architecture.md#2-persist-and-process-vault-data-on-the-device), [A06](architecture.md#6-separate-vault-logic-from-platform-integrations), [UX04](ux.md#4-make-everyday-use-delightful), [UX10](ux.md#10-make-offline-and-synchronization-states-reassuring), [UX18](ux.md#18-present-a-focused-mac-locked-screen).
  - Depends on: [T034](#t034), [T035](#t035), [T036](#t036), [T037](#t037), [T038](#t038), [T039](#t039), [T040](#t040), [T041](#t041), [T042](#t042).
  - Complete when: Build and launch from the command line; verify create/open, multiple-vault unlock, offline CRUD/search/generation, app-wide lock, recovery and draft resumption with disposable vaults. Use the running app for hands-on UX feedback and record remaining scope. Verify on both supported Mac generations before claiming full Mac support; do not wait for mobile apps or demand static mockup approval.

### Provider synchronization, conflicts and data lifecycle

<a id="t044"></a>

- [ ] **T044 — Implement the provider adapter contract and authorization storage**
  - Approved delivery: R1 — real provider synchronization, reconciliation and native Mac status/review; R2/R3 — platform integration.
  - Sources: [F05](specifications.md#5-synchronize-credentials-across-devices), [F22](specifications.md#22-set-up-a-vault-and-connect-additional-devices), [F41](specifications.md#41-synchronize-vault-files-through-icloud-drive-and-google-drive), [A01](architecture.md#1-explore-operation-without-an-application-operated-backend), [A03](architecture.md#3-use-separate-storage-provider-adapters), [A12](architecture.md#12-use-provider-authorization-and-local-vault-unlocking-for-device-setup), [A23](architecture.md#23-bind-each-synchronized-vault-to-one-cloud-provider), [D04](architecture.md#decisions-required-before-core-development).
  - Depends on: [T008](#t008), [T013](#t013), [T018](#t018).
  - Complete when: Implement version-aware encrypted transfer, complete downloads, staged incoming revisions, error/retry/cancellation and single active binding. Use installed-app authorization and protected token storage without a PWDTWO backend. Keep tokens separate from vault keys; locked transfer must not authenticate unknown content or replace the last validated local revision.

<a id="t045"></a>

- [ ] **T045 — Implement Google Drive synchronization adapter**
  - Approved delivery: R1 — real provider synchronization, reconciliation and native Mac status/review; R2/R3 — platform integration.
  - Sources: [F05](specifications.md#5-synchronize-credentials-across-devices), [F35](specifications.md#35-share-entries-and-vaults-with-other-people), [F41](specifications.md#41-synchronize-vault-files-through-icloud-drive-and-google-drive), [A03](architecture.md#3-use-separate-storage-provider-adapters), [A09](architecture.md#9-evaluate-provider-based-sharing-of-separate-encrypted-containers), [A23](architecture.md#23-bind-each-synchronized-vault-to-one-cloud-provider).
  - Depends on: [T007](#t007), [T044](#t044).
  - Complete when: Implement account authorization, file selection/creation, resumable encrypted transfers and the validated concurrency/deletion/sharing operations for all four platforms. Handle expired authorization, quotas, interruptions and lost permissions while preserving pending changes. Verify stale writes cannot silently erase unseen versions.

<a id="t046"></a>

- [ ] **T046 — Implement iCloud Drive synchronization adapter**
  - Approved delivery: R1 — real provider synchronization, reconciliation and native Mac status/review; R2/R3 — platform integration.
  - Sources: [F05](specifications.md#5-synchronize-credentials-across-devices), [F35](specifications.md#35-share-entries-and-vaults-with-other-people), [F41](specifications.md#41-synchronize-vault-files-through-icloud-drive-and-google-drive), [A03](architecture.md#3-use-separate-storage-provider-adapters), [A09](architecture.md#9-evaluate-provider-based-sharing-of-separate-encrypted-containers), [A23](architecture.md#23-bind-each-synchronized-vault-to-one-cloud-provider).
  - Depends on: [T007](#t007), [T044](#t044).
  - Complete when: Implement native coordinated file access, full local availability, conflict-copy capture and the validated publication/deletion/sharing behavior on Mac/iPhone/iPad. Do not treat NSFileCoordinator as a cross-device lock or resolve provider conflicts before preserving them. Android exposes Google Drive/local choices only.

<a id="t047"></a>

- [ ] **T047 — Implement durable reconciliation and locked-vault staging**
  - Approved delivery: R1 — real provider synchronization, reconciliation and native Mac status/review; R2/R3 — platform integration.
  - Sources: [F05](specifications.md#5-synchronize-credentials-across-devices), [F07](specifications.md#7-use-the-password-manager-offline), [F12](specifications.md#12-resolve-conflicting-changes-without-losing-either-version), [F15](specifications.md#15-recover-generated-passwords-from-interrupted-workflows), [F17](specifications.md#17-delete-and-restore-entries), [F18](specifications.md#18-inspect-and-restore-previous-versions), [F29](specifications.md#29-organize-entries-with-favorites-folders-and-tags), [F41](specifications.md#41-synchronize-vault-files-through-icloud-drive-and-google-drive), [A02](architecture.md#2-persist-and-process-vault-data-on-the-device), [A03](architecture.md#3-use-separate-storage-provider-adapters), [A05](architecture.md#5-preserve-concurrent-changes-durably), [A34](architecture.md#34-organize-each-vault-with-nested-folders-and-multiple-tags), [A37](architecture.md#37-separate-synchronized-vault-settings-from-device-preferences), [A40](architecture.md#40-scope-password-health-exceptions-to-specific-findings), [A42](architecture.md#42-keep-minimal-encrypted-device-status-records).
  - Depends on: [T008](#t008), [T015](#t015), [T025](#t025), [T026](#t026), [T029](#t029), [T044](#t044).
  - Complete when: Integrate the reviewed operation/revision protocol with real encrypted vault files. Preserve local pending edits and competing revisions through restart; merge only after required unlocking and validation. Reconcile disjoint edits and retain differing versions, including deletion/clear/folder/settings races. Track transferred-but-unmerged state accurately; reject tampering/known rollback and retry safely after lost acknowledgements.

<a id="t048"></a>

- [ ] **T048 — Implement credential-change reconciliation**
  - Approved delivery: R1 — real provider synchronization, reconciliation and native Mac status/review; R2/R3 — platform integration.
  - Sources: [F10](specifications.md#10-recover-access-using-a-recovery-key), [F12](specifications.md#12-resolve-conflicting-changes-without-losing-either-version), [F32](specifications.md#32-lock-manually-and-change-the-master-password), [F35](specifications.md#35-share-entries-and-vaults-with-other-people), [A04](architecture.md#4-isolate-vault-keys-and-recovery-paths), [A05](architecture.md#5-preserve-concurrent-changes-durably), [D03](architecture.md#decisions-required-before-core-development), [D04](architecture.md#decisions-required-before-core-development).
  - Depends on: [T017](#t017), [T019](#t019), [T045](#t045), [T046](#t046), [T047](#t047).
  - Complete when: On authenticated discovery of changed credentials, require the new password before reopening, including through extensions, while retaining local edits. Test real independently encrypted branches after concurrent password changes/recovery; let users unlock each and explicitly choose the credential generation before reconciling content. Keep unopenable branches pending and preserve offline/old-backup limits.

<a id="t049"></a>

- [ ] **T049 — Implement conflict review and resolution UI**
  - Approved delivery: R1 — real provider synchronization, reconciliation and native Mac status/review; R2/R3 — platform integration.
  - Sources: [F12](specifications.md#12-resolve-conflicting-changes-without-losing-either-version), [A05](architecture.md#5-preserve-concurrent-changes-durably), [UX34](ux.md#34-make-conflicting-entry-versions-easy-to-compare-and-resolve).
  - Depends on: [T039](#t039), [T047](#t047), [T048](#t048).
  - Complete when: Mark Needs review and show masked field differences side by side on wide screens or through a compact version selector. Offer Use This Version and Decide Later; persist all unresolved branches across restart and synchronize explicit resolutions. Distinguish entry conflicts from credential conflicts needing additional unlocking.

<a id="t050"></a>

- [ ] **T050 — Implement sync status and informational device activity**
  - Approved delivery: R1 — real provider synchronization, reconciliation and native Mac status/review; R2/R3 — platform integration.
  - Sources: [F23](specifications.md#23-view-known-device-activity-and-understand-access-controls), [F24](specifications.md#24-see-synchronization-status), [A02](architecture.md#2-persist-and-process-vault-data-on-the-device), [A03](architecture.md#3-use-separate-storage-provider-adapters), [A42](architecture.md#42-keep-minimal-encrypted-device-status-records), [UX10](ux.md#10-make-offline-and-synchronization-states-reassuring).
  - Depends on: [T045](#t045), [T046](#t046), [T047](#t047).
  - Complete when: Show per-vault provider, local-only/offline/syncing/pending/error state, last success and retry, separately from conflicts. Keep one encrypted latest device record with name/platform/app version/last reported sync and manual removal/reappearance semantics. Avoid metadata sync loops and authoritative enrollment/revocation claims; provide provider/OS access guidance.

<a id="t051"></a>

- [ ] **T051 — Implement local removal and whole-vault deletion**
  - Approved delivery: MVP — local-only deletion/cleanup; R1 — cloud removal/deletion and backup retirement; R2/R3 — native mobile UI.
  - Sources: [F21](specifications.md#21-create-and-restore-encrypted-backups), [F40](specifications.md#40-manage-multiple-independently-protected-vaults), [F45](specifications.md#45-keep-a-vault-local-without-cloud-synchronization), [A26](architecture.md#26-support-local-only-vault-storage), [A44](architecture.md#44-separate-local-vault-removal-from-cloud-file-deletion).
  - Depends on: [T026](#t026), [T032](#t032), [T045](#t045), [T046](#t046), [T047](#t047), [T050](#t050).
  - Complete when: Separate Close, Remove from This Device, Delete Cloud Vault and Delete Local-only Vault. Warn about pending edits/sole copies and identify exact file scope. Retain backup by default with unchecked Also delete; stop scheduled backup work and track partial failures. Clean local keys/drafts/indexes. On confirmed remote deletion preserve local data, stop sync and offer local-only/removal; distinguish permission loss and never recreate automatically.

<a id="t052"></a>

- [ ] **T052 — Implement recoverable storage migration**
  - Approved delivery: R1 — migration and the optional one-backup schedule/handover; R2/R3 — native mobile execution.
  - Sources: [F46](specifications.md#46-change-an-existing-vaults-storage-mode-or-cloud-provider), [A23](architecture.md#23-bind-each-synchronized-vault-to-one-cloud-provider), [A26](architecture.md#26-support-local-only-vault-storage), [A27](architecture.md#27-migrate-vaults-between-local-and-cloud-storage), [D04](architecture.md#decisions-required-before-core-development).
  - Depends on: [T032](#t032), [T045](#t045), [T046](#t046), [T047](#t047), [T048](#t048), [T051](#t051).
  - Complete when: Move local↔cloud and iCloud↔Drive using the reviewed transaction, preserving identity, contents/history/attachments/pending work and credentials. Verify the destination and reconcile newer source revisions before switching then deleting the old cloud file. Persist cleanup/retry state, coordinate concurrent moves and stale-device rebinding, and never leave two active provider bindings or revive retired source files.

<a id="t053"></a>

- [ ] **T053 — Implement the single-backup scheduler and writer handover**
  - Approved delivery: R1 — migration and the optional one-backup schedule/handover; R2/R3 — native mobile execution.
  - Sources: [F21](specifications.md#21-create-and-restore-encrypted-backups), [A08](architecture.md#8-make-backups-independent-of-synchronization-history), [A37](architecture.md#37-separate-synchronized-vault-settings-from-device-preferences), [A44](architecture.md#44-separate-local-vault-removal-from-cloud-file-deletion), [UX37](ux.md#37-present-each-vaults-backup-settings-on-one-clear-screen).
  - Depends on: [T031](#t031), [T045](#t045), [T046](#t046), [T047](#t047), [T048](#t048), [T051](#t051).
  - Complete when: Implement opt-in user-selected frequency and exactly one replaceable backup per vault, beside its cloud file or in a chosen local folder. Synchronize configuration, designate one writer, fence former/in-flight writers after handover without requiring the old device and perform overdue online work when execution permits. Validate the new backup before replacement and preserve the previous usable one on failure; retain original-generation credentials and complete contents. Provide truthful status and separate manual exports, with no history count or mandatory daily/pre-operation backup.

<a id="t054"></a>

- [ ] **T054 — Implement encrypted backup export and reviewed restoration**
  - Approved delivery: MVP — manual encrypted backup and local restore; R1 — cloud-backed selection and coordinated replacement; R2/R3 — native mobile flows.
  - Sources: [F10](specifications.md#10-recover-access-using-a-recovery-key), [F21](specifications.md#21-create-and-restore-encrypted-backups), [F40](specifications.md#40-manage-multiple-independently-protected-vaults), [A08](architecture.md#8-make-backups-independent-of-synchronization-history), [UX37](ux.md#37-present-each-vaults-backup-settings-on-one-clear-screen), [UX38](ux.md#38-preview-a-backup-before-choosing-how-to-restore-it).
  - Depends on: [T017](#t017), [T027](#t027), [T053](#t053).
  - Complete when: Export complete encrypted entries, attachments, history, Trash, conflicts and required recovery metadata without exposing the recovery secret. Select/unlock/preview name/date/content before restore; open a separate vault by default without the original live binding. Explicit replacement identifies the target and validates first. Selective recovery copies chosen entries between unlocked vaults; do not add automatic whole-backup merge.

<a id="t055"></a>

- [ ] **T055 — Implement history, Trash and folder-restoration interfaces**
  - Approved delivery: MVP — local history/Trash/copy/move and selective recovery UI; R1 — synchronized conflict cases; R2/R3 — native mobile UI.
  - Sources: [F17](specifications.md#17-delete-and-restore-entries), [F18](specifications.md#18-inspect-and-restore-previous-versions), [F29](specifications.md#29-organize-entries-with-favorites-folders-and-tags), [A05](architecture.md#5-preserve-concurrent-changes-durably), [A34](architecture.md#34-organize-each-vault-with-nested-folders-and-multiple-tags), [UX12](ux.md#12-make-reversible-actions-forgiving), [UX35](ux.md#35-preview-dated-history-versions-before-restoring), [UX36](ux.md#36-make-trash-accessible-and-restoration-straightforward).
  - Depends on: [T024](#t024), [T025](#t025), [T026](#t026), [T039](#t039), [T049](#t049).
  - Complete when: Provide dated history previews/diffs and full-version restore confirmation with prior current version retained. Put Trash in sidebar or compact Items filters, label vaults and confirm Empty Trash with scope/count. Show duplicate restoration and restored-folder naming accurately, preserve eligible Undo and keep unresolved conflicts separate from history clearing.

<a id="t056"></a>

- [ ] **T056 — Implement cross-vault copy/move and selective recovery UI**
  - Approved delivery: MVP — local history/Trash/copy/move and selective recovery UI; R1 — synchronized conflict cases; R2/R3 — native mobile UI.
  - Sources: [F21](specifications.md#21-create-and-restore-encrypted-backups), [F40](specifications.md#40-manage-multiple-independently-protected-vaults), [A05](architecture.md#5-preserve-concurrent-changes-durably), [A08](architecture.md#8-make-backups-independent-of-synchronization-history), [UX39](ux.md#39-make-the-destination-and-effect-of-copying-or-moving-clear).
  - Depends on: [T027](#t027), [T038](#t038), [T054](#t054).
  - Complete when: Expose Copy to Vault/Move to Vault in More with source, count, destination vault/folder and a clear effect explanation. Show success only after the appropriate durable steps; preserve source on failure and present resumable partial operations without duplicate moves. Use this same workflow for selected entries from a separate restored backup.

### Migration, sharing and advanced records

<a id="t057"></a>

- [ ] **T057 — Implement Mac migration imports**
  - Approved delivery: MVP — Mac imports from all four agreed sources with explicit coverage reporting; R4 — extend supported advanced content.
  - Sources: [F13](specifications.md#13-import-existing-passwords), [A30](architecture.md#30-resolve-import-duplicates-without-silent-replacement), [UX11](ux.md#11-give-the-first-launch-a-warm-focused-welcome), [UX40](ux.md#40-preview-imports-and-review-possible-duplicates-before-applying-them).
  - Depends on: [T011](#t011), [T022](#t022), [T023](#t023), [T024](#t024), [T025](#t025), [T033](#t033).
  - Complete when: Validate current Google Password Manager, 1Password, LastPass and Apple Passwords export routes and build parsers/fixtures for supported formats. Preserve supported login fields, notes, organization and custom fields. Preview destination, exact duplicates skipped by default, differing matches with Skip/Keep Both/Update and omissions. Updates retain history; report every outcome. Do not add legacy Keychain Access support or mobile migration-import UI.

<a id="t058"></a>

- [ ] **T058 — Implement Mac CSV and encrypted KDBX migration exports**
  - Approved delivery: R1 — Mac CSV/KDBX migration export; R4 — extend supported advanced content with explicit omissions.
  - Sources: [F20](specifications.md#20-export-vault-data), [F25](specifications.md#25-create-synchronize-use-and-transfer-passkeys), [F42](specifications.md#42-prefer-portable-keepass-compatible-vault-files-where-feasible), [F43](specifications.md#43-add-long-notes-to-every-password-and-credit-card), [A07](architecture.md#7-treat-kdbx-as-a-conditional-format-choice), [A30](architecture.md#30-resolve-import-duplicates-without-silent-replacement), [UX41](ux.md#41-make-export-scope-format-and-protection-explicit).
  - Depends on: [T005](#t005), [T011](#t011), [T023](#t023), [T025](#t025), [T026](#t026), [T033](#t033).
  - Complete when: Select scope and preview coverage/source vaults before native Save. CSV is explicitly plaintext; KDBX uses a chosen/confirmed independent password and no PWDTWO recovery. Export active entries by default, with History and Trash independently off by default for KDBX. Rebuild selected payloads so excluded history/attachments/secrets do not leak; disclose unsupported fields and passkeys. Test external compatibility only to the documented profile.

<a id="t059"></a>

- [ ] **T059 — Implement encrypted individual-copy transfer**
  - Approved delivery: R4 — encrypted individual sharing, shared vaults and passkey lifecycle across supported native platforms.
  - Sources: [F25](specifications.md#25-create-synchronize-use-and-transfer-passkeys), [F35](specifications.md#35-share-entries-and-vaults-with-other-people), [F36](specifications.md#36-send-an-encrypted-copy-of-an-item), [A09](architecture.md#9-evaluate-provider-based-sharing-of-separate-encrypted-containers), [A10](architecture.md#10-transfer-encrypted-individual-copies-without-expiring-links), [D01](architecture.md#decisions-required-before-core-development), [UX46](ux.md#46-preview-an-independent-copy-and-separate-its-file-from-its-transfer-password).
  - Depends on: [T006](#t006), [T011](#t011), [T016](#t016), [T022](#t022), [T023](#t023).
  - Complete when: Implement the reviewed authenticated transfer container with a new strong random transfer password. Preview current fields only and optional notes/attachments; exclude history, source credentials and unrelated data. Keep Share Encrypted File separate from Copy Transfer Password. Receiver enters password, previews and chooses an unlocked vault for an independent copy. Validate version/item compatibility and tamper handling; promise no expiry, one-use, revocation or named-person authentication.

<a id="t060"></a>

- [ ] **T060 — Implement equal-access shared vaults and credential delivery**
  - Approved delivery: R4 — encrypted individual sharing, shared vaults and passkey lifecycle across supported native platforms.
  - Sources: [F10](specifications.md#10-recover-access-using-a-recovery-key), [F23](specifications.md#23-view-known-device-activity-and-understand-access-controls), [F35](specifications.md#35-share-entries-and-vaults-with-other-people), [F36](specifications.md#36-send-an-encrypted-copy-of-an-item), [A01](architecture.md#1-explore-operation-without-an-application-operated-backend), [A09](architecture.md#9-evaluate-provider-based-sharing-of-separate-encrypted-containers), [A11](architecture.md#11-exclude-trusted-contact-emergency-access), [A12](architecture.md#12-use-provider-authorization-and-local-vault-unlocking-for-device-setup), [D01](architecture.md#decisions-required-before-core-development), [UX47](ux.md#47-distinguish-shared-file-access-from-shared-vault-credentials).
  - Depends on: [T007](#t007), [T017](#t017), [T045](#t045), [T046](#t046), [T048](#t048), [T059](#t059).
  - Complete when: Finalize and implement secure separate delivery/redistribution of the shared password and recovery key to every participant, including after recovery. Integrate provider invitations/opening and Manage Access subject to provider permissions, with Shared badge and equal content access. Test concurrent participant changes and provider write access. Explain removal affects future file access, not downloaded copies; do not introduce internal roles or private-vault recovery authority.

<a id="t061"></a>

- [ ] **T061 — Implement shared-core passkey storage and lifecycle**
  - Approved delivery: R4 — encrypted individual sharing, shared vaults and passkey lifecycle across supported native platforms.
  - Sources: [F25](specifications.md#25-create-synchronize-use-and-transfer-passkeys), [F35](specifications.md#35-share-entries-and-vaults-with-other-people), [F36](specifications.md#36-send-an-encrypted-copy-of-an-item), [A41](architecture.md#41-preserve-passkey-lifecycle-and-sharing-semantics), [UX44](ux.md#44-identify-passkeys-clearly-and-use-native-sign-in-flows).
  - Depends on: [T010](#t010), [T014](#t014), [T016](#t016), [T023](#t023), [T025](#t025), [T026](#t026), [T059](#t059).
  - Complete when: Preserve credential keys, relying-party/account metadata and required state across offline storage, sync, history, backup and supported transfers. Exclude trashed credentials from active provider indexes and reinstate only on restore. Preserve relying-party binding when assigning new local copy identities and identify unsupported transfers. Validate real authentication after sharing; local restoration cannot recreate a website-side registration.

### Mac browser and application integrations

<a id="t062"></a>

- [ ] **T062 — Implement destination-bound autofill authorization**
  - Approved delivery: R1 — Mac login authorization and trusted IPC; R2/R3 — native mobile adaptations; R4 — advanced credential/fill extensions.
  - Sources: [F04](specifications.md#4-autofill-credentials-from-the-browser), [F08](specifications.md#8-autofill-credentials-in-mobile-applications), [F19](specifications.md#19-choose-accounts-and-match-websites-correctly), [F33](specifications.md#33-autofill-in-mac-applications), [F38](specifications.md#38-store-and-fill-payment-cards-and-identity-information), [A06](architecture.md#6-separate-vault-logic-from-platform-integrations), [A17](architecture.md#17-keep-browser-automation-separate-from-native-application-views), [A31](architecture.md#31-match-website-credentials-to-explicitly-approved-hosts), [A38](architecture.md#38-preserve-optional-card-and-identity-fields-across-native-clients).
  - Depends on: [T010](#t010), [T011](#t011), [T019](#t019), [T021](#t021), [T031](#t031).
  - Complete when: Implement exact approved-host matching with canonicalization, internationalized-name, scheme/port, frame and multi-page rules. Bind grants to actual caller/document/destination/fields/session and invalidate on lock/navigation. Require deliberate selection; mismatch offers Fill once, Add approved website and fill, or Cancel, suppressing first-fill auto-submit. Keep native app associations and passkey relying parties outside this override.

<a id="t063"></a>

- [ ] **T063 — Implement trusted extension-to-native communication**
  - Approved delivery: R1 — Mac login authorization and trusted IPC; R2/R3 — native mobile adaptations; R4 — advanced credential/fill extensions.
  - Sources: [F04](specifications.md#4-autofill-credentials-from-the-browser), [F09](specifications.md#9-unlock-with-a-master-password-or-optional-biometrics), [F11](specifications.md#11-lock-the-vault-automatically), [A06](architecture.md#6-separate-vault-logic-from-platform-integrations), [A17](architecture.md#17-keep-browser-automation-separate-from-native-application-views), [D05](architecture.md#decisions-required-before-core-development).
  - Depends on: [T009](#t009), [T010](#t010), [T019](#t019), [T062](#t062).
  - Complete when: Build and package native host/extension IPC with verified callers, bounded framing, validated requests, cancellation and session-bound short-lived authorization. Expose only credentials needed for the approved request. Test replay, malformed/oversized messages, forged caller context, process restarts and lock races using actual installed integrations, not only a subprocess harness.

<a id="t064"></a>

- [ ] **T064 — Implement Safari on Mac login autofill**
  - Approved delivery: R1 — Safari/Chrome login filling, save/update prompts and generator capture on Mac.
  - Sources: [F04](specifications.md#4-autofill-credentials-from-the-browser), [F19](specifications.md#19-choose-accounts-and-match-websites-correctly), [A14](architecture.md#14-recommend-swift-for-each-apple-application), [A17](architecture.md#17-keep-browser-automation-separate-from-native-application-views), [A31](architecture.md#31-match-website-credentials-to-explicitly-approved-hosts), [UX28](ux.md#28-present-a-compact-login-autofill-chooser-in-mac-browsers).
  - Depends on: [T033](#t033), [T062](#t062), [T063](#t063).
  - Complete when: Install/enable the validated Safari integration and a compact native chooser with destination, matching accounts, source-vault labels and search. Unlock before credential disclosure; fill offline local credentials and apply mismatch and optional supported login auto-submit rules. Keep application/chooser views native and verify supported Safari/OS versions.

<a id="t065"></a>

- [ ] **T065 — Implement Chrome on Mac login autofill**
  - Approved delivery: R1 — Safari/Chrome login filling, save/update prompts and generator capture on Mac.
  - Sources: [F04](specifications.md#4-autofill-credentials-from-the-browser), [F19](specifications.md#19-choose-accounts-and-match-websites-correctly), [A17](architecture.md#17-keep-browser-automation-separate-from-native-application-views), [A31](architecture.md#31-match-website-credentials-to-explicitly-approved-hosts), [UX28](ux.md#28-present-a-compact-login-autofill-chooser-in-mac-browsers).
  - Depends on: [T033](#t033), [T062](#t062), [T063](#t063).
  - Complete when: Implement narrowly scoped browser scripts with the Chrome-launched native host and native chooser. Do not substitute an HTML vault popup. Validate account selection, exact-host matching, navigation/frame races, offline access and optional login submission across current/previous Chrome majors; manual submission remains available.

<a id="t066"></a>

- [ ] **T066 — Implement browser save/update and generator capture**
  - Approved delivery: R1 — Safari/Chrome login filling, save/update prompts and generator capture on Mac.
  - Sources: [F06](specifications.md#6-generate-passwords), [F14](specifications.md#14-capture-and-update-logins-from-websites), [F15](specifications.md#15-recover-generated-passwords-from-interrupted-workflows), [F19](specifications.md#19-choose-accounts-and-match-websites-correctly), [A17](architecture.md#17-keep-browser-automation-separate-from-native-application-views), [UX29](ux.md#29-offer-a-compact-browser-prompt-to-save-or-update-a-login).
  - Depends on: [T029](#t029), [T038](#t038), [T040](#t040), [T064](#t064), [T065](#t065).
  - Complete when: Recognize supported signup/signin/password-change flows and offer non-blocking Save Login/Update Login/Not Now with website, username and destination. Let users select the matching existing account for updates and keep its vault. Preserve generated values before use, require normal unlocking and explicit save/update, and retain history without silently overwriting.

<a id="t067"></a>

- [ ] **T067 — Implement reviewed card, identity and OTP fills on Mac**
  - Approved delivery: R4 — reviewed card/identity and authenticator-code filling on validated Mac surfaces.
  - Sources: [F26](specifications.md#26-generate-and-fill-authenticator-codes), [F38](specifications.md#38-store-and-fill-payment-cards-and-identity-information), [A17](architecture.md#17-keep-browser-automation-separate-from-native-application-views), [A38](architecture.md#38-preserve-optional-card-and-identity-fields-across-native-clients), [UX43](ux.md#43-make-authenticator-codes-easy-to-read-and-copy), [UX45](ux.md#45-review-the-destination-and-fields-before-filling-cards-or-identities).
  - Depends on: [T030](#t030), [T041](#t041), [T062](#t062), [T064](#t064), [T065](#t065).
  - Complete when: For validated surfaces, select a record and show trustworthy destination and fields before explicit Fill; bind that approval to the actual target. Respect masking in previews, never submit payment/identity forms, and use native authorized verification-code filling where supported. Provide manual copy when reliable target/field authorization or filling is unavailable.

<a id="t068"></a>

- [ ] **T068 — Implement autofill in compatible Mac applications**
  - Approved delivery: R1 — compatible Mac application password autofill and manual fallback.
  - Sources: [F33](specifications.md#33-autofill-in-mac-applications), [A06](architecture.md#6-separate-vault-logic-from-platform-integrations), [A14](architecture.md#14-recommend-swift-for-each-apple-application), [UX08](ux.md#8-make-search-and-quick-actions-feel-effortless).
  - Depends on: [T010](#t010), [T033](#t033), [T062](#t062), [T063](#t063).
  - Complete when: Specify supported application surfaces, native invocation and necessary permissions; implement account selection/unlock and offline field filling through validated OS APIs. Do not claim arbitrary app coverage. Explain setup and retain manual copy fallback when a destination cannot be filled.

<a id="t069"></a>

- [ ] **T069 — Implement Mac passkey registration, sign-in and supported transfer**
  - Approved delivery: R4 — actual Mac passkey ceremonies and supported transfer routes.
  - Sources: [F25](specifications.md#25-create-synchronize-use-and-transfer-passkeys), [F35](specifications.md#35-share-entries-and-vaults-with-other-people), [F36](specifications.md#36-send-an-encrypted-copy-of-an-item), [A17](architecture.md#17-keep-browser-automation-separate-from-native-application-views), [A41](architecture.md#41-preserve-passkey-lifecycle-and-sharing-semantics), [UX44](ux.md#44-identify-passkeys-clearly-and-use-native-sign-in-flows).
  - Depends on: [T061](#t061), [T063](#t063), [T064](#t064), [T065](#t065), [T068](#t068).
  - Complete when: Complete actual native registration and assertion ceremonies with truthful user-presence/verification handling, correct account/destination selection and vault access policy. Verify Safari/Chrome and compatible applications, cross-device/shared-vault use, Trash/index updates and supported transfer interoperability. Report unsupported routes instead of claiming CSV carries passkeys.

<a id="t070"></a>

- [ ] **T070 — Implement optional Mac autofill setup guidance**
  - Approved delivery: R1 — optional Mac login-autofill onboarding; R4 — update guidance for advanced capabilities.
  - Sources: [F04](specifications.md#4-autofill-credentials-from-the-browser), [F22](specifications.md#22-set-up-a-vault-and-connect-additional-devices), [F33](specifications.md#33-autofill-in-mac-applications), [A17](architecture.md#17-keep-browser-automation-separate-from-native-application-views), [UX50](ux.md#50-offer-optional-platform-specific-autofill-onboarding).
  - Depends on: [T034](#t034), [T064](#t064), [T065](#t065), [T068](#t068).
  - Complete when: After the first opened vault, offer a short native checklist with relevant system/browser setup links and explicit instructions. Later preserves full manual vault use; keep guidance in Settings → Autofill & Clipboard. Report actual enabled state where available rather than assuming installation means activation.

### Health, notifications and private support

<a id="t071"></a>

- [ ] **T071 — Implement local weakness/reuse assessment and exceptions**
  - Approved delivery: R4 — offline password health, opt-in free leak checks and actionable native health views.
  - Sources: [F27](specifications.md#27-review-password-health), [A40](architecture.md#40-scope-password-health-exceptions-to-specific-findings), [UX42](ux.md#42-present-actionable-password-health-findings-with-clear-scope).
  - Depends on: [T011](#t011), [T014](#t014), [T016](#t016), [T021](#t021), [T047](#t047).
  - Complete when: Apply documented scoring and reuse grouping only to unlocked entries. Keep findings actionable, reassess after password changes, and scope ignored weak/reused warnings by entry, type and password generation. Synchronize reversible exceptions inside the vault for all shared participants; resolve concurrent changes without suppressing unrelated findings.

<a id="t072"></a>

- [ ] **T072 — Implement opt-in free leaked-password checks**
  - Approved delivery: R4 — offline password health, opt-in free leak checks and actionable native health views.
  - Sources: [F28](specifications.md#28-check-passwords-against-known-leaks), [A33](architecture.md#33-make-leaked-password-checks-opt-in-through-hibp), [A37](architecture.md#37-separate-synchronized-vault-settings-from-device-preferences), [UX42](ux.md#42-present-actionable-password-health-findings-with-clear-scope).
  - Depends on: [T011](#t011), [T016](#t016), [T031](#t031).
  - Complete when: Keep checks disabled until device-local informed consent. Send only the five-character SHA-1 prefix of complete passwords to HIBP over HTTPS with padding and compare suffixes locally; never send account/email data or require a paid key. Provide Check now and optional user-frequency scheduling only while online/unlocked, bounded retries and dated stale/offline results. Do not retain decrypted material to check locked vaults.

<a id="t073"></a>

- [ ] **T073 — Implement the Password Health experience**
  - Approved delivery: R4 — offline password health, opt-in free leak checks and actionable native health views.
  - Sources: [F27](specifications.md#27-review-password-health), [F28](specifications.md#28-check-passwords-against-known-leaks), [A40](architecture.md#40-scope-password-health-exceptions-to-specific-findings), [UX42](ux.md#42-present-actionable-password-health-findings-with-clear-scope).
  - Depends on: [T033](#t033), [T071](#t071), [T072](#t072).
  - Complete when: Provide Weak/Reused/Leaked groups, checked-vault scope, entry/vault/issue rows and Review actions. Show leak checks not enabled before consent, last-check dates and honest unavailable/stale states. Keep ignored findings accessible and reversible and distinguish a leaked password from evidence of account takeover.

<a id="t074"></a>

- [ ] **T074 — Implement generic configurable notifications**
  - Approved delivery: R1 — conflict/sync/backup notifications; R2/R3 — mobile equivalents; R4 — leak notifications.
  - Sources: [F12](specifications.md#12-resolve-conflicting-changes-without-losing-either-version), [F21](specifications.md#21-create-and-restore-encrypted-backups), [F24](specifications.md#24-see-synchronization-status), [F28](specifications.md#28-check-passwords-against-known-leaks), [A36](architecture.md#36-keep-system-notification-content-generic), [A37](architecture.md#37-separate-synchronized-vault-settings-from-device-preferences).
  - Depends on: [T031](#t031), [T049](#t049), [T050](#t050), [T053](#t053), [T072](#t072).
  - Complete when: Notify for unresolved conflicts, persistent sync/backup failures and newly detected leaks with generic content only. Honor OS permission and per-device category controls, define persistence/grouping/deduplication, keep routine success quiet and require normal unlock after opening a notification. Verify payloads contain no vault/website/account details.

<a id="t075"></a>

- [ ] **T075 — Implement local diagnostics and manual support reports**
  - Approved delivery: MVP — bounded local Mac diagnostics and manual reports; R2/R3 — native mobile support; R4 — advanced component sanitization.
  - Sources: [F47](specifications.md#47-share-on-device-diagnostics-in-a-bug-report), [A21](architecture.md#21-publish-the-application-source-under-the-mit-licence), [A28](architecture.md#28-keep-diagnostics-on-device-with-deliberate-support-exports), [C3](constitution.md#3-on-device-diagnostics-and-deliberate-sharing), [UX48](ux.md#48-let-users-review-a-diagnostic-report-before-sharing-it).
  - Depends on: [T003](#t003), [T011](#t011), [T033](#t033).
  - Complete when: Collect only allowlisted sanitized technical fields on-device, enforce seven-day/10 MB log limits and manual clearing, and exclude diagnostics from sync. Test secret-bearing error paths and third-party defaults. Generate reports offline, preview/omit sections, Save Report or Open GitHub Issue with manual attachment guidance; no automatic upload, issue submission, screenshots, vault files or raw memory. Finalize report packaging.

### Separate native mobile applications

<a id="t076"></a>

- [ ] **T076 — Implement the dedicated iPhone application**
  - Approved delivery: R2 — separate native iPhone and iPad products with released feature parity; R4 — advanced-feature UI additions.
  - Sources: [F01](specifications.md#1-access-the-password-manager-on-supported-devices), [A13](architecture.md#13-build-four-separate-native-applications), [A14](architecture.md#14-recommend-swift-for-each-apple-application), [A18](architecture.md#18-support-the-current-and-previous-major-os-generations), [A22](architecture.md#22-distribute-mobile-applications-through-the-platform-stores), [UX01](ux.md#1-feel-at-home-on-each-platform), [UX02](ux.md#2-adopt-liquid-glass-on-apple-platforms), [UX03](ux.md#3-follow-established-platform-conventions), [UX08](ux.md#8-make-search-and-quick-actions-feel-effortless), [UX19](ux.md#19-use-items-search-and-settings-tabs-on-iphone), [UX22](ux.md#22-create-and-edit-entries-in-an-appropriately-sized-native-form), [UX24](ux.md#24-offer-biometrics-automatically-when-deliberately-opening-the-locked-app), [UX25](ux.md#25-use-clear-recognizable-entry-rows-across-platforms), [UX26](ux.md#26-keep-entry-details-clearly-organized-across-platforms), [UX33](ux.md#33-organize-settings-by-purpose-and-make-preference-scope-clear).
  - Depends on: [T009](#t009), [T013](#t013), [T019](#t019), [T021](#t021), [T022](#t022), [T031](#t031), [T043](#t043).
  - Complete when: Create its own iPhone target with Liquid Glass Items/Search/Settings tabs, filters, native push/back details, toolbar + and full-screen Save/Cancel editor. Implement shared-session unlock with one deliberate automatic biometric attempt, no retry loop and vault-password/exclusion options. Preserve encrypted drafts, source/destination labels and native grouped Settings; connect platform capabilities through their validated adapters.

<a id="t077"></a>

- [ ] **T077 — Implement the dedicated iPad application**
  - Approved delivery: R2 — separate native iPhone and iPad products with released feature parity; R4 — advanced-feature UI additions.
  - Sources: [F01](specifications.md#1-access-the-password-manager-on-supported-devices), [A13](architecture.md#13-build-four-separate-native-applications), [A14](architecture.md#14-recommend-swift-for-each-apple-application), [A18](architecture.md#18-support-the-current-and-previous-major-os-generations), [A22](architecture.md#22-distribute-mobile-applications-through-the-platform-stores), [UX01](ux.md#1-feel-at-home-on-each-platform), [UX02](ux.md#2-adopt-liquid-glass-on-apple-platforms), [UX03](ux.md#3-follow-established-platform-conventions), [UX08](ux.md#8-make-search-and-quick-actions-feel-effortless), [UX20](ux.md#20-adapt-the-ipad-layout-to-the-available-window-width), [UX22](ux.md#22-create-and-edit-entries-in-an-appropriately-sized-native-form), [UX23](ux.md#23-keep-ipad-search-close-to-the-entry-list), [UX24](ux.md#24-offer-biometrics-automatically-when-deliberately-opening-the-locked-app), [UX25](ux.md#25-use-clear-recognizable-entry-rows-across-platforms), [UX26](ux.md#26-keep-entry-details-clearly-organized-across-platforms), [UX33](ux.md#33-organize-settings-by-purpose-and-make-preference-scope-clear), [UX49](ux.md#49-add-and-inspect-attachments-through-native-controls).
  - Depends on: [T009](#t009), [T013](#t013), [T019](#t019), [T021](#t021), [T022](#t022), [T031](#t031), [T043](#t043).
  - Complete when: Create a separate iPad target with Liquid Glass, three/two/one-column layouts based on window width, preserved selection/scroll during multitasking, touch/pointer/keyboard and ⌘F above-list search or compact search view. Use appropriately sized editors, protected drafts and mobile unlock behavior, native pickers and attachment drag/drop. This is not an iPhone compatibility screen or the Mac product.

<a id="t078"></a>

- [ ] **T078 — Implement the dedicated Android application**
  - Approved delivery: R3 — separate native Android product with released feature parity; R4 — advanced-feature UI additions.
  - Sources: [F01](specifications.md#1-access-the-password-manager-on-supported-devices), [A13](architecture.md#13-build-four-separate-native-applications), [A15](architecture.md#15-recommend-kotlin-for-the-android-application), [A18](architecture.md#18-support-the-current-and-previous-major-os-generations), [A22](architecture.md#22-distribute-mobile-applications-through-the-platform-stores), [UX01](ux.md#1-feel-at-home-on-each-platform), [UX03](ux.md#3-follow-established-platform-conventions), [UX08](ux.md#8-make-search-and-quick-actions-feel-effortless), [UX21](ux.md#21-use-material-3-navigation-adapted-to-the-window-size), [UX22](ux.md#22-create-and-edit-entries-in-an-appropriately-sized-native-form), [UX24](ux.md#24-offer-biometrics-automatically-when-deliberately-opening-the-locked-app), [UX25](ux.md#25-use-clear-recognizable-entry-rows-across-platforms), [UX26](ux.md#26-keep-entry-details-clearly-organized-across-platforms), [UX33](ux.md#33-organize-settings-by-purpose-and-make-preference-scope-clear).
  - Depends on: [T009](#t009), [T013](#t013), [T019](#t019), [T021](#t021), [T022](#t022), [T031](#t031), [T043](#t043).
  - Complete when: Create the Kotlin/Compose product with Material 3 dynamic color, phone Items/Search/Settings navigation and labeled New Item FAB; adapt larger windows to a rail and list/details. Implement Android Back, compact/wide native editing, protected drafts and one deliberate biometric attempt with password/exclusion fallback. Build/test the selected ABIs and supported OS generations.

<a id="t079"></a>

- [ ] **T079 — Validate mobile lock, secure-storage and local-only behavior**
  - Approved delivery: R2 — Apple mobile security/local-only slice; R3 — Android slice. Do not couple one platform’s completion to the other.
  - Sources: [F07](specifications.md#7-use-the-password-manager-offline), [F09](specifications.md#9-unlock-with-a-master-password-or-optional-biometrics), [F10](specifications.md#10-recover-access-using-a-recovery-key), [F11](specifications.md#11-lock-the-vault-automatically), [F16](specifications.md#16-view-copy-and-edit-credentials-manually), [F32](specifications.md#32-lock-manually-and-change-the-master-password), [F40](specifications.md#40-manage-multiple-independently-protected-vaults), [F45](specifications.md#45-keep-a-vault-local-without-cloud-synchronization), [A04](architecture.md#4-isolate-vault-keys-and-recovery-paths), [A06](architecture.md#6-separate-vault-logic-from-platform-integrations), [A26](architecture.md#26-support-local-only-vault-storage), [A35](architecture.md#35-make-password-clipboard-clearing-optional), [A43](architecture.md#43-preserve-unsaved-edits-as-encrypted-local-drafts), [A45](architecture.md#45-reauthorize-biometric-unlocking-after-enrollment-changes).
  - Depends on: [T018](#t018), [T019](#t019), [T020](#t020), [T032](#t032), [T076](#t076), [T077](#t077), [T078](#t078).
  - Complete when: On real supported devices, verify enrollment changes, no device-PIN fallback, shared-session authentication, lock/background/termination races, optional re-entry and post-sync password requirements. Validate local-only cloud-backup exclusion, encrypted drafts, clipboard change tracking and preview/key cleanup. Record platform execution limits accurately rather than weakening lock guarantees.

<a id="t080"></a>

- [ ] **T080 — Connect mobile storage, sync, migration, backup and sharing**
  - Approved delivery: R2 — Apple mobile storage/sync/backup workflows; R3 — Android equivalent; R4 — shared-vault/individual-share integration.
  - Sources: [F05](specifications.md#5-synchronize-credentials-across-devices), [F07](specifications.md#7-use-the-password-manager-offline), [F21](specifications.md#21-create-and-restore-encrypted-backups), [F22](specifications.md#22-set-up-a-vault-and-connect-additional-devices), [F23](specifications.md#23-view-known-device-activity-and-understand-access-controls), [F24](specifications.md#24-see-synchronization-status), [F35](specifications.md#35-share-entries-and-vaults-with-other-people), [F36](specifications.md#36-send-an-encrypted-copy-of-an-item), [F39](specifications.md#39-store-documents-and-attachments), [F40](specifications.md#40-manage-multiple-independently-protected-vaults), [F41](specifications.md#41-synchronize-vault-files-through-icloud-drive-and-google-drive), [F45](specifications.md#45-keep-a-vault-local-without-cloud-synchronization), [F46](specifications.md#46-change-an-existing-vaults-storage-mode-or-cloud-provider), [A03](architecture.md#3-use-separate-storage-provider-adapters), [A08](architecture.md#8-make-backups-independent-of-synchronization-history), [A09](architecture.md#9-evaluate-provider-based-sharing-of-separate-encrypted-containers), [A23](architecture.md#23-bind-each-synchronized-vault-to-one-cloud-provider), [A26](architecture.md#26-support-local-only-vault-storage), [A27](architecture.md#27-migrate-vaults-between-local-and-cloud-storage), [A29](architecture.md#29-keep-attachments-within-the-complete-local-vault).
  - Depends on: [T045](#t045), [T046](#t046), [T047](#t047), [T048](#t048), [T050](#t050), [T051](#t051), [T052](#t052), [T053](#t053), [T054](#t054), [T059](#t059), [T060](#t060), [T079](#t079).
  - Complete when: Integrate Google Drive on iPhone/iPad/Android and iCloud on Apple only with native authorization/file pickers. Expose create/open/recovery, full downloads, conflicts, device status, deletion/migration, backups and sharing through each app. Test actual Apple↔Android synchronization via Drive and Apple↔Apple via iCloud, preserving full attachments and offline edits.

<a id="t081"></a>

- [ ] **T081 — Implement Apple mobile Safari and app autofill**
  - Approved delivery: R2 — Safari and compatible Apple mobile app password autofill/save; R4 — OTP/card/identity enhancements where supported.
  - Sources: [F04](specifications.md#4-autofill-credentials-from-the-browser), [F08](specifications.md#8-autofill-credentials-in-mobile-applications), [F14](specifications.md#14-capture-and-update-logins-from-websites), [F19](specifications.md#19-choose-accounts-and-match-websites-correctly), [F26](specifications.md#26-generate-and-fill-authenticator-codes), [F38](specifications.md#38-store-and-fill-payment-cards-and-identity-information), [A06](architecture.md#6-separate-vault-logic-from-platform-integrations), [A14](architecture.md#14-recommend-swift-for-each-apple-application), [A17](architecture.md#17-keep-browser-automation-separate-from-native-application-views), [A31](architecture.md#31-match-website-credentials-to-explicitly-approved-hosts), [A38](architecture.md#38-preserve-optional-card-and-identity-fields-across-native-clients), [UX29](ux.md#29-offer-a-compact-browser-prompt-to-save-or-update-a-login), [UX43](ux.md#43-make-authenticator-codes-easy-to-read-and-copy), [UX45](ux.md#45-review-the-destination-and-fields-before-filling-cards-or-identities), [UX50](ux.md#50-offer-optional-platform-specific-autofill-onboarding).
  - Depends on: [T010](#t010), [T030](#t030), [T062](#t062), [T076](#t076), [T077](#t077), [T079](#t079).
  - Complete when: Build entitled native credential providers for the distinct iPhone/iPad products. Validate Safari and compatible app login selection, association/unlock rules, offline filling and supported save/update/OTP/card/identity surfaces. Apply explicit fill review and no payment submission, plus login-only auto-submit only where supported. Add optional native setup instructions; disclose platform limitations rather than silently dropping scope.

<a id="t082"></a>

- [ ] **T082 — Implement Android Chrome and application autofill**
  - Approved delivery: R3 — Chrome and compatible Android app password autofill/save; R4 — OTP/card/identity enhancements where supported.
  - Sources: [F04](specifications.md#4-autofill-credentials-from-the-browser), [F08](specifications.md#8-autofill-credentials-in-mobile-applications), [F14](specifications.md#14-capture-and-update-logins-from-websites), [F19](specifications.md#19-choose-accounts-and-match-websites-correctly), [F26](specifications.md#26-generate-and-fill-authenticator-codes), [F38](specifications.md#38-store-and-fill-payment-cards-and-identity-information), [A06](architecture.md#6-separate-vault-logic-from-platform-integrations), [A15](architecture.md#15-recommend-kotlin-for-the-android-application), [A17](architecture.md#17-keep-browser-automation-separate-from-native-application-views), [A31](architecture.md#31-match-website-credentials-to-explicitly-approved-hosts), [A38](architecture.md#38-preserve-optional-card-and-identity-fields-across-native-clients), [UX29](ux.md#29-offer-a-compact-browser-prompt-to-save-or-update-a-login), [UX43](ux.md#43-make-authenticator-codes-easy-to-read-and-copy), [UX45](ux.md#45-review-the-destination-and-fields-before-filling-cards-or-identities), [UX50](ux.md#50-offer-optional-platform-specific-autofill-onboarding).
  - Depends on: [T010](#t010), [T030](#t030), [T062](#t062), [T078](#t078), [T079](#t079).
  - Complete when: Integrate the validated Android credential/autofill APIs for Chrome and compatible apps with verified associations, account choice, offline data and lock enforcement. Validate supported save/update and OTP/card/identity filling with explicit destination/field review. Honor login-only auto-submit capability and native setup guidance on supported Android/Chrome versions; provide manual fallback where required.

<a id="t083"></a>

- [ ] **T083 — Implement and verify mobile passkeys**
  - Approved delivery: R4 — mobile passkey creation, sign-in, sharing and supported transfer.
  - Sources: [F25](specifications.md#25-create-synchronize-use-and-transfer-passkeys), [F35](specifications.md#35-share-entries-and-vaults-with-other-people), [F36](specifications.md#36-send-an-encrypted-copy-of-an-item), [A41](architecture.md#41-preserve-passkey-lifecycle-and-sharing-semantics), [UX44](ux.md#44-identify-passkeys-clearly-and-use-native-sign-in-flows).
  - Depends on: [T061](#t061), [T080](#t080), [T081](#t081), [T082](#t082).
  - Complete when: Complete real creation/sign-in and supported transfer on iPhone/iPad/Android, preserving RP binding and platform verification requirements. Test Apple↔Android use via Drive, shared-vault access, independent copies where supported, Trash/index lifecycle and offline local access. Record unsupported current transfer routes explicitly.

<a id="t084"></a>

- [ ] **T084 — Complete platform-native mobile feature workflows**
  - Approved delivery: R2 — released Apple mobile feature workflows; R3 — Android equivalents; R4 — remaining advanced workflows on all mobile apps.
  - Sources: [F03](specifications.md#3-save-login-entries), [F06](specifications.md#6-generate-passwords), [F10](specifications.md#10-recover-access-using-a-recovery-key), [F12](specifications.md#12-resolve-conflicting-changes-without-losing-either-version), [F15](specifications.md#15-recover-generated-passwords-from-interrupted-workflows), [F16](specifications.md#16-view-copy-and-edit-credentials-manually), [F17](specifications.md#17-delete-and-restore-entries), [F18](specifications.md#18-inspect-and-restore-previous-versions), [F21](specifications.md#21-create-and-restore-encrypted-backups), [F26](specifications.md#26-generate-and-fill-authenticator-codes), [F27](specifications.md#27-review-password-health), [F28](specifications.md#28-check-passwords-against-known-leaks), [F29](specifications.md#29-organize-entries-with-favorites-folders-and-tags), [F30](specifications.md#30-store-secure-notes-and-custom-fields), [F34](specifications.md#34-generate-memorable-passphrases), [F35](specifications.md#35-share-entries-and-vaults-with-other-people), [F36](specifications.md#36-send-an-encrypted-copy-of-an-item), [F38](specifications.md#38-store-and-fill-payment-cards-and-identity-information), [F39](specifications.md#39-store-documents-and-attachments), [F40](specifications.md#40-manage-multiple-independently-protected-vaults), [F43](specifications.md#43-add-long-notes-to-every-password-and-credit-card), [F47](specifications.md#47-share-on-device-diagnostics-in-a-bug-report), [UX04](ux.md#4-make-everyday-use-delightful), [UX05](ux.md#5-give-each-vault-a-recognizable-identity), [UX06](ux.md#6-make-successful-actions-feel-satisfying), [UX07](ux.md#7-make-the-password-generator-enjoyable-and-readable), [UX09](ux.md#9-give-each-entry-type-a-pleasing-useful-presentation), [UX10](ux.md#10-make-offline-and-synchronization-states-reassuring), [UX11](ux.md#11-give-the-first-launch-a-warm-focused-welcome), [UX12](ux.md#12-make-reversible-actions-forgiving), [UX22](ux.md#22-create-and-edit-entries-in-an-appropriately-sized-native-form), [UX27](ux.md#27-generate-a-password-or-passphrase-from-the-entry-editor), [UX30](ux.md#30-guide-vault-creation-through-focused-steps), [UX31](ux.md#31-guide-opening-an-existing-vault-from-its-storage-location), [UX32](ux.md#32-present-recovery-as-a-dedicated-guided-flow), [UX34](ux.md#34-make-conflicting-entry-versions-easy-to-compare-and-resolve), [UX35](ux.md#35-preview-dated-history-versions-before-restoring), [UX36](ux.md#36-make-trash-accessible-and-restoration-straightforward), [UX37](ux.md#37-present-each-vaults-backup-settings-on-one-clear-screen), [UX38](ux.md#38-preview-a-backup-before-choosing-how-to-restore-it), [UX39](ux.md#39-make-the-destination-and-effect-of-copying-or-moving-clear), [UX42](ux.md#42-present-actionable-password-health-findings-with-clear-scope), [UX43](ux.md#43-make-authenticator-codes-easy-to-read-and-copy), [UX44](ux.md#44-identify-passkeys-clearly-and-use-native-sign-in-flows), [UX45](ux.md#45-review-the-destination-and-fields-before-filling-cards-or-identities), [UX46](ux.md#46-preview-an-independent-copy-and-separate-its-file-from-its-transfer-password), [UX47](ux.md#47-distinguish-shared-file-access-from-shared-vault-credentials), [UX48](ux.md#48-let-users-review-a-diagnostic-report-before-sharing-it), [UX49](ux.md#49-add-and-inspect-attachments-through-native-controls).
  - Depends on: [T027](#t027), [T028](#t028), [T029](#t029), [T030](#t030), [T049](#t049), [T055](#t055), [T056](#t056), [T071](#t071), [T072](#t072), [T073](#t073), [T074](#t074), [T075](#t075), [T080](#t080), [T081](#t081), [T082](#t082), [T083](#t083).
  - Complete when: Deliver the agreed generator sheets/history, rich entry editing, copy/reveal, notes/attachments/previews, conflict/history/Trash, copy/move, backup/restore, health, sharing and diagnostic flows in each app’s native presentation. Preserve phone haptics where supported and exact copied values. Keep Mac-only external migration import/export out of mobile UI; vault opening, encrypted backups and received shares remain available.

<a id="t085"></a>

- [ ] **T085 — Validate mobile background work and overdue scheduling**
  - Approved delivery: R2/R3 — native sync/backup/background behavior per platform; R4 — unlocked leak checks and advanced notifications.
  - Sources: [F05](specifications.md#5-synchronize-credentials-across-devices), [F21](specifications.md#21-create-and-restore-encrypted-backups), [F28](specifications.md#28-check-passwords-against-known-leaks), [F41](specifications.md#41-synchronize-vault-files-through-icloud-drive-and-google-drive), [A03](architecture.md#3-use-separate-storage-provider-adapters), [A08](architecture.md#8-make-backups-independent-of-synchronization-history), [A33](architecture.md#33-make-leaked-password-checks-opt-in-through-hibp), [A36](architecture.md#36-keep-system-notification-content-generic).
  - Depends on: [T053](#t053), [T072](#t072), [T074](#t074), [T080](#t080), [T084](#t084).
  - Complete when: Exercise OS scheduling, suspension, low power, provider authorization loss, offline periods and process termination on iPhone/iPad/Android. Perform due backup after reconnection when permitted, verify writer assignment before publication, and run leak checks only while unlocked/online. Preserve pending work and accurate status without promising exact execution times the OS cannot provide.

### Cross-platform verification, polish and release preparation

<a id="t086"></a>

- [ ] **T086 — Verify native delight and accessibility in running apps**
  - Approved delivery: P0 — preview UX feedback; MVP/R1 — Mac scope; R2 — Apple mobile scope; R3 — Android scope; R4 — complete all-platform UX coverage.
  - Sources: [UX01](ux.md#1-feel-at-home-on-each-platform), [UX02](ux.md#2-adopt-liquid-glass-on-apple-platforms), [UX03](ux.md#3-follow-established-platform-conventions), [UX04](ux.md#4-make-everyday-use-delightful), [UX05](ux.md#5-give-each-vault-a-recognizable-identity), [UX06](ux.md#6-make-successful-actions-feel-satisfying), [UX07](ux.md#7-make-the-password-generator-enjoyable-and-readable), [UX08](ux.md#8-make-search-and-quick-actions-feel-effortless), [UX09](ux.md#9-give-each-entry-type-a-pleasing-useful-presentation), [UX10](ux.md#10-make-offline-and-synchronization-states-reassuring), [UX11](ux.md#11-give-the-first-launch-a-warm-focused-welcome), [UX12](ux.md#12-make-reversible-actions-forgiving), [UX13](ux.md#13-use-a-three-column-mac-main-window), [UX14](ux.md#14-place-mac-search-in-the-top-toolbar), [UX15](ux.md#15-separate-reading-and-editing-within-the-mac-detail-pane), [UX16](ux.md#16-create-mac-entries-from-the-toolbar), [UX17](ux.md#17-confirm-navigation-away-from-unsaved-mac-edits), [UX18](ux.md#18-present-a-focused-mac-locked-screen), [UX19](ux.md#19-use-items-search-and-settings-tabs-on-iphone), [UX20](ux.md#20-adapt-the-ipad-layout-to-the-available-window-width), [UX21](ux.md#21-use-material-3-navigation-adapted-to-the-window-size), [UX22](ux.md#22-create-and-edit-entries-in-an-appropriately-sized-native-form), [UX23](ux.md#23-keep-ipad-search-close-to-the-entry-list), [UX24](ux.md#24-offer-biometrics-automatically-when-deliberately-opening-the-locked-app), [UX25](ux.md#25-use-clear-recognizable-entry-rows-across-platforms), [UX26](ux.md#26-keep-entry-details-clearly-organized-across-platforms), [UX27](ux.md#27-generate-a-password-or-passphrase-from-the-entry-editor), [UX33](ux.md#33-organize-settings-by-purpose-and-make-preference-scope-clear).
  - Depends on: [T043](#t043), [T076](#t076), [T077](#t077), [T078](#t078), [T084](#t084).
  - Complete when: Review all four running apps with VoiceOver/TalkBack, keyboard/pointer/touch, system text size, contrast, appearance, reduced motion/transparency and haptic preferences. Validate Liquid Glass in Apple navigation/control layers, Material 3 on Android and all eight accepted delightful touches. Ensure readable labels/non-color cues, stable controls, correct focus and no decoration delaying lock or revealing secrets. Record feedback as concrete follow-up tasks.

<a id="t087"></a>

- [ ] **T087 — Validate capacity, performance and failure bounds**
  - Approved delivery: MVP — local Mac validation/review; R1 — Mac sync/browser scope; R2 — Apple mobile scope; R3 — Android scope; R4 — complete integrated coverage.
  - Sources: [F02](specifications.md#2-search-for-passwords), [F07](specifications.md#7-use-the-password-manager-offline), [F18](specifications.md#18-inspect-and-restore-previous-versions), [F39](specifications.md#39-store-documents-and-attachments), [F43](specifications.md#43-add-long-notes-to-every-password-and-credit-card), [A02](architecture.md#2-persist-and-process-vault-data-on-the-device), [A05](architecture.md#5-preserve-concurrent-changes-durably), [A07](architecture.md#7-treat-kdbx-as-a-conditional-format-choice), [A16](architecture.md#16-share-one-native-vault-library-across-four-separate-applications), [A29](architecture.md#29-keep-attachments-within-the-complete-local-vault).
  - Depends on: [T015](#t015), [T023](#t023), [T047](#t047), [T053](#t053), [T061](#t061), [T079](#t079), [T085](#t085).
  - Complete when: Measure large-vault/history/attachment operations, search, KDF unlock and memory in all apps and credential processes on both supported generations. Exercise disk full, resource exhaustion, canceled previews/downloads, malformed archives and parser/decompression bounds. Tune documented limits without truncating data or treating the configurable attachment limit as a parser safety boundary.

<a id="t088"></a>

- [ ] **T088 — Review and harden the integrated security implementation**
  - Approved delivery: MVP — local Mac validation/review; R1 — Mac sync/browser scope; R2 — Apple mobile scope; R3 — Android scope; R4 — complete integrated coverage.
  - Sources: [F09](specifications.md#9-unlock-with-a-master-password-or-optional-biometrics), [F10](specifications.md#10-recover-access-using-a-recovery-key), [F19](specifications.md#19-choose-accounts-and-match-websites-correctly), [F25](specifications.md#25-create-synchronize-use-and-transfer-passkeys), [F32](specifications.md#32-lock-manually-and-change-the-master-password), [F35](specifications.md#35-share-entries-and-vaults-with-other-people), [F36](specifications.md#36-send-an-encrypted-copy-of-an-item), [F42](specifications.md#42-prefer-portable-keepass-compatible-vault-files-where-feasible), [A04](architecture.md#4-isolate-vault-keys-and-recovery-paths), [A06](architecture.md#6-separate-vault-logic-from-platform-integrations), [A07](architecture.md#7-treat-kdbx-as-a-conditional-format-choice), [A09](architecture.md#9-evaluate-provider-based-sharing-of-separate-encrypted-containers), [A10](architecture.md#10-transfer-encrypted-individual-copies-without-expiring-links), [A16](architecture.md#16-share-one-native-vault-library-across-four-separate-applications), [A17](architecture.md#17-keep-browser-automation-separate-from-native-application-views), [A31](architecture.md#31-match-website-credentials-to-explicitly-approved-hosts), [A41](architecture.md#41-preserve-passkey-lifecycle-and-sharing-semantics), [A45](architecture.md#45-reauthorize-biometric-unlocking-after-enrollment-changes), [C1](constitution.md#1-open-source-under-the-mit-licence), [C2](constitution.md#2-public-source-and-private-release-credentials), [C3](constitution.md#3-on-device-diagnostics-and-deliberate-sharing), [C4](constitution.md#4-owner-controlled-recovery), [D02](architecture.md#decisions-required-before-core-development), [D03](architecture.md#decisions-required-before-core-development), [D04](architecture.md#decisions-required-before-core-development), [D05](architecture.md#decisions-required-before-core-development).
  - Depends on: [T048](#t048), [T059](#t059), [T060](#t060), [T063](#t063), [T069](#t069), [T075](#t075), [T079](#t079), [T083](#t083), [T085](#t085), [T087](#t087).
  - Complete when: Review actual crypto/recovery, dependencies, bindings, IPC/caller trust, parser boundaries, key lifecycle and authenticated sync against the threat model. Run meaningful corruption/fuzz/fault tests and secret-leak checks; resolve findings and document residual limits before trusted release. Passing the earlier experiments is not a security review of production code.

<a id="t089"></a>

- [ ] **T089 — Run end-to-end preservation and compatibility tests**
  - Approved delivery: MVP — local Mac validation/review; R1 — Mac sync/browser scope; R2 — Apple mobile scope; R3 — Android scope; R4 — complete integrated coverage.
  - Sources: [F01](specifications.md#1-access-the-password-manager-on-supported-devices), [F04](specifications.md#4-autofill-credentials-from-the-browser), [F05](specifications.md#5-synchronize-credentials-across-devices), [F07](specifications.md#7-use-the-password-manager-offline), [F10](specifications.md#10-recover-access-using-a-recovery-key), [F12](specifications.md#12-resolve-conflicting-changes-without-losing-either-version), [F13](specifications.md#13-import-existing-passwords), [F17](specifications.md#17-delete-and-restore-entries), [F18](specifications.md#18-inspect-and-restore-previous-versions), [F20](specifications.md#20-export-vault-data), [F21](specifications.md#21-create-and-restore-encrypted-backups), [F25](specifications.md#25-create-synchronize-use-and-transfer-passkeys), [F32](specifications.md#32-lock-manually-and-change-the-master-password), [F35](specifications.md#35-share-entries-and-vaults-with-other-people), [F36](specifications.md#36-send-an-encrypted-copy-of-an-item), [F39](specifications.md#39-store-documents-and-attachments), [F40](specifications.md#40-manage-multiple-independently-protected-vaults), [F41](specifications.md#41-synchronize-vault-files-through-icloud-drive-and-google-drive), [F42](specifications.md#42-prefer-portable-keepass-compatible-vault-files-where-feasible), [F45](specifications.md#45-keep-a-vault-local-without-cloud-synchronization), [F46](specifications.md#46-change-an-existing-vaults-storage-mode-or-cloud-provider), [A05](architecture.md#5-preserve-concurrent-changes-durably), [A07](architecture.md#7-treat-kdbx-as-a-conditional-format-choice), [A08](architecture.md#8-make-backups-independent-of-synchronization-history), [A18](architecture.md#18-support-the-current-and-previous-major-os-generations), [A23](architecture.md#23-bind-each-synchronized-vault-to-one-cloud-provider), [A27](architecture.md#27-migrate-vaults-between-local-and-cloud-storage).
  - Depends on: [T057](#t057), [T058](#t058), [T064](#t064), [T065](#t065), [T066](#t066), [T067](#t067), [T068](#t068), [T069](#t069), [T080](#t080), [T083](#t083), [T084](#t084), [T085](#t085), [T087](#t087).
  - Complete when: Test common fixtures across all four apps and actual providers: offline edits, concurrent credential changes, locked staging, delete/edit races, migration with late writers, backup handover, wrong-key restore and full attachment/history preservation. Exercise current/previous OS and Chrome versions, bundled Safari, native autofill and passkey ceremonies. Validate claimed external KDBX/import/transfer compatibility and local-only network/backup exclusions; preserve evidence and repair failures.

<a id="t090"></a>

- [ ] **T090 — Review running applications against every UX requirement**
  - Approved delivery: P0 — preview UX feedback; MVP/R1 — Mac scope; R2 — Apple mobile scope; R3 — Android scope; R4 — complete all-platform UX coverage.
  - Sources: [UX01](ux.md#1-feel-at-home-on-each-platform), [UX02](ux.md#2-adopt-liquid-glass-on-apple-platforms), [UX03](ux.md#3-follow-established-platform-conventions), [UX04](ux.md#4-make-everyday-use-delightful), [UX05](ux.md#5-give-each-vault-a-recognizable-identity), [UX06](ux.md#6-make-successful-actions-feel-satisfying), [UX07](ux.md#7-make-the-password-generator-enjoyable-and-readable), [UX08](ux.md#8-make-search-and-quick-actions-feel-effortless), [UX09](ux.md#9-give-each-entry-type-a-pleasing-useful-presentation), [UX10](ux.md#10-make-offline-and-synchronization-states-reassuring), [UX11](ux.md#11-give-the-first-launch-a-warm-focused-welcome), [UX12](ux.md#12-make-reversible-actions-forgiving), [UX13](ux.md#13-use-a-three-column-mac-main-window), [UX14](ux.md#14-place-mac-search-in-the-top-toolbar), [UX15](ux.md#15-separate-reading-and-editing-within-the-mac-detail-pane), [UX16](ux.md#16-create-mac-entries-from-the-toolbar), [UX17](ux.md#17-confirm-navigation-away-from-unsaved-mac-edits), [UX18](ux.md#18-present-a-focused-mac-locked-screen), [UX19](ux.md#19-use-items-search-and-settings-tabs-on-iphone), [UX20](ux.md#20-adapt-the-ipad-layout-to-the-available-window-width), [UX21](ux.md#21-use-material-3-navigation-adapted-to-the-window-size), [UX22](ux.md#22-create-and-edit-entries-in-an-appropriately-sized-native-form), [UX23](ux.md#23-keep-ipad-search-close-to-the-entry-list), [UX24](ux.md#24-offer-biometrics-automatically-when-deliberately-opening-the-locked-app), [UX25](ux.md#25-use-clear-recognizable-entry-rows-across-platforms), [UX26](ux.md#26-keep-entry-details-clearly-organized-across-platforms), [UX27](ux.md#27-generate-a-password-or-passphrase-from-the-entry-editor), [UX28](ux.md#28-present-a-compact-login-autofill-chooser-in-mac-browsers), [UX29](ux.md#29-offer-a-compact-browser-prompt-to-save-or-update-a-login), [UX30](ux.md#30-guide-vault-creation-through-focused-steps), [UX31](ux.md#31-guide-opening-an-existing-vault-from-its-storage-location), [UX32](ux.md#32-present-recovery-as-a-dedicated-guided-flow), [UX33](ux.md#33-organize-settings-by-purpose-and-make-preference-scope-clear), [UX34](ux.md#34-make-conflicting-entry-versions-easy-to-compare-and-resolve), [UX35](ux.md#35-preview-dated-history-versions-before-restoring), [UX36](ux.md#36-make-trash-accessible-and-restoration-straightforward), [UX37](ux.md#37-present-each-vaults-backup-settings-on-one-clear-screen), [UX38](ux.md#38-preview-a-backup-before-choosing-how-to-restore-it), [UX39](ux.md#39-make-the-destination-and-effect-of-copying-or-moving-clear), [UX40](ux.md#40-preview-imports-and-review-possible-duplicates-before-applying-them), [UX41](ux.md#41-make-export-scope-format-and-protection-explicit), [UX42](ux.md#42-present-actionable-password-health-findings-with-clear-scope), [UX43](ux.md#43-make-authenticator-codes-easy-to-read-and-copy), [UX44](ux.md#44-identify-passkeys-clearly-and-use-native-sign-in-flows), [UX45](ux.md#45-review-the-destination-and-fields-before-filling-cards-or-identities), [UX46](ux.md#46-preview-an-independent-copy-and-separate-its-file-from-its-transfer-password), [UX47](ux.md#47-distinguish-shared-file-access-from-shared-vault-credentials), [UX48](ux.md#48-let-users-review-a-diagnostic-report-before-sharing-it), [UX49](ux.md#49-add-and-inspect-attachments-through-native-controls), [UX50](ux.md#50-offer-optional-platform-specific-autofill-onboarding).
  - Depends on: [T043](#t043), [T070](#t070), [T084](#t084), [T086](#t086).
  - Complete when: Maintain a 50-requirement walkthrough checklist using running native builds, starting with Mac feedback from T012/T043 and continuing as each mobile app becomes available. Include empty/loading/offline/locked/failure states and all confirmation/default behaviors. Refine concrete issues from use without reopening the completed UX interview or requiring static mockups.

<a id="t091"></a>

- [ ] **T091 — Implement and verify the Sparkle Mac updater**
  - Approved delivery: R1 — verified Sparkle update path for the first planned public Mac release; maintain it for later releases.
  - Sources: [F44](specifications.md#44-update-the-mac-application-from-within-pwdtwo), [A20](architecture.md#20-distribute-the-notarized-mac-application-through-github-and-66ideascom), [A24](architecture.md#24-use-sparkle-for-built-in-macos-updates-following-md22), [C2](constitution.md#2-public-source-and-private-release-credentials), [C3](constitution.md#3-on-device-diagnostics-and-deliberate-sharing).
  - Depends on: [T033](#t033), [T042](#t042), [T075](#t075).
  - Complete when: Use MD22’s integration approach with a maintained pinned Sparkle version and PWDTWO-specific signed HTTPS feed/archive configuration. Check every 24 hours when possible, allow disabling checks and retain manual checks; require explicit approval for every installation. Disable automatic-install opt-in, embedded HTML release notes and system profiling. Validate signatures/rejection, offline use, postponement and safe relaunch preserving drafts/pending changes and recoverable format migration.

<a id="t092"></a>

- [ ] **T092 — Prepare signed and notarized Mac release artifacts**
  - Approved delivery: R1 — Mac-only release preparation after its scoped reviews; R4 — updated Mac release for advanced features.
  - Sources: [F01](specifications.md#1-access-the-password-manager-on-supported-devices), [F44](specifications.md#44-update-the-mac-application-from-within-pwdtwo), [A18](architecture.md#18-support-the-current-and-previous-major-os-generations), [A19](architecture.md#19-support-apple-silicon-exclusively-on-macos), [A20](architecture.md#20-distribute-the-notarized-mac-application-through-github-and-66ideascom), [A21](architecture.md#21-publish-the-application-source-under-the-mit-licence), [A24](architecture.md#24-use-sparkle-for-built-in-macos-updates-following-md22), [A25](architecture.md#25-use-pwdtwo-as-the-application-name), [C1](constitution.md#1-open-source-under-the-mit-licence), [C2](constitution.md#2-public-source-and-private-release-credentials).
  - Depends on: [T088](#t088), [T089](#t089), [T090](#t090), [T091](#t091).
  - Complete when: Select packaging and exact GitHub asset/appcast/66ideas.com link locations; prepare reproducible arm64 builds with correct nested signatures, Hardened Runtime/entitlements and timestamps. Notarize/staple/verify Gatekeeper and downloaded artifacts with private credentials outside source. Finalize Safari/Chrome extension distribution and installation/update compatibility. Publication is a separate deliberate release action, not part of generating this backlog.

<a id="t093"></a>

- [ ] **T093 — Prepare separate iPhone and iPad store releases**
  - Approved delivery: R2 — separate iPhone/iPad App Store release preparation; R4 — advanced-feature releases.
  - Sources: [F01](specifications.md#1-access-the-password-manager-on-supported-devices), [A13](architecture.md#13-build-four-separate-native-applications), [A14](architecture.md#14-recommend-swift-for-each-apple-application), [A18](architecture.md#18-support-the-current-and-previous-major-os-generations), [A21](architecture.md#21-publish-the-application-source-under-the-mit-licence), [A22](architecture.md#22-distribute-mobile-applications-through-the-platform-stores), [A25](architecture.md#25-use-pwdtwo-as-the-application-name), [C1](constitution.md#1-open-source-under-the-mit-licence), [C2](constitution.md#2-public-source-and-private-release-credentials), [C3](constitution.md#3-on-device-diagnostics-and-deliberate-sharing).
  - Depends on: [T088](#t088), [T089](#t089), [T090](#t090).
  - Complete when: Prepare distinct signed products, identifiers, provisioning and App Store metadata/screenshots, privacy declarations and review instructions matching actual capabilities and diagnostics behavior. Verify both supported generations and store delivery/updates, preserving separate native iPhone and iPad products and keeping official credentials private.

<a id="t094"></a>

- [ ] **T094 — Prepare the Android Google Play release**
  - Approved delivery: R3 — Android Google Play release preparation; R4 — advanced-feature release.
  - Sources: [F01](specifications.md#1-access-the-password-manager-on-supported-devices), [A13](architecture.md#13-build-four-separate-native-applications), [A15](architecture.md#15-recommend-kotlin-for-the-android-application), [A18](architecture.md#18-support-the-current-and-previous-major-os-generations), [A21](architecture.md#21-publish-the-application-source-under-the-mit-licence), [A22](architecture.md#22-distribute-mobile-applications-through-the-platform-stores), [A25](architecture.md#25-use-pwdtwo-as-the-application-name), [C1](constitution.md#1-open-source-under-the-mit-licence), [C2](constitution.md#2-public-source-and-private-release-credentials), [C3](constitution.md#3-on-device-diagnostics-and-deliberate-sharing).
  - Depends on: [T088](#t088), [T089](#t089), [T090](#t090).
  - Complete when: Prepare the signed Android artifact for selected ABIs, current validated target SDK requirements, store metadata/screenshots, data-safety declarations and credential-provider setup. Verify update/data preservation across supported generations and keep signing material outside public source. Store submission remains a deliberate release step.

<a id="t095"></a>

- [ ] **T095 — Document builds, recovery, compatibility and support**
  - Approved delivery: MVP — development-build documentation/readiness; R1/R2/R3 — each release’s scoped documentation and checks; R4 — final full-scope closure.
  - Sources: [F10](specifications.md#10-recover-access-using-a-recovery-key), [F13](specifications.md#13-import-existing-passwords), [F20](specifications.md#20-export-vault-data), [F21](specifications.md#21-create-and-restore-encrypted-backups), [F23](specifications.md#23-view-known-device-activity-and-understand-access-controls), [F25](specifications.md#25-create-synchronize-use-and-transfer-passkeys), [F35](specifications.md#35-share-entries-and-vaults-with-other-people), [F36](specifications.md#36-send-an-encrypted-copy-of-an-item), [F41](specifications.md#41-synchronize-vault-files-through-icloud-drive-and-google-drive), [F42](specifications.md#42-prefer-portable-keepass-compatible-vault-files-where-feasible), [F44](specifications.md#44-update-the-mac-application-from-within-pwdtwo), [F45](specifications.md#45-keep-a-vault-local-without-cloud-synchronization), [F46](specifications.md#46-change-an-existing-vaults-storage-mode-or-cloud-provider), [F47](specifications.md#47-share-on-device-diagnostics-in-a-bug-report), [A07](architecture.md#7-treat-kdbx-as-a-conditional-format-choice), [A20](architecture.md#20-distribute-the-notarized-mac-application-through-github-and-66ideascom), [A21](architecture.md#21-publish-the-application-source-under-the-mit-licence), [A22](architecture.md#22-distribute-mobile-applications-through-the-platform-stores), [A24](architecture.md#24-use-sparkle-for-built-in-macos-updates-following-md22), [A25](architecture.md#25-use-pwdtwo-as-the-application-name), [A28](architecture.md#28-keep-diagnostics-on-device-with-deliberate-support-exports), [C1](constitution.md#1-open-source-under-the-mit-licence), [C2](constitution.md#2-public-source-and-private-release-credentials), [C3](constitution.md#3-on-device-diagnostics-and-deliberate-sharing), [C4](constitution.md#4-owner-controlled-recovery).
  - Depends on: [T057](#t057), [T058](#t058), [T060](#t060), [T075](#t075), [T088](#t088), [T089](#t089), [T091](#t091).
  - Complete when: Write source-build/configuration instructions, dependency notices, supported OS/browser matrix, format/transfer limits, local-only/cloud setup, recovery and old-backup credential guidance, safe sharing/migration and manual diagnostic bug-report instructions. Explain the single-backup policy and lost-secret/data limits clearly. Provide release/update operation guides and the confirmed GitHub/website destinations without exposing release secrets.

<a id="t096"></a>

- [ ] **T096 — Complete release readiness and scope accounting**
  - Approved delivery: MVP — development-build documentation/readiness; R1/R2/R3 — each release’s scoped documentation and checks; R4 — final full-scope closure.
  - Sources: [F01](specifications.md#1-access-the-password-manager-on-supported-devices), [A18](architecture.md#18-support-the-current-and-previous-major-os-generations), [A20](architecture.md#20-distribute-the-notarized-mac-application-through-github-and-66ideascom), [A21](architecture.md#21-publish-the-application-source-under-the-mit-licence), [A22](architecture.md#22-distribute-mobile-applications-through-the-platform-stores), [C1](constitution.md#1-open-source-under-the-mit-licence), [C2](constitution.md#2-public-source-and-private-release-credentials), [C3](constitution.md#3-on-device-diagnostics-and-deliberate-sharing), [C4](constitution.md#4-owner-controlled-recovery), [D01](architecture.md#decisions-required-before-core-development), [D02](architecture.md#decisions-required-before-core-development), [D03](architecture.md#decisions-required-before-core-development), [D04](architecture.md#decisions-required-before-core-development), [D05](architecture.md#decisions-required-before-core-development).
  - Depends on: [T092](#t092), [T093](#t093), [T094](#t094), [T095](#t095).
  - Complete when: Verify every task and source acceptance criterion for the approved release scope, with test evidence, closed relevant gates and explicit unresolved limitations. Check public-source hygiene, dependency notices, artifact integrity and recovery/upgrade paths. Use the approved release assignments and document any subsequent agreed changes; prepare concrete artifacts before any publication decision. This task does not authorize publishing from the present planning request.

## Completion and phase planning

A task is complete only when its stated outcome and applicable source acceptance criteria are implemented and verified on the platforms it covers. Record relevant test/build evidence and limitations alongside its completion. Do not check off platform security or cloud behavior using only synthetic models. Release work does not authorize uploading private data or publishing automatically.

The approved sequence is **P0 → MVP → Release 1 (Mac sync/autofill) → Release 2 (iPhone/iPad) → Release 3 (Android) → Release 4 (advanced capabilities)**. The user approved this implementation baseline on 2026-10-09. T001, T004 and T012 are complete; 93 parent tasks remain pending. A phase slice does not close an umbrella task prematurely. No feature has been removed and no release has been published.


## Phase 0 execution log — 2026-10-09

Phase 0 implementation is in progress. The native sample-data preview lives in `dev/macos-preview/`; it is separate from the earlier feasibility experiments and the future production vault engine.

| ID | Task | Error / observation | Resolution / status |
| --- | --- | --- | --- |
| P0-E01 | T002/T010 | A sandboxed `simctl list devices booted` could not connect to CoreSimulator services. | Mobile runtime validation remains unperformed; it is not required to build the dedicated Mac preview. No emulator result is claimed. |
| P0-E02 | T012 | Swift's Observation macro compiler could not start its nested sandbox (`sandbox_apply: Operation not permitted`). | Resolved: the same SwiftUI build passes with normal compiler service access, Swift 6 and warnings as errors. |
| P0-E03 | T012 | AppKit `cacheDisplay` captured incomplete transparent SwiftUI/Glass layers; a successful PNG write did not establish correct visual output. | Resolved: captured only explicitly identified preview windows with screencapture and visually inspected seven native states. |
| P0-E04 | T010 | Sandboxed passive LocalAuthentication returned service error 4099. | Resolved by rerunning with ordinary OS service access: biometrics available, zero protected item reads; active proof still pending. |
| P0-E05 | T005 | Initial mutation-review test used an attachment method on `EntryTrack` instead of `EntryMut`. | Corrected the test to use the public `as_mut()` adapter and rerun against the unchanged candidate. |
| P0-E06 | T005 | Two new candidate-library regressions reproduced: orphaned historical attachment bytes after entry removal, and missing historical custom-icon references. | Resolved for the two reproduced cases in an isolated copy: 20 active checks pass, two independent-reader checks are explicitly skipped. The original evaluated fork remains unchanged. See the mutation-review report; production adoption is still open. |
| P0-E07 | T005 | Review patch script rejected a source anchor with an extra blank line. | Corrected the exact source anchor; the script failed before changing the baseline, as intended. |


### Current evidence and remaining work

- T002/T003: Mac native baseline, reproducible command-line preview build, licensing and secret exclusions are in place. Complete mobile toolchains, production dependency pinning and CI remain pending; the parent tasks stay open.
- T005: [additional mutation review](../dev/experiments/kdbx-mutation-review/README.md) reproduces two failures and verifies isolated candidate fixes without changing the prior evaluated fork. This does not select a production dependency.
- T010: the provisioned [biometric probe](../dev/experiments/biometric-session/README.md) passes protected two-key reads; the optional Mac preview now opens two encrypted root fixtures through Touch ID. Enrollment changes, OS lock triggers and extension behavior remain unverified.
- P0 is still in progress: format/recovery adoption, shared-core boundaries, real provider concurrency and remaining biometric/extension checks must close before the dependent production features begin. Dedicated cloud test resources and a second device are needed for the provider checks.

### Preview refinement — vector wordmarks, 2026-10-09

User reported jagged sidebar/Settings wordmarks. Replaced runtime PNG downscaling with native SwiftUI paths generated directly from the unchanged supplied light/dark SVGs. The build compiler preserves the original viewBox, outlined curves and fills and rejects unsupported SVG constructs. Sidebar, Settings and lock-screen wordmarks share this renderer. The actual sidebar and a dedicated native six-variant render verify the wordmarks at 128/150/190 points in light/dark appearances; no vault/model behavior changed.

- P0-E08 (T012 refinement): the full render walkthrough failed to complete alongside an existing preview session. A Launch Services retry produced four captures but no completion result. Used a dedicated native brand-render harness for this change; it captured successfully and all six variants were inspected. Full walkthrough completion remains unverified for this refinement.

- P0-E09 (T012 Settings refinement): initial own-window capture failed after title-bar assertions passed. Tightened scene selection to the visible Settings window and explicitly brought it forward before capture; visual verification follows.


### Settings title-bar refinement — 2026-10-09

Separated Settings navigation from the native title bar: removed full-size content underlap, restored an opaque title bar with a separator, and confined the sidebar background to its content area. Swift 6 build and strict signature verification passed. The user inspected the running revision and confirmed, “Looks good now.” Own-window automated capture attempts through Launch Services failed; this acceptance is based on the user's visual confirmation, not a claimed screenshot-check pass.


### Direct favorite toggle — 2026-10-09

Replaced the Mac detail menu's Add/Remove Favorite actions with a star button beside Edit. Outline/filled SF Symbols show the current state, and Star/Unstar tooltips plus accessibility labels/value describe the action and state. Uses the existing favorite operation; Trash remains in the overflow menu. Updated UX15 to preserve the accepted interaction.

Validation: native Swift 6 build, arm64/deployment checks and strict ad-hoc signature verification passed. Opened the rebuilt preview. Model behavior was unchanged; no additional model tests were needed for this presentation change.


### Direct Move to Trash button — 2026-10-09

Replaced the detail overflow menu with a native trash-can button beside the star. It has a Move to Trash tooltip/accessibility label and uses the existing recoverable operation, including Undo. Trashed entries still show Restore. Updated UX15. Swift 6 compilation, arm64/deployment checks and strict ad-hoc signature verification passed; model logic was unchanged.


### Locked-screen refinements — accepted 2026-10-09 (T012 preview; T035/T043 production integration)

- [x] L1 — Add a static blue/indigo glow, adapted to light/dark and increased contrast (UX18.1).
- [x] L2 — Enlarge the supplied icon, add a soft shadow and retain the vector wordmark (UX18.2).
- [x] L3 — Use “Welcome back.” and “Your vaults are locked.” with clear preview disclosure (UX18.3).
- [x] L4 — Add a generous native glass unlock action; retain honest preview labeling. Production Touch ID eligibility remains part of the existing authentication tasks (UX18.4).
- [x] L5 — Add a short unlock-only fade; Reduce Motion and every locking path remain immediate (UX18.5).

These are refinements to the completed synthetic preview, not closure of production authentication tasks.


Locked-screen refinement validation: all five preview items complete. Swift 6 build, strict ad-hoc signature verification and all 28 existing model checks passed, including immediate lock, rejection of locked operations, repeated lock and draft resumption. Inspected the shared LockedScreen view in a dedicated native light/dark render at /private/tmp/pwdtwo-locked-redesign.png. Unlock uses a 0.22-second opacity transition, with animations disabled for locked state and Reduce Motion. Real biometric availability, authentication and production integration remain pending under their original tasks; no biometric symbol or success is simulated here.

- P0-E10 (overnight storage hardening): the raw-component constructor initially used Rust struct-update syntax on a zeroizing Drop type. Replaced it with explicit initialization, preserving zeroization ownership.

- P0-E11 (overnight tests): a synthetic recovery-key mutation test attempted Display on a Zeroizing wrapper. Changed the test to explicitly borrow its string, without adding Display or diagnostic output to the secret type.

- P0-E12 (candidate hardening checks): direct dependency test invocation needed an explicit workspace member. Registered only the generated keepass copy in the experiment workspace; prior experiment sources remain unchanged.


- P0-E13 (2026-10-10 resume): the unattended turn stalled awaiting tool permission for dependency fetch and local OS file services. The completed test artifacts survived. After restart, fetched missing upstream test dependencies and reran the local coordinator successfully. No cloud account or Touch ID interaction occurred.
- P0-E14 (local probe): the sandboxed file-coordination run raised Cocoa error 512. The same binary passes with normal OS access. Replaced top-level fatal-error reporting with a controlled numeric error result; resource measurement remains separate from functional success.

- P0-E15 (hardening validation): upstream test-with 0.17 requires Rust 1.95, newer than the installed 1.92 toolchain. Pinned the isolated candidate’s test-only helper to 0.16.0 (declared MSRV 1.88); production library dependencies are unchanged.

- P0-E16 (upstream unit-test compilation): adding the raw component field required updating one explicit DatabaseKey initializer in the isolated upstream tests. Updated the generated candidate patch; no original vendor source was edited.

- P0-E17 (validation harness): UniFFI generation needs the comparison crate as its working directory; corrected that invocation. Kotlin generation succeeds without optional ktlint. Scoped warnings-as-errors Clippy to our candidate crate with --no-deps; unrelated pre-existing upstream lint findings remain outside that claim.

- P0-E18 (2026-10-10 user-present biometric test): Data Protection Keychain item creation returns -34018 with an ad-hoc command-line signature. Cleanup passes and no protected item is read. Real biometric-only authentication subsequently passes in the native test bundle. A matching provisioned native target is prepared; account-backed signing and protected multi-item reads remain pending.

- P0-E19 (2026-10-10 Xcode account check): saved Apple account list is empty. The installed Xcode 26.6 UI cannot launch on macOS 27.0.1 (-10664, incompatible application version); Apple's support matrix limits that Xcode to macOS 26.x. A compatible Xcode 27 app and user sign-in are required for account-backed provisioning. Existing CLI build results remain valid within their recorded experiment scope; no account or OS settings were changed.

- P0-E20 (2026-10-10 provisioned biometric build): after Xcode 27 update and user sign-in, automatic signing reported that this Mac was not registered and no matching development profile existed. Resolved using explicit device-registration support: development signing/profile verification and the protected two-key run pass.

- P0-E21 (2026-10-10 signing verification): the updated codesign display defaults to human-readable entitlement output, which the plist reader rejected. Resolved by requesting --xml explicitly; app identifier, isolated Keychain group, embedded profile and strict signature verification pass.


### Actual multi-vault opening and Mac Touch ID interface — 2026-10-10

- [x] T009/P0 experiment — Add an explicit exact-32-byte component opening API across Rust/C/Swift, retaining bounded preflight and authenticated metadata checks. Test password identity, password rotation, wrong components, tampered/truncated data and malformed ABI lengths.
- [x] T010/P0 experiment — Open both encrypted fixture files before publishing a shared unlocked state. Permanently retire per-attempt core handles synchronously on lock; reject cancellation/stale callbacks and partial opening. Eight additional real-decryption scenarios pass.
- [x] T010/T035/P0 interface experiment — Connect the provisioned biometric-only adapter to the native locked screen, with busy/cancel/retry states and no sample-unlock bypass. Observe successful actual two-vault opening and shared manual lock in the GUI; verify protected-item/file cleanup in a separate final-build quit run.
- [x] T012/P0 regression — All 32 preview model checks, Swift 6 build, Apple Development/profile isolation, strict signature and arm64/macOS 26 deployment checks pass. Reopen and inspect the final locked screen.

Evidence: [integration result](../dev/experiments/biometric-session/results/preview-integration.json), [cleanup result](../dev/experiments/biometric-session/results/preview-cleanup.json), [foundation suite](../dev/experiments/foundation/results/run-all.json), [Mac validation](../dev/macos-preview/VALIDATION.md). Current Rust suite: 41 passed, two opt-in independent-reader checks not run in this invocation. No new build/test failure occurred in this slice.

These checkboxes close only experimental slices. Parent production tasks stay open: root fixtures are encrypted and opened, but interface entries/edits/drafts remain in memory. Real biometric-enrollment changes, OS lock triggers, extensions, macOS 26 runtime, password/recovery UI, encrypted CRUD and the D02–D05 reviews still remain.

The final signed preview also produced a [local active-session report](../dev/experiments/biometric-session/results/preview-active-session.json) with `actualEncryptedVaultsOpened: 2` and authenticated expected identities. This report is distinct from the separate quit/cleanup run. Settings now explicitly describes the temporary encrypted fixtures, protected keys and optional credential-free local report.

- P0-E22 (optional preview compilation): Xcode 27 emitted transitive-import warnings for the timer’s Combine type in the unprotected build. Added the explicit Combine import; both preview configurations compile cleanly. No authentication behavior changed.

- P0-E23 (local transaction tests): default temporary-directory permissions did not satisfy the private-store policy, so all initial transaction fixtures were rejected. Set test directories explicitly to 0700; the store continues rejecting permissive directories.

- P0-E24 (preview payload bridge compilation): a broad match-arm edit also inserted the payload read into the revision-length validator. Narrowed it to the copy-kind switch; the compiler caught the mistake before any runtime build.

- P0-E25 (preview envelope tests): generic camelCase mapping produced vaultId while Swift writes vaultID. Added explicit acronym mappings in both record and envelope types; the strict interoperability tests caught the mismatch before GUI use.


### Local transaction and encrypted sample-entry slice — 2026-10-10

- [x] T006/T015/P0 candidate — Authenticated staged-file readback, file flush, revision recheck, same-directory publication and explicit post-publication durability uncertainty; no retained automatic backup copy. Cooperating local processes use advisory exclusion. Production/provider durability gates stay open.
- [x] T009/P0 candidate — Connect local publication through the ticketed C ABI and Swift actor; reject stale revisions, wrong keys, duplicate creation and cross-vault identity replacement, including rotation/recovery. A held core-generation guard serializes lock/cancel with publication.
- [x] T005/T014/P0 evaluation — Strict versioned login/card/note preview envelope in encrypted custom data; preserve other supported metadata, reject unknown/future fields/types, duplicates and owner changes. This is not production schema adoption or full accepted-feature coverage.
- [x] T012/T035/P0 preview — Load saved fictional entries from encrypted files after shared authorization. Persist Save/star/Trash/Undo operations before changing the active model; keep failed drafts, remove active records on lock, reject late callbacks and delay Save Changes navigation/close until publication succeeds. Cross-vault moves remain explicitly unconnected.
- [x] T088/P0 checks — Eight local process/transaction checks (including abrupt exits at eight stages, competing writers and a real write failure), native persistence and encrypted-record/model workflows, plus 38 preview model checks. Complete foundation regressions and both native build configurations are verified in the recorded result below.

The preview files remain disposable and reset on normal exit. Unsaved drafts and generator history remain in memory; no production encrypted-CRUD completion is claimed. Parent tasks and D02–D05 adoption/provider/platform reviews stay open. The next model work is the full required schema with history, attachments, conflicts and unknown-data preservation, followed by durable production lifecycle and native password/recovery setup.

Current slice evidence: 46 unit + eight transaction tests, native persistence and encrypted record/model workflows pass in the [foundation report](../dev/experiments/foundation/results/run-all.json); 38 model checks and both UI configurations pass. See [Mac validation](../dev/macos-preview/VALIDATION.md) and [transaction contract](../dev/experiments/foundation/README.md). No parent task count changes.

The rebuilt development-signed preview is open. Its own isolated entitlements and successful preparation of both protected encrypted sample vaults were verified. Latest-stage sensor unlocking was not repeated in the unattended regression suite; prior real Touch ID evidence remains separate. [Curated persistence summary](../dev/experiments/foundation/results/local-persistence-summary.json).


### Persistent local password/recovery interface experiment — 2026-10-10

- [x] T032/T034/P0 native slice — Add a separate local-vault development app and private app-owned, backup-excluded storage. Native name/password/confirmation setup stages the encrypted file until explicit recovery-key save acknowledgement. Use one test vault; do not adopt a production schema or reduce the multi-vault requirement.
- [x] T035/P0 native slice — Open the retained local file by password after a fresh launch, authenticate its envelope and publish only after complete success. Clear password bindings after submission; deny the ordinary preview-unlock bypass. Keep the existing disposable Touch ID mode separate.
- [x] T036/P0 native slice — Stage recovery/new-password replacement, show and confirm the replacement key, preserve entries, and CAS-publish before opening. Cancellation before confirmation preserves the existing file; stale writes and uncertain publication retain honest outcomes. Ordinary password-change UI remains pending.
- [x] T012/T037/T038/P0 integration — Connect the native controller to encrypted saves/favorites/Trash, retain files on quit, clear active records/handles on lock, and distinguish persistent storage in status/Settings/footer. Unsaved drafts/history and preferences still remain in memory.
- [x] T088/P0 evidence — 41 model checks, isolated real controller/model/core workflow and native lifecycle failure/restart checks pass. Native first-launch/create screens were inspected without entering a personal password or creating a user vault. Three build modes are checked separately.

These checkboxes close experimental slices only; the parent completion count stays 3/96. One local vault is a temporary test scope. Multiple independently protected vaults, persistent Touch ID, complete schema/drafts/history, imports/open-file handling and the remaining D02–D05 gates remain required. See [local-mode procedure](../dev/macos-preview/README.md#experimental-persistent-local-vault) and [UI validation](../dev/macos-preview/VALIDATION.md).

- P0-E26 (persistent Touch ID compilation): an attribute-only Keychain check used a deprecated authentication-UI flag, rejected by warnings-as-errors. Replaced it with a noninteractive LAContext; protected material is still never read by the presence check.

- P0-E27 (combined local/Touch ID build): enabling the shared signing flag also compiled the disposable fixture controller without its fixture sources. Restricted that controller to the disposable build; the persistent build uses only its own lifecycle/controller and Keychain service.


### Persistent local Touch ID connection — 2026-10-10

- [x] T010/T034/T035/P0 native slice — Optional, explicitly enabled Touch ID for the persistent local vault. Password-authorized enrollment and Settings control; protected per-device Keychain component retained across quits; native unlock button with password fallback.
- [x] T009/T010/T036/P0 boundary checks — Authenticate the current file before publication, invalidate contexts on shared lock/cancel, reject stale callbacks, require password-authorized re-enrollment, retire stale components and recovery-era enrollment. Never fall back to unprotected key storage or a system-password biometric bypass.
- [x] T088/P0 candidate checks — Controlled adapter plus real persistent encrypted-vault workflow validates enrollment, fresh-controller reuse, failed/cancelled authorization, late callback, password fallback, disabling/re-enabling, recovery rotation and externally stale components. Signing/profile and native compilation checked separately; user-present enrollment/sensor test still required.

The parent tasks remain open; this is the one-vault development mode, not full multi-vault or OS lifecycle acceptance. After rebuilding, save edits and restart, unlock with the password, then enable Touch ID in Settings → Security & Unlocking.

Persistent adapter evidence: [targeted checks and signing](../dev/experiments/foundation/results/persistent-touch-id-summary.json), [usage](../dev/macos-preview/README.md#touch-id-for-the-persistent-local-vault). No user-vault enrollment or hardware prompt was performed by the agent.

Persistent Touch ID user follow-up: native Settings enrollment state was observed off → on during user interaction; the agent did not enable it. [Enrollment-state observation](../dev/experiments/foundation/results/persistent-touch-id-user-enrollment.json). Actual locked-vault sensor opening remains the next hands-on check.

- P0-E28 (multi-vault adapter compilation): a property replacement also altered the protocol declaration into a method body. Restored its get-only requirement and kept the implementation in the concrete adapter; compiler caught this before an app build.

- P0-E29 (multi-vault biometric regression): the password-fallback display mode prevented an explicit retry of Touch ID, leaving the controlled delayed-authorization test waiting. Explicit Touch ID requests now select the biometric mode before validating required passwords; fallback remains the default after an authentication failure.

- P0-E30 (multi-vault UI compilation): the new setup sheet used a projected binding on an immutable controller reference. Made the root reference Bindable so native sheet presentation tracks the existing observable controller.


### Multiple persistent local vaults — 2026-10-10

- [x] T032/T034/P0 native slice — Add independently passworded/recoverable vaults via a native New Vault setup sheet, resolving pending edits before setup. Retain the original personal file/key item; additional files use canonical UUID identities. Cancelled staging preserves existing files and active records.
- [x] T010/T035/T037/P0 shared-session slice — Authenticate every included file/envelope before publishing any records; collect separate passwords and/or use one grouped biometric authorization. Explicitly exclude a vault while retaining file/enrollment. Persist opaque registered/included IDs and retain unavailable registrations until the user chooses to exclude them.
- [x] T009/T036/T038/P0 boundary slice — Validate filename/envelope ownership, save only the owning file, recover only the selected vault and retire only that enrollment. Recovery leaves the shared UI locked until all included members qualify. Scope held in-memory drafts to their owner, including excluded-vault sessions, and keep independent password fields when membership changes.
- [x] T088/P0 evidence — 45 model checks, existing lifecycle/controller/biometric regressions and the new multi-vault real-encryption workflow pass. Full foundation regressions pass with 47 Rust unit + eight transaction checks. Native UI/build/signature checks are recorded separately.

Parent completion count remains 3/96. Names before first opening use opaque labels, the evaluation bound is 16 vaults, and the complete catalog/schema, encrypted drafts/history, normal password-change UI, providers and remaining production/platform gates remain open. The user's successful single-vault Touch ID report is recorded separately from multi-vault sensor validation.

- P0-E31 (native multi-vault UI fixture): workspace-hosted encrypted fixtures had two hard links and correctly failed the private-file read policy. Fresh single-link fixtures in the system temporary directory reopen successfully in both CLI and native GUI; the hard-link rejection remains unchanged.

- T034/P0 confirmation refinement: Swift String equality treats canonically equivalent Unicode as equal, while the approved vault passwords preserve their exact UTF-8 bytes. Native confirmation now compares bytes; controlled UI tests reject differently encoded lookalike confirmations and accept an exact match.

Multiple-vault handover evidence: [current source hashes, native checks and signed artifact](../dev/experiments/foundation/results/multiple-local-vaults-summary.json). Save edits and quit/reopen PWDTWO Local Vault before testing the new build.


### Ordinary local vault password changes — 2026-10-10

User follow-up: the user reported that the launched multiple-vault version works. This does not separately identify physical multi-vault biometric outcomes.

- [x] T017/T036/P0 native slice — Native selected-vault password-change sheet from File and Vaults settings; current-password authentication enforced by the shared core after biometric opening, exact new-password confirmation, preserved recovery key and records, targeted protected-item retirement, cancel/selection/lock input clearing and pending-edit interception.
- [x] T009/T018/T038/T088/P0 boundary evidence — Real encrypted-file checks for wrong current credentials, biometric-only rejection, targeted file/key preservation, original recovery-key usability, old-password/component rejection, unchanged backup protection, failed key retirement, stale writer/shared-lock handling, generation cancellation and re-enrollment.

Parent tasks remain open until their complete production/platform requirements pass.

Password-change evidence: [current-source checks, signed build and isolated native UI](../dev/experiments/foundation/results/password-change-summary.json). 51 model checks, the new credential-change integration and prior persistent/multi-vault workflows pass. The full foundation runner passes (47 unit/eight transaction checks), all 26 source hashes match, and both previous native variants compile. Physical user-present password-change/re-enrollment remains a hands-on check; parent completion remains 3/96.


### Local device settings and optional clipboard clearing — 2026-10-10

- [x] T031/T042/P0 device slice — Retain the supported masking, inactivity timeout and optional clipboard-clearing controls in the local app's own preferences domain, with accepted defaults, bounded values, explicit device scope and no vault content. Test-directory/sample modes remain ephemeral.
- [x] T039/T088/P0 clipboard slice — Route sensitive field/recovery-key Copy through one native adapter; default clearing off, adjustable delay, ownership/change-count checking, later/equal-text copy preservation, locked-session maintenance and opted-in quit cleanup. Do not read/retain clipboard plaintext to decide cleanup.

The full production tasks and remaining preferences/integrations stay open.

- P0-E32 (sample variant compile): Swift 6 warnings-as-errors rejected an unreachable standard-defaults branch where the sample configuration always uses ephemeral settings. Moved service construction into its compile-time configuration branches; the persistent local branch retains its runtime test-directory isolation.

- P0-E33 (native settings test launch): the UI clone was launched without its explicit isolation argument and reached the normal local-vault route. Closed the clone without automated entry edits. Test-suffixed apps and malformed test-directory invocations now fail closed before folder discovery/Keychain setup; a controller regression checks this gate. UI checks will launch the executable with verified arguments. Build artifacts are staged, signed and verified before replacing their published bundle path, avoiding in-place writes to a running executable.

- P0-E34 (empty-catalog native startup): the isolated empty-folder app trapped in PreviewStore.vault during a stale SwiftUI row lookup after startup cleared the catalog. Replaced the unconditional first-vault fallback with a neutral descriptor retaining the requested owner ID; added empty/unknown-catalog model regressions. This startup crash also explains why the first GUI selector relaunched the test clone without its original isolation arguments.

Device-settings handover: 58 model checks and 26 settings/clipboard checks pass, including independent-process reload, named native pasteboard ownership, write/cleanup races, invalid defaults, explicit recovery Copy gating and missing-isolation rejection. Prior persistent/multi-vault/password-change workflows pass; both sample variants compile. Fixed empty-folder native startup and Settings defaults were inspected. [Current-source/artifact evidence](../dev/experiments/foundation/results/device-preferences-summary.json). Parent completion remains 3/96.


### Manual encrypted backup export — 2026-10-10

- [x] T054/T042/P0 export slice — Review one open vault's saved-item/Trash scope, resolve pending edits, authenticate the current saved file, and use a native save dialog for a complete encrypted snapshot. Keep that generation's password/recovery protection; no automatic backups, rekeying, biometric material or plaintext recovery secret are exported.
- [x] T009/T088/P0 export checks — Reject stale live state, live-folder/alias/link destinations, cancellation before publication and detected competing destination revisions; stage private bytes, verify them, sync before rename, distinguish post-publication durability failure and preserve prior files on earlier failure. Existing-file replacement is not atomic CAS against non-cooperating external writers.

Restore UI, complete production backup packaging/schema and scheduled/provider coordination remain separate open slices.

- P0-E35 (native backup filename): configuring NSSavePanel's content type after its suggested name produced a duplicate `.kdbx` suffix. Apply the extension policy first, then the suggested filename; verify the actual native save dialog.

Backup-export handover: 61 model checks, 26 settings/clipboard checks, the new real-encryption export harness and prior local/controller/controlled-biometric/multiple-vault/password-change workflows pass. Native two-vault fixtures verify File and per-vault Settings routes, correct selection/counts, cancellation, a single `.kdbx` extension and successful save with retained records; exported bytes equal the source and are private (0600). Final published signature passes. [Current-source/artifact evidence](../dev/experiments/foundation/results/manual-backup-export-summary.json). No full foundation rerun or new physical sensor test is claimed; parent completion remains 3/96. Save edits and quit/reopen the local app before testing this build.

### Separate local backup restoration — 2026-10-10

- [x] T054/T042/P0 restore slice — Choose and authenticate a captured encrypted backup, review all supported entries/Trash and filesystem date, then create a new local vault with independent vault/entry identities. Password restoration preserves original protection; recovery requires a new password and acknowledged replacement key. Preserve current vaults and source; no sync resumption or partial included-session publication.
- [x] T009/T088/P0 restore boundary — Verify schema/content preservation and unknown-data rejection, password/recovery opening, original-key retention or replacement, independent restart, cancellation/shared lock, absent-file create-only publication and failed/uncertain outcome handling.

Whole-vault replacement, selective cross-vault copying, authenticated backup-date packaging, full schema and production reviews remain open.

- P0-E36 (restore model fixture): the locked-data assertion used the earlier in-memory sample configuration, which intentionally retains fictional rows. Mark the fixture as encrypted before locking so it tests the persistent-vault record-clearing policy.

- P0-E37 (development build overlap): Swift rejected a source modified while a compile was running. Keep implementation files stable during compilation; rerun targeted restore checks, then the complete native build from a fixed source state. No failed staged bundle was published.

- P0-E38 (open-session restored records): the model accepted authenticated record installation only while locked, so a restored file could be saved without immediately appearing in the already-open catalog. Add an explicit persistent-local expansion path gated by an active lifecycle commit, keeping ordinary installation locked-only; regress immediate contents, unauthorized replacement and restart.

- T009/T054/P0 create-only hardening: use exclusive native rename for absent-file publication on Apple targets, and check a non-cooperating external creation at the last publication gate. Ordinary existing-file updates still use the previously documented advisory/revision boundary.

- P0-E39 (exclusive-publication race fixture): the shared setup already created the test's original destination, so the new race check stopped at the earlier revision gate. Use a fresh destination identity to exercise the last-gate external creation and verify exclusive publication preserves it.

- P0-E40 (exclusive-publication lint): warnings-as-errors rejected an unnecessary return in the Apple branch. Use the branch's final Result expression; rerun the required checks without suppressing the lint.


Restore handover: 67 model/26 device checks, real-encryption backup restoration/export and prior local/controller/controlled-biometric/multiple-vault/password-change workflows pass. The full foundation runner passes 48 Rust unit + nine transaction checks, native/offline/provider-fixture/iOS-target checks, lint and release build; all 26 foundation source hashes match. Both prior native variants compile. Isolated native File/Settings routes, locked-state cancellation, real picker, authenticated contents review, immediate three-vault contents and fresh-process grouped reopening pass. Original fixture files and the backup remain byte-identical; the independent saved file is private (0600). Final published signing verification passes. [Current-source/artifact evidence](../dev/experiments/foundation/results/backup-restoration-summary.json). Parent completion remains 3/96; no new physical sensor or production-adoption claim is made. Save edits and quit/reopen PWDTWO Local Vault before testing.

### Selected-entry cross-vault copying — 2026-10-10

- [x] T027/T056/P0 copy slice — Native copy review for selected active entries from one unlocked source, another unlocked destination and an existing folder/top level. Keep originals; create independent destination records, preserving supported fields except explicitly chosen folder/owner/identity. Preserve all existing destination records; pending edits must be resolved.
- [x] T009/T088/P0 copy boundary — Authenticate both encrypted containers, append copies plus an encrypted operation receipt in one destination transaction, reject invalid/reused identities/targets/Trash, verify same-operation replay, original protection and restart, and handle stale writers/lock/cancel/failure without silent loss.

Move, complete history/attachment/organization schema, interrupted-operation resume UI and production adoption remain open. Copy is exposed through an explicit icon, File command and row context menu, retaining the user's direct Star/Trash controls.

- P0-E41 (parallel compatibility compiles): the main build regenerated BrandVectors.swift while earlier sample compiles were reading it. Their compiler guards correctly rejected changing input. Rerun those compiles after asset generation, from stable sources; do not suppress the guard. The main staged build and vault files were unaffected.


Copy handover: 71 model/26 device checks, the new real-encryption copy harness and prior local/export/restore workflows pass. Full foundation validation passes 49 Rust unit + nine transaction checks and required lint/release/native/offline/iOS-target checks; all 26 source hashes match. Both previous native variants compile; strict published signing verifies. Isolated native icon/File/context-menu routes, cancellation, bulk selection, destination folder, immediate seven-row catalog and fresh-process reopening pass. Original source bytes are unchanged; destination authentication verifies independent IDs, all current fields and retained existing records. [Current-source/artifact evidence](../dev/experiments/foundation/results/cross-vault-copy-summary.json). Parent completion remains 3/96. Save edits and quit/reopen the local app before testing. Next: safe Move.


## Autonomous macOS development batch — 2026-10-10

User authorized completing independently actionable macOS work and a consolidated handover. Keep account/hardware/publication-dependent validation explicit; continue independent implementation without per-step review.

- [x] T027/T056 local move — encrypted source intent, destination receipt before source Trash, fresh-process resumption and keep-originals escape path.
- [x] T025/T055 current record history — dated complete snapshots, reviewed restoration and explicit clearing, preserved by copy/move/backup.
- [x] T028/T040 secure generator — licensed substantial English wordlist, unbiased cryptographic choices and category guarantees.
- [x] T029 retained generator values — encrypted per-vault history before use, restart and native review.
- [x] T020 encrypted local drafts — durable device-only preservation, no sync/autofill publication, lock/restart resumption.
- [x] T075 diagnostics — on-device sanitized report with native review/export.

- P0-E42 (move FFI edit): an additive result-kind patch also matched the unrelated expected-revision length switch. Compiler rejected the out-of-scope state reference; restrict the new arm to the output-copy switch and preserve the strict 0/32-byte revision contract. No failed build was published.

- P0-E43 (header changed during compile): the generator ABI was added while the move app was compiling. Its PCH guard rejected the changed header. Keep all Swift/header inputs stable during validation; rebuild the final batch after implementation. The move harness passed and no failed staged bundle was published.

- P0-E44 (stale core linkage): a richer Swift reader was tested against the prior release library and its increased output capacity was correctly rejected by the old ABI resource bound. Rebuild the current locked Rust dependency set before linking native checks; record current core inputs alongside the final artifact. No failed staged bundle was published.

- P0-E45 (offline harness assertion): a throwing decode was placed inside a nonthrowing precondition autoclosure. Decode into a local first, then assert the checked value; retain warnings-as-errors.

- P0-E46 (CSV review initializer): mapping rows captured the partially initialized struct through its baseline property. Capture a fully constructed local baseline instead. Update the oversized-backup fixture to the new explicit 32 MiB container bound introduced for embedded attachments; retain its boundary-rejection assertion.

- P0-E47 (KDBX export adapter): the controlled library exposes attachment iteration through EntryRef and database entry counts through num_entries. Use those inspected APIs; compiler errors are retained and no failed artifact was published.

- P0-E48 (migration test lifetime): a GroupRef borrowed through a temporary root reference. Retain the root binding for the assertion scope; keep the independent database/history/binary checks.

- P0-E49 (independent export assertion): the first external-reader assertion expected an unqualified custom-field name; the adapter deliberately uses a UUID-qualified namespace to retain colliding field names. Verified the actual protected value, history and binary through PyKeePass; no export data loss.
- P0-E50 (native fixture helper): a temporary helper used the controller's testDirectory label for LocalVaultDirectory. Use its inspected directory initializer; the fixture was not created before the compiler rejected the call.
- P0-E51 (folder rename and lint): the subtree regression caught validation that temporarily removed a parent and consequently rejected its descendants. Validate the name and sibling collision without breaking the tree. Collapse the Rust metadata guard to satisfy the required Clippy lint. No failed app stage was published.

- [x] T022/T023/T025/T041 local rich-record slice — identities/documents, sensitive custom fields, configurable attachments, full-field retained history and standard migration export.
- [x] T024/T026/T055 local organization slice — nested/empty folders, tags, recursive Trash warning, retained tree restoration and explicit Empty Trash.
- [x] T057/T058 local migration slice — reviewed current-source CSV import, duplicate choices, plaintext CSV and independent-reader standard KDBX export.
- [x] T017/T035/T042/T051 local management slice — encrypted names/appearance, supported-file independent opening and confirmed targeted local deletion.

[Consolidated macOS handover and explicit outstanding work](macos-handover-2026-10-10.md). Parent completion remains 3/96; local slices do not close four-platform production tasks.

- P0-E52 (restored Trash references): independent backup copies create new entry IDs; retained deleted-folder maps must remap their entry references in the same authenticated copy operation. Preserve folder IDs/structure and all other fields, validate the exact remapping in Rust, and exercise complete-tree restore on the separate encrypted copy.

- P0-E53 (concurrent static-library publication): rebuilding Rust while a native harness linked the same library triggered the compiler's changed-input guard. No failed bundle was published. Freeze final sources/library and run the coherent final suites; avoid mutating build inputs during compilation.
- [x] T017/T036 local recovery-key delivery — explicit unencrypted-file warning, private selected-location save and native printing; acknowledgement remains the user's responsibility.

- P0-E54 (licence inventory): two locked package archives omit their root licence files. Retain the BLAKE2 notice from its recorded exact commit, and clearly identify the deprecated block-modes placeholder's upstream successor notice; keep its exact historical audit as a release gate. All other normal macOS dependency notices are retained from local locked package sources.

- P0-E55 (native file-panel transition): application-modal CSV selection above a SwiftUI sheet left native automation timing out after the panel closed. The isolated process was idle, not burning CPU, and both files remained byte-identical. Reuse the established attached-sheet presentation for CSV/attachment/migration/diagnostic/recovery file panels, and repeat native selection/review. Also replace SF Symbol identifiers in the icon chooser with human-readable labels. These are UI-only changes; domain/core harness results remain applicable.

Native review also caught duplicated document notes and a missing identity full-name field. Render notes once and show the identity’s dedicated full name; this is a view-only refinement. Final signed build/review follows; previously passing domain checks remain applicable.

Autonomous batch handover: 71 model/26 preference checks and all 13 local feature/lifecycle harnesses pass. Foundation checks pass 51 Rust unit, nine transactions and one standard-migration check, dependency hardening, required lint/release/native/offline-provider/iOS-target checks, plus the pinned independent reader. Native attached CSV selection/review, masked history and generated values, folders/tags/deletion warning, migration options, diagnostics, richer details, Move review/cancellation, note Save/history, exact Keep Draft quit preservation and fresh-process resumption/save pass using fictional isolated files only. Final native UI refinements compile in all three configurations. Strict final development signing, arm64 and macOS 26 deployment target pass; no source/hash drift in domain/core checks. Recovery save uses the separately tested private writer; physical printing/recovery-key GUI export was not exercised. [Current source/artifact evidence](../dev/experiments/foundation/results/macos-batch-summary.json). User vaults/settings/Keychain were untouched; owned test fixtures and clone were cleaned up. Parent tasks remain 3/96; the report explicitly lists independent engineering and external verification still outstanding.

The first native quit action saved the fictional note, as verified after reopening with its retained original version. A separate explicit Keep Draft and Close test captured ciphertext/active-file hashes before and after, confirmed process exit without active-file changes, then authenticated fresh-process draft resumption and Save. Do not mistake a Save result for draft-only preservation evidence.


## Cloud sync and Mac autofill implementation — 2026-10-10

User requested these as the next priorities. The scoped development slice is implemented and signed; parent production tasks remain open.

- [x] T044/T045/T046/T047/T080 development slice: native provider-folder binding, immutable encrypted revisions with authenticated ancestry, local offline copy, original-identity enrollment on another Mac, locked incoming quarantine, branch review/keep-both conflicts, retry/restart and truthful provider-delivery state. Direct Drive OAuth/mobile adapters, rotation, settings conflict UI, retention/compaction and real provider evidence remain open.
- [x] T062/T063/T065/T066 development slice: Chrome MV3 activeTab integration, signed native host with bounded framing/verified peers, native exact-origin account chooser, document/navigation/lock/replay guards and explicit save capture into native editor. Installed Chrome basic fill/cancel/locked/capture-review checks pass; Safari/system ceremonies, compatibility matrix, mismatch flow, multi-page/generation/update/auto-submit remain open.
- [x] T064/T068 packaging slice: compiled, entitled, embedded Safari web extension and system credential-provider executables with authorized App Group profiles. Fail closed without shared-container authorization. Installed activation, sandboxed IPC and actual platform filling remain open.

- P0-E56 (first sync compile): Swift rejected an unmarked throwing comparison, a throwing boolean short-circuit, and integer indexing into a Set. Make throwing boundaries explicit and use the Set's first element; no failed app was published.
- P0-E57 (format check): the additive Rust ancestry validation failed rustfmt formatting checks; apply the canonical formatter and rerun required lint/tests.
- P0-E58 (input changed during compile): a status/retry refinement landed while the new cloud harness compiled. The compiler correctly rejected changing inputs. Freeze source changes before coherent final verification; do not suppress the guard. Existing fictional and user vault files were unaffected.

- P0-E59 (browser harness publication): the synthetic harness attempted to assign a deliberately private record setter. Use the existing encrypted-catalog installation/unlock boundary; do not relax production model access for tests.
- P0-E60 (Xcode build database): automatic integration provisioning obtained authorized main/Safari/credential profiles, but the workspace-volume build database reported disk I/O failure. Retrying products/intermediates on /private/tmp succeeded. A fourth separately entitled browser-host bundle was also provisioned automatically. No manual account setup was required.

App Group and autofill capability provisioning succeeded through Xcode using the existing signed-in team. Replace the earlier profile blocker with an actual entitled package/installation validation gate. Safari/system activation and browser ceremonies remain unverified until performed.

- P0-E61 (setup API owner): Swift rejected Safari preferences routing on SFSafariExtensionManager; the installed SDK declares it on SFSafariApplication. Correct the API owner and compile the complete app. All prior offline/cloud/browser harnesses had passed before this view-only failure; no failed app was published.

Final boundary refinements add an authenticated provider declaration, reject changing providers without a migration protocol, clear bindings after local removal, and preserve missing staged cloud revisions without automatically recreating removed provider files. Rerun the changed core/cloud tests and compile the complete entitled app; earlier unchanged offline regressions remain recorded.

- P0-E62 (extension executable packaging): deep signature verification passed, but explicit entitlement extraction showed the raw native targets had been linked as dylibs, so their intended process entitlements were absent. Build actual extension executables with the SDK's NSExtensionMain entry point and application-extension checks; require exact runtime-entitlement readback before staged publication. The provisional package was not launched against user or test vaults. Rebuild and verify the corrected nested executables.

- P0-E63 (isolated launch lifetime): the first directly spawned app process ended with its short command session; selecting the stopped app launched the default locked catalog. It was closed without unlocking or mutating any user vault. Use Launch Services with explicit test arguments and verify the live process command before selecting its UI. The confirmed fictional-directory launch disables persistent PWDTWO preferences and real Keychain enrollment.
- P0-E64 (fixture bookmark identity): a security-scoped bookmark created by an unsigned helper was not reusable by the signed native app. Reconnect only the fictional folder through its native picker, creating the bookmark under the actual app identity; verify a fresh signed process. This is a fixture-authorization issue, not evidence of live provider failure.

Native signed-App-Group IPC reached the real SwiftUI chooser with a separately provisioned fictional client; native cancellation returned a bounded cancelled response without releasing credentials. This validates shared-container socket and mutual code-identity enforcement, not Chrome parent launch or Safari/system sandbox ceremonies. Native File commands, provider picker/connection, two retained branches/keep-both review and setup panel were visually inspected; no conflict resolution or browser credentials were submitted through UI. The final footer truncation/grammar refinement compiled and was reviewed in a fresh signed process.

Final integration handover: 52 foundation unit/9 transaction/1 standard-migration checks, required lint/hardening/native/offline/iOS-target/independent-reader checks and final core hash comparison pass. The native model/preference/13 prior harness regressions and the new cloud/browser checks pass; changed cloud/provider/broker/script boundaries were rerun. Targeted deletion additionally passes retained cloud-file/other-binding checks. Final arm64/macOS26 Apple Development signing and exact nested runtime entitlements verify. Chrome host registration is installed; extensions/system provider activation requires pending user confirmation. Live cloud delivery and installed browser/system filling remain unverified. [Scope, test evidence and remaining engineering](cloud-autofill-handover-2026-10-10.md). These checked slice entries do not mark their production parent tasks complete.

- P0-E65 (evidence collector): the standalone collector assumed a nonexistent root entitlement filename. Read the builder's actual Preview.entitlements file; final main/host/Safari/system runtime comparisons and source hashes pass. This affected report collection only, not the signed build.

- P0-E66 (installed Chrome request): extension installation succeeded, but immediate UI observations did not expose the pending chooser. A later frontmost-sheet observation and host sample showed a real native request waiting for selection. Added static badge/tooltip diagnostics and temporary-field cleanup on every exit; installed fill/cancel/locked/capture checks subsequently passed without secret logging. User explicitly approved Chrome extension installation/testing.

- [x] T062/T063/T065/T066 installed Chrome slice — User-approved unpacked installation in Chrome154, real signed Chrome-parent host launch, native chooser selection, visible fictional username/masked password fill, fresh-page cancellation, locked refusal and explicit capture into masked native review/editor. Cancelled capture retains one saved item; no browser Login or native entry Save performed by agent. Safe badge/tooltip/temporary-field cleanup checks pass. Safari/system installation and broader browser compatibility/features remain open. See the updated integration handover/evidence.

## Field-triggered browser UX correction — 2026-10-10

The user rejected toolbar-only/native-sheet use as the everyday browser UX. Implement the accepted compact chooser inside Chrome when a supported username/password field is focused, with locked unlocking, matching accounts and cross-site search plus explicit one-time mismatch approval. Preserve native application UIs and current destination/document/lock guards.

- [ ] T062/T063/T065/T066 inline chooser acceptance: optional persistent HTTPS focus detection, extension-owned isolated chooser, metadata-only catalog, native single-use selection grants, locked/changed-record/navigation guards, other-site explicit Fill once, updated setup guidance and installed validation. Approved-address persistence, generation, advanced multi-page continuity and final Safari equivalents remain open. Basic isolated username-only/password-only steps are implemented.

- P0-E67 (inline installed rendering): Chrome showed the injected field panel with a blank document. Native grants and mocked transport pass; inspect the installed frame-loading boundary before claiming the inline UI works. Keep account metadata isolated and do not replace it with page-readable HTML.

P0-E67 investigation: installed diagnostics confirm a replacement `srcdoc` document rather than PWDTWO’s extension origin. Browser automation also rejects direct extension-page navigation by protocol policy. Fail closed with a static notice; do not remove replacement attributes or place the account list in page-readable HTML. Actual chooser render/fill and optional persistent permission activation require a manual Chrome check in this environment.

- [x] Inline protocol/native broker implementation: metadata-only matching/all-site search, single-use grants, explicit mismatch confirmation, session/current-record/destination/document binding and release limited to the current username/password step. Native and mocked transport/renderer checks pass.
- [x] Inline extension development package: optional HTTPS focus scripts, isolated browser chooser/search/unlock UI, options permission controls, safe replacement-document failure and Chrome-specific settings routing. Complete signed macOS app compiles; production acceptance remains open.
- [x] Installed basic inline acceptance, user-reported — on 2026-10-10 the user confirmed both automatic chooser appearance beside the focused field and entry selection filling the form (“Yes and yes”). This is manual user evidence, separate from the earlier blocked automation attempt.
- [ ] Remaining installed inline ceremonies: other-site search/cancellation/one-time fill, locked state/native unlocking and broader form compatibility. Exact website and permission settings were not independently inspected.

- P0-E68 (inline evidence collection): byte comparison initially rejected the packaged manifest because the builder adds icon declarations. Compare the manifest against the source plus these explicit builder additions; keep byte comparisons for all unchanged resources. Corrected collection passes strict signing, required nested entitlements and exact packaged resource checks.

Final inline candidate: targeted native/browser/renderer checks, complete signed build, exact required nested entitlements and packaged resource comparisons pass. Chrome 0.2.0 was reloaded. Installed inline acceptance and persistent permission activation remain explicitly open; normal catalog is restored locked and isolated files retained. [Inline handover](inline-autofill-handover-2026-10-10.md).

User follow-up: basic installed automatic suggestions and filling are confirmed. Preserve earlier automation failure as historical evidence; parent production tasks and broader installed ceremonies remain open.

## Chrome generation and capture prompts — 2026-10-10

- [x] T062/T066 Chrome generation and save/update development slice: native generation controls, encrypted history before fill, same-site submitted-form capture prompts, explicit vault/account choice and transactional create/update with retained entry history. No automatic account submission or silent vault save.
- P0-E69 (renderer mock shape): the existing mock omitted the new password-target array and failed during anchor detection. Update the mock to the actual descriptor and add multi-password/capture/generation boundary checks; no failing app was published.

- P0-E70 (async harness assertions): Swift precondition autoclosures cannot await browser operations. Use a synchronous Bool-check helper after evaluating the awaited result; keep production code unchanged and recompile the harness.

- P0-E71 (mutation harness): an assertion failed in the new synthetic mutation harness. Add line-only assertion diagnostics, identify whether the native operation or harness scheduling is responsible, and resolve before publication. No credentials appear in diagnostics.

P0-E71 resolved: the synthetic fixture had not enabled persistent-record mode, so completeLocalUnlock correctly kept it locked. Initialize the fixture through the same persistent/encrypted flags as the existing broker harness. Preserve production unlock guards.

- [x] New browser mutation and real encrypted-vault persistence harnesses: explicit create/update, full prior history/notes/attachments, native random/passphrase generation, history-before-release, failure/dismissal/replay/lock guards and reopening pass. The 71 model checks, cloud regression and final mocked browser/renderer/controls checks also pass.
- [x] Complete signed 0.3.0 package and installed extension reload: required nested entitlements and exact packaged browser resources verify; Chrome reports 0.3.0 with the previously user-granted On all sites setting. Normal app relaunched; no credentials or new permissions entered/granted by agent.
- [x] Manual Chrome 0.3.0 generation/fill/new-entry acceptance, user-reported on 2026-10-11: “It works fine. I create a new password in the browser. It is autofilled, and a new entry is created in the application.” This confirms the reported end-to-end new-password/new-entry flow; the agent did not operate the credential ceremony.
- [ ] Remaining manual Chrome 0.3.0 acceptance: history recovery, selected-account Update, Not Now and same-site post-submit prompt. Passphrase and confirmation-field behavior still need specific installed verification. Safari equivalents and broader/iframe/AJAX compatibility remain separate open work.

[Generation/capture handover and evidence](browser-generation-capture-handover-2026-10-10.md). Development-slice completion does not close production parent tasks.


## Safari connection and chooser state correction — 2026-10-11

- P0-E72 (T062/T065 installed Safari): the user enabled Safari and confirmed the extension rendered, but it displayed Unlock while the native app was open. SafariHandler logs showed a security-framework permission failure. A signed sandboxed state-only client reproduced the failure with PID verification and with audit-only verification. Use the kernel socket-peer audit token plus the exact signed server Info.plist for dynamic code validation; retain the same app identifier, Apple anchor and development-team requirement, and verify the Info.plist hash against the running code. Do not disable the sandbox or broaden entitlements.
- [x] Sandbox regression: the signed client reaches the existing real app's state endpoint; wrong identifier, altered/empty Info.plist proof and invalid socket are refused. No catalog, credential, unlock or vault mutation requested.
- [x] Chooser state correction: show Unlock only for a confirmed locked native session; connection/setup failures clear private metadata and show a separate Retry connection action. Mocked locked/connection-state and existing browser generation/selection checks pass.
- [x] Complete signed 0.3.1 build: native broker/mutation/persistence and mocked browser regressions pass; strict nested signing, existing App Group/sandbox entitlements, exact server-Info.plist copies and packaged resources verify. Signed sandbox state-only/negative checks also pass against the restarted new native app.
- [x] Installed Safari unlocked chooser verified in 0.3.3: matching account, search and save/generate controls render; incorrect Unlock and Connecting messages are absent. Opened the existing test-window toolbar chooser without reload, selection or credential entry. Account-selection/fill ceremonies remain separate open checks. [Native fix evidence](../dev/experiments/foundation/results/macos-safari-connection-summary.json).


## Safari stalled chooser follow-up — 2026-10-11

- P0-E73 (T062/T065): user’s 0.3.1 chooser remained on Connecting despite an unlocked native app. Installed inspection confirms its static resource and JavaScript loaded, the chooser DOM was visible, and no native handler request occurred. A closed browser-context response left the initial status unchanged; classify this as incomplete browser integration, not successful native connection acceptance. Native sandbox peer checks still pass.
- [x] Browser 0.3.2 correction: prefer Safari’s browser API namespace; return a Promise from its background message listener; normalize extension-host case while preserving exact scheme/path/token/document/target binding; package Safari’s supported nonpersistent background page and version its native bundle. Display a visible closed-context message, bound reads to eight seconds, serialize refresh requests and reject late catalog publication after timeout/page exit. New mock response-path, timeout/retry, Safari namespace/host-case and existing browser regressions pass.
- P0-E74 (test timing): the first send wrapper deferred dispatch by a microtask, while the dismissal test correctly required that its close request had begun immediately. Dispatch exactly once inside the Promise executor with a synchronous-throw guard; keep the deadline and rejection cleanup. The controls test now passes.
- [x] Signed browser-only update installed without restarting the native app: native disassembly and main Info.plist are unchanged, entitlements match the original app/plugin, strict nested signing passes and PlugInKit registers Safari 0.3.2. Native sandbox state/negative checks continue to pass.
- [x] Installed Safari 0.3.3 functional catalog acceptance: screenshot verifies the unlocked matching account and search/save/generate controls, with no connection failure or Unlock action. The earlier 0.3.2 failure is resolved in this observed session.
- [ ] Remaining Safari credential ceremonies: deliberate account selection/fill, explicit save/update, history recovery, dismissal and locked/reconnect transitions. Before agent inspection, the toolbar already reported generated-password history retention and fill, with a masked password present; record this as an observed status, not an agent-run ceremony or verified website authentication.

- [x] Browser 0.3.3 compatibility slice: for Safari’s own extension UI only, resolve an omitted tab/frame association using its existing opaque context after own-extension URL/ID/token validation. Still require the browser-supplied UI document ID and bind it on first message; the destination’s original browser document/URL/anchor/grant checks remain enforced. Chrome’s tab/frame rules remain unchanged. Tests cover the actual Promise/callback listener paths, Safari host-case/no-tab UI, missing/replaced document, wrong extension/page origin, forged reply and navigation refusal. The signed browser-only 0.3.3 package is registered; installed unlocked catalog rendering is verified; the remaining credential ceremonies are listed above. [Current follow-up evidence](../dev/experiments/foundation/results/macos-safari-stalled-chooser-summary.json).

## Mac integration readiness — 2026-10-11

- P0-E79 (sync metadata/content commit): the preserved-content rename API correctly rejected using it to publish merged records. Construct the payload update and reviewed title change in memory through their existing validated APIs, then publish once against the original encrypted revision. Keep rename's preservation guard unchanged. The failed harness stopped publication; rerun cloud/lifecycle checks before installing this refinement.

P0-E79 resolved: the final cloud merge and delayed-delivery checks pass, including one-sided rename plus concurrent record edits. Local-controller, multiple-vault and vault-management regressions were recompiled against the shared lifecycle change and pass. Final signed package publication and read-only preflight pass.

- P0-E75 (patch preparation): a combined replacement patch targeted one file twice and was rejected before applying. Split the edit into valid operations; no partial or failed package was installed.
- [x] T047 stale review protection: compare the complete provider revision set and local ciphertext before approval, then recheck the provider set after encrypted save. Changed/deleted provider input invalidates the review and requests Sync Now; source revisions remain retained. Automated arrival/removal checks verify refusal before local mutation.
- [x] T068 development lifecycle slice: native OS-provider destination/fallback guidance, single-flight selection, retry, explicit cancellation, presentation-bound replies and late-response refusal. Bound cancel-fill retires the native chooser, including cancellation before dispatch and at replay-ledger capacity. No unattended credentials or new permissions.
- [x] Read-only Mac package preflight: nested signing, profile authorization for the current Mac, required capabilities, arm64/macOS26–27 and exact signed server Info.plist resources. Current Mac passes; a second Mac must run its own preflight.
- [x] Final signed 0.3.4 build/publication and normal locked-app restart: targeted integration checks, exact packaged resources/server identity proofs, strict signing and current-Mac preflight pass. Safari and system plugins are registered at 0.3.4; signed sandbox state-only checks pass against the final process. [Evidence](../dev/experiments/foundation/results/macos-integration-readiness-2026-10-11/summary.json).
- [x] Delayed-delivery regression: separate local provider folders, paused transfer, independent offline edits, restart, locked ciphertext staging, explicit merge/convergence and interrupted-upload restart pass using isolated fictional vaults. This is simulated delivery, not iCloud/Google cloud evidence.
- [ ] User acceptance: Safari selection/save/update/history/dismissal/lock transitions, real two-Mac provider delivery and installed macOS password-provider completion. The [hands-on guide](macos-integration-test-guide-2026-10-11.md) separates those checks from automated evidence.

- P0-E76 (preflight requirement syntax): codesign interpreted the test-requirement expression as a filename. Prefix inline requirements with `=`; the corrected Apple-anchor/team/bundle verification passes. No package or system permissions changed.
- P0-E77 (Chrome reload): browser URL policy rejected extension-manager navigation. Do not use another surface or indirect command to bypass it. Packaged Chrome resources are 0.3.4; installed Chrome reload is a manual user step.
- P0-E78 (evidence collection): helper discovery assumed /private/tmp, but Python used the macOS per-user temporary directory. Resolve tempfile.gettempdir() and select only the owned helper prefix. Corrected final state-only checks/evidence collection pass; no build failure or vault mutation.

## Cloud review and optional autofill submission — 0.4.0, 2026-10-11

- [x] T047 development slice: compare retained entry versions, choose all/one/deletion, and move unselected edited versions to Trash. Preserve source ciphertext and unchanged-review selections. Multi-head reconciliation deduplicates identical concurrent versions. Full side-by-side changed-field highlighting remains open.
- [x] T046/T047 independent settings/history slice: merge nonconflicting attachment limits, tags, folder records, appearance fields, generated-history append/clear and one-sided vault renames. Incompatible same-setting edits, roots and encryption-key changes still stop with all revisions retained.
- [x] T046 interrupted merged-upload recovery: preserve authenticated combined ancestry after local save/upload interruption and restart. Async provider reads/writes, generation invalidation and known iCloud stale/unavailable-file download requests are implemented. Fictional delayed delivery passes; actual iCloud downloads and two-Mac transfers are not verified.
- [x] T050/T066 device-local optional login submission: default off, v1 preference migration, typed v2 storage, native exact-site grant flag and one-attempt foreground simple same-origin POST login submission. Other-site/partial/signup/generated/ambiguous forms remain manual. Native and mocked browser/form race/refusal checks pass; no website was submitted.
- [x] Complete signed 0.4.0 Mac package: model/preference/cloud/delivery/native browser/mutation/persistence/provider and browser transport/renderer checks pass; shared lifecycle regressions pass; nested signing/profile/current-Mac preflight and exact packaged resources verify. Safari/system bundles registered at 0.4.0 without permission changes. [Evidence](../dev/experiments/foundation/results/cloud-autofill-0.4.0-2026-10-11/summary.json).
- [ ] Installed 0.4.0 GUI/browser and live-provider acceptance: manual native restart, Chrome reload, Safari/system ceremonies and real two-Mac provider convergence remain open. Direct Drive API/mobile adapters, key rotation, incompatible settings/root resolution, migration and retention/compaction remain implementation work.
- P0-E80 (final native UI inspection): PWDTWO accessibility and screenshot calls timed out; reselecting its exact app path did not restore access. A read-only process sample showed its main thread waiting normally for events, not a demonstrated crash. Do not force termination with pending-edit state unknown. Leave the existing 0.3.4 process intact; the signed 0.4.0 package is ready for manual quit/reopen. New conflict/settings GUI inspection remains pending.

## Dedicated iPhone development — 2026-10-11

- [x] T076/T079 first native iPhone development slice: dedicated phone-only arm64 iOS target (minimum26/SDK27, no Catalyst/Mac compatibility), Liquid Glass Items/Search/Settings, shared native encrypted core, independent vaults/grouped authorization/exclusion/remembered selection, CRUD/history/Trash, encrypted drafts, generator history before release and offline recovery with replacement-key acknowledgement. Eight native iOS26.2 simulator checks and both simulator/unsigned-device builds pass. Native fictional UI inspection verifies Items/Settings, search filtering, masked card details/back and manual lock. Parent T076/T079 remain open for physical biometrics/protection, OS27 runtime and full feature parity. [Evidence](../dev/iphone/results/2026-10-11/summary.json).
- P0-I01 (first iPhone compile), resolved: a catch block shadowed the session error property, a Combine type needed its explicit import, and Xcode's SQLite build database reported disk I/O failure on the external SD checkout. Qualify the property, import Combine and keep DerivedData on the internal temporary volume; preserve the failed log and publish only successful products. Disable the obsolete headermap mode. Subsequent native compilation and simulator execution succeed.
- P0-I02 (first XCTest startup): the first simulator run stalled at test-host launch before any test executed. Interrupt only that owned test runner; preserve its logs. Retry with a warm simulator and an internal-volume result bundle. Eight tests subsequently executed; do not count the aborted run as a pass or infer an application crash from it.
- P0-I03 (simulator protection assertion), resolved: the simulator returned no file-protection attribute after successful complete-protection API calls. Keep production protection calls and physical-device assertions intact; limit simulator assertions to API success/no contradictory weaker attribute and independently verify backup exclusion. Physical Data Protection remains unverified. All eight revised simulator checks pass.
- P0-I04 (native UI verification), resolved: Items and Settings worked, but Search and manual lock did not activate; the locked card also clipped its subtitle. Move searchable onto the navigation root, use explicit activity callbacks rather than a TabView gesture, and allow the branded card to grow. The rebuilt installed app now activates Search, filters the fictional card, opens masked details, navigates back and locks immediately. Preserve the distinction between model checks and UI evidence.
- P0-I05 (evidence crop tooling), resolved: Sharp could not load in the restricted UI REPL because its package metadata import was unsupported. Use the existing macOS image utility to crop captured screenshots; retain only the phone and exclude unrelated device-sidebar information. No software download or policy workaround.
- [ ] T080/T081/T084 mobile follow-up: provider enrollment/sync and direct Google authorization, Safari/compatible-app credential provider, import/export/backup/sharing and advanced native workflows. These are not advertised as connected by the initial local iPhone app. Physical provisioning and installation are not required for the completed unattended simulator slice.
- [x] Shared Apple biometric prompt refinement: phone enrollment uses a platform-appropriate reason while the Mac default and protection/policy behavior remain unchanged. Recompiled controlled Mac local-biometric checks pass. MIT/dependency/EFF notices and privacy declarations are bundled; final simulator/device products contain no XCTest host artifacts. No personal vault or Keychain enrollment was operated.
- [x] Physical iPhone build preparation (2026-10-11): command-line automatic Apple Development signing succeeds for the dedicated phone target; strict nested signature verification passes. Build and filtered provisioning evidence are retained in ignored `dev/iphone/build/iphone-signing.log` and `iphone-signing-summary.json`; signed product is under `build/Products/signed-iphoneos/`. This does not prove installability: the paired iPhone is unavailable, reports Developer Mode disabled, and is not included in the generated profile. Device registration/provisioning and actual installation remain pending connection and the user's on-device Developer Mode steps. No device data was changed; mobile cloud synchronization remains unimplemented.
- [x] Physical iPhone installation (2026-10-11): after the user enabled Developer Mode and reconnected by USB, Xcode's destination-specific automatic provisioning included the paired iPhone. Strict signature verification and the actual signed application identity pass. `devicectl` confirms installation and launch; a filtered process check confirms PWDTWO running on the iPhone 14 Pro Max. No simulator fixture, Mac vault, user credential or biometric enrollment was transferred or changed. GUI review, actual Face ID/Data Protection and cloud delivery remain unverified; mobile sync is still unimplemented. [Filtered evidence](../dev/iphone/results/2026-10-11/physical-install.json).
- P0-I06 (physical-device preparation), resolved: initial device queries/destination discovery timed out while developer disk support connected. The existing compatible developer image was available; pairing and a bounded retry allowed Xcode to prepare the device and build. Preserve the first failure log. A verification guard initially rejected a valid team wildcard provisioning profile; require the exact **signed app** identity plus permitted profile scope and the paired device instead. An attempted install of the consequently uncopied product failed without changing the phone; retry only after successful verification/copy. Final install, launch and running-process checks succeed.

## iPhone iCloud folder sync — 0.2.0, 2026-10-11

- [x] T080 development slice: native Files directory selection/bookmark binding, existing cloud-vault enrollment with original identity, local offline copy, foreground reconciliation and locked ciphertext staging, one authenticated provider per vault, native keep-all/select-version/Trash review and stale approval refusal. Reuse the Mac engine rather than introduce a mobile cryptographic/merge implementation. Sync blocks while editing; device-only drafts remain excluded. Upload failure refreshes the phone model from durable local state before subsequent edits. No background/cloud delivery acknowledgement is claimed.
- [x] Shared Apple folder refinements: scope is active for directory validation; iOS document-picker bookmarks avoid unavailable macOS-only options. Recognized evicted iCloud revision placeholders prevent an empty-folder interpretation and request download when ubiquitous. Current native Mac cloud/delayed-delivery regressions pass; the existing user's Mac process was not restarted or its vaults changed.
- [x] Fourteen regular iPhone native XCTest checks pass (eight local plus six sync), including restart/offline convergence, enrollment/wrong-password refusal, two-version conflicts/stale-provider review refusal, locked staging/late sync cancellation, draft exclusion, disconnected file retention, interrupted upload followed by editing/restart and provider mismatch/evicted revisions. No actual accounts, Keychain enrollment or user vaults are used. Two additional interop cases pass separately against encrypted revisions produced by a native Mac peer compiled from the Mac application's real shared sources: identity-preserving opening, two offline conflicts/edit-versus-Trash review, rename, locked staging, exact six-record convergence and seventh-record iPhone return to Mac. Transport is CLI copying between independent folders; it does not prove live cloud delivery or the Mac GUI flow.
- P0-I07 (interop orchestration), resolved: the first phone-send test passed, but the Mac merge fixture saw no returned branch. XCTest installation relocated the app data container; the driver held its old path and silently globbed a missing directory. Resolve the current container after each test run and refuse transfers from a missing folder. Retain failed host fixtures, and remove only the owned failed phone cache fixture for retry. Diagnostic guard reported zero branches before the fix. The complete native Mac/iPhone exchange then passes; no production vault or merge policy was altered to satisfy the test.
- [x] Current 0.2.0 (2) arm64 simulator/device builds and strict development signing/device coverage pass. The update is installed and launched on the physical iPhone without uninstalling or copying simulator data. Native simulator inspection verifies locked setup, system Files picker/cancel, Settings cloud management/dismissal, existing fictional unlock and manual lock. [Evidence](../dev/iphone/results/2026-10-11/cloud-0.2.0/summary.json).
- [ ] Live iCloud acceptance: a separate CLI-prepared fictional Mac test vault has one encrypted revision in the dedicated `PWDTWO Sync Test 2026-10-11 c6da61` iCloud folder. The user's on-device folder selection/enrollment is pending; no remote delivery or hardware bookmark/protection proof yet. Local fixture paths are in ignored `dev/iphone/build/live-sync-fixture.json`. Parent T044/T045/T046/T047/T080 remain open for actual provider/device coverage, background execution, direct Google authorization, key changes, incompatible settings/roots, migration and compaction.
- Live iCloud visibility investigation (2026-10-11): the user does not see the test folder on the phone. Mac Foundation resource values report both the folder and its encrypted revision as ubiquitous, uploaded/current and not uploading, with no upload error. This confirms Mac-reported upload, not iPhone visibility or a round trip. The simulator inspection showed the system picker initially opens Recents; ask the user to switch to Browse → iCloud Drive before attributing the missing folder to provider integration. [Upload evidence](../dev/iphone/results/2026-10-11/cloud-0.2.0/mac-icloud-upload.json). Python's host build lacked `os.listxattr`; use native Foundation resource values rather than infer upload state from existence or extended attributes.

- [x] User-requested mobile-friendly fictional sync password: prepared a separate `PWDTWO Sync Test Easy 9921a1` fixture with fifteen ones, the shortest allowed by the current vault core. Creation, encrypted publication, and native Mac reopen/sync pass. Updated the live fixture pointer and phone test guide; original fixture retained, production validation unchanged, iPhone enrollment/delivery still pending.

- P0-I08 (live Mac test-vault UI enrollment), resolved in 0.4.2: native computer control repeatedly times out selecting the running PWDTWO window by exact path/display name, including after resetting the control session. A bounded native process sample shows the main thread in its normal AppKit event loop, so a hang is not confirmed. Existing Mac process/data are retained; no GUI enrollment or unlock claimed. Manual File → Cloud Sync → Choose Existing Provider Folder remains available for the dedicated fictional Easy fixture.

- [x] iPhone Search activation fix — 0.2.1 (3): move native searchable binding to the TabView and activate text entry on Search-tab selection using `tabViewSearchActivation(.searchTabSelection)`. Clear query on grouped lock. Simulator UI confirms focused field, typed Travel filtering, clear/reset, and manual lock; simulator/device builds and strict signing pass. Installed/launched the physical iPhone update without uninstalling or injecting data. Physical OS27 UI confirmation remains pending; the platform question is unanswered, so this change explicitly covers iPhone only. [Evidence](../dev/iphone/results/2026-10-11/search-0.2.1/summary.json).

- [x] Physical iPhone Search acceptance, 2026-10-11: user confirms Search now works after 0.2.1. User is disconnecting the phone and asks to continue later. Leave device work stopped; resume with live Mac/iPhone iCloud acceptance and Mac cloud-vault GUI enrollment (P0-I08), without assuming either is complete. The current fictional fixture is `PWDTWO Sync Test Easy 9921a1`, password fifteen ones; all original fixtures retained.

## Physical iPhone / live iCloud continuation — 2026-10-12

- [x] Physical iPhone connection verified; resumed testing after the user reconnected. Three original-provider revisions downloaded and authenticated by the native Mac peer, retaining original vault identity with three records, one added record and edited original notes; no pending conflict. Read-only USB inspection of this exact fictional vault confirms the physical phone ciphertext matches the authenticated provider revision and its binding/journal persist. No copied transport was used to populate the phone or provider. [Evidence](../dev/iphone/results/2026-10-12/live-icloud/summary.json).
- [x] Native Mac peer created/published the fictional return note “Mac sync check · 2026-10-12”; Foundation reports the fourth encrypted revision uploaded/current. Physical phone arrival and GUI confirmation are pending. Existing regular Mac app/vaults are untouched; P0-I08 native window-control timeout persists.
- P0-I09 (CLI fixture diagnostics), resolved: an expected iCloud download state escaped the fixture helper’s throwing main and generated a diagnostic-process SIGTRAP. Catch pending-download/error conditions and exit normally with distinct pending/refusal statuses. Provider revisions subsequently downloaded and authenticated. A proof extension initially accessed private sync state and failed compilation; removed that access without weakening production encapsulation. Rebuild passes and invalid-fixture refusal exits normally. An initial read-only physical metadata query used an incorrect private-storage subdirectory; retry using the controller’s actual PWDTWO/Vaults path succeeds and filters only the fictional owner. No phone files were changed.

- [x] Live iCloud round-trip convergence, 2026-10-12: after the user unlocked the physical iPhone/PWDTWO, its actual encrypted fictional vault became byte-identical to native Mac return revision `6e6a454974e4d46abcc7633e0bf41ed891353bc0d2a435612413f095c65dfd99`; phone journal tip/local match that revision and session selection includes the same original vault identity. Native Mac authenticates the converged four-record payload. USB was used only to read proof snapshots, never to populate either peer/provider. This proves device/native-Mac-engine delivery in both directions for the fixture, not actual Mac GUI enrollment, broad race coverage, offline/device-lock protection or production readiness. [Proof](../dev/iphone/results/2026-10-12/live-icloud/round-trip-proof.json).

## Automatic cloud synchronization — 2026-10-12

- [x] T046/T080 automatic foreground development slice: durable local saves, unlock/foreground return and native provider-folder notifications queue sync after a short debounce. One serialized queue retains pending owners through busy editors, suspension and failures, with bounded retry. Existing 30-second phone/60-second Mac checks remain fallback. Manual Sync Now is optional retry, not required for routine publication. Explicit conflict review and encrypted device-only draft exclusion remain intact. Incoming changes do not extend user inactivity.
- [x] Seventeen native iPhone checks pass (three new automatic plus six cloud and eight local); two separate fixture-dependent interop cases skip in the ordinary run. Seven native Mac programs pass: AutomaticCloudChecks, CloudSyncChecks, CloudDeliveryChecks, LocalControllerChecks, MultipleVaultChecks, CrossVaultCopyChecks and CrossVaultMoveChecks. Tests use isolated fictional vaults.
- [x] Strict development signing/device coverage and installation of iPhone 0.2.2 (4) succeed without uninstalling or replacing vault data. Mac 0.4.1 (401) is now published and running after the user safely closed the previous app; read-only package preflight, nested signing, profile authorization and extension registration pass. The previous bundle is retained for rollback; native UI confirms the normal locked screen and Touch ID availability. Existing profiles/permissions are retained.
- [x] Live automatic arrival: after reconnect/unlock, the physical iPhone ciphertext exactly matches the native Mac peer and dedicated iCloud revision `4666f2ff13ef3ac4b6055676edbc0911425435d0c8e32b3f62efeb9d74c79bfa`. Native Mac authenticates five retained records with no pending review, including the published “Automatic sync check · 2026-10-12” note. No manual phone sync was triggered by the agent, and no phone/provider data was injected through USB. This verifies the new revision arrived, without measuring delivery latency or distinguishing notification from foreground fallback. [Proof](../dev/iphone/results/2026-10-12/live-icloud/automatic-receive-proof.json).
- P0-A01 (shared compile), resolved: Swift's nested notification closure required explicit self; qualify capture references and preserve main-actor lease validation.
- P0-A02 (Mac test compilation), resolved: a throwing decode in precondition's nonthrowing autoclosure failed compilation. Decode first, then assert the result.
- P0-A03 (Mac automatic fixture), resolved: the test expected a synchronous save return and created its draft before selecting a vault. Native persistence is asynchronous and requires an unchanged authenticated draft owner. Select the vault before creating the draft and wait for durable publication; preserve production draft validation. Corrected automatic and six regression checks pass.
- P0-A04 (physical verification), resolved: launch and read-only inspection were refused while the phone was locked. After the user reconnected/unlocked it, the same exact fictional-vault read succeeds and proves five-record convergence. No protection settings or phone files were changed to bypass the refusal; this is a narrow observed locked/unlocked access result, not comprehensive physical Data Protection certification.
- P0-A05 (Mac update activation), resolved: after the user closed the app, publish the verified 0.4.1 bundle with the previous bundle retained for rollback, register its existing extensions and launch it. Native accessibility now responds and confirms the locked screen. No forced quit, credential entry or vault enrollment was performed. P0-I08 actual shared-vault GUI enrollment remains open; its earlier window-control blocker is cleared.

Parent provider tasks remain open for background execution, direct Google authorization, provider migration, key changes, incompatible vault-level conflicts, retention/compaction and broader real-device acceptance.

- P0-A06 (native Mac cloud enrollment), resolved: after selecting the fictional shared iCloud folder, the second revision-file picker was not visible. The nested completion used NSApp.keyWindow while the first panel could still be key. Capture the original review window and present the second picker on it after the dismissal callback returns. The signed UI-only 0.4.2 fix now presents both native picker steps; existing-password enrollment succeeds with original identity preserved.

- [x] Mac cloud enrollment UI correction — 0.4.2 (402): capture the original review window before showing the folder panel, defer the next sheet until its completion returns and attach to that captured window. Signed package/current-Mac preflight and publication pass. Native UI now shows both folder and revision pickers and the existing-password field; enrollment reports success and preserves the same original test-vault identity. The actual installed Mac ciphertext matches the authenticated five-record iCloud/phone revision and its binding persists. Personal credentials/data are not changed. User-approved grouped Touch ID unlock succeeds, with the original five-record fictional vault visible beside Personal. A sixth fictional note saved through the Mac GUI reaches the physical iPhone automatically, with exact Mac/provider/phone ciphertext equality; no manual sync or USB injection. Reverse installed-GUI delivery also passes: the user-created iPhone note “123” appears automatically on the Mac, and all three seven-record encrypted copies match. [Evidence](../dev/iphone/results/2026-10-12/automatic-sync/mac-gui-enrollment.json).

- [x] Live installed Mac GUI → physical iPhone automatic sync, 2026-10-12: ordinary Save on the secure note “Mac app automatic sync · 2026-10-12” in the fictional shared vault creates/reconciles the sixth record. Installed Mac, iCloud and actual phone ciphertext all match `13d27fb4c337eed49151b2e01fac74eab88bfa67d45cf148f3b49d16f05deb5b`. Original records are retained; Personal was not edited. USB reads proof snapshots only. [Delivery proof](../dev/iphone/results/2026-10-12/automatic-sync/mac-gui-save-delivery.json), [native GUI](../dev/iphone/results/2026-10-12/automatic-sync/mac-gui-save.png).

P0-I08 resolution: native window control recovered after the safe app update. The corrected two-step native picker and existing-password flow enrolled the original live iCloud fixture; user-approved grouped unlock displays its five records. Subsequent ordinary Mac GUI Save delivers a sixth record to the physical phone automatically. The earlier timeout remains historical evidence.

- [x] Live installed iPhone → installed Mac automatic receipt, 2026-10-12: user saves note “123” on the phone; Mac interface adds it automatically and shows seven retained records without agent manual Sync Now. Actual Mac/provider/phone ciphertext all match `b652c75101e110bae394f1519be93ba6bbd712393e89a6ef5e01eb7909a2d588`. Together with the Mac GUI Save → phone check, this completes the dedicated fictional iCloud installed-GUI round trip. Timing/notification-versus-fallback is not measured, and background/offline/race/provider/OS coverage remains separate. [Proof](../dev/iphone/results/2026-10-12/automatic-sync/gui-roundtrip-proof.json), [Mac UI](../dev/iphone/results/2026-10-12/automatic-sync/mac-phone-converged.png).

## Production readiness work — 2026-10-12

User authorised security/storage hardening, sync failure handling and backup/recovery after the installed Mac/iPhone iCloud round trip. Existing development products and user vaults remain untouched during isolated checks. Parent production tasks remain open until their full criteria and independent review requirements are satisfied.

- [x] T015/T088 local transaction hardening development slice: pin the validated directory descriptor; perform file reads/locks/staging/publication/cleanup relative to it; refuse directory/ancestor replacement and permission/ownership changes. Test failures and abrupt transaction boundaries with fictional data.
- [ ] T006/T013/T016/T088 dependency and key-boundary assessment: reproducible advisory scan, secret-copy/ownership review, malformed-vault resource checks and remaining production adoption decisions. An automated scan is not independent cryptographic approval.
- [ ] T048 sync password/recovery generation transitions: preserve both generations and pending edits, require correct new authorisation, retain unresolved branches and verify interrupted transitions.
- [ ] T053/T054 backup readiness: full-content recovery checks and the user-configured single-backup/designated-writer scheduler with safe overwrite, overdue execution and writer handover.

- P0-S01 (descriptor hardening compile), resolved: Darwin mode_t is a 16-bit type, which cannot be passed directly to variadic openat. Promote the creation mode to c_uint as required by C argument promotion; no failed build is published.
- P0-S02 (dependency audit), resolved: the full workspace lockfile contains known vulnerable regex/thread_local and unmaintained tooling through unused upstream rustfmt/test-with dev dependencies. These are absent from the active app graph. Unused library-test tools were removed reproducibly and the regenerated full lockfile passes the advisory scan without suppressed findings. Production dependency/security adoption remains separately open.

- P0-S03 (audit preparation), resolved: the first manual manifest-removal pattern did not match and a broad lockfile refresh also advanced cc/syn. Replace the fragile pattern with exact section removal and restore the unrelated versions through targeted updates. The final full lockfile scan reports zero known advisories/warnings, without ignores.
- P0-S04 (native test compile), resolved: the directory-binding harness used throwing file reads in precondition autoclosures. Read into local values first; directory-binding, native persistence and lifecycle checks now pass. Production reads/publication bind to a pinned identity through ABI 2; running products are unchanged until rebuilt.

- P0-S05 (credential-sync regression), in progress: the concurrent-change test found that a device using the selected password could open the combined head but not another retained ancestor. Authenticate the received combined source directly with the existing authorized component before using its encrypted history to inspect those ancestors; never use an old key to authorize a newer protection. No installed app was changed.

- P0-S05 resolved: native credential regression now passes, including concurrent changed protections, authorization retirement on lock and interrupted publication/restart. Existing selected-password authorization can authenticate a received combined head and use that head's history to read retained concurrent ancestors.
- P0-S06 (iPhone test target), resolved in source: the shared credential harness lacked the app-module import when compiled in XCTest. Add an iOS-only testable module import; rerun mobile checks before claiming verification.

- [x] T006/T013/T016/T088 automated assessment slice: pinned full-workspace advisory scan without ignores, owned custom-data wipe regression, own-core malformed input/resource/credential tests, patched-library regressions, Clippy and device/simulator Rust checks pass. Independent review, complete memory ownership and production format adoption remain open.
- [x] T048 native implementation validation/deployment slice: changed-password authorisation, selected credential protection, retained ancestors, pending offline edits, lock retirement and interrupted upload/restart are implemented. Both native targets and signed packages pass; Mac 0.5.0 and iPhone 0.3.0 are installed. Actual physical changed-credential ceremonies remain separate.
- [x] T053/T054 native implementation validation/deployment slice: opt-in user frequency, one backup, encrypted designated-writer assignment/completion, safe replacement/overdue/restart, local/provider folders and iPhone export/review/separate restoration/recovery implemented. Both targets and packages pass and are installed. Mac GUI opens the previous seven-record fictional vault and shows the schedule disabled by default. Delayed remote assignment, installed cloud handover, background/device protection and cloud-vault deletion remain open.

[Implementation decisions, current limits and evidence](production-readiness-2026-10-12.md). Parent task status is not closed by these development slices.

- P0-S07 (native build input consistency), resolved by freezing source before the final checks: adding OS file coordination to the scheduled-backup publisher while a broad Mac runner was compiling triggered Swift's input-file-modified refusal. No failed product was installed. Earlier passing unchanged suites remain evidence for their slices; rerun the affected scheduler/browser-persistence builds and complete the remaining Mac checks against frozen source.

- T015/T053 additional publication gate check: re-read staged bytes inside the final publication guard, after external/session validation, to refuse in-place modification of the same staging inode. Directed Rust/native regressions require the original vault/backup to survive this interference. Final checks and package builds use the frozen resulting sources.

- P0-S08 (backup callback compatibility), resolved in source: adding a zero-argument publication callback before the existing stage callback caused Swift 6 to bind old trailing closures to the wrong parameter. Keep the stage callback first and explicitly label the scheduler's final-validation callback. The tests retain their original stage-injection behavior; rerun export/scheduler/mobile checks before publishing.

- P0-S09 (same-password changed generation), resolved in source: a higher authenticated generation using the same password could decrypt but yield no eligible verified protection choice. Require explicit password entry before outgoing writes for that generation, co-authenticate requested revisions with the entered password, and reuse only directly authenticated sources with the same generation/recovery authority. Protection choices deduplicate by authority and component, not generation alone. Temporary sync-source inspection also enforces the app owner. New directed regressions are required before installation.
- T053 cancellation refinement: provider validation runs before acquiring the short publication/cancellation mutex. A blocked provider check must not delay app locking, and cancellation must preserve the prior backup. A bounded semaphore regression verifies this.

- P0-S10 (cancellation harness compile), resolved: Swift 6 forbids semaphore waits directly in an async context and isolated lifecycle property access in a detached task. Run the bounded start wait through a synchronous nonisolated helper on a detached task, and capture the immutable directory URL before leaving the main actor. This changes the test orchestration, not application cancellation behavior.

- T010/T048 authorization marker refinement: an ordinary content merge must not count as password entry. Credential reconciliation marks the selected password as entered only when its exact component/authority was verified, or previously password-authorized current protection was retained. Choosing current protection after a biometric-only open does not authorise new biometric enrollment. A controlled native controller regression covers ordinary merge followed by attempted re-enrollment, and the credential harness covers selected-source proof.

- P0-S11 (authorization harness save expectation), resolved: encrypted model saves return a deferred result while the native transaction runs. The new test incorrectly expected synchronous success. Wait for the controller, then assert that the editor closed and the saved record is installed before creating the concurrent peer branch. No application save behavior was changed.

- [x] Current batch deployment: Mac 0.5.0 (500), iPhone 0.3.0 (5). Normal locked Mac quit before package replacement; previous application retained; strict nested signing/current-Mac profile and unchanged existing extension registration pass. Mac GUI opens the previous fictional sync vault with seven records including `123`, shows native scheduled-backup controls off by default, and returns to the original included selection in a locked state. No user password/recovery key or backup schedule was changed. Physical iPhone install and installed-version query pass without uninstalling or copying test vaults.
- P0-S12 (physical iPhone launch), user-device state pending: the installed update cannot be launched through USB while the iPhone is locked. CoreDevice explicitly reports `Locked`. Open PWDTWO after unlocking the phone; no code change, reinstall or security bypass is required. Native simulator checks pass; no physical new-generation/backup ceremony is claimed.
- Current results: 56 core unit checks, 15 local transaction checks, one migration check, four patched-library checks; zero advisory findings/warnings; three native security-boundary programs and five final native readiness programs pass. The full phone suite passes 20 checks and skips two separately driven interop fixtures; the final changed backup/recovery/credential surface passes three checks, and selected-password proof checks pass again on iPhone. Earlier broad Mac development checks pass, with final affected surfaces rerun against fingerprinted frozen sources.

[Batch/deployment/remaining gates](../dev/security/results/2026-10-12/readiness-summary.json). Independent production review and the parent tasks remain open. Next application feature: iPhone Safari/app autofill.


### iPhone native AutoFill — 2026-10-12

- [ ] T062/T079/T081 iPhone password-provider development slice: separate AuthenticationServices native extension; included-vault ciphertext App Group snapshots; per-request grouped password authorization; exact HTTPS matching, metadata search and explicit other-site Fill once; one-result and current-snapshot checks; optional native setup. Build, signing, installation and simulator checks are in progress. Face ID within the extension, OS identity suggestions, capture/generation and physical Safari/app acceptance remain separate follow-up slices.
- P0-AF01 (extension build), resolved in source: shared backup schema decoder is gated by LOCAL_VAULT_PREVIEW. Enable that existing candidate-format compilation condition in the new extension target rather than duplicate the decoder. Rebuild pending.
- P0-AF02 (test compilation), resolved in source: Foundation DirectoryEnumerator is unavailable directly from an asynchronous test context. Enumerate through a synchronous helper, retaining the same ciphertext-only assertions. Rebuild pending.
- P0-AF03 (package runtime entry point), resolved in source: explicitly named Objective-C provider class requires the same unqualified NSExtensionPrincipalClass. Match the plist to the runtime class and enable the supported first-run configuration UI attribute. Package symbol/plist verification pending.
- P0-AF04 (physical signing), in progress: automatic provisioning created the credential-provider entitlement but returned empty App Group scopes for both iPhone profiles. Signing correctly refuses the requested group. Resolve capability/profile association and verify exact signed/profile group scopes before installation; do not use an entitlement-stripped package.

- P0-AF05 (temporary provisioning diagnostic), resolved: derivedDataPath requires a scheme, and provisioning entitlement paths are relative to the temporary project location. The temporary experiment did not alter app data or install a package. Add capability metadata directly to the reproducible project after the full simulator run has finished.
- Full iPhone regression: 28 executed, two separately driven interop fixtures skipped, zero failures. Six AutoFill checks pass. Final setup-label/capability metadata recompilation pending.
- [x] T062/T079/T081 iPhone provider compilation/security development slice: separate native password-provider target, private Data Protection ciphertext-only shared copies of included vaults, grouped per-request password unlock, exact HTTPS matching, explicit other-site Fill once, current-group/hash and single-use completion checks, background/cancel retirement, local delivery/mutation gate, optional native setup and copy removal. Full simulator regression passes 26 cases (two standalone interop fixtures skipped); final six AutoFill cases pass again; final device/simulator app and extension compile, runtime class/plist match, and unchanged source hashes pass. [Evidence](../dev/iphone/results/2026-10-12/autofill/summary.json).
- [ ] T081 physical iPhone install/acceptance: P0-AF04 remains blocked by empty App Group scopes returned by Apple automatic provisioning. User setup for both target associations has been requested and Xcode project opened. Keep installed 0.3.0 unchanged until a strictly verified 0.4.0 (6) package can be signed. Actual Safari/compatible-app selection, device protection, memory budgets and iOS27 runtime remain unverified. [Handover](iphone-autofill-2026-10-12.md).
- P0-AF01/AF02/AF03/AF05 resolved and verified: correct shared decoder compilation condition, synchronous test file enumeration, actual Objective-C provider entry point/configuration metadata, and canonical capability/project paths. Final simulator and device compilation pass. P0-AF04 requires the pending Apple App Group association; no permission stripping, vault/data migration or user credential changes.
- P0-AF06 (package evidence check), resolved in source: Xcode Debug products use an executable trampoline and explicitly linked .debug.dylib. Verify the actual provider class in the executable or that linked packaged library, retaining strict deep code signing, rather than incorrectly requiring the class in the trampoline. Recheck pending; no installation occurred.
- P0-AF06 verified: final simulator/device products contain the exact principal class in their explicitly linked debug library. Phone build inputs match the recorded frozen source hashes. Final runnable copies retain the AutoFill extension and exclude XCTest artifacts. App Group signing setup (P0-AF04) remains pending.


### iPhone optional clipboard clearing — 2026-10-14

- [x] T031/T039/T079 iPhone clipboard slice: default off; device-local enable/delay (15/30/60/120 seconds); iOS item-owned expiry/local-only copying; passwords, generated values, recovery keys and sensitive fields use the same adapter; usernames stay unexpired; setting changes apply to future copies. Defaults/locality, exact copying, locked refusal, expiry and later same-text/new-text preservation pass using isolated fictional pasteboards. Six new clipboard checks and eight existing controller regressions pass; final device/simulator 0.4.1 (7) compilation/products and frozen-source fingerprints verify. No general clipboard or user vault was accessed by checks. Physical installation still requires the pending AutoFill App Group association. [Evidence](../dev/iphone/results/2026-10-14/clipboard/summary.json), [behavior/limits](iphone-clipboard-2026-10-14.md).


### iPhone entry history — 2026-10-14

- [x] T025/T055/T084/UX35 iPhone history slice: dated newest-first native list; read-only full entry preview with changed-field indicators and masking/reveal/copy; explicit whole-version restoration preserving current and previous history, custom fields and historical attachments. Session/current-entry guards refuse stale/locked/replayed review, drafts, Trash, no-op and foreign-controller authorization. Existing encrypted CAS/sync publication path is reused. Seven history, eight existing session and six AutoFill regressions pass (21 total), plus final restored-version/restart check after the mask-control UI change. Final 0.4.2 (8) device/simulator compilation/products and frozen source fingerprints verify. [Evidence](../dev/iphone/results/2026-10-14/history/summary.json), [behavior/limits](iphone-history-2026-10-14.md). Installation remains gated by the pending AutoFill App Group association.
- P0-H01 (history/conflict regression), in progress: after aligning retained-version timestamps with macOS, the concurrent restore/peer-edit test reports a missing exact prior-current snapshot following keep-all reconciliation. Local full-version restore, automatic publication, stale/draft/lock guards and other regressions pass. Inspect the actual retained history/conflict representation before accepting the change; no failed package installed.

- P0-H01 diagnosis/correction: the failing assertion was the restored full EntryContent equality, not loss of the prior-current historical snapshot. Existing keep-all reconciliation annotates one branch's title with “(conflict copy)” depending on branch order. Assert that expected title annotation explicitly and compare every other restored field/file exactly; keep the prior-current history and both-peer convergence assertions. The merge implementation is unchanged. Final rerun pending.

- P0-H01 resolved/verified: final combined run passes all 21 cases (seven history, eight existing session, six AutoFill). The full restored content survives reconciliation with its expected optional conflict-copy title annotation; the prior-current snapshot, historical files and both-peer convergence are retained. Automatic restored-version publication passes without a manual Sync call. Final mask-control UI compilation and device packaging are pending.

- [x] Final iPhone history development packaging: 0.4.2 (8) device/simulator products compile, preserve the native AutoFill extension, match its runtime principal class, exclude XCTest runtime artifacts and match frozen final build inputs. Final mask-control UI/restoration check passes. No physical installation, user vault operation or credential change was performed. Parent history/mobile/release tasks and physical acceptance remain open.

### iPhone generator, accessibility, diagnostics and search — 2026-10-14

- [x] T028/T029/T040/T084 generator development slice: native options/preview/Generate Again/Use in Entry; local option persistence; encrypted history before release; Cancel does not alter the draft; stale/lock/replay guards. Four generator checks pass.
- [x] T086 accessibility development slice: large-text adaptive action rows, 44-point copy/reveal targets, field-specific entry/action labels and keyboard focus/Done; independent detail reveals; native largest-text snapshots and search interaction checks. Physical VoiceOver acceptance remains separate.
- [x] T075 mobile diagnostics development slice: typed allowlisted local events, seven-day/2,000-event/10-MiB bounds, private Data Protection storage outside synced vault payloads, background serialized persistence, section-optional preview/manual JSON export and clearing. Three schema/retention/clearing/malformed-content checks pass. No automatic upload; GitHub issue URL is not configured in this repository.
- [x] User screenshot correction: remove the top search from Settings and Items by scoping searchable to the native Search tab; retain the bottom Search role/control. Native runtime checks show no Settings search field and a bottom Search input accepting text.
- Final 0.4.3 (9) validation: full suite passes 48 cases, skips two separately driven interop fixtures, no failures; ten final generator/diagnostics/native-interface cases pass after UI-only refinements. Largest-text Settings/Generator/Diagnostics/detail snapshots inspected. Both final arm64 device/simulator products compile, preserve the AutoFill extension, match principal class/plist and frozen source hashes, and exclude XCTest artifacts. Device output is unsigned; installed 0.3.0 is unchanged while P0-AF04 App Group signing remains pending. Parent tasks remain open, including physical VoiceOver/Files export/iOS27 acceptance and wider feature criteria. [Evidence](../dev/iphone/results/2026-10-14/polish/summary.json), [behavior and limitations](iphone-polish-2026-10-14.md).

### End-user documentation — 2026-10-14

- [x] Create a screenshot-illustrated GitHub Markdown user guide and matching standalone HTML using the 66ideas.com layout; distinguish current availability and preserve fictional-only images. Nineteen topics cover implemented Mac/iPhone workflows with seven native fictional screenshots. HTML embeds the images, unchanged logo and licensed Outfit font; Markdown retains GitHub-relative images. Root AGENTS.md makes guide/screenshot review part of every feature, and a dependency-free check plus GitHub push/PR workflow catches stale HTML, changed image provenance and unreviewed feature sources. [Guides/maintenance](../docs/README.md), [validation](../dev/docs/results/validation.json).
- DOC01 (existing screenshot harness): the sample preview's menu-driven capture stops before New Login creates a draft (PWDTWO.Render 5). No user vault was opened. Use a dedicated sample-only native-view capture for documentation rather than changing application menu behavior for this task.
- DOC02 (documentation capture compile): the first standalone Mac host omitted WindowHooks, which is defined alongside the product entry point. Reuse the existing hooks/notification definitions from that file in the temporary capture build; retain the documentation host without persistent-controller startup.
- DOC03 (guide narrow layout): the 390-point browser check found a grid child inheriting the table's minimum width and overflowing the page. Set the content grid child minimum width to zero; retain scrolling inside tables and recheck the actual phone-width page.
- DOC04 (topic navigation sizing): lazy screenshot decoding without intrinsic image dimensions shifted content after anchor navigation. Emit the native PNG dimensions in the HTML so image space is reserved before decoding; recheck topic navigation.
- Documentation validation: DOC01's existing menu capture remains unmodified; the dedicated real-view sample-only host avoids persistent-controller startup and produced both Mac images. DOC02 compile omission is corrected by reusing the actual window hooks. DOC03/04 corrections pass browser review at 1280/390 pixels, with no phone-width page overflow, valid topic targets and reserved image dimensions. One native iPhone documentation capture case passes; all seven images inspected. Temporary-repository checks confirm clean success and rejection of stale HTML, unreviewed feature changes and modified screenshot provenance. No user vault, password, clipboard, cloud account or physical phone was accessed; no application behavior changed.

### Approved iPhone identifiers — 2026-10-14

- [x] Replace the temporary iPhone app/extension identifiers with `com.66ideas.pwdtwo.iphone` and `com.66ideas.pwdtwo.iphone.autofill`; use `group.com.66ideas.pwdtwo` for their shared storage. Generated project, entitlements, runtime group, biometric service, package verifier and simulator interop runner are aligned. User explicitly accepts discarding existing meaningless test data; no migration added. Both native products compile and their identities/arm64/minimum OS/provider principal class/test-runtime exclusion verify. Six AutoFill and eight session checks pass. New Apple profiles exist for both approved IDs, but shared-group authorization still blocks signing/installation. Current deployment instructions, architecture decision and both end-user guides updated; visible controls/screenshots remain unchanged. [Evidence](../dev/iphone/results/2026-10-14/identifiers/summary.json).
- ID01 (new-identity provisioning): simulator/device compilation and all 14 targeted checks pass. Apple automatic signing creates profiles for the approved main/extension identifiers, but both profiles still reject the requested App Group entitlement. Check the new group's account association; no entitlement-stripped package is eligible for installation.
- ID01 remains pending: filtered Apple profiles confirm empty App Group scopes for both new identifiers; the extension does have the required password-provider entitlement. Native Xcode navigation/input did not respond reliably enough to complete the association. No account capability change, new physical installation or test-data deletion is claimed. The names/configuration change is complete; the separate physical AutoFill deployment gate stays open.

### iPhone physical deployment — 2026-10-19

- [x] User confirms the new App Group is assigned to both approved identifiers and explicitly requests installation. Automatic provisioning, signed device build and strict main/extension identity/profile/team/device/group/provider/principal/architecture verification pass. Staged installation copy matches the verified package. Physical iPhone queries confirm installed 0.4.3 (9), `com.66ideas.pwdtwo.iphone` and `group.com.66ideas.pwdtwo`. Foreground launch succeeds and the same process remains running on the final scoped query. Source matches the prior verified six AutoFill/eight session checks; no implementation change or redundant test rerun. No vault migration, fixture injection, credential change or automatic OS provider enabling was performed. The older 0.3.0 test app remains separate and untouched. Markdown/generated HTML guides, README and current deployment status updated; documentation check passes. Existing fictional screenshots remain accurate because visible UI is unchanged. [Filtered installation/signing evidence](../dev/iphone/results/2026-10-19/installation/summary.json).
- P0-AF04/ID01 signing blockers resolved: refreshed Apple profiles now authorize the exact new shared group for both targets. The extension's AutoFill capability and embedded runtime class verify. The physical-install part of T081 is complete; actual user-enabled Safari/compatible-app credential completion, hardware/biometric and broader runtime/security acceptance remain open.

### Temporary three-character development passwords — 2026-10-19

- [x] User explicitly requests a three-character vault-password minimum during development, restored to 15 when development finishes. Apply it consistently to iPhone Debug creation/recovery/backup recovery and shared core operations. Default/Release core and UI retain 15; use separate configuration-specific native archives and verify linked core/UI policy agreement. Update visible messages, native fictional screenshots and both guides; check new creation/recovery/AutoFill/backup boundaries and sign/install 0.4.4 (10) on the iPhone. Existing passwords are not changed.
- [ ] Release gate: remove the temporary development override and restore 15 characters in all development configurations before declaring development complete or shipping a production build. Release builds already retain 15; this user-requested final cleanup remains tracked.
- SP01 (simulator test launch): the first native run compiled successfully but stalled in the simulator testmanager launch request before any test process or result. Both full core configurations pass 57 checks (two historical fixtures ignored), and the signed device build succeeds. Cancel the stalled agent-owned run and restart the simulator's test runtime before retrying; no failed or unverified package is installed.

- Temporary password update verified/installed: both full core configurations pass 57 checks (two fixture cases ignored in each). Native Debug passes 17 cases; Release passes the actual linked-core 15-character creation/recovery/AutoFill/backup boundary case. Strict signed/staged package verification passes with the explicit development-password flag. Physical queries confirm installed 0.4.4 (10), expected group and successful foreground launch with its process still running. Existing passwords and the site-password generator are unchanged; no personal vault or clipboard access. Fresh fictional New Vault/Items/Generator/Diagnostics native captures reviewed, guide/provenance updated; standalone HTML regenerated and documentation check passes. [Evidence](../dev/iphone/results/2026-10-19/short-passwords/summary.json).
- SP01 resolved: canceling the stalled simulator launch and restarting its runtime allowed all 17 selected native checks to pass. No application code correction was required. The first failed launch remains recorded in the evidence folder.

### iPhone missing AutoFill provider in Settings — 2026-10-19

- [x] AFREG01: user reports PWDTWO missing from iPhone AutoFill settings after installing 0.4.4 (10). The containing app has only the shared-group entitlement; the provider has AutoFill authorization. Apple requires the AutoFill entitlement on both. Add main-target entitlement/capability, require it in both signed main/extension profiles in the verifier, build/sign/install 0.4.5 (11), and recheck the native provider regressions. Preserve the temporary three-character development policy and existing vaults. Update guides and affected fictional screenshots. Physical Settings discovery and filling require user confirmation; do not claim those from signing alone.

- AFREG01 correction verified: automatic provisioning refreshed the main app profile with the required AutoFill authorization. Both signed targets and profiles pass the stricter verifier; staged package matches. Eight targeted native checks pass (six provider regressions, configured password boundary and fictional documentation capture). Physical iPhone confirms installed 0.4.5 (11), correct shared group and successful launch with matching running process. No existing vault/password changes or provider enabling performed. Guides, setup/troubleshooting and native Diagnostics screenshot updated; HTML regenerated and documentation check passes. [Evidence](../dev/iphone/results/2026-10-19/autofill-registration/summary.json).
- [ ] AFREG01 physical completion: user confirmed PWDTWO is listed after 0.4.5. Safari/compatible-app credential selection and completion remain for confirmation after AFUI01.

### iPhone blank AutoFill overlay — 2026-10-19

- AFREG01 physical discovery confirmed by user: PWDTWO is now listed in system AutoFill settings after 0.4.5.
- [x] AFUI01: user-created fictional amazon.de login opens an empty white provider overlay. Scoped device process query confirms PWDTWOAutoFill is running. Investigate the actual controller lifecycle/presentation and system callback path; existing six provider tests exercise the data/session layer, not the extension screen. Add native controller coverage with isolated fictional data, fix the diagnosed problem, validate/sign/install an update and refresh both guides/affected native screenshots. Do not claim physical filling until user verifies.

- AFUI01 diagnosed on physical iOS27.0.1: scoped selector breakpoint catches Apple calling `prepareCredentialListForServiceIdentifiers:requestParameters:` on the provider. PWDTWO inherits Apple’s no-op (`ret`) implementation, so no chooser is built. Add the mixed-request override delegating to the password list, retaining password-only capability. Debugger detached; no vault/request parameter/account content inspected. Add actual controller rendering tests and a runtime selector-ownership regression.

- AFUI02 (test-host compilation): the injected native controller store factory initially dropped the shared store factory’s MainActor isolation, and Swift6 rejected compilation before tests. Preserve `@MainActor` on the closure type, then rerun. No failed package installed.

- AFUI02 corrected: native store factory retains MainActor isolation; the interim actual-controller and existing AutoFill regression run passes all nine cases. The new selector test compares runtime method implementations against Apple’s base class; the native host renders a secure password field with isolated fictional data and explicit unavailable/configuration views. Final versioned package verification remains pending.

- AFUI01 correction verified/installed: all 11 final native cases pass, including actual extension-controller secure input/unavailable/setup views and runtime ownership of both credential-list methods. The strengthened package check rejects the prior 0.4.5 missing mixed callback; signed 0.4.6 (12) and its staged installation copy pass both callbacks and strict identity/profile/capability checks. Physical device queries confirm installed version/group and successful launch with matching running process; frozen inputs match. Debug three-character policy remains, user vaults unchanged. New fictional native AutoFill image and updated Diagnostics screenshot inspected; guide/setup/troubleshooting/version text and provenance updated. [Evidence](../dev/iphone/results/2026-10-19/autofill-interface/summary.json).
- [ ] AFUI01 physical acceptance: user confirmed the 0.4.6 unlock form after resetting PWDTWO in iPhone AutoFill settings. Selected credential completion remains pending. Physical diagnosis establishes the original failure; new simulator/controller tests do not claim this acceptance.

- AFUI01 documentation validation complete: canonical Markdown includes the provider unlock screenshot and blank-overlay troubleshooting; standalone HTML regenerated with embedded assets, feature review recorded, and `build_guide.py --check` passes.

### iPhone AutoFill still blank after callback correction — 2026-10-19

- [x] AFUI03: user reports a blank sheet again with installed 0.4.6 (12). The callback correction and native host checks do not establish physical presentation success. Initial scoped query confirms main version 0.4.6 but no currently running provider; no PWDTWOAutoFill crash report is listed. Capture another actual system request, including receiver class and loaded product identity, before proposing another fix. Keep AFUI01 physical acceptance open.

- AFUI03 clarification: user confirms PWDTWO is missing only from Safari’s picker and remains present in iPhone AutoFill settings. Reverified 0.4.6 signatures/profiles/callback metadata and registered extension container; inspect the public enabled state separately from the app toggle. No further package installed or vault modified.

- AFUI03 physical presentation follow-up: user confirms PWDTWO remained present in system Settings and disappeared only in Safari. After turning the provider off and back on in Settings and starting a fresh AutoFill → Passwords request, user confirms the unlock form opens. Retained signed 0.4.6; no new source/package change. A scoped public enabled-state debugger query was inconclusive and interrupted; all debug sessions detached/closed. No vault content inspected. Record provider-reset troubleshooting in both guides; final unlock/credential completion remains pending. [Follow-up evidence](../dev/iphone/results/2026-10-19/autofill-interface/follow-up.json).

- AFUI03 guide review/check complete: documented the observed Settings-provider reset and fresh Safari Passwords request, with final credential completion still pending. Existing native unlock screenshot remains accurate; no source or visible UI change required a new capture. Markdown/standalone HTML and feature review are current; documentation check passes.

### iPhone AutoFill exact-host matching diagnosis — 2026-10-19

- [x] AFMATCH01: user reports a fictional Amazon login appears only with Search all logins when saved as amazon.de/http://amazon.de/https://amazon.de. User confirms the sheet destination is https://www.amazon.de. Inspecting the actual matcher confirms exact HTTPS-origin comparison; the different www hostname explains the absent result, consistent with the functional exact-host acceptance criterion and architecture entry 31. Give the exact current Website value, save/fresh-request instructions and explicit Fill once alternative. No automatic parent/subdomain authorization added. Current bare/http-format and additional-approved-address editor limits are documented rather than described as implemented. No application source/UI/deployment change; source tests and fresh screenshots are unnecessary for this documentation-only clarification, existing native captures remain accurate. Final selected credential completion still requires user verification.

- AFMATCH01 documentation validation: canonical guide and generated HTML now describe exact HTTPS-host matching, www/subdomain differences, saved-format limitations and the explicit Fill once alternative. Documentation review recorded and check passes.

### iPhone tolerant matching and convenient AutoFill unlocking — 2026-10-19

- [x] AFC01 user changes the matching policy: treat one leading www as equivalent to the bare domain, without automatically authorizing other subdomains, suffix lookalikes or nonstandard/insecure destinations. Accept bare, http and https saved website spellings for comparison to a secure HTTPS request. Preserve actual destination display and explicit other-site confirmation. Update the superseded exact-host-only documentation.
- [x] AFC02 user requests recent app authorization to carry to the extension and Face ID / Touch ID. Implement device-only shared Keychain authorization, five-minute default with Never/1/5/15-minute choices, expiry/boot/time/revision/revocation binding, automatic recent reuse and biometrics, password fallback, grouped all-or-none authorization and late-callback guards. Background app hiding preserves the bounded grant; manual/inactivity/protected-data locking, disabling and changed ciphertext invalidate it. Reuse the approved App Group as the Keychain group (Apple-supported), without adding an account capability. Shared biometric enrollment becomes available to both targets; reenrollment may be required for prior app-private items. No PIN fallback, plaintext group files or cloud key sharing.
- [x] Validate with isolated native fixtures including cross-instance recent reuse/expiry/reboot/time tamper, explicit lock/disable/revision revocation, biometric cancellation/all-or-none/late completion, WWW/lookalike/unrelated-host boundaries and actual controller views. Verify signing/package, install iPhone update, refresh affected fictional screenshots and Markdown/generated HTML guides. Physical Face ID/Touch ID and Safari completion require user acceptance.

- AFC03 (first integration compile): the existing manifest is Codable/Equatable, so the initial scripted insertion missed the grace field; the best-effort grant cleanup also required a mutable decoded component dictionary. Correct both before retrying. No failed package installed.

- AFC04 (recent access first-enable test): new expiry/revocation fixtures found that first enabling AutoFill published ciphertext before setting the enabled flag, so grant creation was skipped. Move optional authorization publication after successful enablement. Existing session/controller regressions passed; new tests retain the first-enable boundary as a regression. No candidate installed.

- AFC04 corrected: all seven initial authorization/matching tests now pass, including recent reuse, fixed expiry, manual lock, revision rebinding, stale-request refusal, malformed/partial grants and biometric cancellation/late completion. Added delivery-time expiry and explicit-provider-authentication coverage for final checks. Shared biometric sources also typecheck with the unchanged default Mac API.
- AFC05 (native UI checker): the full run reports that the recent-unlock screen still contains a text field. The checker currently counts every UITextField, including the matching list’s native search field. Inspect the fixture screenshot and narrow the assertion to secure password fields before rerunning; do not infer a successful screen from model checks alone.

- AFC05 confirmed by native capture: the recent-authorized matching list already renders the fictional www request and saved bare-host login correctly; the remaining text field is Search logins. Narrow the test to secure password fields. The full initial run executes 65 cases: two interop skips, 62 passes, one erroneous UI assertion. Recheck all affected authorization/controller/session surfaces after the correction and final best-effort wipe, unknown-destination presentation and opt-in legacy biometric cleanup refinements. No failed candidate is installed.


- AFC03/04/05 resolved; final development slice verified and installed as 0.4.7 (13). All 28 final targeted native cases pass, including eight recent-authorization/matching, four actual-controller UI/callback, six existing provider, eight session, one Debug policy and one documentation capture check. Separate linked Release policy check passes with 15. Earlier broad result remains accurately recorded as 62 passes/two interop skips/one corrected test-only assertion. Mac shared biometric defaults are unchanged and focused Swift6/macOS26 typechecking passes; no Mac user-visible change or Mac guide screenshot refresh is needed. Strict signed/staged verification is identical, final frozen source hashes match and device query confirms version/build; group authorization verifies in both signed targets. Existing vaults and passwords are unchanged; no personal data inspected. Four fresh fictional native views are reviewed and guides updated. Physical launch (phone locked), Face ID/Touch ID and Safari completion remain open; this does not close production parent/release tasks. [Evidence](../dev/iphone/results/2026-10-19/autofill-convenience/summary.json).

- [ ] AFC06 physical acceptance: unlock/open 0.4.7, reenroll Face ID / Touch ID once for shared enrollment, verify www matching and selected credential delivery, recent reuse/default and Never/expired biometric fallback, manual lock and phone protection. Do not infer hardware acceptance from fixtures or installation.

- AFC documentation handoff: actual native screenshots and implemented behavior reviewed; canonical Markdown and standalone generated HTML updated, provenance/hashes current, feature review recorded and documentation check passes. Release readiness is summarized separately without closing the independent security, hardware or later-platform gates.

- AFC06 launch follow-up: user unlocked the connected iPhone. Exact installed 0.4.7 (13) confirmed, foreground launch succeeded, and a separate PID-scoped query confirmed the same app remained running. No vault was opened by the agent. Face ID/shared reenrollment, recent reuse and Safari filling remain user-present acceptance. Guide deployment wording reviewed/updated; no application UI/source change, so the existing fictional screenshots remain accurate.

- [x] AFC06 Face ID subcheck (2026-10-19): user reports “Face id works” after the requested iPhone AutoFill test. Record physical Face ID success for installed 0.4.7 (13); do not infer selected-credential delivery, www matching, grace timing, Touch ID or device-protection acceptance from this narrower report. AFC06 parent and release gates remain open. This is acceptance-status documentation only; no source/UI/default/deployment change, so existing fictional native captures and provenance remain accurate. Canonical guide, generated HTML, current deployment/readiness and evidence updated.

- [x] AFC06/AFUI01 selected Safari credential completion subcheck (2026-10-19): user answers “yes” when asked whether selecting the saved login fills the fields correctly in Safari, following Face ID success. This confirms the reported saved-login completion flow on installed 0.4.7 (13). Do not infer www normalization (the saved hostname was previously edited), grace timing, Touch ID, compatible-app filling or other protection cases. Those broader AFC06/release criteria remain open. Acceptance-status documentation only: no application source/UI/default change; existing fictional captures/provenance remain accurate. Guide, current deployment/readiness and evidence reviewed/updated; HTML regenerated and documentation check passes.


### iPhone native attachments — 2026-10-19

- [x] AT01/T023/T041/T084 native mobile attachment slice: Add Attachment… through Files, validated original-file limit (default 1 MB), protected draft/Cancel/Save/history preservation, explicit removal, filename/type/size rows, bounded in-memory image/PDF/plain-text previews and explicit unencrypted Export to Files… confirmation. Add per-vault synced Attachment limits settings; do not truncate existing content. Late picker/read results, stale/foreign/locked reviews and total encrypted-payload capacity must fail safely.
- [x] AT02 validation/deployment/docs: isolated import/read/limit/symlink/late-completion/history/restart/sync/export/preview fixtures, real native UI captures, signed app/provider verification and 0.4.8 candidate packaging. Retain Debug3/Release15 and existing physical AutoFill acceptance; never operate personal vaults for these checks.

- AT03 (first test compilation): native attachment application sources compile, but the new fixture source helper needs MainActor isolation and asynchronous file reads must finish before XCTest assertion autoclosures. Correct those test-only issues; no failed package installed. Also keep total-payload checks at final native commit/limit save, not only file import.

- AT03 resolved: all eight initial attachment cases pass, including actual coordinated file reads, late-lock refusal, protected draft/history/restart, payload limits, native image/PDF/text construction, provider-folder convergence and encrypted backup recovery. Before final verification, expose the already-supported Document record type in the phone New item menu/Documents filter, disable editor inputs during a file read, and capture the actual attachment editor section without the unrelated keyboard covering it. No candidate installed yet.

- AT04 packaging review: the new native attachment reader (and existing chosen provider-folder reads) inspect user-selected file metadata. Add Apple's3B52.1 reason alongside container-onlyC617.1 to the shared privacy manifest; require both in strict main/provider verification. The full suite already running has frozen application/test sources; this correction changes packaging declarations/verifier only. Rebuild and verify the final signed package, and run final Release policy validation from the regenerated project. [Apple metadata reasons](https://developer.apple.com/documentation/bundleresources/app-privacy-configuration/nsprivacyaccessedapitypes/nsprivacyaccessedapitype).

- AT05 preview lifecycle refinement: reviewing the completed suite/source found that the review accessor's busy guard would dismiss an unchanged file during routine sync. Keep current saved previews readable during busy work, while disabling Export and rechecking busy/current authority at export confirmation. Lock, background and actual entry revision changes still retire the preview. Add a controlled busy/read regression, rerun all eight attachment cases and rebuild/verify/reinstall the final package. Earlier full71-pass/two-skip evidence is retained as the pre-refinement baseline, not silently relabeled. No default visible layout/control name changes; reviewed native captures remain accurate.

- AT04/AT05 final verification complete: full pre-refinement suite passes71 cases, skips the two separately driven interop fixtures and has no failures; final eight attachment cases pass after the busy-preview correction (including the controlled busy/current-preview regression). Final Release linked-core policy case passes with15. Both final signed targets and staged installation copy pass strict signature/profile/group/identity/runtime/capability/password/metadata-reason checks; source hashes and installation copy match. Physical query confirms final0.4.8 (14) installation without uninstalling or changing existing passwords. Phone locked afterward; no personal vault, clipboard or browser was accessed.
- AT documentation handoff: six fresh fictional native images reviewed; final attachment captures repeated after refinement (three identical, detail image re-inspected). Markdown/standalone HTML, deployment status, provenance and release readiness updated. Browser review at1280/390pixels shows no page overflow, embedded images, valid20-topic navigation and correctly sized attachment images. Review receipt/check completes below. No Mac code behavior, format or crypto change; existing Mac guide screenshots remain accurate. Temporary Debug password cleanup and parent security/physical/platform/release gates remain open.
- [ ] AT06 physical release acceptance: Files-provider selection/download/cancellation, export completion and recipient-copy handling, resource budgets, phone protection and both supported OS generations. Native/model fixtures and successful installation are not evidence of these user/system ceremonies.

- AT final documentation verification: canonical guide and affected fictional captures reviewed, final HTML regenerated with embedded assets, feature review recorded and documentation check passes. No remaining development-slice packaging/doc work; AT06 physical acceptance and broader production gates remain explicitly open.

### Mac updater and release packaging — 2026-10-20

- [x] MU01/T091 implementation and scoped validation: pinned Sparkle updater, native manual check/settings, daily optional checks, explicit installation approval, no HTML notes/profiling/automatic installation, safe postponement for pending saves/drafts. Validate isolated fixtures and signed update tamper refusal.
- [ ] MU02/T092: reproducible arm64 candidate build, nested Developer ID signing, authorized distribution profiles, notarized/stapled app and DMG, signed appcast/archive and checksums; no public publication. Update both guides and native fictional screenshots.
- MU03 provisioning attempt: selecting Developer ID directly on the development-only provisioning project fails with conflicting automatic development signing settings. No candidate installed. Use Xcode's Developer ID archive-export path to obtain the correct distribution profiles rather than ship development profiles or remove capabilities.

- MU04 distribution export: the correct Xcode archive-export route is reached, but Xcode reports “No Accounts” and no Developer ID profiles for the four existing Mac identifiers. The local Developer ID certificate and notarization Keychain authentication are present; they do not authorize profile issuance. Full-capability production packaging must fail closed until the Xcode team account/profiles are restored. Continue updater implementation, isolated signed fixtures and release tooling without modifying app capabilities or user data.

- MU05 initial compile: Swift rejects splitting a Boolean expression across conditional compilation blocks in the relaunch guard. Replace it with explicit return branches; rerun compilation and focused updater checks. No failed candidate installed.

- MU06 Sparkle binding compile: the delegate import requires an optional profile-key array and the full `shouldDownloadReleaseNotesForUpdate` Swift selector. Correct both against the pinned framework headers. The network-free updater state/policy checks already pass; rerun the actual linked native build.

- MU07 isolated fixture compile: Swift6 rejects an unhandled throwing validation task and an unannotated nested view traversal. Handle errors explicitly and keep native view traversal on MainActor. No real app launched or failed package installed. The complete 0.5.1 source candidate now compiles, signs with authorized development profiles and Hardened Runtime, and passes strict nested signature/arm64 checks.

- MU08 real installer/source audit: Sparkle asks `updaterShouldRelaunchApplication` before its postponement callback. Returning the busy/edit predicate there would abort an approved update before the deferral runs. Keep that initial permission independent of temporary save/edit state; defer through the actual postponement callback, retaining the app's termination guard for later races. Add a real two-version isolated installation test using the production coordinator and actual native update choices, rather than relying only on model checks.

- MU09 first real installation fixture: the native helper timed out before its first offer (phase0), so no successful installation is claimed. Defer its initial manual check until Sparkle reports it can check, log only its own native button titles, and rerun with the corrected MU08 production callback. The separately notarized app/DMG offline fixture already passes both Gatekeeper checks, signed feed/archive verification and mounted-DMG/extracted-ZIP round trips.

- MU10 native installation harness: with automatic checks disabled, Sparkle intentionally hides Remind Me Later; postponement of a manual offer is through its close button. The harness must close that actual offer, then request it again, and exclude controls hidden by ancestors (including the correctly hidden automatic-install opt-in). Its prior phase0 timeout is not a successful acceptance result. Keep the production automatic-install prohibition; correct the fixture's interaction rather than change policy.

- MU11 additional native tamper fixture: its first offline precheck timed out, so no native tampered-feed acceptance is claimed from that run. The error receipt was scheduled through an async continuation while Sparkle can run a modal error loop. Move the fixture-only receipt/quit timer into both default and modal-panel run-loop modes and retain timeout output; retry. The prior full notarized offline/DMG fixture and real installation fixture successes remain separately recorded.

- MU12 native tamper follow-up: both additional ad-hoc fixture prechecks timed out before an error receipt, whereas the Developer ID/Hardened Runtime offline and installation fixtures pass. The release targets a signed runtime; use that same identity/runtime for the additional native tamper test even without submitting another notarization. Do not claim the unverified ad-hoc runs prove release behavior.

- MU13 native refusal harness diagnosis confirmed from its own view tree: Sparkle's error acknowledgement is “Cancel Update”, not “OK”; its failure callback finishes after that acknowledgement. The fixture left the error window open, producing the earlier timeouts. This supersedes the unconfirmed modal-timing/ad-hoc hypotheses in MU11/12. Acknowledge only the fixture's actual error button (never the progress Cancel), then assert the actual error code and no embedded WebView. Retry before claiming native feed refusal.

- MU05/06/07/08 resolved in the final 0.5.1 (501) candidate: complete authorized development profiles, inside-out arm64 signing with Hardened Runtime/timestamps, exact browser/server identity resources and strict current-Mac capability verification pass. The existing installed 0.5.0 (500) app and vaults were not replaced/opened.71 model and 28 preference/clipboard checks pass; focused updater settings/state, cancellation and actual app-termination checks pass. Three release-policy cases pass, including real Sparkle archive/feed signatures and byte-tamper refusal.
- MU09/10 resolved: the final unrelated native version 1→2 fixture uses the production updater engine/coordinator and fictional in-memory record model. It declines a manual offer through its native close control, checks again, explicitly approves installation, retains the unsaved edit while waiting, waits for the controlled pending save, then really replaces/relaunches version 2 with the fictional saved record and its isolated preference intact. No embedded WebView is found. This does not establish encrypted-format migration, personal-vault security or released-PWDTWO acceptance.
- MU11/12/13 resolved: after acknowledging Sparkle's actual native Cancel Update error control, the final signed native fixture passes offline/manual-with-scheduled-off checks (error 2001) and rejects a modified signed appcast (error 1000), with no embedded WebView and automatic-install opt-in disabled. Earlier timeouts remain explicitly unsuccessful harness runs.
- [x] MU02a local release tooling and isolated artifact validation: pinned checksum-verified Sparkle 2.10.0, PWDTWO-specific public key/private Keychain account, signed HTTPS feed, versioned DMG/ZIP/appcast/checksums/manifest and explicit 66ideas.com download-link target implemented. Real Developer ID fixture app and DMG each receive Apple Accepted, staple/validate and pass Gatekeeper; signed archive/feed and mounted-DMG/extracted-ZIP round trips pass. Full-app distribution preflight correctly refuses the development-signed candidate before packaging. No production private key exported and nothing published.
- [x] MU02b full PWDTWO local distribution-artifact preparation: account recognition is repaired; normal Developer ID export and all four authorized profiles pass. The full app and DMG have Apple Accepted, stapled tickets, passing Gatekeeper and mounted-DMG/extracted-ZIP checks. After user authorization, final archive/feed signing and checksum/manifest generation pass; actual configured-public-key verification and altered-byte refusal also pass. Nothing published; see MU21 below. Do not drop capabilities, replace IDs or sign development profiles as a release workaround. Secure update-key backup, real released-PWDTWO upgrades/browser distribution, both OS generations and independent security acceptance remain production gates; T091/T092 stay open. The iPhone Debug 3 cleanup gate remains unchanged.
- MU documentation validation: actual fictional native Settings capture inspected; canonical Markdown and standalone generated HTML updated with candidate/installed/publication distinctions, exact controls, offline/restart/disabled-feed instructions and troubleshooting. Browser review at 1280/390 shows 21 topics, no horizontal overflow and the embedded new screenshot at suitable widths. Release config/script changes now participate in the guide review guard. Final review/check runs are recorded below. [Filtered evidence](../dev/macos-release/results/2026-10-20/summary.json), [release commands and account step](../dev/macos-release/README.md).

- MU final handoff: Markdown/native screenshot review and standalone HTML regeneration completed; `build_guide.py --check` passes with current updater/release sources and all 21 topic links/images. Candidate source hashes and filtered receipts are saved. No public release or installed-app replacement occurred.

### Mac distribution account recognition correction — 2026-10-20

- MU14: user correctly reports an existing Xcode sign-in. Direct read-only Settings verification confirms the named Apple account and existing developer team with Admin access; the earlier “not signed in” diagnosis was unjustified. CLI/GUI both use Xcode27.0 from the same app and the same user/home. The command-line account registry is empty although Xcode's cached account-to-team metadata identifies the existing team. Refreshing existing manual profiles and retrying the normal export still reports No Accounts. Do not sign the user out, clear account defaults, read/export tokens or require redundant sign-in.
- User requires uninterrupted computer access: stop GUI interaction and continue only background work; do not take focus again without arranging an interruption.
- MU15: a process-only account-registry argument with separate value is rejected as an invalid Xcode option. Retry the supported argument-assignment form for the existing cached account identifier; no persistent settings, credentials or permissions changed.

- MU14 account status correction: the GUI confirms the existing account/team; the CLI's No Accounts message is not a reliable sign-out diagnosis. Both normal retry and a per-process argument-assignment override still fail. An isolated preferences/reference test is in progress; it contains only the existing account identifier and public team metadata, does not change HOME, persistent Xcode preferences, credentials or Keychain permissions, and will clean up its temporary files. Distribution documentation corrected. Existing end-user UI/screenshots and installed versions are unchanged; no new capture is appropriate for account diagnostics.

- MU14 isolated account-reference export also still reports No Accounts; it did not resolve profile issuance. Temporary preference/profile copies were cleaned up and the real GUI sign-in/preferences were untouched. Try one ordinary background development build of the existing provisioning targets to initialize build services before a final export retry; no app launch, device use or window control. The remaining issue is CLI recognition/provisioning, not the user's signed-in status. [Correction receipt](../dev/macos-release/results/2026-10-20/account-recognition-followup.json).

- MU16 background provisioning build exposed a stale helper-project dependency: CredentialProvider.swift now uses CredentialProviderSession, but that source was absent from the provisioning target (the real app builder already includes it). Add the existing session source to that target and rerun with two jobs; no installed binary, identity, capability or visible behavior changes. This tooling-only correction does not require guide text/screenshot changes.

- MU14 export diagnostic improved: No Accounts now explicitly reports a command-line account-resolution failure and warns against inferring GUI sign-out or resetting credentials. This release-tool diagnostic has no end-user app/UI/default/deployment effect; canonical guide status and current fictional screenshots remain accurate. Review the release instructions and run the existing policy/doc checks.

- MU16 resolved: the corrected provisioning helper project builds/signs all four existing targets successfully using background Xcode tools, authorized development profiles and the existing team. No GUI use, installed-app replacement or credential change. This does not establish Developer ID profile availability; run one final export retry after build-service initialization. Canonical guide release status/screenshots reviewed and remain accurate; regenerated HTML/review receipt and documentation check pass.

- MU14 final background export still reports CLI No Accounts/missing distribution profiles after the successful helper build. No further GUI interaction was used after the user's availability constraint. The real account remains signed in; production packaging is still pending account recognition or manually issued distribution profiles. Corrected release instructions avoid redundant sign-in/reset advice. No end-user app/version/UI change; existing guide and screenshots remain accurate.

- MU14 follow-up validation: the two focused release policy/profile checks pass; the changed export diagnostic is verified by the real failed retry. The optional repetition of the unchanged signing/tamper test stalled in its test-only sign_update process and was interrupted to avoid a possible interactive wait while the user works; its temporary key/files cleanup ran. Do not report that interrupted rerun as a pass. The prior complete signature/tamper/native-installer/notarization successes remain the baseline. No new app feature or signing policy changed.

### Repair CLI account lookup — 2026-10-20

- MU17: user explicitly requests fixing the issue; continue in the background without taking focus. Local Xcode framework inspection confirms its account list expects dictionaries with identifier/username references. A read-only inspection with Keychain interaction disabled does not load credentials from a separate diagnostic process; no token is exported and no prompt is permitted. The previous temporary argument/home overrides did not establish that the actual preference registry had been repaired.
- MU18: cautiously restore only the empty production account-reference list using the existing cached account-to-team mapping, preserving all other preferences. Save the original key value with private permissions; on failed export restore it only if still equal to our attempted repair, so independent changes are not overwritten. This selects an existing account; it does not change credentials, access permissions or the GUI sign-in. Run normal export to validate rather than treating metadata presence as success.

- MU18 repair verified: restoring the missing existing account-reference dictionary resolves the CLI lookup. The normal Xcode Developer ID export succeeds and obtains distribution profiles. Retain the repaired reference and its reversible metadata-only backup; no logout, credential change or GUI interaction was needed.
- MU19 actual distribution verification exposes a release-tool bug not reached by development-signature rejection tests: codesign's optional certificate-extraction prefix must be attached with `=`, otherwise it is mistaken for a bundle path. Correct the argument and rerun verification against the real exported bundle; keep all certificate/profile checks.

- MU19 resolved: the actual full-capability Developer ID export passes certificate/profile, all nested IDs/groups/AutoFill/browser trust, secure timestamp/Hardened Runtime and nine arm64 executable checks after correcting the codesign certificate-prefix argument. No validation was weakened.
- MU20 unattended staging: add separate prepare/finalize stages so notarization and download verification finish without reading the Sparkle update key or prompting while the user works. Finalization verifies immutable prepared hashes before key access; four focused policy/profile/drift/path checks pass. The full app and DMG both receive Apple Accepted and staple/Gatekeeper checks pass. The final mounted-DMG check fails with hdiutil Permission denied; investigate the OS's documented diskutil image route before claiming round-trip completion. No public assets, installed-app changes or GUI interactions.

- MU20 resolved: the read-only DMG mount succeeds with an internal temporary mount point. The checkout is on removable storage; mounting beneath it failed. Update the packaging verifier to use an isolated local temporary mount and compare both mounted/extracted app metadata with the verified candidate. Revalidate the existing Apple Accepted app/DMG tickets, strict signatures/Gatekeeper and both round trips without resubmitting or replacing assets. Four focused policy/profile/preparation cases pass after the final source change; earlier failed mount attempts remain unsuccessful.
- [x] MU21a account repair/local artifact preparation: normal Developer ID export succeeds, all four exact existing distribution profiles/capabilities and all nine protected arm64 executables pass; real full app and DMG each receive Apple Accepted, staple/validate and Gatekeeper acceptance. Read-only DMG and ZIP extraction pass with matching app metadata and /Applications link. Immutable preparation hashes/filtered evidence are recorded; no personal vaults opened, installed app replaced, credential/ACL changed or public publication.
- [x] MU21b final archive/appcast signing and release checksums/manifest: the existing PWDTWO key trusts only its creating generate_keys executable for signing/decryption. First use by the official signing tools may require Keychain approval. Ask about a convenient brief interruption only after the concrete notarized/verified artifacts are ready; leave pending unless the user agrees. Do not export the key or broaden ACLs to avoid the prompt. The staging command reads no Sparkle private key, and finalization refuses artifact drift before accessing it. User availability requested; no prompt triggered.
- MU documentation review: this repair and staging affect release/deployment status only, not app controls/defaults or installed versions. Canonical Markdown reviewed and updated with actual Developer ID/notarization/download-verification status and remaining update-signing/publication gates. Existing isolated fictional native screenshots/provenance remain accurate; no account, Keychain or desktop capture belongs in the user guide. Update both generated HTML/review receipt and final check before handoff.

- MU21 staging review: the official appcast generator scans both ZIP and DMG files. Since staged preparation now creates both before signing, isolate only the immutable stapled-app ZIP for generation and require its exact expected enclosure URL; do not let the manual DMG enter the automatic-update feed. Five focused cases pass, including the new ZIP/DMG-selection regression (mocked external generator, not claimed as a cryptographic integration test). Prior real signature/tamper acceptance remains separate; actual PWDTWO signing is still pending user availability. This correction does not alter visible app controls/settings, so reviewed guide instructions and fictional captures remain accurate.
- MU21 final background handoff: canonical Markdown/status and unchanged fictional screenshots reviewed; standalone HTML regenerated, review receipt recorded and documentation check passes after the final staging correction. Five focused policy/profile/preparation cases pass. All temporary verification mounts are detached and the internal copy removed. The original failed mount/terminated probe are retained as failures, not acceptance evidence. Account repair and notarized local preparation are complete; final update signing remains pending the availability question. No GUI prompts or public/installed-app changes occurred.

### Final Mac update signing — 2026-10-20

- MU21b completed: the user explicitly authorized running signing now and could approve a Keychain prompt. The normal finalize command reverified immutable preparation hashes, the full app and stapled ticket; official generate_appcast/sign_update then generated and verified the actual ZIP/feed successfully. Final manifest remains published:false/productionApproved:false; all final asset and manifest checksums match. No agent ACL changes, private-key export, installed-app replacement, personal vault access or public publication.
- MU22 independent artifact check: CryptoKit uses only the configured public Ed25519 key to verify the actual final ZIP and exact signed feed bytes/length, then rejects a changed byte in each in memory. Exact versioned ZIP enclosure, archive size, three manifest asset hashes and all four checksum entries pass. This is final-artifact evidence, distinct from the prior unrelated installer fixtures and not a production security/upgrade sign-off. Filtered [finalization receipt](../dev/macos-release/results/2026-10-20/release-finalization.json) retains results.
- MU documentation/status review: canonical guide now records completed local notarized/signed packaging, separate installed/candidate versions and the still-unpublished feed/download. Release README, readiness/architecture and receipts updated; no app UI/default changed, so the reviewed fictional screenshots and provenance remain accurate. Keep T091/T092 publication/platform/security acceptance, secure signing-key backup and iPhone Debug-password cleanup gates open. Generate standalone HTML, record the actual review and run the documentation check before handoff.
- MU22 final handoff validation: final archive/feed signatures and altered-byte refusal pass using only the configured public key; asset/checksum/manifest verification passes. Canonical Markdown and existing native fictional captures reviewed, standalone HTML regenerated, review receipt recorded and documentation check passes. Local 0.5.1 (501) artifacts are complete; installed Mac 0.5.0 (500) and iPhone 0.4.8 (14) are unchanged. No public release or production approval occurred.

### Install and launch Mac 0.5.1 — 2026-10-20

- [x] MU23 user-authorized installation: confirm the existing app is not running, verify the final ZIP hash, extract into a staging folder, rerun complete Developer ID/profile/capability/arm64 checks plus stapled ticket/Gatekeeper, then replace at the existing app path with rollback on failed signature checks. Retain the prior 0.5.0 binary separately. Keeping the app path preserves Chrome's existing host manifest. Installer did not touch vault files/preferences or change passwords.
- [x] MU24 launch confirmation: open the exact installed path and independently query NSRunningApplication. Version0.5.1/build501, correct bundle URL, finishedLaunching:true, hidden:false and a live process are confirmed. No agent unlock or inspection of vault contents. Actual user workflows/biometric/browser/upgrade-data acceptance remain open; launch is not security approval. [Installation receipt](../dev/macos-release/results/2026-10-20/mac-installation.json).
- MU documentation review: update canonical guide, README, release instructions/readiness and current evidence to installed0.5.1; iPhone stays0.4.8. This is installation status, with no native UI/default source change. The existing fictional Settings capture remains an accurate development-channel example and is explicitly distinguished from the installed release-configured controls; no user app/desktop capture is used. Regenerate HTML, record review and check before handoff.

### Public specifications repository — 2026-10-20

- [x] GH01 user explicitly authorizes creating public GitHub repository 66IDEAS/PWDTWO and publishing only specs/ for now. Review all specification files for credentials/private keys/personal account data, normalize the one local checkout path and add a specifications-only index explaining intentionally unavailable code/evidence links. Stage and commit only specs/; application code, guides, root files, workflows, binaries and local data remain unpublished. Use the authenticated GitHub account's noreply address for new public commit metadata without changing the user's Git configuration.
- Publication changes repository availability, not application behavior/settings. Update the local end-user guide to explain that only specifications are public; no app/update-feed/download publication or production approval is implied. Existing fictional screenshots/provenance remain accurate and do not require replacement.

- [x] GH02 repository creation and scoped initial push: create public https://github.com/66IDEAS/PWDTWO, connect origin via HTTPS and push main with upstream tracking. The first commit contains 24 Markdown files exclusively under specs/. Private keys/credential-pattern/email/personal-host and inline high-entropy checks found no sensitive account credentials; the historical test password is explicitly fictional. One machine-specific checkout path is now relative, and specs/README.md explains intentionally unavailable local-code/evidence links. Public commit uses the authenticated GitHub account's noreply email; global/local author configuration is unchanged.
- [x] GH03 publication documentation: update architecture, local README and canonical user guide to distinguish public specifications from unpublished application source, local guides and release/update assets. No application source, UI/default or installed version changes; current fictional captures/provenance remain accurate. Run the guide review/check locally, without adding any non-specification file to the public commit. Verify public visibility, exact remote tree and branch tracking before final handoff.

- GH final validation: GitHub reports PUBLIC, default branch main and a nonempty repository whose sole root entry is specs/. Local main tracks origin/main. Canonical Markdown/publication status and unchanged fictional images reviewed; standalone HTML regenerated, actual review receipt recorded and documentation check passes. These local guide/root-file changes remain uncommitted and unpublished as requested. No application tests are needed for this repository/documentation-only change.

### Public project README — 2026-10-20

- [x] GH04 user requests publishing README.md with the same structure as 66IDEAS/MD22 and 66IDEAS/CRMThree. Read both current GitHub READMEs, then adapt their centered theme-aware branding, badges, specification-first introduction, repository map, specification navigation, contribution/license sections and 66IDEAS footer to PWDTWO. Describe planned scope separately from private Mac/iPhone builds; do not invent public installers, application source or production/security approval.
- [x] GH05 supporting files are limited to the existing root MIT LICENSE and byte-identical original light/dark SVG wordmarks copied into assets/. Their hashes match the existing reviewed user-supplied brand provenance. Preserve the illustrated local guide links with an explicit unpublished/full-checkout-only explanation. No application code, guides, workflows, binaries or private signing material is included. The prior local README's detailed build notes are retained in an ignored dev/docs/build backup; platform-specific local build guides remain available.
- [x] GH06 guide/status review: update the canonical guide and public specs index/architecture to include README/branding/license availability alongside the specifications. No app behavior, settings, deployment version or native view changed, so existing fictional captures/provenance remain accurate. Regenerate standalone HTML, record review/check locally, and publish only the explicitly scoped documentation/supporting files.

- GH README final verification: GitHub's actual Markdown renderer retains the theme-aware picture, badges, tables, section structure and explicit unpublished-guide caveat. The live README blob matches the local file. The public 28-file tree contains only specs/ plus README.md, LICENSE and the two original wordmarks; no application source/guides/workflows/binaries were uploaded. Canonical guide/status and unchanged fictional captures reviewed; standalone HTML regenerated, review receipt recorded and documentation check passes. Native application tests are unnecessary for this documentation-only change.
