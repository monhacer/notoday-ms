<p align="right">
  <a href="README.md">English</a> | 
  <a href="READMEfa.md">فارسی</a>
</p>

# notoday-ms 😌🛑

> _“Not today, Microsoft. Not today.”_

**notoday-ms** is a tiny, no-nonsense Windows Registry tweak that politely (and persistently) tells Windows Update to take a **very long vacation** — roughly 20 years.

Because sometimes… you just want your OS to chill.

---

## 🧠 What does this do?

This project applies two simple registry changes:

1. **Extends the maximum Windows Update pause limit**
   - From “a few weeks”  
   - To **~7,300 days (≈ 20 years)**

2. **Disables automatic Windows Updates via Group Policy**
   - No surprise downloads  
   - No random reboots  
   - No “Updating… 30%” at the worst possible moment

---

## 🔧 How it works

The registry file modifies the following keys:

- `FlightSettingsMaxPauseDays`  
  Allows Windows Update to be paused for an absurdly long time.

- `NoAutoUpdate`  
  Disables automatic update behavior system-wide.

Windows Update isn’t destroyed — it’s just… **politely ignored**.

---

## 📦 Installation

1. Download or clone this repository
2. Double-click `justclickme.reg`
   - Or right-click → **Run as administrator**
3. Click **Yes** when Registry Editor asks if you’re sure  
   (you are)
4. (Optional but recommended) Restart Windows

To actually pause updates:
- `Settings → Windows Update → Pause updates`
  
Now enjoy your 20-year pause.

---

## 🔄 Can I still update manually?

Yes.  
You’re in control now.

- Manual updates still work
- Microsoft Store usually still works
- Windows Defender may still receive signature updates

This project blocks **automatic chaos**, not your freedom.

---

## ⚠️ Important Notes

- Works best on **Windows Pro / Enterprise**
- Feature Updates may reset policies (thanks, Microsoft)
- Future Windows versions may ignore this entirely
- Use at your own risk — you break it, you own it

---

## 🔙 Undo / Restore Windows Updates

Changed your mind? Microsoft won? It’s okay.

To undo everything and restore default Windows Update behavior:

1. Download **`undo.reg`**
2. Double-click it (or right-click → **Run as administrator**)
3. Confirm the Registry prompt
4. Restart Windows

That’s it. No drama.

---

## 🤡 Why does this exist?

Because:
- Forced updates are annoying
- “Restart required” is a threat
- Control should belong to the user

**notoday-ms** doesn’t hate Windows.  
It just sets boundaries.

---

## 🪪 License

Do whatever you want.  
Seriously. Microsoft probably will anyway.

---

> _Built with love, sarcasm, and registry keys._
