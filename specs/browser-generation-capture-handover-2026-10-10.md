# Chrome generation and save/update — 2026-10-10

The signed macOS application and installed unpacked Chrome extension now include version **0.3.0**. Native generation/persistence and mocked browser/control checks pass. Chrome's installed extension details show 0.3.0 and the user's existing **On all sites** setting; the agent granted no broader permissions. The normal app was relaunched. On 2026-10-11 the user confirmed creating a new password in the browser, successful autofill and a new entry appearing in the native app. This is user-reported installed verification, not an agent-operated credential ceremony. History recovery, selected-account update, dismissal, post-submit prompts and specific passphrase/confirmation-field behavior still need manual verification. Earlier user confirmation covers 0.2.0 automatic chooser/fill.

## Using the new features

Reload existing login/registration pages after the extension update. Keep PWDTWO running and unlocked, and finish any active native edit before a browser write.

- Focus a supported password field, choose **Generate a password…**, select the history vault and either a random password or English passphrase, then **Generate & fill**. Random passwords default to 24 characters with all four character categories enabled. Passphrases default to six English words with a number and special character; word count and separator are adjustable. Native Rust generation supplies the values. A successful encrypted history write must finish before any value is released to the bound page. The chooser receives no generated password. Generation neither saves a login nor submits/changes the website account.
- Choose **Save or update this login…** to review credentials currently entered in a supported form. A trusted form submission after entering or generating credentials can also offer a compact review prompt, including after navigation within the exact same HTTPS origin. The prompt shows the website and username; its password stays hidden. Choose **New login** and a destination vault, or a matching existing account to update. A single matching username defaults to that account; multiple accounts remain selectable.
- **Save Login** or **Update Login** is the explicit commit. Success is reported only after native encrypted publication. Updates stay in the selected entry's vault and retain notes, attachments, other fields and prior credential history. **Not Now** before committing makes no vault change. Submitting unchanged credentials already in an available vault does not solicit another automatic save.
- Registration confirmation fields and current/new/confirmation password-change forms are supported when their roles can be determined safely. Generation fills the new password targets, leaving the current password and username intact. Unlabelled ambiguous forms fail closed. An intervening target replacement, edited value, lock/session change or navigation prevents generated filling; a value already retained remains recoverable from native Generator History.

## Capture and operation boundaries

Pending captured credentials live only in native memory for at most three minutes, bound to the unlocked vault session and exact origin. Chrome retains only an opaque ticket in worker memory, with no credential storage in Chrome local/session storage. Capture metadata is delivered only to the bound extension-owned frame; credentials are not exposed to chooser HTML or page messages. Browser sender, extension-frame document, URL, owner and single-use grant validation remain enforced. Lock, app exit and expiry discard pending captures; worker restart can lose the prompt ticket. A review grant lasts at most 90 seconds and an outstanding native mutation at most two minutes. The source document is bound at capture; same-origin navigation can open a fresh explicit review, which binds its own destination document.

Transient capture is not proof that the website accepted a sign-in or password change. Saving remains a user decision. AJAX flows that do not emit a supported submit event can use the explicit Save/update control. Third-party iframe forms, advanced staged account continuity, broader form compatibility and Safari equivalents remain open. No new auto-submit behavior or approved-site persistence was added.

## Verification

- 71 freshly compiled model checks pass, including publication-before-visible-mutation, failed saves and late completion after locking.
- Native catalog/broker regressions and new mutation checks pass. The new checks cover metadata-only capture, cross-origin/replay/dismissal refusal, failure without publication, unchanged-submit suppression, retained prior passwords, generation release after history publication and locking during an operation.
- The new real-vault harness creates a private fictional KDBX, saves a new login, updates another while retaining notes/attachments/history, generates through the shared Rust engine, and reopens it through a fresh controller. Passwords, passphrases and their retained history persist; the checked files contain no corresponding plaintext values. Temporary harness files are removed by the harness.
- Mocked browser/DOM/control tests cover target roles and confirmation mismatch, same-origin submitted capture tickets across navigation, selected generated-secret release directly to the bound document, changed-value/target/navigation refusal, explicit vault/account choices, invalid generator controls, Not Now without saving and clearing private metadata on lock/page exit.
- Cloud regression checks pass. Complete app, native host and Safari/system extensions compile; strict signing, required App Group/sandbox/autofill entitlements and exact packaged browser-resource comparison pass. The bundled manifest differs from source only by the builder's explicit icon declarations.

[Current source/signing/test evidence](../dev/experiments/foundation/results/macos-browser-generation-capture-summary.json) and [installed Chrome version](../dev/experiments/foundation/results/browser-generation-capture-2026-10-10/installed-chrome-0.3.0.png).

No user vault password was entered, website credential changed, browser login submitted, or real login saved/updated by the agent. Native app relaunch and extension reload do not verify the new installed UI flow. Parent production tasks remain open.

Primary API references: [Chrome native messaging](https://developer.chrome.com/docs/extensions/develop/concepts/native-messaging) and [tab lifecycle/message APIs](https://developer.chrome.com/docs/extensions/reference/api/tabs).

## User verification — 2026-10-11

The user reported: “It works fine. I create a new password in the browser. It is autofilled, and a new entry is created in the application.” This records the observed outcome without inferring which save control or submission route was used. Generation continues to retain encrypted history before fill; saving a login remains an explicit user decision.
