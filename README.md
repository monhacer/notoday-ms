<p align="right">
  <a href="README.md">English</a> | 
  <a href="READMEfa.md">فارسی</a>
</p>

# notoday-ms 😌🛑

> _"Not today, Microsoft. Not today."_

**notoday-ms** is a tiny, no-nonsense Windows Registry tweak that politely (and persistently) tells Windows Update to take a **very long vacation** — roughly 20 years.

Because sometimes… you just want your OS to chill.

---

## 🧠 What does this do?

This project ships **two registry files**, each tailored to a different generation of Windows Update UI:

| File | Target Windows Versions | UI Type |
|------|------------------------|---------|
| `justclickme.reg` | Windows 10 / 11 (older builds) | **Dropdown Selector** (days-based pause) |
| `not-again.reg` | Windows 11 26H1 Build 28000+ | **Date Picker** (calendar-based pause) |

Both files apply the same core idea — extend the maximum pause duration and disable auto-updates — but they use different registry strategies because Microsoft changed how the Pause feature works.

---

## 📦 Which file should I use?

### 🟢 `justclickme.reg` — For builds with **Dropdown Selector**

Use this if:

- Your Windows Update pause menu shows a **dropdown list** (e.g., "Pause for 1 week, 2 weeks, … 5 weeks")
- You're on Windows 10, Windows 11 21H2 / 22H2 / 23H2 / 24H2, or early 25H2 builds

**What it does:**

- `FlightSettingsMaxPauseDays` → extends max pause to **~7,300 days (≈ 20 years)**
- `NoAutoUpdate` → disables automatic update behavior system-wide

After applying, you'll see a **much longer pause option** in the dropdown.

---

### 🔵 `not-again.reg` — For builds with **Date Picker**

Use this if:

- Your Windows Update pause menu shows a **calendar / date picker** (like the one in Build 28000)
- You're on Windows 11 26H1 Build 28000 or newer
- The old `FlightSettingsMaxPauseDays` trick no longer works for you

**What it does:**

- Writes **explicit start and end dates** directly into the pause keys
- Still sets `NoAutoUpdate` as a safety net

---

## 🔧 Registry Keys Used

### For `justclickme.reg` (Dropdown Selector)

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsUpdate\UX\Settings
    FlightSettingsMaxPauseDays = dword:00001c84

HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU
    NoAutoUpdate = dword:00000001
```

### For `not-again.reg` (Date Picker)

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsUpdate\UX\Settings
    PauseFeatureUpdatesStartTime = "2026-09-29T00:00:00Z"
    PauseFeatureUpdatesEndTime   = "2046-12-31T00:00:00Z"
    PauseQualityUpdatesStartTime = "2026-09-29T00:00:00Z"
    PauseQualityUpdatesEndTime   = "2046-12-31T00:00:00Z"
    PauseUpdatesStartTime        = "2026-09-29T00:00:00Z"
    PauseUpdatesExpiryTime       = "2046-12-31T00:00:00Z"
    FlightSettingsMaxPauseDays   = dword:00002727

HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU
    NoAutoUpdate = dword:00000001
```

---

## 📄 Full Registry File Contents

### `justclickme.reg`

```registry
Windows Registry Editor Version 5.00

; -------------------------------------------------
; Windows Update UX Settings
; Extend maximum pause duration (~20 years)
; For builds with Dropdown Selector
; -------------------------------------------------
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsUpdate\UX\Settings]
"FlightSettingsMaxPauseDays"=dword:00001c84

; -------------------------------------------------
; Disable Automatic Windows Updates (Policy)
; -------------------------------------------------
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU]
"NoAutoUpdate"=dword:00000001
```

### `not-again.reg`

```registry
Windows Registry Editor Version 5.00

; -------------------------------------------------
; Windows Update UX Settings
; Pause until 2046 using explicit dates
; For builds with Date Picker (26H1 Build 28000+)
; -------------------------------------------------
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsUpdate\UX\Settings]
"PauseFeatureUpdatesStartTime"="2026-09-29T00:00:00Z"
"PauseFeatureUpdatesEndTime"="2046-12-31T00:00:00Z"
"PauseQualityUpdatesStartTime"="2026-09-29T00:00:00Z"
"PauseQualityUpdatesEndTime"="2046-12-31T00:00:00Z"
"PauseUpdatesStartTime"="2026-09-29T00:00:00Z"
"PauseUpdatesExpiryTime"="2046-12-31T00:00:00Z"
"FlightSettingsMaxPauseDays"=dword:00002727

; -------------------------------------------------
; Disable Automatic Windows Updates (Policy)
; -------------------------------------------------
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU]
"NoAutoUpdate"=dword:00000001
```

---

## 📦 Installation

1. Download or clone this repository
2. Pick the right file for your Windows version:
   - **Dropdown Selector** → `justclickme.reg`
   - **Date Picker** → `not-again.reg`
3. Double-click the file
   - Or right-click → **Run as administrator**
4. Click **Yes** when Registry Editor asks if you're sure  
   (you are)
5. (Optional but recommended) Restart Windows

To actually pause updates:

- **Dropdown version:** `Settings → Windows Update → Pause updates` → pick the longest option
- **Date Picker version:** `Settings → Windows Update → Pause updates` → the end date should already be set far in the future

---

## 🔄 Can I still update manually?

Yes.  
You're in control now.

- Manual updates still work
- Microsoft Store usually still works
- Windows Defender may still receive signature updates

This project blocks **automatic chaos**, not your freedom.

---

## ⚠️ Important Notes

- Works best on **Windows Pro / Enterprise**
- Feature Updates may reset policies (thanks, Microsoft)
- **Build 28000+**: Microsoft may ignore `FlightSettingsMaxPauseDays` — use `not-again.reg` instead
- **Future Windows versions** may ignore all of this entirely
- Use at your own risk — you break it, you own it

---

## 🔙 Undo / Restore Windows Updates

Changed your mind? Microsoft won? It's okay.

To undo everything and restore default Windows Update behavior:

1. Download **`undo.reg`**
2. Double-click it (or right-click → **Run as administrator**)
3. Confirm the Registry prompt
4. Restart Windows

That's it. No drama.

---

## 🤡 Why does this exist?

Because:

- Forced updates are annoying
- "Restart required" is a threat
- Control should belong to the user
- **Microsoft keeps changing the rules** — so we keep changing the registry

**notoday-ms** doesn't hate Windows.  
It just sets boundaries.

---

## 🪪 License

Do whatever you want.  
Seriously. Microsoft probably will anyway.

---

> _Built with love, sarcasm, and registry keys._
