# Chrome inline autofill candidate — 2026-10-10

PWDTWO now contains a Chrome 0.2.0 development candidate for field-triggered browser suggestions. It is compiled, Apple Development signed and reloaded in the installed unpacked extension. **The user has confirmed that the automatic chooser appears and selecting an entry fills the form.** This is user-reported installed Chrome verification. Native broker and mocked browser/renderer checks also pass; broader installed search/mismatch/lock ceremonies remain open.

## Implemented behavior

- Optional HTTPS website access registers top-level focus detection. A focused supported username or password field opens an extension-owned chooser beside it. Without that permission, the toolbar supplies temporary current-page access to the same chooser.
- Matching login rows show entry title, username and vault. Search other websites expands the list; selecting an unmatched entry requires a destination warning and explicit **Fill once on this website**. This does not persist an approved website.
- Locked vaults return no catalog. **Unlock PWDTWO** activates the native app; authentication stays native. Background polling does not launch the app or keep its session unlocked.
- A native, short-lived single-use grant binds the displayed record snapshot, current vault session, URL, browser document and current field stage. Selection fails after lock/reopen, record changes, navigation or field replacement.
- The chooser receives metadata only. On deliberate selection the background sends credentials directly to the bound top-level document. Username-only steps receive no password; password-only steps receive no username. A later step requires a new selection. No form is submitted.
- If a browser tool replaces the iframe with a `srcdoc` or page-origin document, the renderer releases no catalog there and shows a static loading error. It does not remove replacement attributes, fetch privileged HTML into the page, or weaken browser protections.
- Chrome-specific setup routing and extension options expose enable/disable controls for automatic suggestions. Existing explicit save capture/native review remains available from the page context menu.

## Verification and installed limitation

Targeted native broker, browser-field, inline transport and renderer checks pass. Coverage includes matching and cross-site confirmation, password-excluded search, locked/Trash/unopened-vault exclusions, document/record/session/field-stage guards, selected-only release and refusal of page/forged-extension messages. Renderer checks cover the static fail-closed replacement behavior. These are synthetic native/mocked tests.

The final complete app and nested native host/Safari/system extensions compile for Apple Silicon and macOS 26. Strict deep signing and required App Group/sandbox/autofill entitlements verify. Packaged browser resources match source; the manifest includes only the builder's explicit additional icon declarations.

During the installed test on a public fictional login form, Chrome displayed the injected panel but its document was empty. The content script's local diagnostic confirmed a replacement `srcdoc` document. Direct inspection of `chrome-extension://…/inline.html` was also rejected by the browser-control tool's protocol policy. The replacement's originator was not independently identified. No restriction was bypassed and no installed inline-fill success is claimed.

The earlier successful installed **native-sheet** fill/cancel/locked/capture evidence remains historical evidence for that earlier implementation, not acceptance of this inline candidate. See [earlier integration handover](cloud-autofill-handover-2026-10-10.md).

Evidence: [final source/signing/check record](../dev/experiments/foundation/results/macos-inline-autofill-summary.json), [installed extension reload](../dev/experiments/foundation/results/inline-autofill-2026-10-10/installed-extension-0.2.0.png), [frame diagnostic](../dev/experiments/foundation/results/inline-autofill-2026-10-10/frame-diagnostic.json). The replacement screenshot/diagnostic predate the final static-error refinement; final renderer behavior is currently covered by mocks only.

The agent did not grant persistent HTTPS access, fill credentials during the inline test, unlock the normal user catalog or delete the isolated catalog. The retained test catalog includes edits made by the user during testing. The owned browser test tab was closed and the normal signed app was reopened locked with Touch ID available.

## User-reported installed verification

On 2026-10-10, after instructions to enable automatic suggestions, reload a login page and focus a username/password field, the user replied **“Yes and yes”** to whether the chooser appears beside the field and whether selecting an entry fills it. Record both as passed by user report. No exact website, permission settings, browser version, screenshot or credential values were supplied in that report; do not infer those details or treat it as agent-observed evidence. This resolves the basic installed render/fill acceptance despite the earlier automation limitation.

## Remaining user-present checks

In Chrome → Extensions → PWDTWO → Details → Extension options, enable automatic field suggestions and accept Chrome's HTTPS website-access prompt. This access lets PWDTWO detect supported login fields across HTTPS websites; passwords remain selection-gated. User confirmation is required before the agent grants this broader permission through computer automation.

Basic automatic field focus and entry filling are now confirmed by the user. Additional installed checks remain for other-site search/cancellation/one-time fill, locked state and native unlocking. The automation replacement/protocol limitation still applies to agent-operated verification.

## Still open

Approved additional website persistence; advanced multi-page account continuity; iframe/complex-form/browser compatibility; generator and save/update prompts; optional auto-submit; equivalent Safari inline UX and real Safari/system ceremonies. Live cloud-provider delivery and the broader production security/release gates remain separately open. Native app interfaces remain SwiftUI/AppKit; browser resources do not create an HTML application shell.

Implementation references: [Chrome content scripts](https://developer.chrome.com/docs/extensions/develop/concepts/content-scripts), [web-accessible resources](https://developer.chrome.com/docs/extensions/reference/manifest/web-accessible-resources), [Chrome permissions](https://developer.chrome.com/docs/extensions/develop/concepts/declare-permissions).
