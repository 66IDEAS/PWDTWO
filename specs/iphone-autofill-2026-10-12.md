# iPhone password AutoFill — development handover

**Identifier update, 2026-10-14:** the user approved `com.66ideas.pwdtwo.iphone`, extension `com.66ideas.pwdtwo.iphone.autofill` and App Group `group.com.66ideas.pwdtwo`. Use the [current deployment instructions](iphone-deployment.md). The signing attempts and old group named below are historical evidence, not the identifiers to configure now. Existing disposable test data does not require migration.

PWDTWO iPhone 0.4.0 (6) adds a separate native SwiftUI/UIKit AuthenticationServices credential-provider extension. It is compiled for iPhone on iOS 26/27, with no web view, Catalyst, or Mac compatibility. This is a password-filling slice of T062/T079/T081, not closure of mobile AutoFill or production security validation.

## Behavior

- In the unlocked app, Settings → AutoFill lets the user enable or remove encrypted copies of the currently included vaults. Excluded vaults are absent. The setting is off initially.
- The app publishes an opaque manifest and complete KDBX ciphertext into its entitled App Group. No password, unlocking component, recovery key, title, username, website, or plaintext search catalog is stored there. Files use private permissions, complete iOS Data Protection, and OS backup exclusion. Old ciphertext generations are removed after replacement; disabling removes the copies.
- Safari and compatible apps present the native provider. Every request requires the passwords for all included vaults before any login rows appear. Vault numbers follow the order in the app's Settings → Vaults. Main-app Face ID authorization is not reused across processes.
- Matching logins appear first. Matching requires one unambiguous supported HTTPS origin, exact host and the default HTTPS port. Other login search requires an explicit switch and a destination warning followed by Fill once. An absent/unsupported app service address receives the same explicit confirmation. No automatic submission occurs.
- Login selection excludes Trash, non-login entries and empty passwords. Search covers visible login metadata only. Passwords and secret notes never drive matching. The application’s broader ordinary search behavior is unchanged.
- App operations retire the catalog before changing local vault files, credentials or included selection, and refresh it afterwards. A retirement failure blocks the operation before mutation. The provider compares the current entire group and ciphertext hashes before unlock publication and credential completion. A short shared advisory lock keeps credential delivery and app mutation from racing at this final boundary. It is local process coordination, not a provider/cloud transaction.
- A result consumes the presentation; cancellation, disappearance and device/background lock retire its session. An expired request cannot return credentials. The provider retains no unlocked keys between requests. The app's own lock does not transfer authorization: an encrypted copy can still be opened independently by entering the included vault passwords in the provider.

This does not revoke old offline copies, backups, or credentials that the OS already received. Cloud delivery still requires the existing app's sync workflow; the provider never writes or syncs vaults.

## Setup and signing

1. Both `PWDTWOiPhone` and `PWDTWOAutoFill` need the same authorized App Group: `group.com.sixtysixideas.pwdtwo`. The extension additionally needs the AutoFill Credential Provider entitlement. The project contains both capability declarations and entitlement files.
2. Xcode automatic signing currently returns profiles with the provider entitlement but **empty App Group lists**, including after refreshing only these two cached profiles. The signed build is correctly refused. No entitlement-stripped build was installed. The existing physical iPhone installation remains 0.3.0 (5).
3. User setup requested: open the project, choose the existing developer team in Signing & Capabilities for each target, then select the group under App Groups for both. Xcode manages the association/profiles. [Apple’s App Group configuration](https://developer.apple.com/documentation/xcode/configuring-app-groups) describes selecting or creating groups for the related targets.
4. After this succeeds, build with the existing team/device and run `dev/iphone/verify_autofill.py` against the signed product. It checks both signatures, exact identities/team/profile/device/group scopes, expiry, architecture, versions, provider capabilities and runtime principal-class symbol. Only a passing package may be installed.
5. On the iPhone, unlock PWDTWO and enable Use included vaults with AutoFill in Settings. Use its Open iPhone AutoFill settings button to enable PWDTWO through Apple's supported settings API. Then select Passwords/PWDTWO in a Safari or compatible-app login field and unlock the native chooser.

The original local vault directory and passwords are unchanged. No Mac/iPhone fixture or real password was injected or rotated. Old profile cache files were retained under ignored `dev/iphone/build/pre-autofill-profile-cache`; fresh automatically fetched profiles remain in Xcode's cache.

## Validation and limits

The full iPhone simulator suite executed 28 cases: 26 passed and two separately driven interop fixtures skipped. All six new AutoFill cases passed again after the final setup-label/capability changes. Device and simulator app/extension compilation pass, including matching the Objective-C principal class against the packaged executable. Frozen phone source hashes were checked after the final builds. [Recorded results](../dev/iphone/results/2026-10-12/autofill/summary.json).

New cases cover ciphertext-only storage; grouped password failure without partial visibility; included/excluded vaults; Trash/non-login filtering; strict/malformed destinations and explicit other-site confirmation; app edit invalidating a prior chooser; one-use consumption; disable cleanup; cancellation during asynchronous unlock; tampered/symlinked copies; delivery-gate contention; and a failed retirement preventing app mutation.

Physical Safari/app acceptance is pending successful signing/installation and enabling the OS provider. The native chooser has not yet been observed through the physical OS extension ceremony. iOS 27 runtime and real extension memory/performance budgets remain unverified. Copies are bounded to 16 vaults, 32 MiB each and 64 MiB total for this evaluation; the provider reads complete ciphertext and the existing bounded preview payload. These are development resource bounds, not promised product capacity.

Next mobile slices: extension Face ID through separately protected shared Keychain enrollment and credential-generation validation; optional OS-managed account identity suggestions; supported save/update and password-generation ceremonies; OTP/passkey/card workflows; dedicated iPad provider; independent security review. None of these capabilities is advertised by the current extension.
