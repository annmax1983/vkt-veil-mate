# VKT VeilMate

English | [中文](languages/README_zh.md) | [Español](languages/README_es.md) | [Deutsch](languages/README_de.md) | [日本語](languages/README_ja.md) | [Français](languages/README_fr.md)

A privacy curtain for your browser: one click covers every tab, and unlocking puts everything back exactly as it was — no page reloads, no lost forms, no broken video.

> Chrome · Edge · Firefox · Manifest V3 · Minimal permissions · No tracking · 100% local

---

## Why VKT VeilMate?

You step away for coffee. Someone glances at your screen: half-written email, a bank tab, a private message. You want a blanket to throw over the browser — not a security product.

Existing "browser lock" extensions mostly do one of two things badly:

| Their approach | What goes wrong |
|---|---|
| Navigate every tab to a lock page | Unlocking reloads everything — forms gone, video restarts, SPA state destroyed |
| Promise to "prevent unauthorised access" | A new profile, a private window or the task manager walks straight past it, and the reviews say so |

VKT VeilMate takes the opposite position:

| Our approach | Result |
|---|---|
| **Cover, never navigate** — a shadow-DOM overlay is injected into each page | Unlocking is instant and lossless |
| **Say what it cannot do** — on the settings page and in the store listing | No dashed expectations, no one-star reviews for a promise nobody can keep |
| **No way back in** — no recovery code, no reset endpoint, and the lock survives a browser restart | A curtain you can walk around is not a curtain; forgetting the password means removing the extension, and every screen says so |
| **Honest about its own plumbing** — the extension talks to itself over `chrome.runtime` messages, and anyone who can open DevTools on an extension page can send those messages too | Documented instead of claimed away: the password is the boundary, the biometric shortcut is a convenience on top of it |

---

## Features

### Free, forever

| Feature | Detail |
|---|---|
| One-click lock | Toolbar button and a right-click menu — no keyboard shortcut is registered |
| Exempt list | Up to 10 domains stay readable while everything else is covered |
| Lossless overlay | Every http/https tab is covered in place; nothing reloads |
| Interaction blocking | Clicks, scrolling, typing, drag, copy and context menu are stopped on covered pages, and focus is pulled back out of iframes so keystrokes cannot land in a document behind the curtain |
| New-tab & address-bar trap | New tabs, new windows and typed URLs are caught while locked |
| Password unlock | PBKDF2-SHA256, 310,000 iterations, random salt, constant-time comparison |
| Lock that stays | Lock state lives in `storage.local`; restarting the browser does not clear it |
| No recovery path | Removing the extension in `chrome://extensions` is the only way out of a forgotten password |
| Idle auto-lock | Uses the browser's own idle detection |
| Brute-force cooldown | Five failures → 30 seconds, then 2 min, 10 min, 30 min, capped at one hour. Every password check — unlock *and* change-password — goes through the same counter |
| Hidden tab titles | While locked, the tab strip and window title show a neutral name instead of the page you were reading |
| Big clock | Large lock-screen clock, 12/24-hour, optional date |
| Six languages | English, 中文, 日本語, Deutsch, Español, Français |

### Pro (license required)

| Feature | Detail |
|---|---|
| Targeted lock | Switch the domain list to "cover only…" — lock the intranet, leave everything else readable. Also available from the right-click menu. The free plan is capped at 10 domains and always runs "cover everything except…" |
| Scheduled lock | Cover everything at a fixed time (e.g. 18:00), every day or weekdays only. One-shot alarm, re-armed after each run, so it survives service-worker recycling |
| Quick-unlock window | For a few minutes after a real unlock, locking again can be undone without typing the password. Not extended by the shortcut itself, and always cleared by a browser restart |
| Biometric unlock | Windows Hello / Touch ID via WebAuthn. **A convenience path, not a stronger boundary**: the assertion is verified in the lock page, and the message that opens the lock can be sent by anyone who can open DevTools on an extension page — exactly like the person standing at your keyboard. The password remains the boundary; biometrics only save typing |
| Focus-loss lock | Lock a few seconds after you switch to another app |
| System-lock link | Follow the operating system's screen lock |
| Lock at browser start | Ask for the password the first time the browser opens |
| Privacy curtain | Blur the current page without locking; click to reveal. Also on the right-click menu |
| Decoy page | Covered pages look like an ordinary "this site can't be reached" error instead of an obvious lock screen. The unlock screen itself is unchanged |
| Lock activity log | Local record of unlock attempts on this device, including the password checks made from the change-password form |
| Wallpaper & message | Six built-in gradients or your own image, plus a custom line on the lock screen |
| Cross-device sync | Lock-screen appearance, clock, auto-lock preferences **and the domain list** ride on `chrome.storage.sync` (Chrome via Google, Edge via Microsoft, Firefox via Firefox Sync). Changes are pushed automatically a moment after you make them, and pulled as soon as the other device writes. The password never syncs; an uploaded wallpaper exceeds the 8 KB per-item quota, so only the built-in gradients travel |

---

## What it can and cannot do

This table is also on the settings page. It is the point of the product.

### ✅ It can

| Scenario | How |
|---|---|
| Someone walking past sees your tabs | Every page is covered the instant you lock |
| A colleague clicks around | Clicks, scrolls and keys are intercepted on covered pages |
| "New tab" while locked | `tabs.onCreated` sends it to the lock page |
| A new window (`Ctrl+N`, "open in new window") | `windows.onCreated` + `tabs.onCreated` cover it, including windows restored from a session |
| A new private window | Also covered once you switch on "Allow in Incognito" — the extension ships with `incognito: spanning` |
| Typing a URL while locked | `tabs.onUpdated` intercepts and redirects |
| Refreshing a covered page | The content script re-injects the overlay |
| Walking away without locking | Idle / focus-loss / system-lock triggers (Pro for the last two) |
| Leaving at the same hour every day | Scheduled lock covers everything at the time you set (Pro, weekdays optional) |
| A site you deliberately exempted | The domain list is checked on every lock, every new tab and every navigation — listed domains stay readable while the rest is covered |

### ❌ It cannot

| Bypass | Why |
|---|---|
| Disabling or removing the extension | An extension cannot stop itself from being disabled — and store policy forbids trying |
| Opening a different browser profile or another Windows user | Separate profile, separate extension instance, separate state |
| Ending the browser in the task manager | Process-level actions live outside the extension sandbox |
| Opening DevTools on the lock page and posting the extension's own messages | Extension pages and their DevTools console share the same API access. It is the same class of bypass as disabling the extension: it requires someone who already controls the machine. What it does buy: the attempt counter, the escalating cooldown and the locked-state guard all sit in the background script, so guessing over that path is no faster than typing on the lock screen |
| Someone looking at your actual screen | The overlay covers the browser, not your monitor |
| A link that swaps the address inside an already-open single-page app | `pushState` is not a navigation the browser reports, so the domain list is re-checked on real navigation and on reload, not mid-app. Fixing that needs the `webNavigation` permission |
| Pages with no hostname escaping the exempt list | They are always covered — `chrome://`, `file://`, `about:blank` and local PDFs never honour the list |

> **One sentence:** VKT VeilMate hides your tabs from people. It is not encryption, and it does not defend against someone who controls the machine.

---

## Preview

> 📸 Store artwork and screenshots are kept in [`screenshots/`](screenshots/) — six 1280×800 shots plus the 1400×560 and 440×280 promotional tiles.

| Screenshot | Shows |
|---|---|
| [`01-lock-all-tabs.png`](screenshots/01-lock-all-tabs.png) | One click covers every tab in every window |
| [`02-lock-screen.png`](screenshots/02-lock-screen.png) | Unlocking on the lock screen with the big clock |
| [`03-popup.png`](screenshots/03-popup.png) | The toolbar popup: lock, set password, Pro state |
| [`04-auto-lock-scope.png`](screenshots/04-auto-lock-scope.png) | Idle auto-lock and the domain list (lock scope) |
| [`05-honest.png`](screenshots/05-honest.png) | The "it can / it cannot" panel |
| [`06-security.png`](screenshots/06-security.png) | Password and biometric settings |

---

## Supported Browsers

| Browser | Status | Minimum version | Notes |
|---------|--------|-----------------|-------|
| Google Chrome | ✅ Fully supported | Chrome 116+ | Manifest V3, service worker |
| Microsoft Edge | ✅ Fully supported | Edge 116+ | Same build, chromium-based |
| Other Chromium browsers (Brave, Vivaldi, Opera) | ⚠️ Best effort | Chromium 116+ | Untested; the same APIs are used |
| Mozilla Firefox | ✅ Fully supported | Firefox 121+ | MV3 build maintained in the dedicated Firefox repository |
| Mobile browsers | ❌ Not supported | — | No toolbar to click and no window model to cover |

> **Windows Hello / Touch ID** need the platform's WebAuthn support: Windows 10 1903+ with a PIN or fingerprint reader enrolled, or macOS with Touch ID. The password is always available as a fallback, so a machine without biometrics loses nothing but the convenience.

---

## FAQ

**Does it survive closing the browser?** Yes. The lock state is written to `storage.local`, so the browser opens locked until you unlock it.

**Is it a security product?** No. It hides tabs from people walking past. Someone who controls the machine can disable it in `chrome://extensions`, use another profile or end the browser in the task manager. Every one of those is listed in the store listing too.

**Why is there no password recovery?** A recovery code is a second key, and a second key is a backdoor. The only exit is removing the extension, which is documented on the lock screen itself.

**Is the biometric unlock a second way in?** It is a shortcut, not a second key. The password check lives in the background script, and both places that submit a password — unlock and change-password — go through the same attempt counter and cooldown. The quick-unlock window never checks a password at all: it only works for a few minutes after a real unlock, and records a `quick` entry in the activity log. But if you can open DevTools on an extension page, you can drive the extension's own message API, and no extension can prevent that. Treat biometrics as "less typing", not "more security".

**What happens after the fifth wrong password?** A 30-second pause, then 2 minutes, 10 minutes, 30 minutes, and finally one hour between attempts. The counter is per device and is visible in the activity log.

**Does it upload anything?** No page content, no URLs, no keystrokes, no screenshots. The only outbound request is licence activation or validation.

**Why does the free plan cap the domain list at 10?** The free mode is "cover everything except…" — a short list covers the realistic case (webmail, calendar, one page you are reading). The inverse mode, "cover only…", is what a work laptop needs and is part of Pro.

**Can I use one licence on two browsers?** Yes, one licence activates two browsers, and removing it from one frees that slot again.

---

## Install

| Store | Link |
|---|---|
| Chrome Web Store | — not published yet (use Edge or Firefox) |
| Microsoft Edge Add-ons | [Install for Edge](https://microsoftedge.microsoft.com/addons/detail/cpfboknaflpnbcpajkemmmopkmpfieec) |
| Firefox Add-ons (AMO) | [Install for Firefox](https://addons.mozilla.org/firefox/addon/vkt-veilmate/) |

> Install only from the official stores above.

---

## Usage

1. Click the toolbar icon → **Set password**. There is no recovery code to write down — write the password itself down somewhere safe.
2. Click **Lock now** whenever you step away.
3. Unlock on the lock page with your password or biometrics (Pro).

### If you forget your password

There is exactly one way out: **remove the extension in `chrome://extensions` and install it again.**

That also erases the wallpaper and every setting. There is no recovery code, no reset endpoint, no support email that can unlock you — a lock with a backdoor is not a lock. Closing the browser does not help either: the lock state lives in `storage.local` and is still there after a restart.

The forget-password panel on the lock page links straight to `chrome://extensions/?id=<this extension>` so you are never stuck without an exit.

---

## How it works

```
Trigger (button / idle / focus loss / system lock / startup)
  → lock state written to storage.local (survives a browser restart)
  → for every http(s) tab: tabs.sendMessage({type:'veil:lock'}) → overlay injected
  → for tabs that cannot be injected: remember the URL, tabs.update(lock.html)
  → tabs.onCreated / tabs.onUpdated keep catching anything new
  → windows.onCreated covers Ctrl+N, "open in new window" and private windows
  → chrome://extensions/?id=<self> is the only built-in page let through, so the
    extension can always be removed
Unlock
  → password / WebAuthn verified in the extension page
  → state cleared, overlays removed, replaced tabs restored in place
```

Design decisions worth knowing:

- **Passwords are only typed in extension pages.** A page's own JavaScript never sees the field, so no site can sniff it.
- **Hashing happens in the service worker.** Only `{salt, iter, hash}` is stored; the password itself is never written anywhere.
- **Constant-time comparison.** Hash comparison does not leak timing information.
- **The overlay is a closed shadow root.** Site CSS cannot restyle it, and site scripts that delete it are countered by a MutationObserver.

---

## Privacy

- No analytics, no telemetry, no ads, no accounts.
- No page content, URL, title or keystroke ever leaves the browser.
- Your wallpaper and lock-screen message stay on your device: images you upload are resized and kept in this browser profile, never sent anywhere.
- Cross-device sync (Pro) uses `chrome.storage.sync`, the browser's own sync channel. We have no server in that path and cannot read it. The password is deliberately excluded from sync, and uploaded wallpapers exceed the quota, so only preference fields travel.
- The only network request is license activation / validation, and only if you paste a license key.

- [Full Privacy Policy](https://annmax1983.github.io/vkt-veil-mate/privacy-policy.html)

---

## Permissions

| Permission | Why |
|---|---|
| `storage` | Save settings (hashes only), the persistent lock state, and Pro sync data via `storage.sync` |
| `tabs` | Cover tabs, catch new tabs and typed addresses while locked |
| `windows` | React to window focus changes for the focus-loss lock |
| `idle` | Idle auto-lock |
| `https://api.annmax1983.com/*` | License activation and validation only |

Content scripts run on `http://*/*` and `https://*/*` and do exactly one thing: draw the overlay when the service worker asks them to.

---

## Copyright Disclaimer

1. VKT VeilMate covers the browser's own pages on your own device. It does not modify, store or transmit the content of any website.
2. All page content that ends up behind the curtain remains the property of its publisher, and VKT VeilMate claims no rights over it.
3. Users must comply with local laws and with their employer's device and acceptable-use policies when using this extension.

---

## Source Code Notice

> ⚠️ **This repository is maintained for development and release packaging.** The source code is proprietary and may not be redistributed or repackaged. The extension is distributed through official browser extension stores (Chrome Web Store, Microsoft Edge Add-ons, Firefox Add-ons (AMO)); no offline installation packages are distributed to end users.

---

## License

Copyright © 2026 VKT VeilMate. All rights reserved.

This software is closed-source proprietary software. Without official written authorization, the following are strictly prohibited:
- Decompiling, cracking, or modifying the program code
- Repackaging, redistribution, sharing, or commercial resale
- Embedding the program into other software for bundled distribution

---

## ❤️ Support

**[👉 Get a licence key](https://annmax1983.com/extensions/veilmate)** · **[☕ Buy me a coffee](https://ko-fi.com/annmax?ref=vkt-veil-mate)** · [Source on GitHub](https://github.com/annmax1983/vkt-veil-mate) · [Official website](https://annmax1983.com/)

---

## Links

- **Official website:** https://annmax1983.com/
- **This extension:** https://annmax1983.com/extensions/veilmate
- **Privacy policy:** https://annmax1983.com/privacy
- **Contact:** support@annmax1983.com
- **☕ Support this project (Ko-fi):** https://ko-fi.com/annmax?ref=vkt-veil-mate
