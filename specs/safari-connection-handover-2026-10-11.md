# Safari connection correction — 2026-10-11

The user enabled Safari and observed the chooser, but it showed Unlock while the native app was unlocked. Native SafariHandler logs showed Security-framework permission failure. A signed sandboxed client reproduced the problem with the PID-based verifier and audit-only lookup. A kernel-authenticated socket audit token plus dynamic code verification against the exact main app Info.plist now succeeds. Security verifies the supplied plist against the running process’s signed hash; the same identifier, Apple anchor and team requirements remain enforced. The sandbox and App Group entitlements are unchanged. The native server also binds client signature verification to its socket audit token.

The build packages the exact main Info.plist into each native client's resources before signing. A separate signed sandbox harness checks state only, including wrong identifier, altered/empty proof and invalid socket refusal. No catalog, credential, unlock or mutation is requested. This harness passes against the restarted final app. Browser/native integration regression checks, strict nested signing and resource/entitlement readback pass.

Chooser UI shows Unlock only for a confirmed locked session. Connection/setup failures clear private metadata and show Retry connection. Browser resources are version 0.3.1. No new website permissions were granted. The app was restarted and is observed unlocked; the agent did not unlock it or enter credentials.

Installed unlocked chooser rendering was subsequently verified in 0.3.3 (see below). Account-selection/fill validation remains separate from the sandbox state-only test.

[Build, signing, source hashes and sandbox evidence](../dev/experiments/foundation/results/macos-safari-connection-summary.json).


## Follow-up: stalled chooser

The user’s 0.3.1 Safari panel stayed on Connecting. Installed inspection found a visible chooser document with its script loaded but no native requests. A closed context response left the initial message untouched. 0.3.2 introduces a visible closed/error response, bounded eight-second reads, single-flight refresh, late-reply/page-exit rejection, Safari Promise messaging and a nonpersistent background page. Installed 0.3.2 now displays a connection failure, so it is not complete functional acceptance.

0.3.3 adapts Safari’s optional tab/frame association for extension-origin UI: resolve only an own-extension URL/ID/hash context, still requiring and binding its browser document ID. Native secret release remains bound to the original top-level destination document and anchor. Chrome’s original tab/frame requirements remain. Registered-listener and negative mock tests pass. Native code/disassembly, main Info.plist, running app process and signing entitlements are preserved by the browser-only update, with strict signing/resource checks. The native sandbox state/negative harness continues to pass.

After the user replied ready, the agent opened the existing Safari test-window toolbar chooser. Its screenshot shows the matching account and search/save/generate controls, with neither Unlock nor Connecting nor a connection failure. This verifies installed 0.3.3 unlocked catalog rendering. No page reload, account selection, generation, save/update or submission was performed by the agent. Before opening the chooser, the existing toolbar reported “Generated password retained in vault history and filled” and the page had a masked password. This is an observed completion status from prior activity, not an independently executed credential ceremony or proof of vault persistence/website authentication. Deliberate selection/fill, save/update, history recovery, dismissal and locked/reconnect checks remain open. [Current follow-up evidence](../dev/experiments/foundation/results/macos-safari-stalled-chooser-summary.json).


![Installed Safari 0.3.3 unlocked chooser](../dev/experiments/foundation/results/safari-connection-2026-10-11/safari-0.3.3-chooser.png)
