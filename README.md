<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/pwdtwo-dark.svg">
    <img src="assets/pwdtwo-light.svg" alt="PWDTWO" width="380">
  </picture>
</p>

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-2E62E8" alt="MIT license"></a>
  <a href="specs/specifications.md"><img src="https://img.shields.io/badge/spec-published-2E62E8" alt="Specification published"></a>
  <a href="https://66ideas.com"><img src="https://img.shields.io/badge/by-66IDEAS-16181D" alt="By 66IDEAS"></a>
</p>

**PWDTWO is a specification-first, open-source password manager designed for
macOS, iPhone, iPad and Android.** Save logins, credit cards and secure notes,
find them quickly, and fill credentials in browsers and compatible apps.
Keep access to your vaults when you are offline.

The specifications describe the product; native implementations bring it to life.
Each platform has its own application and interface, with a shared native vault
engine. Apple apps follow native Liquid Glass conventions; Android follows its
own platform conventions. No web-container application UI.

**This repository currently publishes the specifications, this README and its
branding, and the MIT license.** Mac and iPhone development builds exist and are
being tested privately. Application source, build tools, illustrated user guides
and downloads have not been published here. There is no production release or
public update feed yet. The independent iPad and Android apps remain planned.

## What PWDTWO is designed to do

The following describes the agreed product scope, not a list of released features:

- **Your vaults, your control:** multiple separately protected vaults, local-only
  use, optional biometric unlocking and an owner-held recovery key.
- **Work offline:** search, create and edit locally, then synchronize encrypted
  changes when the chosen cloud provider is available.
- **Use your own cloud storage:** optional iCloud Drive or Google Drive, with
  one provider per vault and no separate PWDTWO account or hosted sync backend.
- **Fill and save credentials:** Safari and Chrome on Mac, Safari on iPhone and
  iPad, Chrome on Android, and compatible operating-system app integrations.
- **Keep more than passwords:** credit cards, secure notes, documents,
  attachments, custom fields, folders, tags, favorites, history and Trash.
- **Generate and recover:** random passwords and English-word passphrases,
  explicit recovery, encrypted exports and user-configured backups.

See the [release-readiness summary](specs/release-readiness-2026-10-19.md) and
[task list](specs/tasks.md) for implemented development slices, remaining
acceptance checks and later phases. Development test results do not constitute
independent security approval or production readiness.

## Get started

### Read the specification

Start with the [functional specification](specs/specifications.md), then the
[UX specification](specs/ux.md) and [architecture](specs/architecture.md).
They describe the behavior, native interactions and technical constraints.
The [specifications index](specs/README.md) introduces the dated development
reports and explains references to files that are not yet public.

### Use or build an app

Public installers, App Store/Google Play listings and application source-build
instructions are not available yet. Do not treat a dated test report as a
published download or buildable implementation.

The private Mac test candidate is **0.5.1 (501)**, signed and notarized; the
private iPhone development build is **0.4.8 (14)**. The Apple support window is
OS generations **26 and 27**, with Apple silicon required on Mac. Separate native
iPad and Android applications are part of the specification, not available apps.
Future Mac downloads will be hosted on GitHub Releases and linked from
[66ideas.com](https://66ideas.com).

For maintainers with the full local development checkout, the illustrated
[Markdown user guide](docs/user-guide.md) and [standalone HTML guide](docs/user-guide.html)
are maintained together. **Those two local guide links are not available in
this public repository yet.** They are not included in this publication.

## Repository layout

| Path | Purpose |
| --- | --- |
| [`specs/`](specs/) | Functional requirements, native UX, architecture, research, implementation tracking and dated verification reports |
| [`assets/`](assets/) | Original light/dark PWDTWO wordmarks used by this README |
| [`README.md`](README.md) | Project introduction, current publication status and navigation |
| [`LICENSE`](LICENSE) | MIT license, copyright 66IDEAS |

Application implementations, build tools and illustrated documentation remain
outside the published tree for now. Some specification reports link to those
local files; those references will become available when their files are published.

## The specification

- [Functional specification](specs/specifications.md): user stories and
  acceptance criteria for vaults, autofill, synchronization, recovery and more.
- [UX specification](specs/ux.md): platform-native layouts, navigation,
  interactions and accessibility behavior.
- [Architecture](specs/architecture.md): native application boundaries, shared
  vault engine, storage, security decisions and unresolved design gates.
- [Project constitution](specs/constitution.md): MIT licensing, private signing
  credentials, local diagnostics and owner-controlled recovery.
- [Task list](specs/tasks.md) and [release readiness](specs/release-readiness-2026-10-19.md):
  agreed phases, implementation evidence and remaining release requirements.

The functional and UX specifications are the starting point for an implementation.
Preserve the native platform requirements and document any deliberate divergence
rather than assuming a development experiment is a final security design.

## Privacy

The specification requires on-device vault processing, offline access and
encrypted cloud synchronization without a separate PWDTWO account. Cloud storage
is optional. There is no application-operated vault or synchronization service.

The project policy excludes automatic analytics, telemetry and crash-report
uploads. Diagnostics stay on the device until the user reviews and explicitly
exports them. Update checks and optional cloud-provider access are separate from
vault-content processing. See the [constitution](specs/constitution.md) and
[architecture](specs/architecture.md) for the requirements and remaining validation.

## Contributing

[Issues](https://github.com/66IDEAS/PWDTWO/issues) and pull requests are welcome
for the specifications. Propose concrete behavior, UX or architecture improvements
and include acceptance criteria where appropriate. Application implementation
contributions can follow when that source is published.

Keep proposals focused and preserve offline access, native platform behavior and
owner-controlled recovery. Never attach personal vaults, passwords, recovery keys,
signing credentials or access tokens to an issue or pull request.

## License

[MIT](LICENSE) — free to use, modify and distribute, including commercially,
under the terms of the license. Third-party dependencies retain their own licenses.

---

<p align="center"><sub>A <a href="https://66ideas.com">66IDEAS</a> product · WENIGER. ABER BESSER.</sub></p>
