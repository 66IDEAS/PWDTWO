# PWDTWO — UX Requirements

UX requirements capture is complete for the current round. Requirements 1–50 are
confirmed. The user has nothing further to add at present and wants to use the
running applications before deciding on additional UX changes. Treat these
requirements as the current baseline and refine them through hands-on feedback.

Scope: dedicated experiences for macOS, iPhone, iPad, and Android. The user reaffirmed
support for the current stable and immediately previous major OS generations; the
version matrix and rolling support policy remain in architecture requirement 18.
This document captures the resulting user experience rather than implementation.

## Confirmed direction

### 1. Feel at home on each platform

**Description:** Each application must look and behave like an application designed
for its own platform. Adapt navigation, controls, menus, typography, interaction
patterns and use of screen space to macOS, iPhone, iPad and Android. Maintain a
recognizable PWDTWO identity while giving each platform its own appropriate expression.

### 2. Adopt Liquid Glass on Apple platforms

**Description:** Liquid Glass is mandatory in the Mac, iPhone and iPad experiences
across the supported Apple OS generations. Follow Apple's intended use and native
presentation rather than applying a generic glass effect to the entire interface.
Its exact placement in individual screens will be established during UX design.

### 3. Follow established platform conventions

**Description:** Use familiar native interaction and presentation conventions as the
foundation of every screen. Distinctive PWDTWO touches must remain consistent with
the platform's usability and accessibility guidance and preserve recognizable
navigation and controls.

### 4. Make everyday use delightful

**Description:** The applications should be fun and engaging as well as practical.
Use thoughtful feedback, visual personality and pleasant everyday interactions
that suit a password manager. The eight specific touches below are accepted
requirements.

## Confirmed UX details

The following eight accepted requirements elaborate the confirmed direction. All must respect
system appearance, accessibility, motion and haptic preferences. Feedback must have
readable labels and accessible announcements; color, animation and haptics must not
be the only cues. Preserve previously agreed secret-masking, confirmation and lock
behavior. A decorative transition must never delay locking or expose a hidden value.

### 5. Give each vault a recognizable identity

**Description:** Offer a small selection of tasteful icons and accent colors for
vaults. Carry that identity consistently into vault selection, source labels and
destination selection. Retain the vault name so recognition never depends on color
alone. Use platform-appropriate symbols and accents within familiar native controls.

### 6. Make successful actions feel satisfying

**Description:** Let the Copy action briefly show a checkmark and “Copied,” give a
saved entry a restrained visual acknowledgement, and use a subtle confirmation
haptic on compatible phones where appropriate. Feedback follows the completed action
without interrupting the flow. Routine background synchronization remains quiet.
Secret contents must not appear in confirmation messages.

### 7. Make the password generator enjoyable and readable

**Description:** Present a generated passphrase with visually distinguishable word,
number and symbol segments while making the exact resulting string unambiguous.
Provide a prominent native Generate again action and a brief transition when it
changes. Keep the previous value usable until the new one is ready; avoid moving
controls or decorative delays. Apply the agreed display/masking behavior and never
insert formatting characters into the copied password unless they are part of it.

### 8. Make search and quick actions feel effortless

**Description:** Keep search easy to reach and update results promptly, with clear
vault identity and useful empty results. On Mac emphasize keyboard navigation,
standard shortcuts, hover affordances and context menus; on iPad support touch,
pointer and keyboard; on phones provide comfortable touch targets and familiar
platform actions. Important actions remain discoverable without knowing a gesture.
The Mac main-window layout and search placement follow entries 13 and 14.
iPhone search is a dedicated tab under entry 19, and Android search is a navigation
destination under entry 21. iPad search placement follows entry 23.

### 9. Give each entry type a pleasing, useful presentation

**Description:** Give logins, payment cards and secure notes distinct, restrained
visual treatments within native content surfaces. For example, show a card's label
and last four digits in a clean card summary, and give notes comfortable typography
and spacing. Keep field actions consistent. Sensitive fields follow the existing
masking preferences; decoration must not imply information is safe to reveal.

### 10. Make offline and synchronization states reassuring

**Description:** Use concise, accurate status text such as “Saved on this Mac” or
“Saved on this device · Waiting to sync.” Show local success immediately after the
local save completes; distinguish it from cloud completion. Use unobtrusive native
status presentation for ordinary conditions and an actionable explanation when
attention is needed. Make offline access feel like an expected part of everyday use.

**Automatic-sync development, 2026-10-12:** Saved edits and native provider notifications queue synchronization automatically while the app can run; foreground return/unlock and periodic checks catch missed notifications. Sync now is a retry action. Pending edits, device protection, offline delivery and unresolved conflicts retain their existing safeguards; ordinary incoming sync does not reset inactivity. iPhone 0.2.2 is installed; Mac 0.4.1 is installed/running with native locked-screen verification. Live iCloud inspection confirms the physical iPhone received the five-record native Mac test revision; notification-versus-fallback latency is not measured.

### 11. Give the first launch a warm, focused welcome

**Description:** Use a small illustration or expressive system symbol, friendly
language and a few clear choices for the first step. Examples are Create a vault
and Open an existing vault, with Import passwords additionally available on Mac.
Present guidance when it becomes relevant rather than showing a long tour. Keep
required recovery-key and protection steps explicit; the welcoming style must not
make required confirmations appear optional.

### 12. Make reversible actions forgiving

**Description:** Provide a clearly discoverable Undo action for eligible reversible
operations, such as moving an entry to Trash, using platform-appropriate presentation.
Retain required warnings, including the agreed folder-deletion warning. State what
was affected. Permanent deletion must not be presented as undoable, and Undo must
respect the normal vault-unlock boundary.

## Confirmed Mac experience

### 13. Use a three-column Mac main window

**Description:** Use three resizable columns as the default Mac layout. The left
sidebar contains vaults, folders and category filters. The middle column lists
matching entries with source-vault labels. The right column presents the selected
entry's details and actions. Allow the sidebar to collapse to make more space for
the entry list and details. This decision applies to the Mac; iPhone navigation
follows entry 19, iPad layout follows entry 20 and Android layout follows entry 21.

### 14. Place Mac search in the top toolbar

**Description:** Provide a search field in the Mac window's top toolbar, with ⌘F
focusing that field. Show matching entries in the middle column and the selected
result's details in the right column. Search all currently unlocked vaults by
default, with a visible filter for restricting the search to one vault, following
the existing agreed search scope. Keep the active scope apparent to the user.

### 15. Separate reading and editing within the Mac detail pane

**Description:** Open a selected entry in a reading view in the right-hand pane,
with visible Copy and Reveal controls where applicable. An Edit button switches
that same pane into an editable form. Show clear Save and Cancel actions while
editing. Preserve the agreed masking preferences, including direct display when
masking is disabled; copying or revealing a value does not require entering edit
mode. This flow keeps everyday credential access quick and makes deliberate changes
clear.

The Mac detail header places a one-click star button beside Edit. Show an outlined
star for an unstarred item and a filled star for a starred item, with corresponding
Star/Unstar tooltips and accessible state. Do not duplicate this action as Add to
Favorites or Remove Favorite menu entries. Confirmed during preview review on
2026-10-09.

Place a direct trash-can button beside the star, replacing the detail overflow
menu. Its tooltip and accessible label are Move to Trash. Clicking uses the
existing recoverable Trash operation with Undo; it does not permanently delete
the entry. Trashed entries retain their Restore action.

### 16. Create Mac entries from the toolbar

**Description:** Provide a New Item action in the Mac toolbar, also accessible with
⌘N. Let the user choose the entry type, such as Login, Card or Secure Note, then
present the new-entry form in the right-hand pane with clear Save and Cancel
actions. Show the destination vault prominently at the top of the form. When
creating from the combined all-vaults view, require the user to choose a destination
vault. Destination selection follows the existing unlocked-vault requirements.

### 17. Confirm navigation away from unsaved Mac edits

**Description:** When the user selects another entry or closes the window with
unsaved edits, show a native dialog offering Save Changes, Discard Changes and
Keep Editing. Save Changes continues the requested action only after saving
successfully; Discard Changes discards the edits and continues; Keep Editing
cancels the navigation or window closure and retains the current editor. This
dialog must not delay locking. When PWDTWO locks, immediately hide vault contents
and preserve the edits as a device-local encrypted draft under the existing draft
policy, available to resume or discard after the relevant vault is unlocked.

### 18. Present a focused Mac locked screen

**Description:** Replace vault content with a simple locked screen showing the
PWDTWO symbol and a prominent Unlock button. Use Touch ID when the included vaults
are eligible under the existing authentication policy. When vault passwords are
required, present a native sheet identifying the relevant vaults and allowing the
user to exclude a vault from this opening session. Restore the previous view only
after the included vaults meet the agreed shared-session unlocking requirements.
Keep the existing handling of preserved drafts and secret-masking preferences.

### 18.1 Add a gentle background glow

**Description:** Centre a soft blue-to-indigo glow behind the locked-screen content,
fading into the native window background. Adjust intensity for light and dark
appearances, keep text legible, and use decorative content only—never blurred vault
entries. Keep the background still and respect increased contrast preferences.

### 18.2 Give the PWDTWO identity more presence

**Description:** Display a slightly larger app icon with a soft shadow and the crisp
vector wordmark beneath it. Keep the composition centred and spacious without
redrawing or recolouring the supplied brand assets.

### 18.3 Welcome the user back

**Description:** Use “Welcome back.” as the main heading and “Your vaults are locked.”
as supporting text. Keep prototype/sample-data information visible without
competing with the primary message.

### 18.4 Make unlocking inviting and explicit

**Description:** Provide a generous native Liquid Glass unlock button. Show a Touch
ID symbol only when biometric unlocking is actually available for the included
vaults under the existing policy. The prototype retains “Unlock Preview” and a
lock symbol, with an explicit explanation that it does not authenticate or encrypt.

### 18.5 Transition gently after successful unlocking

**Description:** On successful unlock, briefly fade from the locked screen into the
vault interface without artificial delay or continuous animation. Honour Reduce
Motion with an immediate transition. Locking always removes sensitive content
immediately; no animation may retain vault contents during locking.

All five refinements were accepted on 2026-10-09. They refine the existing locked
screen without changing authentication policy or shared-session semantics.

## Confirmed iPhone experience

### 19. Use Items, Search and Settings tabs on iPhone

Search follow-up, 2026-10-11: tapping Search activates the native editable field immediately. The 0.2.1 (3) iPhone update binds search at the TabView and uses native search-tab activation; queries clear when all vaults lock. Simulator inspection confirms selection/focus, typed filtering and clearing. Installed on the physical iPhone; the user confirmed Search works on iOS27. [Evidence](../dev/iphone/results/2026-10-11/search-0.2.1/summary.json).

Development implementation, 2026-10-11: the dedicated iPhone target uses native Liquid Glass Items/Settings tabs and the trailing Search-role tab. Installed iOS 26.2 simulator inspection verifies entry rows, filtering through the native search field, grouped Settings, masked card details with star/edit/trash icons, normal back navigation and shared manual lock using a CLI-prepared fictional encrypted vault. Existing Mac vault/model/lifecycle code is reused without sharing the Mac UI. Physical-device/OS27, mobile cloud/Safari integration and full mobile feature parity remain open. [Phone evidence](../dev/iphone/results/2026-10-11/summary.json).

**Description:** Use a native Liquid Glass bottom tab bar with Items, Search and
Settings. Items presents the entry list with vault and category filters, defaulting
to all currently unlocked vaults and clearly showing the selected scope. Search
provides the agreed search across unlocked vaults. Settings contains preferences
and configuration. Tapping an entry opens its details with normal back navigation.
Provide a + toolbar action for creating an entry.

## Confirmed iPad experience

### 20. Adapt the iPad layout to the available window width

**Description:** In wide windows, show the sidebar, entry list and selected entry's
details together. At medium widths, show the entry list and details, with the
sidebar available on demand. In compact windows, show one view at a time with
normal back navigation. Preserve the selected entry and scroll position when
resizing. Support touch, pointer and keyboard interactions, with Liquid Glass
navigation and controls. Base the presentation on available window space so it
also adapts while multitasking.

## Confirmed Android experience

### 21. Use Material 3 navigation adapted to the window size

**Description:** Use Material 3 styling with colors that adapt to the user's system
theme. On phones, provide bottom navigation for Items, Search and Settings, with a
clearly labeled floating New Item button. Open entry details with normal Android
Back navigation. On larger windows, use a navigation rail and show the entry list
and details side by side. Preserve the agreed browsing and search scope across
currently unlocked vaults, with visible vault identity and filtering.

## Confirmed phone and tablet editing experience

### 22. Create and edit entries in an appropriately sized native form

**Description:** On iPhone, iPad and Android, open existing entries in a reading
view with visible Copy, Reveal and Edit actions where applicable, respecting the
agreed masking preferences. Use a full-screen form for creating or editing entries
on phones and in compact windows; use the detail pane in wider tablet windows.
Keep Save, Cancel and the destination vault clearly visible. When leaving unsaved
edits, offer Save Changes, Discard Changes or Keep Editing with the same outcomes
as the Mac flow in entry 17. Preserve the existing immediate-locking and encrypted
draft behavior; a navigation confirmation must not postpone locking.

## Confirmed iPad search experience

### 23. Keep iPad search close to the entry list

**Description:** Place a search field above the iPad entry list and show results
in that column. Support ⌘F to focus search when a keyboard is attached. In compact
windows, provide a toolbar Search button that opens a dedicated search view.
Clearly display the search scope as All unlocked vaults or the selected vault,
following the existing default scope and vault-filter behavior.

## Confirmed phone and tablet unlocking experience

### 24. Offer biometrics automatically when deliberately opening the locked app

**Description:** On iPhone, iPad and Android, automatically start the appropriate
Face ID, Touch ID or Android biometric prompt when the user deliberately opens
the locked application and biometric unlocking is eligible. If authentication is
canceled or unsuccessful, remain on the locked screen with Unlock to retry and
Use vault password as an alternative; do not repeatedly reopen the prompt without
another deliberate action. Keep required vault-password entry and the option to
exclude a vault from the opening session available. Apply the existing shared-session
unlocking requirements before showing vault contents. This decision concerns the
phone and tablet applications; the Mac presentation remains as described in entry 18.

## Confirmed entry-list presentation

### 25. Use clear, recognizable entry rows across platforms

**Description:** Present one clear row per entry. For logins, show the title with
the username or website underneath where available. For cards, show the label and
last four digits where available. For secure notes, show the title and a note icon.
Give every entry a recognizable type icon and source-vault label. Use comfortable
spacing and a clear selection highlight in layouts where the list and details
appear together. Express these rows through each platform's native visual conventions.

## Confirmed entry-detail presentation

### 26. Keep entry details clearly organized across platforms

**Description:** Show the title, type icon and vault identity at the top of an
entry's detail view. Present the main fields first; for logins these are username,
password and website, with relevant Copy and Reveal controls beside the fields.
Place custom fields, notes and attachments below in clearly labeled sections.
Keep Edit readily visible and provide history, sharing, moving and deletion through
a More menu. Preserve the same information order across platforms while using each
platform's native presentation. Existing masking, sharing, deletion-confirmation
and vault-unlock requirements continue to apply to these actions.

## Confirmed generator interaction

### 27. Generate a password or passphrase from the entry editor

**Description:** Place a Generate button beside the password field while editing.
Open the generator in a popover on Mac and a native sheet on phones and tablets.
Include a Password / Passphrase selector, a preview, the relevant generation
options and Generate Again. Use in Entry inserts the chosen result into the form;
Cancel leaves the entry's password field unchanged. Saving the entry remains a
separate action. Apply the accepted generator presentation in entry 7 and the
existing generator preferences and protected-history requirements.

## Confirmed Mac browser autofill experience

### 28. Present a compact login autofill chooser in Mac browsers

**Description:** In Safari and Chrome on Mac, present a compact chooser that shows
the destination website prominently. List matching logins with their title,
username and source-vault label. Clicking a matching login fills it under the
existing autofill and auto-submit rules. Provide search for another entry, retaining
the agreed explicit website-mismatch warning and confirmation flow. When locked,
show Unlock before displaying credentials. This presentation concerns login
autofill; existing card, identity and passkey interaction requirements remain
separate.

### 29. Offer a compact browser prompt to save or update a login

**Description:** Present a compact, non-blocking prompt for saving a new browser
login or updating an existing one. Clearly show the website, username and
destination vault. Offer Save Login or Update Login, as appropriate, together with
Not Now. For a new login, let the user choose the destination vault. For an update,
identify the existing entry and, when several accounts match, let the user select
which entry to update. Updates stay in the selected entry's vault. Preserve the
existing unlocking and masking rules; dismissing the prompt makes no vault change.

## Confirmed vault-creation experience

### 30. Guide vault creation through focused steps

**Description:** Present a short guided setup for creating a vault. First personalize
the vault with a name, icon and color. Next choose storage: this device, iCloud Drive
where supported, or Google Drive. Then enter and confirm the vault password. Explain
the recovery key's purpose and require confirmation that it has been saved, following
the existing recovery requirements. Finally, offer optional biometric unlocking and
open the empty vault. Show clear progress with Back and Continue controls, keeping
each step focused on one decision and presenting it through native platform controls.

## Confirmed existing-vault opening experience

### 31. Guide opening an existing vault from its storage location

**Description:** Let the user choose the vault's location: this device, iCloud Drive
where supported, or Google Drive. Use the appropriate file picker to select the
vault and show download progress when a download is needed. Then request its vault
password, with a Forgot password? action leading to the existing recovery flow.
After successful password unlocking, offer optional biometric unlocking and show
the vault's entries. Keep the flow native to each platform and preserve the existing
distinction between provider sign-in and vault unlocking.

**iPhone development evidence, 2026-10-11:** 0.2.0 adds native Open cloud vault and Settings → Cloud sync presentations with Apple's Files folder picker, existing-password enrollment, grouped unlocking, status and retained-version review. Setup/management/picker-cancel/dismissal were inspected in the iOS 26.2 simulator. Identity/offline/conflict/Trash/rename behavior passes native Mac/iPhone runtime tests using simulated ciphertext delivery. Live iCloud and physical bookmark restoration are pending user folder selection; direct Google login and background adapters remain unfinished. [Evidence](../dev/iphone/results/2026-10-11/cloud-0.2.0/summary.json).

## Confirmed recovery experience

### 32. Present recovery as a dedicated guided flow

**Description:** Identify the vault and let the user enter or paste its recovery
key. After validating the key, ask the user to choose and confirm a new vault
password. Present the replacement recovery key and require confirmation that it
has been saved. Show a completion message after recovery succeeds, then open the
vault. Explain upfront that recovery replaces both the vault password and recovery
key, following the existing recovery policy. Use a focused native presentation
with clear progress through these steps.

## Confirmed Settings organization

### 33. Organize Settings by purpose and make preference scope clear

**Description:** On Mac, provide a separate native Settings window accessible with
⌘,. On phones and tablets, provide a Settings screen with grouped sections. Use
General & Appearance, Security & Unlocking, Autofill & Clipboard, Notifications,
Vaults, and Help & Diagnostics as the sections. Under Vaults, let the user select
a vault to manage its storage, synchronization and backups. Clearly indicate whether
each preference applies only to this device or to the vault across devices, following
the already agreed preference scopes and actual synchronization availability.

## Confirmed conflict-review experience

Development implementation, 0.4.0 (2026-10-11): File → Cloud Sync exposes masked expandable version previews and a resolution selector. Keep all versions is the default; selecting one or the deletion variant moves other edited records to Trash. Unchanged scans preserve review choices. The review shows the merged vault name. Side-by-side changed-field highlighting and installed visual acceptance remain open.

### 34. Make conflicting entry versions easy to compare and resolve

**Description:** Mark entries with unresolved synchronization conflicts using a
Needs review badge. Show conflicting versions side by side on wide screens and
provide a version selector on phones or compact layouts. Highlight changed fields
while respecting the user's secret-masking preferences. Offer Use This Version to
select the current entry and Decide Later to postpone resolution. Preserve all
conflicting versions when the user postpones, following the existing conflict
policy and vault-unlock requirements.

## Confirmed entry-history experience

### 35. Preview dated history versions before restoring

**Description:** History opens a dated list of previous entry versions, newest
first. Selecting a version shows a read-only preview with changes highlighted
against the current entry, respecting the existing secret-masking preferences.
Allow copying an individual previous value or choosing Restore This Version.
Before restoration, confirm that the complete entry, including its historical
attachments, will be restored. Preserve the version that was current immediately
before restoration in history, following the agreed history policy.

## Confirmed Trash experience

### 36. Make Trash accessible and restoration straightforward

**Description:** Make Trash accessible from the sidebar in wide layouts and the
Items filters on phones. Clearly identify the vault containing each deleted item.
Selecting an item shows a read-only preview with Restore, respecting the existing
unlocking and masking preferences. Empty Trash identifies the selected vault and
affected item count, then requires explicit confirmation. Restoration follows the
agreed duplicate-handling rules, preserving an existing active item and flagging
a possible duplicate when applicable. Existing retention and permanent-deletion
policies remain unchanged.

## Confirmed backup-settings experience

### 37. Present each vault's backup settings on one clear screen

**Description:** Show Scheduled backups, disabled by default, with a frequency
chooser when enabled. Identify the designated Backup device and provide a Change
action. Show the Backup location, last successful backup, and pending or error
status when relevant. Explain clearly: “One backup is kept. Each successful backup
replaces the previous one.” Provide separate Export Backup and Restore from Backup
actions. These actions follow the existing distinction between the single
application-managed backup and separately user-managed manual exports.

## Confirmed backup-restoration experience

### 38. Preview a backup before choosing how to restore it

**Description:** Let the user select and unlock a backup, then preview its vault
name, backup date and contents. Make Open as Separate Vault the primary action,
following the agreed default restoration policy. Offer Replace Existing Vault…
as a secondary action requiring target-vault selection and explicit confirmation.
Once the backup is opened as a separate vault, let the user select entries and
use Copy to Vault… for selective recovery. Preserve the existing unlock requirements
for both source and destination and the separate restored vault's synchronization
boundary.

## Confirmed cross-vault copy and move experience

### 39. Make the destination and effect of copying or moving clear

**Description:** Provide Copy to Vault… and Move to Vault… in the More menu. Use a
native chooser showing the source, selected item count, destination vault and
destination folder. Explain the effect before confirmation: Copy keeps the originals,
while Move sends them to the source vault's Trash only after the destination save
succeeds. Show a brief completion message identifying the destination. Preserve
the existing source/destination unlocking requirements and transfer behavior.

**Mac copy-control implementation clarification:** Preserve the user's direct Star and Trash controls. The Mac development copy slice adds Copy to Vault… through an explicit copy icon, File command and entry-row context menu. Its native sheet starts with the chosen active entry and allows additional active entries from that same source vault, then reviews the unlocked destination and existing folder/top level. When unlocked vault names match, show a short local identity alongside the name to disambiguate the destination. Copy keeps originals and appends independent entries without merging or overwriting matching titles. Move and complete history/attachment coverage remain pending.

## Confirmed Mac import experience

### 40. Preview imports and review possible duplicates before applying them

**Description:** Present a guided Mac import flow. Let the user choose the source
application, its supported export file and an unlocked destination vault. Preview
the entries, exact duplicates and content that cannot be transferred. Present
differing possible matches for review with Skip, Keep Both and Update Existing.
Keep exact duplicates skipped by default, following the agreed import policy.
Require confirmation with Import, then show a summary of imported, skipped and
unsuccessful entries. Preserve the existing entry's prior version when an update
is selected, as required by the functional specification.

## Confirmed Mac migration-export experience

### 41. Make export scope, format and protection explicit

**Description:** In the Mac migration-export flow, let the user select entries or
a vault and choose CSV or Encrypted KDBX. Preview included and omitted content with
source-vault labels. For KDBX, show password and confirmation fields plus separate
Include History and Include Trash switches, both disabled by default. Explain that
this export uses its chosen password without PWDTWO recovery. For CSV, clearly
state: “This file can be read without a password.” Finish with Export… opening the
native save dialog. This presentation applies to migration exports; backup and
individual-sharing workflows retain their separate agreed behavior.

## Confirmed Password Health experience

### 42. Present actionable password-health findings with clear scope

**Description:** Provide a Password Health overview accessible from the sidebar
on wide layouts and from Items on phones. Group findings into Weak, Reused and
Leaked Passwords. Show each affected entry's title, vault and issue, with Review
opening its details. Clearly identify which currently unlocked vaults were checked.
When leak checks are disabled, show Checks not enabled with an opt-in action,
following the existing consent policy. Keep ignored findings in a separate,
accessible section, preserving their agreed scope and behavior.

## Confirmed authenticator-code presentation

### 43. Make authenticator codes easy to read and copy

**Description:** Show the current authenticator code near the login fields, with
digits grouped for readability and a clearly visible Copy Code action. Show a small
countdown ring together with remaining seconds so that timing is understandable
without relying on the graphic alone. Replace the code smoothly when it refreshes,
respecting reduced-motion preferences and the existing vault-unlock boundary.

## Confirmed passkey presentation

### 44. Identify passkeys clearly and use native sign-in flows

**Description:** Identify passkey entries with a recognizable symbol and a Passkey
label. Clearly show the service, account name and vault in the entry details. When
a compatible website or application offers passkey creation, identify the service
and account before the user chooses the destination vault. During sign-in, follow
the platform's native credential-selection and authentication flow, preserving the
existing passkey and vault-unlocking requirements.

## Confirmed card and identity autofill review

### 45. Review the destination and fields before filling cards or identities

**Description:** For supported forms, present a compact review screen showing the
destination website or application prominently. Identify the selected card or
identity and its source vault. Show the fields that will be filled, respecting
the user's masking preferences. Provide clear Fill and Cancel actions and require
explicit Fill confirmation before releasing values. After filling, leave form
submission to the user, following the existing card and identity autofill policy.

## Confirmed individual-sharing experience

### 46. Preview an independent copy and separate its file from its transfer password

**Description:** Preview the current entry with switches for including notes and
attachments; exclude entry history under the existing sharing policy. Clearly label
the operation Send an independent copy. Provide separate Share Encrypted File and
Copy Transfer Password actions, explaining that the generated transfer password
must be communicated separately from the file. On receipt, let the recipient enter
the transfer password, preview the contents, choose an unlocked destination vault
and select Save Copy. Explain that later edits do not update the other person's
copy. Preserve the existing requirement for compatible PWDTWO applications and
the established transfer-protection and masking behavior.

## Confirmed shared-vault settings

### 47. Distinguish shared file access from shared vault credentials

**Description:** Clearly mark shared vaults with a Shared badge. Provide a Sharing
page showing the cloud provider and a Manage Access… action leading to that
provider's sharing controls, subject to the user's provider permissions. Explain
that participants have equal access to the vault's contents. Separate file-access
setup from guidance for securely giving participants the vault password and recovery
key. Explain that removing cloud access cannot erase copies someone already holds.
This presentation preserves the existing distinction between provider permissions
and access to decrypted vault contents; it does not introduce PWDTWO participant
roles or finalize the outstanding credential-delivery mechanism.

## Confirmed diagnostic-report experience

### 48. Let users review a diagnostic report before sharing it

**Description:** Under Help & Diagnostics, provide Report a Problem. Generate the
diagnostic report on the device, then let the user preview its contents and deselect
optional sections. Offer Save Report… and Open GitHub Issue… with instructions for
manually attaching the reviewed report. Clearly state that generating the report
sends nothing automatically. Preserve the existing diagnostic-content exclusions
and explicit-sharing policy; opening the issue page does not itself submit a report.

## Confirmed attachment experience

### 49. Add and inspect attachments through native controls

**Description:** Provide an Attachments section showing each file's name, type and
size. While editing, offer Add Attachment… using the native file picker and support
drag-and-drop on Mac and iPad. Selecting a supported image, PDF or text file opens
a native preview. Other file types offer an explicit Export/Open With… action.
When a file exceeds the configured attachment limit, show a clear message explaining
that limit. Preserve the existing vault-unlock, attachment-storage and entry-editing
behavior.

## Confirmed autofill setup guidance

### 50. Offer optional, platform-specific autofill onboarding

**Description:** After opening the first vault, offer an optional Set Up Autofill
step. Show a short checklist relevant to the device, covering enabling PWDTWO in
system settings and configuring supported browser extensions where needed. Provide
buttons to open the relevant settings with clear instructions. Offer Later and
keep the same guidance available under Settings → Autofill & Clipboard. Deferring
this setup does not prevent using the vault through the application.

## Design references and refinements for running-app review

- Apple places Liquid Glass in the control/navigation layer; entry lists, notes and
  credential detail content should use appropriate content surfaces. Its appearance
  responds to system accessibility and appearance choices.
  [Apple materials guidance](https://developer.apple.com/design/human-interface-guidelines/materials),
  [Adopting Liquid Glass](https://developer.apple.com/documentation/technologyoverviews/adopting-liquid-glass).
- For Android, use current Material 3 conventions, including dynamic color and
  suitable expressive touches. Material provides both expressive and more restrained
  motion schemes. Refine exact component and motion choices through the running
  native applications rather than continuing requirements elicitation now.
  [Material Design 3](https://m3.material.io/),
  [Material motion](https://m3.material.io/styles/motion/overview/how-it-works).

Recommended personality for implementation and hands-on review: calm and friendly overall, with more
playfulness in the generator, vault personalization and first launch. Authentication,
recovery, conflicts and error messages should stay concise and clear.

## Review approach

The user needs to see and use the applications running before making further UX
decisions. Continue with the previously requested Mac-first development scope and
use working native builds for subsequent UX feedback. Revisit the other platform
experiences through their own running applications as development reaches them.
Completion of this UX round does not resolve the separately documented architecture
and integration-validation gates.


## Mac integration development slice — 2026-10-10

File → Cloud Sync and File → Set Up Autofill expose native development panels. Concurrent entry branches offer a combined review retaining both conflicting records; unsupported vault-level conflicts remain explicit and retained. The browser/system credential chooser is native SwiftUI, shows the exact HTTPS destination and source-vault/account labels, masks passwords and returns only the deliberately selected login. Setup routes to Safari/system controls without an HTML application view. Complete mismatch, side-by-side conflict, multi-page login, generation/update and optional auto-submit UX remains outstanding; see the [integration handover](cloud-autofill-handover-2026-10-10.md).

0.4.0 refinement: Settings → Autofill & Clipboard exposes Submit supported login forms after autofill, off by default and scoped to this device. Exact-site matching selection may submit a supported simple login; unsupported forms remain filled for manual submission. Other-site search/Fill once, partial steps, generated values and signup/new-password forms remain manual. Native/mock checks pass; installed submission behavior is not yet accepted. Earlier generation/update development work and Chrome user acceptance are documented in tasks.md; advanced multi-page behavior and broad platform acceptance remain open.

## Browser field suggestions correction — 2026-10-10

User clarified that a supported username/password field should show PWDTWO's chooser automatically when focused. The toolbar-to-Mac-sheet bridge is insufficient as the everyday browser experience. Use an extension-owned browser frame beside the field, matching logins with title/username/source vault, locked Unlock state, search across unlocked logins and an explicit destination warning before filling another site's login once. No automatic submission. The four standalone applications remain native; the browser extension uses browser UI resources and keeps passwords in the native broker until deliberate selection. Persistent focus detection requires optional website access granted in Chrome's own permission UI.

Simple sign-in steps may offer a username alone or a password alone. Release only the value required by that current step; require a fresh selection on a later step. Advanced multi-step account continuity remains separate work. If another browser tool replaces the extension frame with a page-origin document, show a static loading error and release no account metadata into that document.

## Chrome generation and capture development slice — 2026-10-10

Extend the field chooser with Generate a password and Save or update this login. Generation offers native-engine random-password/passphrase controls and explicit history-vault selection; Generate & fill retains encrypted history before inserting a value. For save review, show website/username with password hidden, New login plus vault selection or explicit existing-account Update, and Not Now. Submitted supported forms can reopen a non-blocking review after same-origin navigation using a short-lived native capture ticket. Browser success means native encrypted publication completed; an interrupted generated value remains in native history. Save candidates do not assert successful website authentication. The standalone apps remain native. See the [implementation and acceptance limits](browser-generation-capture-handover-2026-10-10.md).


## Browser connection state correction — 2026-10-11

Show Unlock PWDTWO only when the native app has confirmed its vault session is locked. A transport or setup failure is not evidence of a locked vault: clear the chooser's private metadata, explain that the connection is unavailable and offer Retry connection. An available unlocked catalog hides both actions. Safari and Chrome share this state presentation.


Safari 0.3.3 installed inspection confirms the field-adjacent chooser can display the unlocked matching catalog with search and save/generate controls, hiding Unlock and connection messages. This supersedes the earlier native-sheet-only Safari presentation for this verified flow; broader Safari credential ceremonies remain open. [Installed evidence and limits](safari-connection-handover-2026-10-11.md).


## Mac password-provider lifecycle — 2026-10-11

Use a native destination-labelled system-provider screen with Choose in PWDTWO, Cancel and distinct retry guidance. Disable repeated choices while one is pending. Closing/cancelling the OS presentation retires its native chooser; a late reply cannot complete another presentation. Unsupported or ambiguous OS destinations give manual-copy guidance. This development provider always requires deliberate account selection; activation and actual OS credential completion remain hands-on acceptance gates.

**Live Mac cloud enrollment and automatic save, 2026-10-12:** 0.4.2 corrects sequential native folder/revision picker attachment. The installed Mac interface enrolls the existing fictional iPhone cloud vault, preserves its original identity, and displays it after user-approved grouped Touch ID unlocking. An ordinary Mac GUI save publishes and reaches the physical iPhone automatically; all three encrypted copies match. Reverse installed-GUI acceptance also passes: the user-created iPhone note “123” appears automatically on the Mac, with seven retained records and exact Mac/provider/phone ciphertext convergence.

### 51. Make iPhone AutoFill convenient after app unlocking

**Description:** User-requested 2026-10-19. Treat leading www as the bare-domain spelling while displaying the actual requesting address. Reuse recent app/chooser authorization automatically for the selected short duration; default five minutes, configurable under AutoFill as Keep AutoFill unlocked (Never, 1 minute, 5 minutes, 15 minutes). Then offer Face ID / Touch ID automatically when enrolled, with a visible retry and grouped vault-password fields as fallback. Do not repeatedly trigger biometrics after cancellation. Show clear nonmatching-login guidance and preserve deliberate entry selection and other-site confirmation. App background hiding preserves the bounded AutoFill window; manual Lock ends it. Update both guides and native fictional Settings/chooser screenshots.
