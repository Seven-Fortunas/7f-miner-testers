# 7F Miner for Windows: test guide

What to check when you download, install and use a signed 7F Miner build.
It runs on **testnet**; testnet coins have no money value. Work through the
sections in order and note anything that doesn't match.

## 1. Download

1. Open this repository's
   [Releases](https://github.com/Seven-Fortunas/7f-miner-testers/releases)
   (you must be signed in to GitHub with the account that was invited to
   this repository) and pick the newest **7F Miner \<version\>**.
2. Download `7F-Miner-<version>-setup.exe`. Only use files from a release
   here.
3. Optional: in PowerShell, `Get-FileHash .\7F-Miner-<version>-setup.exe`
   should equal the SHA256 in the release notes.

Look for: any browser or antivirus warning or block (note the exact text, a
screenshot helps).

## 2. Signature

Before running it, right-click the file → **Properties** → **Digital
Signatures**.

- [ ] The tab exists and shows **Seven Fortunas Inc**.
- [ ] **Details** says "This digital signature is OK."
- [ ] **Details** → **Countersignatures** shows a Microsoft timestamp from the
      day the build was signed.

The certificate (**Details** → **View Certificate**) is valid for only about
3 days, often ending before or soon after you test. That is normal: Microsoft
Artifact Signing issues a new short-lived certificate every day, and the
timestamp proves the certificate was valid when the file was signed, so
Windows keeps accepting the signature after the certificate's end date.
Report it only if the signature is no longer "OK".

## 3. Install

Run the setup file.

- [ ] Windows' prompt, if any, names **Seven Fortunas Inc** as publisher, not
      "Unknown publisher". A SmartScreen "Windows protected your PC" screen
      may still appear while Microsoft builds trust in the certificate;
      report it if it does.
- [ ] The welcome page says what 7F Miner does (testnet node, mining only
      after Start Mining, internet use).
- [ ] The Terms of Use page must be accepted to continue.
- [ ] It installs without asking for administrator rights, to
      `%LOCALAPPDATA%\Programs\7F Miner`, with a Start menu entry and, if
      ticked, a desktop shortcut, both with the 7F icon.

**Upgrading:** if 7F Miner is open, Setup says it will close it first, then
upgrades. Your wallet and data stay.

## 4. First start (setup wizard)

You need the **API key** from your testnet invitation. Make sure no one can
see your screen.

- [ ] **App password:** chosen and typed twice. You'll type it at every start.
- [ ] **24 words:** *Create a new wallet* shows 24 words. Write them on paper
      only, not in a file, photo, password manager or email. The wizard then
      asks you to type them back. (*Restore from my words* takes 12 or 24
      words instead.)
- [ ] **Certificate:** enter the API key and press *Get my certificate*. It
      should finish without an error.
- [ ] The main window opens titled **7F Miner (testnet)**.

## 5. Sync and mining

- [ ] **Peers** goes above 0 and **Height** climbs to the chain tip (compare
      with [explore.sevenfortunas.com](https://explore.sevenfortunas.com)).
      The node output shows `[trusted-tip] OK: local chain == consensus tip`.
- [ ] Nothing mines until you press **Start Mining**; the status says "not
      mining; the node keeps syncing".
- [ ] After **Start Mining**: the output shows `RandomX ready.` and
      `mining block <n>...`, and **Hash rate** goes above 0. **Stop Mining**
      stops it while the node keeps syncing.
- [ ] As new blocks arrive the output moves on to the next `mining block`.

Expected and harmless in the output: `already have it`, `duplicate block`,
and a one-off `our height ... is AHEAD of trusted peer max ...` just after
sync.

Look for: lines with `error`, `rejected`, `banned`, `diverge` or `rollback`,
a Height that stops climbing while others' doesn't, or the PC becoming
sluggish.

## 6. Settings

- [ ] **Version** shows `7F Miner <version> (testnet)` matching the release.
- [ ] **CPU threads** and priority change mining at once (watch Hash rate).
      The default is 1 thread at low priority; try more (below).
- [ ] **Show my 24 words** asks for the app password and shows the words
      you wrote down.
- [ ] Optional: **Rebuild** (asks for the password) syncs the chain again
      from the start.

### Hash rate by thread count

**Hash rate** in the main window (H/s, next to Height and Peers) is measured
over the last second, so it jumps around. With the PC otherwise idle, while
mining:

1. Start at 1 thread. Wait about 30 seconds: a change of threads restarts
   RandomX and shows as a dip.
2. Watch Hash rate for another 30 seconds and note a typical value.
3. In Settings, raise **CPU threads** (for example 2, 4, half the cores, all)
   and repeat step 1 and 2 for each.
4. Optional: note CPU use in Task Manager → Performance → CPU, and whether the
   PC still feels responsive.

Report it as a small table:

| Threads | Hash rate (H/s) | CPU % | PC responsive? |
|---|---|---|---|
| 1 | | | |
| 2 | | | |

At low priority the rate also drops whenever other programs are busy.

## 7. Restart, close and reopen

- [ ] Closing the window stops the node cleanly; it doesn't linger in Task
      Manager.
- [ ] Reopening asks for the app password (**Unlock**), then syncs from where
      it was.
- [ ] If the node ever stops by itself, the window says "The node has
      stopped" and offers **Restart** and **Rebuild**. Press **Save log**
      before anything else and send the file.

## 8. Uninstall (optional)

Apps & features → **7F Miner (testnet)** → Uninstall.

- [ ] If the app is open, the uninstaller asks you to close it first.
- [ ] It asks "Also delete your 7F Miner data?" with **No** as the default.
      No keeps `%APPDATA%\7F Miner` (wallet, certificate, chain) for a later
      reinstall. Yes deletes it, and then only your 24 words get you back.

## Reporting

Email Mateo at [mateo@sevenfortunas.com](mailto:mateo@sevenfortunas.com):

- the 7F Miner version, Windows version and antivirus;
- what you did, what you expected and what happened, with screenshots;
- the log: **Save log** writes `sf-miner-gui-log-<time>.txt` into the data
  folder (`%APPDATA%\7F Miner\testnet`) and shows its path.

Never send your 24 words, app password or API key.

What changed in each version: the notes of each release on the
[Releases](https://github.com/Seven-Fortunas/7f-miner-testers/releases)
page.
