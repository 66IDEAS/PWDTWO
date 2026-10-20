# Mac integration checks — 0.4.0

This signed development build adds entry-conflict choices, independent vault-settings/history merging, interrupted-merge upload recovery and device-local optional login submission. Provider revision reads/writes run off the native UI thread. Known iCloud files that are not current request download before reconciliation. Automated checks use fictional files; real cloud delivery and installed credential ceremonies remain separate acceptance gates. Safari's unlocked catalog was visually verified in 0.3.3.

Quit and reopen PWDTWO to load the new native executable. The new package is built and signed, but the existing 0.3.4 process was left running because native UI automation timed out and could not check pending edits. Reload the PWDTWO extension manually in Chrome's extension manager, then reload disposable test pages. Safari/system bundles are registered at 0.4.0; registration does not enable new permissions or prove installed filling.

## Safari: short hands-on check

Keep PWDTWO running and open its vaults. Reload a disposable login page after the extension update, unless it currently contains information you want to keep. Use a fictional test entry whose website exactly matches the HTTPS page; do not submit the site's login form.

1. Focus the username or password field. Select the saved test login from PWDTWO. Check that the relevant fields fill and the chooser does not show Unlock while the app is unlocked.
2. Use **Generate a password… → Generate & fill**, then **Save or update this login…** to explicitly save a fictional new entry. Repeat with another generated value and choose the existing entry under **Save as** to update it. Check the entry's **Entry History** and the app's **File → Generator History…**; existing notes and attachments should remain.
3. Open another save review and choose **Not Now**; no new/updated login should be saved. The generated value should still be in Generator History. Lock PWDTWO, refocus the field and check the locked message, then unlock through the app and refocus. Return to matching suggestions without a stale connection message.

Generation changes the test form and vault history; it does not change the website account. Save/update changes only the chosen PWDTWO vault after your explicit confirmation. The user performs credential entry, generation/fill and saving. No site login/account-change submission is needed for this check. Same-site post-submit prompts, passphrases, confirmation fields and the broader form/version matrix need their own checks.

## Cloud: two Macs, one disposable vault

Use two Apple Silicon Macs running macOS 26 or 27. This is an Apple Development build, not a notarized release. Before using the copied package on the second Mac, run its read-only preflight:

```sh
python3 dev/macos-preview/verify_autofill_package.py '/absolute/path/PWDTWO Local Vault.app'
```

The script checks nested signing, existing capabilities, the exact signed server identity proof, supported OS/architecture and whether the development profiles authorize that Mac. It does not read vaults, change settings or print device identifiers. If the second Mac is not authorized, build/provision for that Mac with Xcode first. Do not bypass macOS security warnings. Use the same candidate version on both devices.

1. On Mac A create a disposable vault containing two fictional logins. Connect it through **File → Cloud Sync… → Connect Provider Folder…**, choosing a new dedicated folder managed by the selected provider. Use **Sync Now**. Choose either iCloud Drive or Google Drive for Desktop; one provider per vault.
2. Wait until the actual provider has made complete revision files locally available on Mac B. In **File → Cloud Sync…**, choose **Choose Existing Provider Folder…**, select an encrypted revision from that folder, and use **Add Cloud Vault** with the test vault password. This adopts the original vault identity. **Restore from Encrypted Backup** creates a separate identity and must not be used for enrollment.
3. Pause delivery/disconnect from the network on both Macs. Edit different test entries, save, quit and reopen PWDTWO. Verify each local edit survives while delivery is paused.
4. Resume delivery. Sync both Macs. If a review appears, inspect it and use **Save Reviewed Combined Version**. Wait for provider delivery and sync again. Verify both devices contain both edits. A one-sided vault rename should also reach the other Mac.
5. Repeat with different edits to the same test entry. **Keep all versions** is the default. Expand the version previews and choose **Use version …; others to Trash** to retain one active version and preserve the others in Trash. Edit/deletion conflicts also offer **Use deletion; edited versions to Trash**. Sync again without new edits while reviewing: your choices should remain. Let a third change arrive while a review is open: confirmation must refuse the stale review and ask for **Sync Now** before another review.
6. Lock Mac B before a transfer. Incoming ciphertext may stage, but current credentials remain unavailable until unlock. After unlock/sync, authenticate and reconcile the received revisions.

Judge delivery by what actually arrives on the other Mac. The application's folder reconciliation status does not acknowledge remote cloud delivery. Offline publication failure must retain local edits and retry after reconnection. A downloading message for iCloud revisions requires another **Sync Now** once files are available; the timer can stage ciphertext while locked. Retained encrypted sync revisions are separate from the single user backup. Direct Drive OAuth/mobile adapters, encryption-key rotation, incompatible settings/independent-root conflict handling, provider migration and revision compaction remain unfinished. Development limits remain 256 provider revisions/128 MiB; limits preserve files and stop reconciliation.

## Optional login submission

**Settings → Autofill & Clipboard → Submit supported login forms after autofill** starts off and stays on this device. With it off, selecting a login fills fields without submitting. After explicitly opting in, exact-site matching selection can submit a simple foreground same-origin POST login form with one username field, one password field and one visible Log In/Sign In button. Unsupported or changing forms stay manual; generation, signup/new-password forms, partial steps, other-site search and Fill once stay manual.

Test submission only on a disposable form/account you intend to submit. Automated tests use mocked forms and do not establish installed browser acceptance. Ordinary filling, generation and save/update remain separately testable with submission disabled.

## Compatible Mac applications

Open **File → Set Up Autofill… → System Autofill Settings…** and explicitly enable PWDTWO as a macOS password provider. This grants the OS integration access to credentials you subsequently select; the agent has not enabled it or changed system permissions.

In an application that invokes macOS password providers and supplies a supported HTTPS service identifier, choose PWDTWO and then **Choose in PWDTWO**. Select only a fictional matching login for this test. Check password-provider completion, **Cancel** in each chooser, return after cancellation, and retry after PWDTWO is unavailable/locked. Cancellation must retire the pending native chooser and prevent late credentials from completing a closed OS presentation.

The provider always requests user interaction. Ambiguous, missing or unsupported destinations show manual-copy guidance; no destination is guessed. Apps that do not implement the OS interface use ordinary manual copy from PWDTWO. No arbitrary application coverage or installed OS credential completion is established by the sandbox state-only check.
