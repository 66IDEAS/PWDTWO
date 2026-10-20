# Current iPhone development deployment

Updated 2026-10-19. Installed development version: 0.4.8 (14). This document supersedes the old identifiers in dated AutoFill/signing reports.

| Item | Approved value |
| --- | --- |
| Main target | `PWDTWOiPhone` |
| Main bundle ID | `com.66ideas.pwdtwo.iphone` |
| Extension target | `PWDTWOAutoFill` |
| Extension bundle ID | `com.66ideas.pwdtwo.iphone.autofill` |
| Shared App Group | `group.com.66ideas.pwdtwo` |
| Existing signing team | `AHBM4Y6VPX` |

The project generator, entitled runtime store, package verifier, device biometric service namespace and simulator interoperability runner use the new naming scheme. Changing the main identifier creates a separate iOS application sandbox. The user explicitly confirmed the previous vaults are meaningless test data; do not add migration code or transfer those fixtures. New identities do not inherit authorization from the old profiles. Historical result files retain their original identifiers as evidence.

## Steps for the user

1. Connect the iPhone by USB, unlock it, trust the Mac if requested, and keep Developer Mode enabled.
2. From the project checkout, open `dev/iphone/PWDTWOiPhone.xcodeproj` in Xcode.
3. Select the blue project icon, then target **PWDTWOiPhone → Signing & Capabilities**.
4. Enable **Automatically manage signing** and choose the existing developer team. Its team ID is `AHBM4Y6VPX`.
5. Check the main bundle ID above. Under **App Groups**, select `group.com.66ideas.pwdtwo`.
6. Repeat for **PWDTWOAutoFill**, using its bundle ID, the same team and same group. Confirm the **AutoFill Credential Provider** capability is present on both **PWDTWOiPhone** and **PWDTWOAutoFill**.
7. If the new group does not appear, refresh the list or register/associate it in the Apple developer account. In Certificates, Identifiers & Profiles, both exact app identifiers must have that App Group assigned. The extension also needs the password-provider capability. [Apple configuration guidance](https://developer.apple.com/documentation/xcode/configuring-app-groups), [account capability association](https://developer.apple.com/help/account/identifiers/enable-app-capabilities/).
8. Once signing is ready, the agent can build, strictly verify, install and launch through the command line. The ordinary `build.py --device` product is unsigned and must not be presented as installable.
9. In the new app, create a fictional vault or open a chosen cloud vault explicitly. Enable **Use included vaults with AutoFill**, open the iPhone's AutoFill settings and enable PWDTWO as a provider. Set **Keep AutoFill unlocked** (five minutes by default), and enable **Face ID / Touch ID** in PWDTWO to share biometric enrollment with the provider. Repeat enrollment once if upgrading from the earlier app-private enrollment.

## CLI verification

Build with the existing team and the connected iPhone as the destination, using automatic provisioning and internal-volume DerivedData. Verify the signed main app and nested provider with `dev/iphone/verify_autofill.py`, supplying the expected team/device. For the explicitly approved three-character Debug build, also supply `--development-passwords`; without that flag the verifier requires the normal 15-character policy. Both signatures and embedded profiles must authorize the approved identifiers and exact new group. Only a passing package is eligible for installation. Do not strip App Group/provider entitlements to make a build succeed.

Initial new-identity deployment completed (2026-10-19): the user associated the new group with both identifiers. Automatic provisioning then produced authorized profiles for the main app and extension. The strict package verifier passed both signatures, exact team/app/group/device scopes, provider capability, runtime principal class, minimum OS/architecture and absence of test runtime. The verified package was installed and foreground-launched on the connected iPhone. Device queries confirm version 0.4.3 (9), `com.66ideas.pwdtwo.iphone` and `group.com.66ideas.pwdtwo`; the running process matches the newly installed bundle. The older 0.3.0 installation remains separate and untouched. [Installation evidence](../dev/iphone/results/2026-10-19/installation/summary.json).

The [2026-10-14 failed signing attempt](../dev/iphone/results/2026-10-14/identifiers/summary.json) is historical. Its empty App Group scopes no longer describe the refreshed profiles. Installed physical delivery does not enable iOS AutoFill automatically or verify Safari/app credential completion; those user-present checks remain open.

## Temporary development password update

The user requested a three-character minimum during development, restored to 15 when development finishes. The signed 0.4.4 (10) Debug update introduced this policy; installed 0.4.8 (14) retains it. New vault creation, recovery and recovered-backup passwords use the matching native/core policy. Existing vault passwords are unchanged; use the existing password or explicitly create/recover a test vault to choose a shorter one. Website password generation is unchanged.

The Rust feature and Swift compilation condition apply only to Debug. Native archives are separated by configuration; startup verifies agreement with the linked core. Default/Release builds retain 15, verified with the actual native/core creation, recovery, AutoFill and backup path. Removing the Debug override before development completion is an open release gate. [Checks and installation evidence](../dev/iphone/results/2026-10-19/short-passwords/summary.json).

## Documentation review

The guide describes the temporary policy and unchanged existing passwords. Four fresh fictional native images capture New Vault, Items, Generator and Diagnostics in 0.4.4 (10); unchanged Settings/Search and Mac images remain accurate. All eight screenshots and provenance were reviewed before regenerating HTML. Previous cloud-delivery proof and physical AutoFill acceptance are not relabeled as evidence for this update.

## Missing provider correction — 0.4.5 (11)

The user reported PWDTWO missing from system AutoFill settings in 0.4.4. Inspection confirmed that the containing app lacked the AutoFill entitlement and profile authorization, although the extension had both. [Apple requires both targets to have the entitlement](https://developer.apple.com/documentation/authenticationservices/ascredentialproviderviewcontroller). The generator now enables the capability/entitlement for both; automatic signing refreshed the main profile. The strict verifier checks signed and profile authorization on each target. The signed 0.4.5 (11) update is installed and launched, with eight targeted native checks passing and source fingerprints verified. The user must reopen Settings → General → AutoFill & Passwords to confirm PWDTWO appears and enable it. Discovery/enabling/filling are not inferred from package validation. [Evidence](../dev/iphone/results/2026-10-19/autofill-registration/summary.json).

No visible native layout changed. Diagnostics now shows 0.4.5 (11), so its isolated fictional screenshot was refreshed; the remaining screenshots remain accurate. Both end-user guides explain the correction and troubleshooting.

## Blank provider overlay correction — 0.4.6 (12)

The user confirmed that 0.4.5 appears in system AutoFill settings. Selecting it on a page with an active passkey request opened an empty sheet. A scoped physical-device selector breakpoint on iOS27.0.1 caught `prepareCredentialListForServiceIdentifiers:requestParameters:` falling into Apple's inherited no-op implementation. No vault or request-parameter contents were inspected. The extension now overrides that callback and delegates to the existing password chooser. It continues to advertise passwords only; no passkey support is added.

The native test target compiles the actual extension controller and uses a private fictional store to verify the secure unlock form, unavailable/configuration views and runtime ownership of both selectors. The signed-package verifier also rejects products missing either list selector in their runtime metadata. Native validation, strict signing/installation and guide/screenshot review are recorded in [the correction evidence](../dev/iphone/results/2026-10-19/autofill-interface/summary.json). The final physical Safari/compatible-app completion is still for the user to confirm after the update.

Deployment of 0.4.6 (12) is confirmed by scoped physical device queries: installation, exact version/group, successful foreground launch and matching running process. The signed staged copy matches the verified package. Eleven final native cases pass with matching frozen inputs. User-created data remains intact; no vault operation was performed by the agent. The unlock-screen documentation capture uses the actual provider controller and an isolated fictional store in a native test host, not a real Safari sheet.

Physical presentation follow-up: the user initially saw the blank sheet again and then found PWDTWO missing only from Safari’s picker, while it remained registered in system Settings. Turning PWDTWO off and back on in AutoFill & Passwords, then starting a fresh login-field AutoFill → Passwords request, opened the expected unlock form. This observation does not prove stale provider state as a root cause; no further package change was made. Credential selection/completion remains pending. The guide records the observed reset steps and retains its accurate fictional native unlock screenshot. [Follow-up](../dev/iphone/results/2026-10-19/autofill-interface/follow-up.json).


## Convenient native AutoFill — 0.4.7 (13)

The signed update is installed; the physical query confirms the exact approved bundle, version and build. After the user unlocked the phone, foreground launch succeeded and a separate scoped query confirmed the same app process remained running. The user subsequently confirmed Face ID works on the physical iPhone and that selecting the saved login fills the fields correctly in Safari. Recent-unlock timing, www normalization without editing the saved host, Touch ID, compatible-app filling and wider device-protection cases remain pending. Installation does not enable the OS provider or enroll biometrics. No personal vault was opened or changed by the agent.

One leading www and the bare hostname now match, including bare/http/https saved spelling against a secure HTTPS destination. Other subdomains, nonstandard ports, insecure destinations and suffix lookalikes remain separate. The actual destination is displayed and other-site filling remains explicit.

The app and provider share a device-only, nonsynchronizing, passcode-bound Keychain recent authorization. **Keep AutoFill unlocked** offers Never/1/5/15 minutes, default five. Reads do not extend the deadline. Grants bind current ciphertext, included owners, revocation nonce, wall/uptime and boot identity. Explicit lock retires them; background hiding preserves the remaining window. Device protection blocks Keychain access, while delayed OS notifications and resumed expiry checks are documented rather than assuming delivery during suspension. Current-biometric-set enrollment is shared; no device PIN fallback is added. [Apple documents an existing App Group identifier as a supported Keychain access group](https://developer.apple.com/documentation/security/sharing-access-to-keychain-items-among-a-collection-of-apps), so no new portal capability is needed.

Final targeted native validation passes 28 cases. The earlier full run had 62 passes, two interop skips and one incorrect UI assertion that counted the native search field as a password field; native screenshots confirmed the matching screen, the assertion was corrected, and all affected surfaces were rerun. The linked Release password-policy check passes separately with 15. Shared biometric sources typecheck for Mac with default behavior unchanged; the Mac app was not rebuilt or installed. Strict signed and staged verification pass with identical results and frozen source hashes. Four fictional native captures update both illustrated guides. [Evidence and open physical acceptance](../dev/iphone/results/2026-10-19/autofill-convenience/summary.json).


## Native attachment update — 0.4.8 (14)

The installed signed update adds native document/attachment workflows without a schema, encryption or key change. Main/provider identities, approved group and temporary Debug3/Release15 policy remain unchanged. Native imports are security-scoped/coordinated, bounded and tied to the originating encrypted editor draft. Existing saves/history, automatic synchronization and encrypted backup paths carry complete file bytes. Previews use only in-memory native ImageIO/PDFKit/plain text; explicit native Files export warns that the copy is unencrypted and outside vault protection. A picker/export system recipient may own data after handoff; locking cannot recall such a copy.

The full native suite passes 71 cases with two separately driven interop fixtures skipped and no failures. Strict signed and staged verification passes, including both container and user-selected metadata privacy reasons. The physical query confirms the approved app at 0.4.8 (14); the phone is locked, so foreground launch is not claimed. Actual Files-provider/export/device-protection acceptance is not inferred from model or native-view captures. Current deployment evidence is in [attachments/summary.json](../dev/iphone/results/2026-10-19/attachments/summary.json). The feature guide and fresh fictional screenshots are reviewed separately before package handoff.

Final attachment preview refinement: all eight attachment cases pass after keeping unchanged previews open during busy work; export remains disabled and rechecked. Final linked Release password-policy case passes with 15. The earlier full suite remains the 71-pass/two-skip baseline; the targeted rerun verifies the final changed surface. Final signed/staged 0.4.8 (14) is installed; the phone is locked, so physical launch and Files-provider/export acceptance remain open.
