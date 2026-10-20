# iPhone/Mac iCloud test — 2026-10-11

The signed iPhone development app is 0.2.0 (2). Fourteen ordinary native iPhone checks, two separately orchestrated Mac/simulator exchange checks, and both Mac cloud regressions pass. Automated cross-platform delivery used copied ciphertext; actual iCloud delivery remains unverified until the following check. The existing Mac GUI application has not been restarted or changed, and the phone installation preserved its data container.

## Prepared disposable fixture

A separate native Mac test process created two fictional secure notes and published an encrypted revision into this iCloud Drive folder:

`PWDTWO Sync Test Easy 9921a1`

Its existing vault password is:

`111111111111111` (fifteen ones; the current 15-character minimum). Use only for this disposable fictional vault.

A fresh fixture replaces the original long-password fixture for this test; the original folder and vault are retained. Select the new **Easy** folder again on the phone. The fixture is independent of all regular Mac vaults. Local paths are recorded in ignored `dev/iphone/build/live-sync-fixture.json`; the provider folder contains only encrypted revisions. The Mac peer uses the application's actual core/lifecycle/sync sources, not a running GUI instance. The physical phone has no injected demo files.

## On the iPhone

1. While locked, choose **Open cloud vault**. If already unlocked, open **PWDTWO’s Settings tab → Cloud sync**, then use the **Open an existing cloud vault** section.
2. Tap **Choose iCloud Drive folder**. The picker initially opens **Recents**; tap **Browse** at the bottom, then **iCloud Drive**. Select the folder above and confirm the system picker's **Open** action. Select the folder itself, not its encrypted file. Selecting the directory is the iOS access grant; it must happen on the phone. Wait for iCloud delivery if the folder/revision is not available yet. Mac Foundation reported the folder and revision uploaded/current during the subsequent visibility check; phone visibility and the round trip remain unverified.
3. Enter the test password above and tap **Add cloud vault**. Select **Open your vaults** when addition completes. Unlock the included vaults; any other local vault still uses its own existing password. Exclude a vault you do not want in this session.
4. Confirm the two fictional notes appear. Edit the first note's Notes field to exactly `iPhone sync test`, then Save.
5. In **PWDTWO’s Settings tab → Cloud sync**, select the fictional shared vault and tap **Sync now**. Keep PWDTWO in the foreground for delivery. Report when the edit is saved/synced, or give the displayed failure text.

## Mac verification

The agent can use the prepared peer to read the isolated provider folder and verify actual arrival without touching regular vaults:

```sh
python3 - <<'PY'
import json, pathlib, subprocess
fixture = json.loads(pathlib.Path('dev/iphone/build/live-sync-fixture.json').read_text())
subprocess.run(['dev/iphone/build/SyncInteropMac', 'check-live', fixture['localFixture']], check=True)
PY
```

`iPhone test marker received=true` demonstrates that edit arrived through the provider and authenticated in the native Mac engine. A pending review needs explicit review; it is not a success. To test the actual Mac GUI independently, use its existing **File → Cloud Sync… → Choose Existing Provider Folder…**, choose this folder and a revision from it, then enter the same fixture password and add/unlock the cloud vault. That GUI enrollment, bidirectional live delivery, device restart/bookmark restoration, offline/provider races and physical protection remain additional checks.

Foreground polling/explicit sync are implemented. iOS background suspension, direct Google authorization, encryption-key rotation, provider migration, independent roots/settings conflicts and revision compaction are not completed by this slice.

[Native/runtime/build evidence](../dev/iphone/results/2026-10-11/cloud-0.2.0/summary.json).

## Live continuation — 2026-10-12

The physical iPhone already contains this fictional shared vault; no repeat folder grant is needed. The native Mac peer received/authenticated three provider revisions with an added entry and edited notes. The phone’s existing encrypted vault matches an authenticated provider revision. It did not contain the exact earlier `iPhone sync test` marker; ordinary edited records arrived nonetheless. This acceptance uses real iCloud delivery, with USB only for read-only proof inspection.

A fourth revision contains the new **Mac sync check · 2026-10-12** secure note, reported uploaded/current by Foundation. Unlock the phone, keep PWDTWO foreground for 30 seconds or choose **Settings → Cloud sync → Sync now**, and confirm that note appears. Actual Mac GUI enrollment remains blocked by window-control timeouts; the native CLI peer is independent of that GUI process. [Current evidence](../dev/iphone/results/2026-10-12/live-icloud/summary.json).

The Settings references above mean the bottom **Settings** tab inside PWDTWO. **Cloud sync** is a button in the **Vaults** section; scroll down if needed. They do not refer to the iPhone system Settings app. On 2026-10-12, after the user unlocked PWDTWO, read-only verification confirmed exact physical iPhone/native Mac ciphertext convergence and matching phone sync journal. No manual Sync now action was needed for that round trip. [Round-trip proof](../dev/iphone/results/2026-10-12/live-icloud/round-trip-proof.json).
