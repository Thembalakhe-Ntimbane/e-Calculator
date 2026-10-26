# e-Panic Calculator (eCalculator)
**404 PayNotFound – FNB AOTY Hackathon 2026**

A fully working calculator that hides a personal-safety toolkit for people at risk of gender-based violence.
Java, Android 7.0+ (API 24+), one dependency (`androidx.security:security-crypto`)


## Secret code & access
| Item | Value |
|---|---|
| Default secret code | **`1379`** |
| How to open | On the calculator type the code (digits only), then **double-tap the 🕘 history button** |
| First login | The app forces you to choose your own 4–8 digit code. `1379` is then rejected. |
| Lock-out | 5 wrong codes → silent 30 s+ lock-out (doubles each time, max 1 h). The calculator keeps working normally. |
| Single tap on 🕘 | Shows normal calculator history (memory only) |
| Quick exit | Cover the screen / phone face-down / screen off → back to calculator, session locked |

**Change the default code before every public release** (`Pin.DEFAULT`) – a code published in a README is only safe because the app forces a change.

## Features
- Calculator: + − × ÷ % ± ⌫ AC, decimal, history, safe parser (no `eval`).
- Dashboard (order): shortcuts bar (history/back, **❓ Safety tips**, **ℹ️ How to use**) → profile name → Location / Audio / Video → **Evidence** → **Emergency contacts** → **Pattern insights** → language & code.
- **Safety tips**: YouTube-style icon cards + SA help-line buttons (opens dialer, you press call).
- **How to use**: 7 big-icon steps, short sentences for ages 10+. Shown automatically once.
- **Languages**: English, Afrikaans, isiZulu, isiXhosa (pre-translated, `res/values-*`). 
- **Location (power ×3 or tap)**: SMS with an OpenStreetMap link to up to 5 contacts, refreshed every 2 min for 45 min. Uses the phone's normal SMS – **no data, no server, no cost to the receiver**. Contains your profile name. Signal has no public API for automated sending, so it is not used.
- **Audio (volume-up ×3 or tap)**: AAC mono 16 kHz 24 kbps ≈ 10 MB/hour, encrypted, in-app only.
- **Video (volume-down ×3 or tap)**: front + back cameras, H.264 ~480×360 @15 fps 300 kbps, audio AAC 32 kbps. Played back **stacked 50/50 (front on top)**.
- Every item carries **timestamp, caption (`TYPE | date time zone | loc lat,lon` or `0,0`), SHA-256**, and a spoofed-GPS flag.
- Status notifications read only “System is searching/downloading/installing for updates (L/A/V)” with the **E** icon.

## Build & install (APK)
1. Download APK
2. Install APK. (If Playstore flags app as dangerous please disable play store before installing 
3. Use App

## Honest platform limits (read before relying on it)
| Wish | Reality on Android |
|---|---|
| Power button ×3 | Apps cannot read the power key. We detect **3 screen on/off events in 3 s** via a foreground service. Works well; can false-trigger rarely. |
| Volume ×3 while locked / app closed | Needs the Accessibility service enabled (user does this once). Some OEMs (Xiaomi, Huawei, Samsung battery savers) kill it – test per brand. |
| Camera/mic started from background | Android 12–14 restrict this. Recording started from the dashboard always works; from the volume shortcut it may be blocked on some versions/OEMs. **Test on your target phones.** Fallback: shortcut opens dashboard. |
| “Permissions permanent” | Android lets users revoke at any time. App re-asks on every dashboard open and sends to Settings if blocked. |
| Dual camera | Needs Android 11+ **and** hardware that supports concurrent cameras; otherwise back camera only. A single merged top/bottom MP4 would need an OpenGL/MediaCodec compositor (roadmap); today the stack is done at playback. |
| “Live link” | No server exists, so “live” = a fresh SMS link every 2 min. A real tracking page would need a backend. |
| Cross-platform | One Java APK runs on all Android 7+ devices. iOS cannot run Java/APK and also forbids most of these background features. |
| Non-obvious notification | Android *requires* a visible notification for background camera/mic/location. We disguise the text; we cannot remove it. |

## Ads
Ads on a covert safety app create network traffic, identifiers and a visible third-party SDK, which can **expose the app or the user**. 



## Project layout
```
app/src/main/java/com/pnf/ecalc/   CalcActivity, DashboardActivity, InfoActivity, ContactsActivity, EvidenceActivity,
                                   TriggerService, KeyShortcutService, LocationAlertService, AudioRecordService, VideoRecordService,
                                   Pin, Store, EvidenceStore, Audit, Integrity, PanicExit, Sms, Loc, Disguise, Lang, ...
app/src/main/res/values{,-af,-zu,-xh}/strings.xml
docs/SSDLC.md
```
## Legal / ethics
Use only on your own device with consent of the person at risk. Verify help-line numbers (`InfoActivity.LINES`) each release. Not a replacement for emergency services (SAPS 10111).
