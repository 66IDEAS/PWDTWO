# PWDTWO — Project Constitution

## 1. Open source under the MIT licence

The project's original source code is to be released under the MIT licence (`SPDX-License-Identifier: MIT`), as requested by the user on 2026-10-08. The root [LICENSE](../LICENSE) contains the standard licence text with the user-confirmed notice: Copyright (c) 2026 66IDEAS.

Preserve third-party licences and required notices. Select dependencies whose terms permit the intended open-source and binary distribution; the project's MIT licence does not replace their terms. Include licence information in source and application releases. [Standard MIT licence](https://opensource.org/license/mit).

## 2. Public source and private release credentials

Document how to build the native applications from source. Keep official signing keys, notarization credentials, private service credentials, and personal vault data outside the public repository. Provide configuration examples that contributors can populate with their own credentials.

The selected public source and Mac release host is GitHub 66IDEAS/PWDTWO, with the Mac download also linked from 66ideas.com. Release automation and exact asset/feed locations remain to be configured. This document records project requirements; it does not indicate that a public repository or signed release has been created.

## 3. On-device diagnostics and deliberate sharing

PWDTWO does not automatically transmit application telemetry, analytics, or crash reports. Keep diagnostics local, bounded, and free of vault contents and secrets. Users may generate, preview, and explicitly export/share a sanitized report with 66IDEAS for support. Diagnostic exports must not silently upload data or create public bug reports. Apply this policy to third-party components as well as application code. Technical details are recorded in architecture requirement 28 and functional story 47.

## 4. Owner-controlled recovery

A vault's password and separate recovery key remain under its owner's control. Provide no vendor, administrator, or trusted-contact recovery backdoor or escrow. Recovery must work offline when the necessary vault file and recovery information are available locally. If both secrets are lost and no existing authorized unlock path remains usable, access is unrecoverable. Deliberate sharing remains supported; timed emergency access for another person is excluded.
