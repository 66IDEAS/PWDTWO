# PWDTWO — Functional Specifications

## Project goal

Create PWDTWO, a password manager with applications running on macOS, iPhone, iPad, and Android devices. Users can search for saved credentials, save login entries, and generate passwords in the applications, with a choice of local-only vaults or vaults that synchronize automatically across their devices. Offline access supports viewing, adding, and editing credentials; cloud-enabled vaults synchronize changes after reconnection. Browser autofill supports Safari and Chrome on macOS, Safari on iPhone and iPad, and Chrome on Android. On macOS, browser access is provided through extensions. Autofill also supports compatible applications on iPhone, iPad, and Android.

Users can maintain multiple independent vaults, each with its own password. Optional Face ID, Touch ID, or Android biometrics can be enabled for individual vaults on supported devices. Device locking locks all open vaults; vaults also lock after a configurable period of inactivity. The accepted recovery-key feature applies separately to each vault.

Users can import existing login credentials from Google Password Manager, 1Password, LastPass, and Apple Passwords / iCloud Keychain exports using the sources' currently supported export routes.

The scope also includes browser capture and update prompts, credential history and deletion recovery, manual credential access, multiple accounts per service, exports and encrypted backups, device setup and activity, passkeys, authenticator codes, password-health and exposure checks, organization and richer records, provider-account security, Mac application autofill, passphrases, deliberate sharing, and documents. Vault files can synchronize through iCloud Drive on macOS, iPhone, and iPad, or through Google Drive across macOS, iPhone, iPad, and Android. Google Drive provides synchronization for vaults used across Apple and Android devices. KeePass-compatible KDBX is the preferred vault-file format subject to the full feature set fitting without major limitations. Every password entry and credit card has a dedicated long-text notes field.

Status: The original scope, proposed additions R01–R12 with trusted-contact emergency access, expiring sharing links, and PWDTWO-managed device approval/revocation removed, and the subsequent multiple-vault, cloud-file synchronization, local-only storage, storage migration, long-notes, built-in Mac updater, and on-device diagnostics requirements are accepted as functional scope. KDBX format selection remains conditional on compatibility assessment. The user approved the phased implementation baseline on 2026-10-09; release assignments and scoped dependencies are maintained in [tasks.md](tasks.md#approved-development-phases). The user explicitly confirmed deliberate sharing as encrypted individual copies or equal-access shared vaults; trusted-contact emergency access and expiring sharing links are removed. Detailed behavior still needing a decision is recorded below.

## Common behavior

- Access to private vault content through the applications and autofill integrations follows the unlocking and locking requirements.
- System notifications use generic messages such as “PWDTWO needs your attention” and do not expose website names, usernames, or vault contents. Details about findings or synchronization problems are shown inside PWDTWO after the relevant vault has been unlocked.
- Notify about unresolved synchronization conflicts, persistent synchronization or backup failures, and newly detected leaked passwords when checks are enabled. Routine successful operations do not generate notifications.
- Each notification category can be enabled or disabled separately on each device, subject to operating-system notification permission.
- Each vault has independent contents and its own password. Open vaults share an application-wide locking session on the device. References to a master password or recovery key mean those of the selected vault, not a single password or recovery key for all vaults.
- Search, autofill, health checks, and other content views use only vaults unlocked for that operation. Results identify their source vault.
- Creating, capturing, importing, sharing, exporting, and restoring entries must identify the intended source or destination vault.
- Synchronization requirements throughout these stories apply to cloud-enabled vaults. Local-only vaults do not synchronize or require a cloud-provider account.
- Entries and organization in cloud-enabled vaults synchronize across the user's connected devices. Shared-vault changes synchronize to participants with provider access; individually shared copies do not synchronize back to their source.
- The attachment-size limit is stored per vault and synchronizes with that vault, like its backup configuration. Local-only vaults retain these settings locally.
- Sensitive-value masking, notification-category preferences, clipboard-clearing controls, auto-submit, generator preferences, periodic password re-entry, and leaked-password-check consent and scheduling stay local to each device. Changing them on one device does not change another device’s preferences or authorize network checks there. Generated-password history remains vault content and follows its separate synchronization rules.
- Cloud-provider sign-in authorizes access to a stored file; it does not by itself unlock the vault inside that file.
- File synchronization, a vault password, owner recovery, and application-managed sharing are distinct capabilities. Format and provider limitations must be reconciled with existing requirements without silently removing them.
- Offline operations use information already available on the device. Network-dependent actions show whether they are pending, unavailable, or complete.
- The accepted browser/platform scope remains Safari and Chrome on macOS, Safari on iPhone and iPad, and Chrome on Android. Application autofill supports compatible applications on macOS, iPhone, iPad, and Android.
- Browser-version support covers Safari versions supplied with the supported macOS, iOS, and iPadOS releases, and the latest stable Chrome major version plus its immediately preceding major version on Mac and Android. Browser beta and developer releases are outside the guaranteed support range.
- All accepted stories remain included; their approved phase assignments are maintained in [tasks.md](tasks.md#approved-development-phases).

## User stories

### 1. Access the password manager on supported devices

**Description:** As a user, I want a password manager application on my devices so that I can access my passwords on each supported platform.

**Acceptance criteria:**

- The signed and notarized Apple-silicon Mac application is downloadable from GitHub Releases for 66IDEAS/PWDTWO, with the download file also linked from 66ideas.com.

- The application runs on macOS.
- The application runs on iPhone and iPad.
- The application runs on Android devices.
- Each supported application provides access to password search, saving login entries, and password generation.

### 2. Search for passwords

**Description:** As a user, I want to search for stored passwords in the application so that I can find the credentials I need.

**Acceptance criteria:**

- I can enter a search query in each supported device application.
- The application displays matching stored entries.
- By default, one combined search covers all currently unlocked vaults. I can restrict the search to one selected vault.
- Ordinary text search includes entry titles, usernames, website addresses, tags, and notes.
- Password values, authenticator secrets, and other hidden secret fields are excluded from ordinary text search.
- I can open a matching entry to access its credentials.
- I can identify the vault containing each result; locked vault contents are excluded until that vault is unlocked.
- The application indicates when there are no matching entries.

### 3. Save login entries

**Description:** As a user, I want to save login entries in the application so that I can find and use my credentials later.

**Acceptance criteria:**

- I can create and save a login entry in each supported device application.
- I can associate a username and password with the website the login belongs to.
- I can save a password I enter myself or one generated by the application.
- I choose the unlocked destination vault when creating the entry.
- Every password entry has a dedicated long-text notes field with the behavior described in story 43.
- Saved login entries are available for search, browser autofill, and autofill in compatible mobile applications.

### 4. Autofill credentials from the browser

**Description:** As a user, I want to autofill username and password fields from within my browser so that I can use my saved credentials while browsing.

**Acceptance criteria:**

- On macOS, I can use the password manager through extensions in Safari and Chrome.
- On iPhone and iPad, browser support is limited to Safari.
- On Android, browser autofill supports Chrome.
- I can use a saved login to autofill its username into a website's username field.
- I can use a saved login to autofill its password into a website's password field.
- Locally available login entries can be used for browser autofill without an internet connection; the destination website may still require connectivity to sign in.
- Account selection and website matching follow story 19.
- Automatic login-form submission is disabled by default: autofill fills the credentials and leaves submission to me.
- I can enable or disable automatic submission in Settings. When enabled, PWDTWO submits a supported login form after my deliberate autofill action.
- Automatic submission does not bypass account selection, website matching, or vault-unlock requirements. If the integration cannot submit the login form, I can submit it manually.

### 5. Synchronize credentials across devices

**Description:** As a user, I want my saved credentials to synchronize automatically across all my devices so that I can access the same passwords wherever I use the application.

**Acceptance criteria:**

- Credentials in cloud-enabled vaults synchronize across my macOS, iPhone, iPad, and Android devices using a provider supported on those devices.
- Synchronization is tracked independently for each vault and its configured storage location.
- Credentials saved on one device become available on my other devices when they are online.
- Synchronization happens automatically without manual export or import.
- Entries created or edited offline synchronize automatically when connectivity returns.
- If the same editable vault entry is changed differently on multiple devices before synchronization, the application preserves the conflicting versions and lets me choose which one to keep, as described in story 12.

### 6. Generate passwords

**Description:** As a user, I want the application to generate passwords with a chosen length and character types so that I can create passwords that fit my needs without inventing them myself.

**Acceptance criteria:**

- Password generation is available in each supported device application.
- I can request a generated password when creating a login entry.
- I can choose the generated password's length.
- I can independently enable or disable uppercase letters, lowercase letters, numbers, and symbols.
- The character-based generator defaults to 24 random characters, with uppercase letters, lowercase letters, numbers, and symbols enabled; these settings remain adjustable.
- Generated passwords have the chosen length and contain only enabled character types.
- If I disable every character type or enter an unsupported length, the application explains the problem and requires a valid configuration before generating a password.
- These generation controls remain available offline.
- I can save the generated password with the login entry and use it later for autofill.
- I can also generate a multiword passphrase as described in story 34.

**Details remaining:** Define the supported length range. The character-based default is confirmed: 24 random characters with all four character categories enabled.

### 7. Use the password manager offline

**Description:** As a user, I want to access and manage my passwords without an internet connection so that I can continue using the password manager while offline.

**Acceptance criteria:**

- Offline support is available in each supported device application.
- I can search for and view credentials already saved or synchronized to the device without an internet connection.
- I can create new login entries and edit existing entries while offline.
- I can generate and save passwords while offline.
- Offline changes remain saved after closing and reopening the application.
- Entries created or edited offline in cloud-enabled vaults synchronize automatically with my other devices when connectivity returns. Local-only vault changes remain local.

### 8. Autofill credentials in mobile applications

**Description:** As a user, I want to autofill credentials in other applications on my mobile devices so that I can sign in without manually copying usernames and passwords.

**Acceptance criteria:**

- Autofill is available in compatible applications on iPhone and iPad.
- Autofill is available in compatible applications on Android.
- I can select a saved login and fill its username and password into compatible login fields.
- Mobile application autofill uses the same saved credentials as the password manager and browser autofill.
- Locally available credentials remain available for autofill while offline; the destination application may still require connectivity for its own sign-in.

### 9. Unlock with a master password or optional biometrics

**Description:** As a user, I want to unlock my saved passwords with a master password and optionally use my device's biometrics so that I can control access to my credentials and choose a convenient way to unlock them.

**Acceptance criteria:**

- I can unlock each vault using that vault's own password on each supported platform.
- When choosing a new vault password during creation, password change, or recovery, it must contain at least 15 characters. Spaces and long passphrases are supported, without mandatory uppercase, number, or symbol composition rules.
- Temporary user-approved testing exception (2026-10-19): the iPhone development/Debug build accepts three-character vault passwords. Release/default builds retain 15; restore the development minimum to 15 when development finishes. Existing vault passwords are not changed by the update.
- PWDTWO shows password-strength feedback while I choose a vault password. Existing vaults protected by shorter passwords remain openable; the new-password policy does not lock users out of existing data.
- Each vault requires valid unlocking material for that vault. Shared-session unlocking must preserve these separate credential requirements.
- Reopening PWDTWO restores the previously open vaults as one session. One biometric authentication reopens the included vaults that have biometric unlocking enabled on this device and do not require password entry.
- If an included vault requires its password, PWDTWO prompts for that vault’s password before completing the shared-session unlock. I can instead remove that vault from the opening session and continue with the others.
- The session opens only after the remaining included vaults meet their unlocking requirements. There is no additional application-wide password; each vault retains its own password and recovery key.
- I can optionally enable Face ID or Touch ID for a vault on Apple devices where the method is available.
- I can optionally enable biometric unlocking for a vault on supported Android devices.
- After a new fingerprint is enrolled or Face ID is reset, affected biometric vault-unlock access requires the vault passwords before biometric unlocking can be re-enabled. Newly registered biometrics do not automatically inherit that access.
- If I have forgotten a required vault password, the established recovery-key process remains available; device credentials do not replace it.
- When biometrics are disabled, unavailable, or unsuccessful, unlocking requires the vault password. The device PIN, screen-lock passcode, or operating-system login password is not an alternative PWDTWO unlock method.
- If I have forgotten the vault password, I can use the separate recovery-key process in story 10.
- Unsuccessful authentication leaves the vault locked.
- A locked vault requires successful unlocking before saved credentials can be viewed or used for autofill.
- On a device already set up with a local vault, master-password unlocking and enabled biometric unlocking work without an internet connection.

- Periodic vault-password re-entry is disabled by default. In Settings, I can enable it even when biometric unlocking is enabled and choose the interval myself.
- Once that interval has elapsed, biometric unlocking alone cannot reopen the vault until its password has been entered successfully.
- This optional policy does not replace the required new-password entry after a synchronized password change or recovery.

**Details remaining:** Define supported interval choices. Periodic password re-entry is disabled by default, and this preference remains local to each device.

### 10. Recover access using a recovery key

**Description:** As a user, I want a separately stored recovery key so that I can regain access to my saved passwords if I forget my master password.

**Acceptance criteria:**

- During each vault's setup, I can have the application generate a separate random recovery key.
- The recovery information identifies its vault; recovering one vault does not unlock or change the passwords of other vaults.
- I can save or print the recovery key, and the application explains that it grants access to my vault and should be stored safely outside that vault.
- I am prompted to confirm that I have saved the recovery key before recovery setup is marked complete.
- The locked application offers a recovery flow in which I can enter my recovery key without knowing my current master password.
- A valid recovery key lets me unlock an available copy of its vault and choose a new password while preserving all supported vault contents in that copy.
- Completing recovery requires a new vault password and a newly generated recovery key. I must confirm that I have saved the replacement recovery key before recovery is marked complete.
- The completed recovered vault uses the new credentials; the replaced recovery key is not accepted for that new vault generation. Older backups and offline copies are not retroactively changed and require credentials valid for their own generation.
- A normal password change outside the recovery flow preserves the existing recovery key.
- An invalid recovery key does not unlock the vault or allow me to change the master password.
- On a previously configured device with the required vault and recovery information available locally, I can recover access offline. Changes synchronize when connectivity returns.
- On a replacement device, I can recover from an available vault file and its required recovery information. An internet connection is needed when that material must be retrieved from remote storage.
- The application explains that the recovery key restores access to available vault data; it cannot recreate data that has been lost from every device and the sync service.
- Recovery remains under my control: there is no vendor, administrator, or trusted-contact reset, escrow, or recovery backdoor.
- If I lose both the vault password and its recovery key and have no usable existing authorized unlock path, nobody can restore my access. Optional biometric unlocking on an already configured device remains supported.
- Deliberate sharing does not grant recipients recovery authority over my private vaults.

**Confirmed reconnection behavior:** After learning of a password change or recovery through synchronization, another device requires the new vault password before reopening that vault. Preserve its unsynchronized edits for reconciliation after successful unlocking. Offline devices can continue using their existing local copy until they reconnect. The same rule applies to all participants in a shared vault.

**Confirmed conflicting-credential behavior:** If devices independently change a vault’s credentials, preserve both encrypted versions. Ask the user to unlock each version and explicitly select which password/recovery-key combination to retain, then reconcile the entry changes under that selected protection. Do not silently choose credentials or discard either version. If a required version cannot yet be unlocked, keep it and the conflict pending. Owner-recovery lifecycle requirements still apply when recovery is used.

**Technical details remaining:** Define authenticated change detection, key rotation, safe reconciliation, and biometric key handling. Recovery-key replacement after use is confirmed. New-device recovery does not require separate PWDTWO approval; provider authorization is required only when retrieving remotely stored material. Reconcile this alternative recovery path with the conditional KDBX format; a KeePass key file is not automatically an equivalent recovery mechanism.

### 11. Lock the vault automatically

**Description:** As a user, I want my vault to lock when my device locks and after a configurable period of inactivity so that further access to my credentials requires unlocking.

**Acceptance criteria:**

- Automatic locking is available on macOS, iPhone, iPad, and Android.
- When a device locks, all unlocked vaults on that device lock automatically.
- The inactivity timeout defaults to five minutes. I can change it in Settings separately on each device; the preference remains local and does not change other devices’ timeouts. All open vaults lock together when the configured period of inactivity elapses.
- Interaction with PWDTWO or deliberate use of its autofill resets the inactivity timer. General browsing, typing in another application, and background synchronization or other background work do not reset it.
- All open vaults share one application-wide inactivity timer on the device. Interaction with any vault or with combined browsing/search, and deliberate autofill use, resets this timer and keeps all currently unlocked vaults open.
- Device locking, expiration of the shared inactivity timer, or manual application locking closes access to all open vaults together.
- Credentials in a vault that has automatically locked cannot be viewed or used for browser or mobile-application autofill until I successfully unlock that vault again.
- I can unlock again using my master password or an enabled biometric method.
- Both automatic-locking triggers work without an internet connection.

**Details remaining:** Define supported timeout choices and validate shared-session coordination across native integrations. Shared reopening is settled in story 9: one biometric authentication for eligible vaults, required passwords before completing the unlock, and an option to exclude a vault from that opening session. The user replaced independent per-vault timers with one application-wide timer: activity anywhere in PWDTWO or deliberate autofill keeps all open vaults unlocked. The default remains five minutes, adjustable separately on each device; device locking locks all open vaults immediately.

### 12. Resolve conflicting changes without losing either version

**Description:** As a user, I want conflicting versions of an editable vault entry to be preserved so that I can review them and choose which version to keep when changes from different devices synchronize.

**Acceptance criteria:**

- When synchronization encounters differing independent edits to the same editable vault entry, the application identifies the entry as having a conflict.
- The conflicting versions remain available until I choose which version to keep; neither is silently overwritten by the other.
- After unlocking the vault, I can review the conflicting versions and select the version to keep.
- I can postpone resolving a conflict without losing either version, including after closing and reopening the application.
- Once I make a choice, the selected version becomes the current entry and the resolution synchronizes to my other devices when they are online.

### 13. Import existing passwords

**Description:** As a user, I want to import passwords from the services I already use so that I can move my existing logins into this password manager without entering them manually.

**Acceptance criteria:**

- Importing supported export files from other password managers is available only in the macOS application; iPhone, iPad, and Android do not offer this import flow.
- I can import saved login entries from Google Password Manager exports.
- I can import saved login entries from 1Password exports.
- I can import saved login entries from LastPass exports.
- I can import saved login entries from Apple Passwords / iCloud Keychain using a password export from the Mac's Passwords app.
- I can select the source and its supported export file, review an import summary, and confirm the import into my unlocked vault.
- Import preserves the website, username, and password supplied for each supported login entry.
- Import also preserves supported titles, notes, organization, and custom fields when these are present in the source export and supported by the destination item type.
- The import preview identifies item types or fields that cannot be transferred, so I can review any incomplete migration.
- Potential duplicates are identified, and importing does not silently overwrite existing login entries.
- Exact duplicates are skipped by default and reported in the import preview and results. Matching only the website or username is not enough to classify entries with different supported details as exact duplicates.
- Possible matches with different details are presented for review; I can skip the incoming entry, keep both entries, or update the existing entry.
- Updating an existing entry preserves its previous version in entry history.
- The import result reports which entries were imported, skipped, or could not be imported, with an explanation for unsuccessful entries.
- Imported logins are available for search and autofill and synchronize to my other devices through the normal synchronization process.

**Source scope:** Imports cover saved passwords through the source applications' currently supported export routes. Compatibility with obsolete export formats is not required. For Apple, the scope is passwords exportable from the Passwords app; legacy application or service passwords available only through Keychain Access are out of scope. See [Apple's Passwords export guide](https://support.apple.com/en-ie/guide/passwords/mchl35b12625/mac), checked on 2026-10-08.

**Details remaining:** Define the precise matching rules for supported item types. Import availability is settled: macOS only. Duplicate handling is confirmed: skip exact duplicates by default, review differing possible matches, offer skip/keep both/update, and preserve the existing version in history when updating.

### 14. Capture and update logins from websites

**Description:** As a user, I want the browser integration to offer to save new logins and update changed passwords so that my vault stays aligned with the accounts I use.

**Acceptance criteria:**

- In supported browser integrations, entering credentials during sign-up or sign-in can prompt me to save a new login.
- In supported website password-change flows, the integration offers to update the corresponding saved login.
- Before saving, I can review the website and username and choose whether to create an entry or update an existing one.
- I can review and select the destination vault before saving a new login; updates remain associated with the selected entry's vault.
- If several saved accounts match, I can select the account to update.
- I can dismiss the prompt without changing my vault.
- Saved changes remain available locally and synchronize through the normal sync process.

### 15. Recover generated passwords from interrupted workflows

**Description:** As a user, I want to retrieve a password I generated even if a website flow was interrupted so that I do not lose the credential before saving the login.

**Acceptance criteria:**

- Passwords and passphrases I use from the generator are retained in a protected generator history.
- Before a generated value is used, an unlocked destination vault is selected for its history. Retained values belong to that vault and require its unlocking before they can be revealed.
- After unlocking, I can identify a generated value by its creation time and associated website when available.
- I can copy a retained value or save it into a new or existing login.
- Retained values survive closing and reopening the application and are accessible offline on the device where they are available.
- Generator history is stored inside the selected encrypted vault and synchronizes across devices for cloud-enabled vaults.
- Generated passwords and passphrases remain in this history until I explicitly clear it; there is no automatic expiration or scheduled cleanup. Clearing generator history also synchronizes for cloud-enabled vaults.

**Confirmed policy:** Retain generator history in the selected encrypted vault until explicitly cleared by the user, and synchronize it across participating devices. Define reconciliation of concurrent generation and clearing as part of the synchronization design.

### 16. View, copy, and edit credentials manually

**Description:** As a user, I want to manage and use credentials directly in the application so that I can sign in even when autofill is unavailable.

**Acceptance criteria:**

- By default, passwords, card security codes, and sensitive custom fields are masked; card numbers show only their last four digits. After unlocking, I can deliberately reveal or hide a value and copy it.
- With masking enabled, temporarily revealed values are hidden again when I leave the entry or lock its vault.
- In Settings, I can disable sensitive-value masking so that these values, including full card numbers, are displayed immediately when I view an unlocked entry. Reopening an entry with masking disabled does not require a Reveal action.
- This display preference applies only to unlocked content; locking the vault still removes its contents from view.
- Sensitive-value masking is configured separately on each device. Changing it does not change another device’s display behavior or another shared-vault participant’s preference.
- I can copy its username or password independently without editing the entry.
- Automatic clipboard clearing for copied passwords is disabled by default. I can enable or disable it in Settings and adjust the clearing delay.
- When enabled, PWDTWO clears only its still-current password copy after the configured delay; it must preserve content copied afterward.
- I can edit the title, username, password, website addresses, and other supported fields, then save or cancel the changes.
- If PWDTWO locks while I have unsaved edits, it preserves them as an encrypted draft on that device. After unlocking the relevant vault, I can resume editing or discard the draft.
- Draft changes do not become active entry data for autofill or synchronization until I explicitly save. For an existing entry, its previously saved version remains the active version.
- Preserving a draft must not delay locking or leave its contents accessible while the vault is locked.
- Manual access and editing work with locally available entries while offline.
- Saved edits synchronize and participate in the conflict-handling behavior in story 12.

### 17. Delete and restore entries

**Description:** As a user, I want to remove unwanted entries and restore accidental deletions so that mistakes do not immediately destroy my saved information.

**Acceptance criteria:**

- I can move an entry to a recoverable trash and undo or restore that deletion.
- Deleted entries remain in the vault’s trash indefinitely until I explicitly empty it; there is no automatic expiration or scheduled cleanup.
- Emptying the trash synchronizes to other devices for cloud-enabled vaults.
- Trashed entries are excluded from normal search and autofill suggestions.
- After unlocking, I can review the trash and restore an entry without re-entering its contents.
- If a matching active entry already exists, restoration keeps both: the deleted entry returns as a separate item, the existing entry remains unchanged, and PWDTWO flags the possible duplicate for review. Restoration does not automatically overwrite or merge the existing entry.
- Permanent deletion requires a deliberate confirmation that explains that the entry will no longer be recoverable from the application's trash.
- Deletions and restorations synchronize to my other devices.
- A deletion that conflicts with another device's edit preserves the competing states for review rather than silently discarding the edit.

**Details remaining:** Define reconciliation of permanent deletion with concurrent offline edits and precise matching rules for duplicate detection. Restoration with a matching active entry keeps both and flags the possible duplicate for review. Trash retention is settled: retain deleted entries until the user explicitly empties the trash, with no automatic cleanup.

### 18. Inspect and restore previous versions

**Description:** As a user, I want access to earlier versions of an entry so that I can recover a previous password or undo an incorrect edit.

**Acceptance criteria:**

- Saved edits retain earlier entry versions indefinitely until I explicitly clear that entry’s history; there is no automatic expiration or scheduled cleanup.
- History preserves all editable fields of an item, including passwords, usernames, notes, card details, and other supported content, so I can restore a complete earlier version.
- Replaced or removed attachments remain available in the earlier versions that reference them until I explicitly clear that history. PWDTWO explains that retained attachment versions contribute to vault size.
- Entry history is stored inside the encrypted vault and synchronizes across devices for cloud-enabled vaults. An explicit history-clear operation also synchronizes.
- Clearing ordinary entry history does not discard unresolved synchronization conflicts.
- After unlocking, I can inspect available previous versions and identify when they were saved.
- I can retrieve a previous password or restore a selected version as the current entry.
- Restoring a version preserves the version that was current immediately before restoration.
- Restoration synchronizes as a new change and preserves any unresolved synchronization conflicts.

**Details remaining:** Define how history clearing reconciles with concurrent offline changes and validate complete-version preservation for each supported record type. History covers all editable fields and replaced or removed attachments. Retention is settled: preserve entry history until the user explicitly clears it.

### 19. Choose accounts and match websites correctly

**Description:** As a user, I want clearly identified account choices and website associations so that the application fills the credentials I intend to use.

**Acceptance criteria:**

- I can save multiple distinct logins for the same website and identify them using titles and usernames.
- When several logins match, the autofill interface lets me choose the intended account.
- Suggestions show the source vault and exclude entries from locked vaults.
- I can associate a login with multiple legitimate website addresses.
- Website autofill treats one leading www as equivalent to the bare hostname (user change, 2026-10-19). Other related subdomains are not automatically treated as matches; I can add each additional approved website address to the entry.
- For example, a login saved for accounts.example.com matches shop.example.com only after that additional address is approved and saved.
- Autofill suggestions reflect the current website or compatible application's association with the saved login.
- Automatic suggestions do not treat an unrelated website as a match merely because its name looks similar.
- Filling requires my selection or another explicit fill action; selecting a mismatched entry must not silently release its credentials to that website.
- When I manually select a login for an unrecognized website, PWDTWO shows the destination hostname and a mismatch warning. I can explicitly confirm Fill once, Add approved website and fill, or Cancel.
- Fill once does not save an association. Add approved website and fill stores that hostname among the entry’s approved addresses for future matching. Neither mismatch-confirmed action automatically submits this first login fill, even if login auto-submit is enabled.

**Details remaining:** Define URL normalization, scheme/port and embedded-frame handling, and behavior for login flows spanning several pages. Deliberate mismatch handling is confirmed: show the hostname and warning, require explicit Fill once or Add approved website and fill confirmation, offer Cancel, and suppress auto-submit for that first fill. Exact-host matching with explicitly added approved addresses is confirmed; automatic related-domain matching is excluded.

### 20. Export vault data

**Description:** As a user, I want to export my data so that I can move it to another application and retain control of my records.

**Acceptance criteria:**

- Bulk export for use in another password manager is available only in the macOS application. Encrypted vault backups and sharing individual entries remain separate workflows.
- After unlocking, I can select entries or an authorized vault for export.
- The export preview identifies the source vaults. Selecting multiple vaults does not silently combine their credentials or protection requirements.
- I can export passwords and other supported records in a documented interoperable format.
- Export formats include unencrypted CSV for basic login migration and encrypted KDBX for richer vault exports, with KDBX interoperability limited to validated content and operations.
- For an encrypted KDBX migration export, I choose and confirm the password protecting the exported file. PWDTWO does not automatically reuse the source vault password.
- KDBX migration exports do not include PWDTWO’s recovery-key mechanism. The export preview explains that the chosen export password is needed to open the file. This does not change encrypted backups, which retain their existing password and recovery behavior.
- The CSV export screen clearly explains that the file is readable without a password. The preview for either format identifies unsupported fields and attachments before export.
- By default, migration exports include current, active entries within my selected scope, with notes and attachments where the selected format supports them.
- KDBX migration exports offer separate Include entry history and Include Trash options, both disabled by default. The export preview reflects these choices and identifies any unsupported content.
- These migration-export defaults do not reduce encrypted backup coverage; backups continue to include all agreed vault contents.
- Before export, I can review which item types and fields the chosen format includes or omits.
- The application states whether the resulting file is encrypted or readable without a password.
- The completed export reports any records that could not be included.
- A participant who can unlock a shared vault can export its contents; PWDTWO does not impose separate export permissions inside that vault.
- Passkey transfer is handled separately from password-only export formats, as described in story 25.

**Details remaining:** Define the CSV schema and KDBX export compatibility profile. KDBX migration export credentials are settled: the user chooses and confirms the export password, without automatic reuse of the source vault password or inclusion of PWDTWO recovery. CSV and encrypted KDBX are confirmed formats; bulk export to other password managers is macOS-only. Shared-vault participants can export readable contents.

### 21. Create and restore encrypted backups

**Description:** As a user, I want an independent encrypted backup so that I can restore my vault after losing its active copies.

**Acceptance criteria:**

- Scheduled encrypted backups are optional and disabled by default.
- In application Settings, I can enable scheduled backups, choose their frequency, change that frequency, or disable them again. PWDTWO does not impose a daily schedule or create user-facing backups on mandatory application-selected triggers.
- Each vault has one backup configuration and exactly one application-managed backup. For synchronized vaults, the configuration and backup synchronize across participating devices. Each successful backup replaces the previous backup; PWDTWO does not retain a backup history or offer a backup-version retention setting.
- For a synchronized vault, its scheduled backup is a separate encrypted file alongside the live vault in the same selected provider, iCloud Drive or Google Drive.
- For a local-only vault, its scheduled backup stays in a user-selected local folder and does not synchronize. Manual exports can be saved elsewhere.
- A failed or interrupted replacement preserves a usable previous backup until a complete new backup can safely replace it. Devices do not create independent backup sets.
- Deleting a cloud vault retains its existing application-managed backup unless I explicitly select Also delete the backup. Scheduled backups for the deleted cloud vault stop, and manual exports remain untouched.
- I choose which device creates the scheduled backups; a Mac is an option, not a requirement. Other devices synchronize the resulting encrypted backups and shared settings.
- I can change the designated backup device in Settings. The application must coordinate the change rather than intentionally running independent schedules on both devices.
- For a synchronized vault, I can select a replacement backup device even if the former device is lost or unavailable; approval from that former device is not required.
- The replacement takes over after connecting and synchronizing the assignment. Before writing another backup, the former device must verify the current assignment and stop if it is no longer designated.
- Changing the designated device preserves the existing backup and configured frequency.
- If the designated backup device is offline when a scheduled backup is due, that device performs the overdue backup when it comes back online.
- I can also manually create an encrypted backup of my authorized vault data and save it to a location I choose.
- The application explains that local backups help with accidental changes or corruption, while surviving loss of the device requires a backup stored elsewhere.
- Backup scope identifies the included vaults and preserves their separate identities and protection requirements.
- Each backed-up vault includes all its supported entries, attachments, history, trash, and the metadata required for recovery. The recovery secret itself remains separately protected; including recovery metadata must not expose an unprotected recovery key.
- The application explains what credentials or recovery material I need to open the backup later. Existing backups retain the password/recovery protection valid when created; changing the live vault's password or completing recovery does not rewrite those backups.
- I can restore from an available backup on a supported device, including while offline when all required files and unlock material are available locally.
- Before changing an existing vault, I can review the backup contents and proposed restore outcome.
- Restoration creates a separate vault by default, preserving the current vault. Replacing an existing vault requires an explicit choice and review; one vault's password or recovery key is not assumed to open another vault's backup.
- A separately restored vault does not silently resume synchronization against the original live vault or overwrite its cloud file.
- To recover selected entries, I open the backup as a separate vault and copy the chosen entries into my current vault. Both vaults must be unlocked; copied entries are independent and existing destination entries remain unchanged.
- Selective recovery uses this copy workflow. There is no automatic whole-backup merge feature; explicit replacement of an entire vault remains available with review.
- An invalid backup or incorrect unlock information does not overwrite my existing vault.
- Restore results identify the backup's date and any records that could not be restored.

**Details remaining:** Define backup packaging, supported frequency choices, safe implementation of backup-device handover, and execution under platform scheduling limits. Selective recovery is settled: open a separate restored vault and copy chosen entries, without automatic whole-backup merging. Handover behavior is confirmed: replacement does not require the former device, takes effect after the replacement connects and synchronizes the assignment, and preserves the backup and frequency. Backup location is settled: a separate encrypted file alongside the live vault in its selected provider for synchronized vaults, or a user-selected local folder for local-only vaults. A backup missed while the designated device is offline is performed by that device when it comes back online. Local-only scheduled backups do not enable cloud storage; explicit manual exports remain available separately. Attachments are embedded in the complete vault file. Optional scheduled backups with a user-selected frequency and designated device, one shared configuration and a single replaceable backup synchronized across devices, manual exports, complete vault coverage, and restoration as a separate vault by default are confirmed. Exactly one application-managed backup is retained; each successful backup overwrites the previous one. Manual exports remain separately user-managed files. The proposed daily schedule, mandatory pre-operation backups, and 30-backup retention limit were not adopted. Existing backups retain their original generation's credentials.

### 22. Set up a vault and connect additional devices

**Description:** As a user, I want guided setup so that I can create my vault and access the same data on additional devices.

**Acceptance criteria:**

- Setup lets me create each vault, choose its own password and either local-only storage or one supported cloud provider, and configure its recovery and optional biometrics.
- On another supported device, I can open an existing vault file from a supported storage location after any required provider authorization and vault unlocking with its password or recovery flow. Local-only setup does not require provider authorization.
- Setup does not require a separate PWDTWO account or approval from another PWDTWO device. Provider account security, including any provider-required MFA, remains separate from vault decryption.
- After unlocking the vault, I can optionally enable biometric unlocking on this device.
- The application distinguishes creating a new vault from opening an existing vault.
- For a cloud-enabled vault, I can see progress and completion of the initial synchronization.
- Once setup and any required initial synchronization are complete, the device can use locally available data offline.

### 23. View known device activity and understand access controls

**Description:** As a user, I want visibility into known device activity and clear guidance on protecting a lost device, without a separate PWDTWO account or managed enrollment system.

**Decision:** PWDTWO-managed remote device revocation is removed by user agreement. Provider account security and device controls remain with Apple, Google, and the operating system.

**Acceptance criteria:**

- Retain an informational view of devices reported as using the vault and their latest known activity, where available. This is not an authoritative inventory of everyone who possesses the file or its credentials.
- Keep one record per device containing its name, platform, PWDTWO version, and last reported synchronization time. Store this information inside the encrypted vault.
- Retain only the latest status for each device until I remove that record. Removing it tidies the list without revoking access; a device that synchronizes again can reappear.
- Activity information may be stale while devices are offline and does not grant or deny vault access.
- The application explains that cloud-account and device access must be managed through the applicable provider/OS controls. It does not offer a PWDTWO remote-revocation button or claim that removing an informational record revokes access.
- The application does not promise to remotely disable or erase downloaded vaults, exported copies, or known secrets.

**Technical details remaining:** Define device-record identity, update/removal reconciliation, timestamp handling, and provider/OS guidance. Fields and retention are confirmed: one latest-status record per device with name, platform, PWDTWO version, and last reported synchronization time, retained until manually removed. Keep device metadata within the vault’s protection boundary and avoid treating it as an enrollment authority.

### 24. See synchronization status

**Description:** As a user, I want clear synchronization information so that I know whether my latest changes have reached my other devices.

**Acceptance criteria:**

- I can see whether the application is offline, synchronizing, up to date, or unable to synchronize.
- Status identifies the affected vault and its configured storage provider/location. Local-only vaults are labelled as local-only, without a misleading synchronization error or pending-upload status.
- I can see the last successful synchronization and whether local changes are pending.
- Synchronization failures show an understandable explanation and a way to retry.
- Failed synchronization preserves local changes.
- Pending conflicts are identified separately from successful synchronization of other entries.

### 25. Create, synchronize, use, and transfer passkeys

**Description:** As a user, I want to manage passkeys alongside passwords so that I can use modern sign-in methods on supported websites and applications.

**Acceptance criteria:**

- I can create and save a passkey when a compatible website or application offers passkey registration.
- Saved passkeys identify the service and account they belong to and synchronize to my supported devices.
- On a compatible sign-in flow, I can select the intended passkey and authorize its use.
- Passkey access follows vault unlocking and the applicable operating-system credential-provider authorization requirements; there is no separate PWDTWO device enrollment.
- I can import or export passkeys through current supported transfer methods where the source and destination allow it.
- Transfer results identify passkeys that cannot be moved; a password CSV is not presented as a complete passkey export.
- Passkeys stored in a shared vault are available to all its participants, subject to vault unlocking and supported native sign-in integrations.
- Where technically supported, I can send a passkey to another PWDTWO user through the existing encrypted individual-copy workflow. The recipient receives sign-in access to the same website account.
- Sharing identifies passkeys that cannot be transferred and does not silently omit them or claim that a transfer succeeded. Native platform support must be validated.
- Deleting a passkey moves it to the vault’s Trash. Trashed passkeys are excluded from sign-in suggestions and use, but remain recoverable until I explicitly empty Trash; deletion and restoration synchronize for cloud-enabled vaults.
- Restoring a passkey makes the retained credential available again in PWDTWO. It cannot undo removal of that passkey from the website’s account settings or guarantee that the website will still accept it.

**Platform scope:** Operating-system versions follow requirement 18 in [architecture.md](architecture.md#18-support-the-current-and-previous-major-os-generations).

**Details remaining:** Define supported transfer methods and validate native passkey sharing capabilities against the browser-version policy in Common behavior. Shared-vault access and individual encrypted-copy sharing are confirmed for supported passkeys. Deletion and restoration follow the ordinary Trash policy; validate credential preservation and removal/reinstatement in native credential-provider indexes. Restoring local credential data does not restore a website-side registration that has been removed.

### 26. Generate and fill authenticator codes

**Description:** As a user, I want verification codes available with my saved logins so that I can complete supported two-step sign-in flows from the password manager.

**Acceptance criteria:**

- I can add time-based authenticator setup information by scanning a QR code or entering a setup key.
- I can associate the authenticator with the correct service and account.
- After unlocking, I can view the current code and its remaining validity, copy it, or fill a compatible verification-code field.
- Saved authenticator configurations synchronize across my devices.
- Code generation works offline once the configuration is available locally.
- Malformed or unsupported setup information produces a clear error. The application identifies the service and account for my review; it does not claim that a syntactically valid setup key has been verified with that service.

### 27. Review password health

**Description:** As a user, I want to identify weak and reused passwords so that I can improve the accounts that need attention.

**Acceptance criteria:**

- The application identifies saved passwords that meet its documented weakness criteria.
- It identifies password reuse across saved accounts.
- I can review an actionable list of affected entries and open an entry to address the issue.
- Findings update after I change the relevant entries.
- I can ignore a specific weak-password or reused-password warning for an entry, including when reuse is intentional. Ignoring one finding does not dismiss other warning types.
- Ignored warnings remain available for review, and I can re-enable them.
- Weak-password and reused-password warning exceptions are stored with the entry inside its encrypted vault. Ignoring or re-enabling one synchronizes across devices for cloud-enabled vaults.
- In a shared vault, the exception applies to all participants, and any participant can reverse it. Local-only vault exceptions remain local with their vault.
- Changing an entry’s password triggers a fresh assessment; an exception for the previous password does not automatically suppress a finding for the replacement password.
- Checks based solely on locally available entries remain available offline.

**Details remaining:** Define scoring, precise reuse grouping, and conflict handling for concurrent exception changes. Exception storage and scope are confirmed: encrypted entry metadata synchronized with its vault, applying equally to shared-vault participants. Per-entry exceptions for specific weak-password and reused-password warnings are confirmed, including intentional reuse; ignored findings remain reviewable and reversible, and password changes trigger fresh assessment.

### 28. Check passwords against known leaks

**Description:** As a user, I want to know whether a saved password appears in a known leaked-password dataset so that I can replace it. Email-address/account breach monitoring and paid monitoring subscriptions are excluded.

**Acceptance criteria:**

- I can enable known leaked-password checks. The application does not query breach services using my email addresses or account identifiers.
- Known leaked-password checks use Have I Been Pwned’s Pwned Passwords service and remain off until I enable them.
- I can start an enabled leaked-password check with a Check now action. I can also enable an optional schedule and choose its frequency in Settings.
- Checks run only when online and the relevant vault is unlocked. Checks that are due while offline or locked wait until those conditions are met.
- PWDTWO sends only a short hash prefix and compares the returned candidates locally; it does not send the password or complete password hash. These checks require no PWDTWO backend or HIBP API subscription.
- Before enabling checks, the application explains that HIBP receives the hash prefix and network request, including the requesting IP address.
- Findings identify the affected saved entries, the leaked-password match, its data source, and when the check completed. A password match does not identify a particular account breach.
- I can open the relevant saved entry and record that I have addressed a finding.
- The application shows when checks last completed and when results are stale or unavailable.
- Offline use preserves previous results without presenting them as a new check.
- Notifications and explanations distinguish reported exposure from an assertion that an account has definitely been taken over.

**Details remaining:** Define supported schedule choices and notification grouping/deduplication. Newly detected leaked passwords can trigger the user-configurable notification category described in Common behavior. Check consent, scheduling, and notification preferences remain local to each device. Manual Check now and an optional user-configured schedule are confirmed; execution waits for connectivity and an unlocked vault. Notification content privacy is settled: generic system messages with details available after unlocking. Free HIBP Pwned Passwords with opt-in hash-prefix lookups is confirmed. The user excluded email-address/account breach monitoring on 2026-10-09 because it would require a paid subscription; do not request an API key or introduce that subscription flow.

### 29. Organize entries with favorites, folders, and tags

**Description:** As a user, I want ways to organize my entries so that I can quickly find related or frequently used information.

**Acceptance criteria:**

- I can mark and unmark favorites and open a favorites view.
- I can create, rename, and remove folders and tags and assign entries to them.
- Folders can be nested within a vault. Each entry belongs to one folder and can have multiple tags.
- I can filter entries using their tags independently of their folder location.
- I can browse or filter entries by their organization as well as search for them.
- Before deleting a folder, PWDTWO warns that the folder, all its subfolders, and all their contents will be deleted, and requires explicit confirmation. Cancelling leaves them unchanged.
- Confirmed folder deletion moves the complete folder subtree and its entries to Trash, following the existing retention policy. Contents are not moved up to the parent folder.
- Restoring a deleted folder restores the complete retained folder tree, entries, attachments, and history to its original location. If its parent folder no longer exists, restoration uses the vault’s top level.
- If a folder with the same name already exists at that destination, restore a separate folder labelled Name (restored), disambiguating further if needed. Do not merge into or overwrite existing folders or entries.
- Removing a tag does not delete the entries carrying that tag.
- Organization is available offline for local entries and synchronizes across my devices.

**Details remaining:** Define reconciliation of concurrent folder/tag edits and robust identity handling during folder restoration. Folder restoration behavior is settled: restore the full retained tree at its original location or at the vault root if the parent is missing, and use a distinct restored folder on a name collision without merging or overwriting. Nested folders within each vault, one folder per entry, and multiple tags per entry are confirmed. Folder deletion is recursive after an explicit warning and confirmation, with the deleted subtree and contents retained in Trash until it is emptied.

### 30. Store secure notes and custom fields

**Description:** As a user, I want to store notes and additional account details so that information such as account numbers, security-question answers, and recovery codes stays with the relevant entry.

**Acceptance criteria:**

- I can create and edit standalone secure notes.
- Standalone secure notes and entry notes use plain multiline text, supporting paragraph breaks and clickable web links; rich-text formatting is not required.
- I can store secure notes in any vault I am authorized to edit.
- I can attach notes and named custom fields to supported entries.
- Every password and credit-card entry includes the dedicated long-text notes field in story 43 without requiring me to create a custom field.
- Sensitive field values follow the configurable masking behavior in story 16 and can be revealed or copied after unlocking.
- Notes and supported custom fields are retained during synchronization, encrypted backup, and compatible import/export.
- The application reports fields that a selected migration format cannot represent.
- Locally available notes and fields can be viewed and edited offline.

### 31. PWDTWO-managed new-device verification — removed from scope

**Status:** Removed by user agreement. There is no separate PWDTWO account, application-managed MFA enrollment, or approval from another PWDTWO device. New-device setup uses any required cloud-provider authorization followed by the vault password or recovery flow, with optional local biometric setup. Provider MFA and device controls remain provider responsibilities. Story 22 defines the accepted setup flow; the number is retained for traceability.

### 32. Lock manually and change the master password

**Description:** As a user, I want direct control over locking and my master password so that I can secure my vault whenever needed.

**Acceptance criteria:**

- I can manually lock PWDTWO, locking all open vaults together on the current device.
- Manual locking restricts access through the application and its autofill integrations until successful unlocking.
- To change a selected vault’s password normally, I must enter its current password, even if the vault is already unlocked or was unlocked with biometrics. Successful authentication lets me change that password without losing entries or changing other vaults’ passwords.
- If I have forgotten the current password, I use the recovery-key process described in story 10.
- An ordinary vault-password change preserves that vault's existing recovery key. Forgotten-password recovery instead replaces both the password and recovery key, as specified in story 10.
- After another device learns of a password change or recovery through synchronization, it requires the new vault password before reopening the affected vault, including through autofill. Existing biometric access does not bypass this required password entry.
- The device preserves unsynchronized edits for reconciliation after successful unlocking instead of discarding or uploading them over the changed vault.
- Offline devices continue using their existing local copy until reconnection. This applies equally to other people using a shared vault.
- The application explains these effects on other devices and participants.

**Details remaining:** Define safe credential-change detection and reconciliation, and biometric reconfiguration after entering the new password. Entering the current vault password is required to initiate an ordinary password change, including from an unlocked session. Preserving the recovery key on an ordinary password change and requiring the new password on other devices after they learn of the change are confirmed.

### 33. Autofill in Mac applications

**Description:** As a user, I want to use saved credentials in compatible Mac applications so that I can sign in outside the browser without manually copying passwords.

**Acceptance criteria:**

- I can invoke autofill from a compatible macOS application.
- I can identify and choose the saved account I intend to use.
- The integration fills supported username and password fields after the required unlocking and selection.
- If the application or fields cannot be filled, I can use manual copy instead.
- Locally available credentials remain usable through supported Mac autofill while offline.

**Clarification needed:** Define supported application types, invocation controls, and any device permissions needed.

### 34. Generate memorable passphrases

**Description:** As a user, I want generated multiword passphrases so that I can choose credentials that are easier to type or remember when needed.

**Acceptance criteria:**

- I can choose passphrase generation alongside character-based password generation.
- I can set the number of words and choose from the supported separator options.
- The application generates a random sequence of words using the selected settings.
- English words are supported. I can generate concatenated, capitalized words with an added randomly generated number and special character, in the style of KitchenWinSaw42#; the example is illustrative, not a reusable credential or a confirmed three-word default.
- Word selection, the number, and the special character are generated locally using cryptographically secure randomness.
- Passphrase mode defaults to six independently random English words, capitalized and joined without separators, followed by a random number and special character. The word count remains adjustable.
- I can copy the result or save it as an entry's password.
- Passphrase generation works offline and participates in the protected generator history.

**Details remaining:** Define word-count limits, optional separator choices, capitalization controls, number range, and symbol choices. The default is confirmed: six random English words, capitalized and joined without separators, plus a random number and special character. Additional languages are not yet specified.

### 35. Share entries and vaults with other people

**Description:** As a user, I want to share selected entries or a shared vault so that family members or other people I choose can use the appropriate credentials.

**Acceptance criteria:**

- I can send a selected entry as an independent copy or invite selected people to an ongoing shared vault.
- An individually shared entry is a snapshot of the content I confirm when sharing. Later changes by either person do not update the other person's copy.
- The recipient can save the received copy into a vault they control; it has no ongoing link to my source entry.
- Ongoing synchronization between people is provided through shared vaults, not individually shared entries.
- Both sender and recipient must have PWDTWO available; sharing is supported only between compatible application versions. There is no browser-only reader for shared secrets.
- Sharing identifies the selected source vault and authorized content; it does not silently distribute unrelated vaults.
- Supported passkeys can be shared through a shared vault or as individual encrypted copies, following story 25 and the existing recipient-compatibility and transfer-protection requirements.
- My personal entries remain private unless I explicitly share them.
- Shared-vault participants have equal access to the vault contents: they can read, add, edit, delete, copy, and export entries. PWDTWO has no owner/editor/viewer roles or per-entry permissions inside a shared vault.
- Every participant receives the shared vault’s password and recovery key, consistent with equal access. Each participant can use that key to recover the shared vault if they forget its password.
- Shared-vault recovery follows the agreed lifecycle: replace the password and recovery key, and make the replacement credentials available to participants through the agreed secure-sharing flow. The delivery mechanism remains to be designed.
- Changes synchronize between participants with write access to the shared cloud file. The intended collaborative setup grants each participant write access.
- Cloud-file access, sharing administration, and deletion of the cloud file follow the storage provider's permissions. Equal access to vault contents does not imply identical cloud-account ownership or file-management rights.
- Where the provider permits me to manage file sharing, I can remove someone's future access through that provider. This cannot revoke their downloaded vault copies or known secrets. Individual shares are encrypted copies without an application-enforced collection deadline or remote revocation, as specified in story 36.
- The interface explains that removing access cannot erase information or offline copies already retained by a recipient.

**Technical details remaining:** Define provider invitation and file-opening flows, secure delivery and redistribution of shared vault passwords and recovery keys, implementation of the agreed concurrent-password-change resolution, and supported item types. An application-managed role system is excluded; cloud-provider permissions remain authoritative for remote file operations.

### 36. Send an encrypted copy of an item

**Description:** As a user, I want to send an encrypted copy of a selected item so that another PWDTWO user can import it into their own vault.

**Decision:** Replaces the earlier expiring-link requirement by user agreement. There is no collection deadline, expiration, or remote revocation feature for individual shares.

**Acceptance criteria:**

- After unlocking, I can select a shareable item and review the exact content included before creating an encrypted copy for transfer.
- An individually shared copy contains current fields only, excluding previous passwords and entry history.
- In the sharing preview, I choose whether to include notes and attachments; only the chosen content is included.
- Both sender and recipient must have compatible PWDTWO applications. Shared secrets are not exposed through a browser-only reader.
- Only the selected content is included; sharing does not disclose the source vault's password, recovery key, or unrelated entries.
- PWDTWO protects each transfer with a newly generated strong random transfer password, independent of both people's vault passwords and recovery keys.
- I send the encrypted file and communicate its transfer password separately. PWDTWO must not automatically bundle the password with the file.
- The recipient opens the file in PWDTWO, enters its transfer password, and chooses a destination vault before importing the received item.
- The interface explains that anyone possessing both the file and transfer password can open that copy. The transfer password is neither expiring nor restricted to a single use.
- An imported item is an independent copy. Later edits or deletion on either side do not affect the other copy.
- The application does not promise a collection deadline, expiry, remote deletion, or revocation of the transferred copy.
- Ongoing synchronization is provided through shared vaults rather than individual shares.

**Technical details remaining:** Define the encrypted transfer format, maintained cryptographic implementation, transfer-password representation, supported transport options, and eligible item types. Separate delivery of the generated transfer password is confirmed. Possession of that password is the decryption authorization; it does not independently authenticate a named recipient or sender.

### 37. Trusted-contact emergency access — removed from scope

**Status:** Removed by the user on 2026-10-08. PWDTWO will not nominate emergency contacts or grant delayed access when the owner cannot respond. Owner recovery remains in story 10; deliberate sharing remains in stories 35–36. This number is retained for traceability, with no implementation work required for the withdrawn feature.

### 38. Store and fill payment cards and identity information

**Description:** As a user, I want to store payment cards and identity or address details so that I can reuse them in compatible forms.

**Acceptance criteria:**

- I can create, edit, and organize payment-card and identity/address records.
- Identity/address records support a record label (such as Home or Work), full name, company, email address, phone number, date of birth, street address, city, state or region, postal code, country, and long-text notes.
- All identity/address fields are optional, and I can save multiple records and select the intended one when filling a compatible form.
- I can store credit cards in any vault I am authorized to edit.
- Credit-card records support a card name or label, cardholder name, card number, expiration month and year, security code (CVV/CVC), billing address, and long-text notes.
- All credit-card fields are optional. I can save incomplete details or omit the security code; the application does not require a complete card to save the record.
- Every credit card includes the dedicated long-text notes field in story 43.
- Card numbers and security codes follow the configurable masking behavior in story 16: masked by default, with full values directly visible in unlocked entries when masking is disabled.
- After unlocking, I can inspect or copy supported fields.
- In compatible forms, I select a card or identity/address record, review the destination website or app and which fields will be filled, and explicitly confirm Fill before PWDTWO releases those values.
- PWDTWO leaves submission of payment and identity forms, including completing a payment, to me. The configurable auto-submit option applies only to supported login forms.
- Private records follow the same access, synchronization, and backup rules as other vault entries.
- Locally available records remain accessible offline.

**Details remaining:** Validate supported autofill surfaces and how each platform provides destination and field information before filling. Confirmation is settled: show the destination and fields, require explicit Fill confirmation, and leave payment and identity form submission to the user. Credit-card and identity/address field coverage is confirmed, with all fields optional and multiple selectable identity/address records supported.

### 39. Store documents and attachments

**Description:** As a user, I want to keep documents and attachments in the vault so that supporting information is available alongside my saved records.

**Acceptance criteria:**

- I can add a document as a vault item or attach a file to a supported entry.
- Attachments may use any file type, subject to the supported storage limits.
- The maximum size per attachment defaults to 1 MB and can be changed in Settings.
- Before adding a file that exceeds the configured limit, the application explains the limit and lets me change the setting or choose another file; it does not silently truncate the file.
- Lowering this limit does not delete or truncate attachments already stored in the vault.
- PDFs, images, and plain-text files have native in-app previews. Other file formats can be exported and opened in an application I choose.
- After unlocking, I can preview supported file types or export a file to a location I choose.
- Documents and attachments are embedded in the encrypted vault file. Once that vault has been downloaded or imported, all its attachments are available offline on that device.
- Opening a cloud vault on a new device requires obtaining a complete local copy; there is no separate on-demand attachment download mode.
- Files synchronize only to devices and recipients authorized to access them.
- Backup and export previews state whether attachments are included, and results identify any omitted files.
- Deleting a file follows the applicable entry-deletion and retention rules.

**Details remaining:** Validate the supported configurable attachment-size range and total-vault capacity, and define exact image/text-format coverage and preview resource limits. Replaced or removed attachments remain in entry history until that history is explicitly cleared, following story 18. The attachment-size limit is a per-vault setting that synchronizes with the vault. The default per-attachment size limit is confirmed as 1 MB, adjustable in Settings. Any attachment file type is allowed; native previews for PDFs, images, and plain text are confirmed, with other formats exported to a user-chosen application. Embedded storage and complete local availability are confirmed.

### 40. Manage multiple independently protected vaults

**Description:** As a user, I want multiple vaults with separate passwords so that I can keep different collections of credentials and sensitive information independently protected.

**Acceptance criteria:**

- I can create, name, open, select, and close multiple vaults on supported devices.
- For a synchronized vault, Remove from this device removes its local copy and saved unlock information without deleting the cloud file or changing other devices’ copies.
- Delete cloud vault is a separate action that identifies and deletes the provider’s vault file only after explicit confirmation, subject to provider permissions. It does not claim to remotely erase previously downloaded copies.
- The cloud-vault deletion dialog keeps the application-managed backup by default and offers an unchecked Also delete the backup option. Its confirmation identifies whether that backup will be retained or deleted.
- Deleting the cloud vault stops its scheduled backups, regardless of whether the existing backup is kept. Manually exported files remain untouched.
- When another device discovers that the cloud vault was deleted, it preserves its local copy and pending changes, stops synchronization, and offers Keep as a local-only vault or Remove from this device.
- PWDTWO does not automatically recreate the deleted cloud file. The user can explicitly enable cloud synchronization again later through the existing storage-migration flow.
- Before removing local data, PWDTWO identifies unsynchronized changes and requires an explicit decision so those changes are not silently lost.
- Every vault has its own password; creating or changing one vault's password does not change another's.
- Vault access works offline when the necessary files and unlocking material are available locally. Open vaults share an application-wide session and lock together; each vault retains its own password and recovery protection.
- Each entry belongs to an identifiable vault, and I select the destination vault when saving new content.
- Each vault can contain supported record types, including password entries, credit cards, and secure notes.
- Locked vault contents are excluded from search results, autofill suggestions, and content previews until that vault is unlocked.
- Combined search covers all unlocked vaults, labels each result with its source vault, and lets me filter to one vault.
- An All unlocked vaults view also supports browsing logins, cards, secure notes, and other supported item types. Each item identifies its source vault, and I can filter the view to one vault.
- Creating an item from the combined view still requires choosing its destination vault. When a vault locks, its items are removed from the combined view.
- Recovery and optional biometric access are configured with an explicit vault scope.
- I can copy or move an entry between vaults when both source and destination vaults are unlocked.
- Copy creates an independent destination entry, preserving its supported contents, notes, attachments, and entry history. Later edits to one copy do not update the other.
- Move first saves the complete entry successfully in the destination, then moves the source entry to the source vault’s trash. A failed destination save does not remove the source entry.

**Details remaining:** Validate shared-session reopening across native integrations according to story 9; its user-facing behavior is confirmed. Combined browsing across supported item types is confirmed, with source-vault labels, a single-vault filter, and explicit destination selection for creation. All open vaults share one application-wide inactivity timer, including activity in combined browsing and search. Moving and copying between unlocked vaults, with notes, attachments, and history preserved, are confirmed. Combined search across unlocked vaults with source labels and an optional single-vault filter is confirmed.

### 41. Synchronize vault files through iCloud Drive and Google Drive

**Description:** As a user, I want my encrypted vault files synchronized through iCloud Drive or Google Drive so that I can use my chosen storage service and access the same vault from my devices.

**Acceptance criteria:**

- On macOS, iPhone, and iPad, I can create or select a vault file in iCloud Drive and synchronize it between my Apple devices.
- On macOS, iPhone, iPad, and Android, I can create or select a vault file in Google Drive and synchronize it between these devices.
- I can choose the storage location independently for each vault.
- Each synchronized vault uses one cloud provider at a time; different vaults can use different providers. The same vault does not synchronize simultaneously through both iCloud Drive and Google Drive.
- Provider authorization and vault unlocking are separate steps.
- Changes to a vault file synchronize automatically through its configured provider when connectivity and platform execution allow.
- Encrypted vault updates can be transferred while the vault is locked, subject to provider authorization and platform execution limits.
- Operations requiring decrypted contents, including merging changes, wait until the required vault revisions are unlocked. Preserve the relevant encrypted versions and pending local changes meanwhile.
- Locally available vaults remain usable offline, and pending updates are preserved until synchronization can resume.
- Concurrent file updates are preserved for reconciliation; a conflicting remote copy does not silently replace unsynchronized local work.
- Entry-level conflicts follow story 12 after the necessary vaults/copies can be unlocked.
- If reconciling a conflict requires unlocking a vault, the application shows that action as pending and preserves both copies until it can proceed.
- The application shows each vault's provider, last successful sync, pending changes, and actionable failures.
- Google Drive provides the route for the same vault to synchronize across Apple and Android devices; iCloud Drive integration on Android is outside the required scope.
- Unavailable provider integrations are explained rather than presented as working synchronization.

**Storage changes:** Migration between local-only storage and cloud providers is covered by story 46.

**Details remaining:** Define provider concurrency handling and platform background-execution mechanisms. Locked-vault encrypted transfer is confirmed; content-dependent merging waits for unlocking and preserves competing versions. Selecting a cloud provider does not yet finalize a vault-file format.

### 42. Prefer portable KeePass-compatible vault files where feasible

**Description:** As a user, I want vault files in KeePass-compatible format if the format does not impose major limitations on the agreed features so that I retain portable, independently usable vault data.

**Decision status:** Conditional preference. “KeyPass” is interpreted as KeePass and its KDBX database format. The user confirmed on 2026-10-08 that vaults are mainly for PWDTWO and full compatibility with other KeePass solutions is unnecessary. PWDTWO-specific extensions are acceptable; final format selection still depends on feasibility and recovery assessment.

**Acceptance criteria if adopted:**

- Vaults use a documented supported KDBX format with documented PWDTWO extensions. PWDTWO is the primary application; any external-client access guarantees are explicitly scoped and tested.
- Core entries, multiline notes, groups, history, attachments, and PWDTWO-specific metadata survive supported PWDTWO open/edit/save round trips without silent loss. Full editing compatibility with other KeePass applications is not required.
- The application states which advanced features depend on this application or extensions and may not work in another KDBX-compatible client.
- Unsupported content or fields are identified before an operation controlled by this application that could discard or change them; guarantees about other clients are limited to the agreed and tested compatibility scope.
- Interoperability is assessed against per-vault recovery, passkeys, authenticator codes, synchronization conflicts, sharing, and local unlocking protections.
- Major limitations remain explicit decisions; choosing KDBX must not silently remove previously accepted features.

**Technical assessment remaining:** Complete the format and recovery design, select the supported KDBX version if adopted, and document the limited external compatibility we can validate. Full external compatibility is not a blocker; limitations affecting accepted PWDTWO features still require a decision.

### 43. Add long notes to every password and credit card

**Description:** As a user, I want a dedicated long-text notes field on every password entry and credit card so that I can keep detailed supporting information with that record.

**Acceptance criteria:**

- Every password entry and every credit-card record includes an optional dedicated notes field.
- The field accepts multiline text, including paragraph breaks, and is not limited to a short single-line description.
- I can add, view, and edit these notes within the unlocked vault, including offline.
- Notes are saved with the entry and follow its synchronization, conflict, history, access, and backup behavior.
- Supported imports and exports preserve the notes; unsupported formats disclose any omission.
- The application does not silently truncate text; any enforced size limit is explained before saving.

**Details remaining:** Define text-size limits. Plain multiline text with paragraph breaks and clickable web links is confirmed; rich-text formatting is not required. Note contents participate in ordinary search within unlocked vaults, as confirmed in story 2.

### 44. Update the Mac application from within PWDTWO

**Description:** As a Mac user, I want a built-in updater so that I can update PWDTWO without manually downloading and replacing the application.

**Acceptance criteria:**

- I can check for a newer compatible PWDTWO release from the Mac application.
- The Mac application checks automatically every 24 hours when connectivity and application execution permit, and informs me when a compatible update is available. I can disable automatic checks in Settings; manual Check for updates remains available.
- Each update requires my explicit approval before installation; it is not installed silently.
- I can decline or postpone installation and continue using the current version.
- The updater can download and install a verified release and relaunch the application when needed.
- Invalid or untrusted update packages are rejected.
- Updating preserves existing vault files, pending local changes, and settings; any required data migration must preserve recoverability.
- Being offline or having an update check fail does not prevent normal offline vault use.
- The Mac updater uses the same technology as MD22: Sparkle, as documented in architecture requirement 24.
- iPhone/iPad and Android application updates use their selected store distribution channels.

**Confirmed policy:** Automatic checks use a 24-hour interval, matching the inspected MD22 configuration, and can be disabled in Settings. Manual checks remain available. Each installation requires explicit user approval.

### 45. Keep a vault local without cloud synchronization

**Description:** As a user, I want local-only vaults so that I can store credentials on a device without connecting that vault to a cloud provider.

**Acceptance criteria:**

- I can create and use a local-only vault on macOS, iPhone, iPad, and Android without signing in to iCloud Drive or Google Drive.
- A local-only vault uses its own password and the same vault protection, optional biometrics, and recovery capabilities as other vaults.
- I can use the supported local operations, including search, entry creation and editing, password generation, and autofill.
- Local changes survive application restarts and do not upload when connectivity returns.
- Local-only vaults can coexist with cloud-enabled vaults on the same device.
- The application clearly identifies the vault as local-only.
- Local-only vaults are excluded from automatic operating-system cloud backups. Cloud transfer of such a vault requires an explicit backup/export choice or a deliberate change of storage mode.
- I can use the supported export and encrypted-backup operations without enabling automatic synchronization.
- Closing a local-only vault preserves its file. Deleting it is a separate action that requires explicit confirmation explaining that this may be the only copy.
- Confirmed deletion removes the local-only vault file and its saved unlock information. Its backup is retained unless I explicitly select Also delete the backup; manually exported files remain untouched.
- Deleting the whole vault cannot be undone through that vault’s internal Trash; recovery requires an independently available backup or copy.

**Storage changes:** Migration between local-only and cloud-enabled storage is covered by story 46.

**Confirmed policy:** Exclude local-only vaults from automatic operating-system cloud backups. Validate the platform-specific exclusion mechanisms and their scope during implementation. Explicit user-selected backups and exports remain available.

### 46. Change an existing vault's storage mode or cloud provider

**Description:** As a user, I want to move an existing vault between local-only storage, iCloud Drive, and Google Drive so that I can change where it is stored without rebuilding the vault.

**Acceptance criteria:**

- I can move a local-only vault to a cloud provider supported on the device.
- I can move a cloud-enabled vault to local-only storage.
- On a supported Apple device, I can move a vault between iCloud Drive and Google Drive in either direction.
- Migration preserves the vault's supported records, notes, attachments, history, unresolved changes, password, and recovery capability.
- The application obtains any necessary destination-provider authorization and verifies the destination copy before completing the switch.
- A vault has only one active synchronization provider after migration, or none when changed to local-only storage.
- A failed or interrupted migration does not silently discard the source vault or pending changes; the application provides a recoverable result.
- Changing a vault to local-only storage stops cloud synchronization on the migrating device after required content has been saved locally.
- The application distinguishes completion on this device from reconnection of other devices, preserving their pending changes for reconciliation.
- After verifying the destination and switching storage, the application automatically deletes the old cloud copy rather than retaining it as a backup.
- The old cloud copy is not deleted before destination verification; newer source changes must be preserved and reconciled before deletion.
- If deleting the old cloud copy fails or is interrupted, the destination remains usable and cleanup is shown as pending with a retry path.
- Deletion of the old cloud copy is not presented as deletion of offline or independently retained copies.

**Clarification needed:** Define how other devices learn about and reconnect after a move, and how concurrent migrations and late-arriving edits are resolved. Deletion of the old cloud copy after verified migration is confirmed.

### 47. Share on-device diagnostics in a bug report

**Description:** As a user, I want diagnostics kept on my device with a way to share a report with the PWDTWO maintainer so that I can report problems without automatic telemetry uploads.

**Acceptance criteria:**

- On all four platforms, PWDTWO keeps its diagnostic records on the device and does not automatically upload analytics or crash reports.
- I can generate a diagnostic report locally, including while offline.
- The report contains useful technical information such as application/build version, OS version, and sanitized error details.
- Reports exclude vault contents, passwords, recovery keys, tokens, other secrets, and identifying vault/account data. They do not automatically attach vault files, screenshots, or raw memory dumps.
- I can preview the report and omit optional sections before sharing it.
- I can save the report or explicitly share it with 66IDEAS, for example as an attachment to a bug report. Sharing requires connectivity only when the selected destination requires it.
- Bug reports use GitHub Issues in the planned public 66IDEAS/PWDTWO repository. I can manually attach a diagnostic report after reviewing it.
- Generating a report does not itself send it or publish an issue.
- Sanitized diagnostic logs are retained for up to seven days and capped at 10 MB per device. Older logs are removed automatically to enforce the limits.
- I can clear the application’s local diagnostic logs immediately in Settings.
- Diagnostics are not included in normal vault synchronization.

**Details remaining:** Define report packaging. Diagnostic-log retention is confirmed at seven days and 10 MB per device, with automatic removal of older logs and manual clearing in Settings. GitHub Issues in the planned public 66IDEAS/PWDTWO repository is the selected bug-report destination.

## Open functional details

- Importing other password managers’ export files is macOS-only. Duplicate handling is settled in story 13; precise matching rules remain implementation work.
- What length range should the password generator offer? Its character-based default is 24 characters with uppercase, lowercase, numbers, and symbols enabled. Passphrase controls and defaults are tracked in story 34.
- Inactivity locking defaults to five minutes and is configurable separately on each device. All open vaults share one application-wide inactivity timer using the device’s configured timeout; supported timeout choices and native integration coordination remain implementation details. Only PWDTWO interaction or deliberate autofill use resets the timer.
- Periodic vault-password re-entry with biometrics is disabled by default and uses a user-selected interval when enabled; supported interval choices remain to be defined. The preference is local to each device. Required new-password entry after learning of a synchronized password change or recovery remains independent of this setting.
- Recovery replaces the password and recovery key; normal password changes preserve the recovery key. Other devices require the new password after learning of the change through synchronization and preserve pending edits; the detection and reconciliation protocol remains technical design work. Separate PWDTWO new-device approval is excluded.
- New-device setup uses provider authorization and vault credentials, without a separate PWDTWO account or approval flow; story 31 is withdrawn.
- Retention periods, export/backup coverage, provider sharing integration, and other feature-specific details are recorded with their stories.
- The approved release sequence and phase grouping are maintained in [tasks.md](tasks.md#approved-development-phases); technical questions still require their recorded validation gates.
- The KDBX preference and cloud-file synchronization must be reconciled with recovery, encrypted copy transfer, shared-vault editing, and offline synchronization. PWDTWO-managed device approval and remote revocation are excluded.

### 48. Reuse recent authorization and biometrics in iPhone AutoFill

**Description:** As a user, I want to reuse a recent app unlock briefly and use Face ID / Touch ID in the password chooser so that I do not type vault passwords for every fill.

**Acceptance criteria:**

- Five-minute initial recent-unlock duration; Never/1/5/15-minute choices in iPhone Settings. Automatic reuse does not extend expiry.
- App/background hiding does not discard an otherwise valid bounded AutoFill grant. Explicit locking, disabling or changed included ciphertext retires prior authority; automatic refresh may rebind an already authorized app session without sliding its original deadline.
- Recent authorization is device-local and passcode-bound in shared Keychain storage. The extension can use the app's shared biometric enrollment after expiration, with vault-password fallback and no device PIN authentication path.
- All included vaults authenticate before any login appears. Cancellation and stale/changed request checks prevent late publication or filling. Filling still requires the chosen login and deliberate mismatched-site confirmation.
