# 7F Miner for Windows: test guide

Thanks for testing 7F Miner! This guide walks you through downloading,
installing and using it, one step at a time, and tells you what you should
see at each step. Tick each box as you go. Whenever something looks
different from what's described, or you're not sure, take a screenshot and
make a note: that's exactly what we want to hear about. You don't need to
fix anything or understand why it happened.

7F Miner runs on the 7fchain **testnet**, a test version of the network.
Testnet coins have no money value, so nothing you do here can lose money.

## Before you start

- **Your PC:** Windows 10 version 22H2 or later, or Windows 11, 64-bit. To
  check, press the Windows key, type `winver` and press Enter.
- **Your API key:** from your invitation email. The app asks for it once.
- **Paper and a pen:** to write down your 24 words (step 4).
- **About an hour,** plus some time to leave it mining if you can.
- **Screenshots:** press **Windows key + Shift + S** and drag over the part
  of the screen you want, then paste it into your email.

### A few words you'll see

| Word | What it means |
|---|---|
| Node | The part of the app that talks to the 7fchain network and keeps a copy of the chain on your PC. |
| Sync | The node downloading the chain from the network until it's up to date. |
| Peers | Other computers on the network your node is connected to. |
| Height | How many blocks your node has. It climbs as it syncs and as new blocks arrive. |
| Mining | Your PC working to add the next block to the chain. |
| Hash rate | How fast your PC is mining, in H/s (hashes per second). Higher is faster. |
| CPU threads | How many parts of your processor mining may use at once. |
| Output | The scrolling text in the app's window that shows what the node is doing. |

## 1. Download

1. Sign in to GitHub with the account that was invited to this repository.
2. Open the
   [Releases](https://github.com/Seven-Fortunas/7f-miner-testers/releases)
   page and find the newest **7F Miner \<version\>** at the top.
3. Under **Assets**, click `7F-Miner-<version>-setup.exe` to download it.
   Ignore the other files. Only use files from this page.

- [ ] Note any warning from your browser or antivirus while downloading:
      write down the exact words or take a screenshot.

**Optional, for the curious:** you can check that the file arrived intact.
Press the Windows key, type `PowerShell` and open it, then type
`Get-FileHash $HOME\Downloads\7F-Miner-<version>-setup.exe` (with the real
version number) and press Enter. The long code it shows should match the
SHA256 in the release notes. Skip this if you prefer; the signature check
below covers it.

## 2. Check the signature

The signature shows the file really comes from Seven Fortunas and wasn't
changed. Before you run it, open your **Downloads** folder, right-click the
setup file, choose **Properties** and open the **Digital Signatures** tab.

- [ ] The tab is there and the list shows **Seven Fortunas Inc**.
- [ ] Select that line and click **Details**: it says "This digital
      signature is OK."
- [ ] In the same window, the **Countersignatures** list shows a timestamp
      (from Microsoft) on the day the build was signed.

You may notice that the certificate (**View Certificate**) is valid for only
about 3 days, and has perhaps already ended. That's normal: the timestamp
proves the certificate was valid when the file was signed, so Windows keeps
accepting it. Only report it if the signature no longer says "OK".

## 3. Install

Double-click the setup file.

- [ ] If Windows shows a prompt, it names **Seven Fortunas Inc** as the
      publisher, not "Unknown publisher".
- [ ] If a blue **"Windows protected your PC"** screen appears, take a
      screenshot for us, then click **More info** → **Run anyway**. It can
      appear while Windows is still getting to know a new app.
- [ ] The first page explains what 7F Miner does: it runs a testnet node,
      mines only after you press Start Mining, and uses the internet.
- [ ] You have to accept the Terms of Use to continue.
- [ ] It installs without asking for an administrator password.
- [ ] Afterwards there's a **7F Miner** entry in the Start menu, and a
      desktop shortcut if you ticked that box, both with the 7F icon.

It installs into `%LOCALAPPDATA%\Programs\7F Miner`. To see that folder,
paste that text into the address bar of File Explorer.

**Installing a newer version later:** if 7F Miner is open, Setup says it
will close it first, then upgrades. Your wallet and data stay.

## 4. First start

7F Miner opens with a short setup. Make sure no one can see your screen.

- [ ] **App password:** choose one and type it twice. You'll type it every
      time you open 7F Miner, so pick one you'll remember.
- [ ] **Your 24 words:** choose *Create a new wallet*. It shows 24 words.
      **Write them on paper only**, not in a file, photo, password manager
      or email. They are the only way back into your wallet if anything
      goes wrong. The app then asks you to type them back. (To use a wallet
      you already have, *Restore from my words* takes its 12 or 24 words
      instead.)
- [ ] **Certificate:** paste your API key and press *Get my certificate*. It
      should finish without an error. The certificate is what allows your
      PC to mine on the testnet.
- [ ] The main window opens, titled **7F Miner (testnet)**.

## 5. Sync and mining

Give the node a few minutes to connect and download the chain.

- [ ] **Peers** goes above 0.
- [ ] **Height** climbs and then keeps up with the number on the
      [7fchain explorer](https://explore.sevenfortunas.com), the website
      that shows the network's latest blocks.
- [ ] Once it's up to date, the output shows a line with
      `[trusted-tip] OK: local chain == consensus tip`.
- [ ] Nothing mines until you press **Start Mining**. Until then the status
      says "not mining; the node keeps syncing".
- [ ] Press **Start Mining**. The output shows `RandomX ready.` and then
      `mining block <number>...`, and **Hash rate** goes above 0. (RandomX
      is the mining method; getting ready can take a moment.)
- [ ] As new blocks arrive, the output moves on to the next
      `mining block` line.
- [ ] Press **Stop Mining**: mining stops, and the node keeps syncing.

These lines in the output are normal and can be ignored: `already have it`,
`duplicate block`, and a single `our height ... is AHEAD of trusted peer
max ...` just after syncing.

**Tell us** if you see lines with `error`, `rejected`, `banned`, `diverge`
or `rollback`, if Height stops climbing while the explorer's keeps going,
or if your PC becomes slow.

## 6. Settings

Open the app's **Settings** page.

- [ ] **Version** shows `7F Miner <version> (testnet)`, the same version as
      the file you downloaded.
- [ ] Changing **CPU threads** or the priority changes mining straight away
      (watch Hash rate). It starts at 1 thread, at low priority so your
      other programs come first. Try more threads below.
- [ ] **Show my 24 words** asks for your app password and then shows the
      same words you wrote down.
- [ ] Optional: **Rebuild** asks for your app password and then downloads
      the whole chain again from the start.

### Hash rate with more threads

This helps us see how mining behaves on different PCs. Hash rate jumps
around from second to second, so look for a typical value. Close other
programs first, and keep mining on.

1. In Settings, set **CPU threads** to 1. Wait about 30 seconds: each change
   restarts mining, so Hash rate dips for a moment.
2. Watch Hash rate for another 30 seconds and write down a typical value.
3. Repeat with more threads, for example 2, 4, half of your processor's
   threads, then all of them. To see how many your processor has, open
   Task Manager (**Ctrl + Shift + Esc**) → **Performance** → **CPU** and
   look at **Logical processors**.
4. Optional: on that same Task Manager page, note the CPU use (%), and
   whether your PC still feels responsive.

Send it to us as a small table, like this:

| Threads | Hash rate (H/s) | CPU % | PC responsive? |
|---|---|---|---|
| 1 | | | |
| 2 | | | |

At low priority, Hash rate also drops whenever other programs are busy.
That's expected.

## 7. Close and reopen

- [ ] Close the 7F Miner window. It closes completely: it doesn't stay in
      Task Manager's list of running apps.
- [ ] Open 7F Miner again. It asks for your app password (**Unlock**), then
      carries on syncing from where it was.
- [ ] If the node ever stops by itself, the window says "The node has
      stopped" and offers **Restart** and **Rebuild**. Press **Save log**
      first, before anything else, and send us the file.

## 8. Uninstall (optional)

Open Windows **Settings** → **Apps** → **Installed apps** (on Windows 10:
**Apps & features**), find **7F Miner (testnet)**, and choose
**Uninstall**.

- [ ] If 7F Miner is open, the uninstaller asks you to close it first.
- [ ] It asks "Also delete your 7F Miner data?", with **No** already
      selected. **No** keeps your wallet, certificate and chain (in
      `%APPDATA%\7F Miner`) for a later reinstall. **Yes** deletes them;
      after that, only your 24 words get your wallet back.

## Reporting

Email Mateo at [mateo@sevenfortunas.com](mailto:mateo@sevenfortunas.com).
Short notes are fine. Please include:

- the 7F Miner version, your Windows version (from `winver`) and your
  antivirus, if you know it (otherwise "Windows Security");
- what you did, what you expected and what happened, with screenshots;
- the log file: **Save log** creates a file named
  `sf-miner-gui-log-<time>.txt` and shows where it saved it (in
  `%APPDATA%\7F Miner\testnet`). Attach that file to your email.

**Never send your 24 words, app password or API key**, to us or anyone.

What changed in each version: see the notes of each release on the
[Releases](https://github.com/Seven-Fortunas/7f-miner-testers/releases)
page.
