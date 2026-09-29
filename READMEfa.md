<p align="right">
  <a href="README.md">English</a> | 
  <a href="READMEfa.md">فارسی</a>
</p>

# notoday-ms 😌🛑

> _«امروز نه، مایکروسافت. امروز نه.»_

**notoday-ms** یک توییک کوچک و بی‌حاشیه در رجیستری ویندوز است که مؤدبانه (و با اصرار) به Windows Update می‌گوید به یک **تعطیلات خیلی طولانی** برود — حدوداً ۲۰ سال.

چون بعضی وقت‌ها… فقط می‌خواهی سیستم‌عاملت حالش را ببرد.

---

## 🧠 این پروژه چه کاری انجام می‌دهد؟

این پروژه **دو فایل رجیستری** ارائه می‌دهد که هرکدام برای نسل متفاوتی از رابط کاربری Windows Update طراحی شده‌اند:

| فایل | نسخه‌های هدف ویندوز | نوع رابط کاربری |
|------|---------------------|------------------|
| `justclickme.reg` | ویندوز ۱۰ / ۱۱ (بیلدهای قدیمی‌تر) | **لیست کشویی** (توقف بر اساس تعداد روز) |
| `not-again.reg` | ویندوز ۱۱ ۲۶H۱ بیلد ۲۸۰۰۰ به بالا | **تقویم انتخاب تاریخ** (توقف بر اساس تاریخ) |

هر دو فایل ایده اصلی یکسانی دارند — افزایش حداکثر مدت توقف و غیرفعال‌سازی آپدیت خودکار — اما از استراتژی‌های رجیستری متفاوتی استفاده می‌کنند، چون مایکروسافت نحوه کارکرد قابلیت Pause را تغییر داده است.

---

## 📦 کدام فایل را استفاده کنم؟

### 🟢 `justclickme.reg` — برای بیلدهای دارای **لیست کشویی**

از این فایل استفاده کن اگر:

- منوی توقف Windows Update تو یک **لیست کشویی** نشان می‌دهد (مثلاً «توقف برای ۱ هفته، ۲ هفته، … ۵ هفته»)
- روی ویندوز ۱۰، ویندوز ۱۱ ۲۱H۲ / ۲۲H۲ / ۲۳H۲ / ۲۴H۲ یا بیلدهای اولیه ۲۵H۲ هستی

**چه کاری انجام می‌دهد:**

- `FlightSettingsMaxPauseDays` → حداکثر مدت توقف را به **حدود ۷,۳۰۰ روز (≈ ۲۰ سال)** افزایش می‌دهد
- `NoAutoUpdate` → رفتار آپدیت خودکار را در کل سیستم غیرفعال می‌کند

بعد از اعمال، یک **گزینه توقف خیلی طولانی‌تر** در لیست کشویی خواهی دید.

---

### 🔵 `not-again.reg` — برای بیلدهای دارای **تقویم انتخاب تاریخ**

از این فایل استفاده کن اگر:

- منوی توقف Windows Update تو یک **تقویم / انتخاب‌گر تاریخ** نشان می‌دهد (مثل همان که در بیلد ۲۸۰۰۰ هست)
- روی ویندوز ۱۱ ۲۶H۱ بیلد ۲۸۰۰۰ یا جدیدتر هستی
- ترفند قدیمی `FlightSettingsMaxPauseDays` دیگر برایت کار نمی‌کند

**چه کاری انجام می‌دهد:**

- **تاریخ شروع و پایان صریح** را مستقیماً در کلیدهای توقف می‌نویسد
- همچنان `NoAutoUpdate` را به‌عنوان تور اطمینان تنظیم می‌کند

---

## 🔧 کلیدهای رجیستری استفاده‌شده

### برای `justclickme.reg` (لیست کشویی)

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsUpdate\UX\Settings
    FlightSettingsMaxPauseDays = dword:00001c84

HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU
    NoAutoUpdate = dword:00000001
```

### برای `not-again.reg` (تقویم انتخاب تاریخ)

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

## 📄 محتوای کامل فایل‌های رجیستری

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

## 📦 نصب

۱. این مخزن را دانلود یا کلون کن
۲. فایل مناسب نسخه ویندوزت را انتخاب کن:
   - **لیست کشویی** → `justclickme.reg`
   - **تقویم انتخاب تاریخ** → `not-again.reg`
۳. روی فایل دوبار کلیک کن
   - یا راست‌کلیک → **Run as administrator**
۴. وقتی Registry Editor پرسید مطمئنی، روی **Yes** کلیک کن
   (مطمئنی)
۵. (اختیاری اما توصیه‌شده) ویندوز را ری‌استارت کن

برای اینکه واقعاً آپدیت‌ها متوقف شوند:

- **نسخه لیست کشویی:** `Settings → Windows Update → Pause updates` → طولانی‌ترین گزینه را انتخاب کن
- **نسخه تقویم:** `Settings → Windows Update → Pause updates` → تاریخ پایان باید از قبل روی تاریخ دوری تنظیم شده باشد

---

## 🔄 آیا هنوز می‌توانم دستی آپدیت کنم؟

بله.
الان کنترل دست خودت است.

- آپدیت‌های دستی همچنان کار می‌کنند
- Microsoft Store معمولاً همچنان کار می‌کند
- Windows Defender ممکن است همچنان آپدیت‌های امضای خود را دریافت کند

این پروژه جلوی **هرج‌ومرج خودکار** را می‌گیرد، نه آزادی تو را.

---

## ⚠️ نکات مهم

- بهترین عملکرد روی **Windows Pro / Enterprise**
- Feature Updateها ممکن است سیاست‌ها را بازنشانی کنند (ممنون، مایکروسافت)
- **بیلد ۲۸۰۰۰+**: ممکن است مایکروسافت `FlightSettingsMaxPauseDays` را نادیده بگیرد — از `not-again.reg` استفاده کن
- **نسخه‌های آینده ویندوز** ممکن است همه این‌ها را کاملاً نادیده بگیرند
- با مسئولیت خودت استفاده کن — خرابش کردی، مال خودت است

---

## 🔙 بازگردانی / برگرداندن Windows Update

نظرت عوض شد؟ مایکروسافت برد؟ اشکالی ندارد.

برای برگرداندن همه چیز و بازگرداندن رفتار پیش‌فرض Windows Update:

۱. فایل **`undo.reg`** را دانلود کن
۲. روی آن دوبار کلیک کن (یا راست‌کلیک → **Run as administrator**)
۳. پیام Registry را تأیید کن
۴. ویندوز را ری‌استارت کن

همین. بدون دردسر.

---

## 🤡 چرا این پروژه وجود دارد؟

چون:

- آپدیت‌های اجباری آزاردهنده‌اند
- «Restart required» یک تهدید است
- کنترل باید متعلق به کاربر باشد
- **مایکروسافت مدام قوانین را عوض می‌کند** — پس ما مدام رجیستری را عوض می‌کنیم

**notoday-ms** از ویندوز متنفر نیست.
فقط مرز تعیین می‌کند.

---

## 🪪 مجوز

هر کاری می‌خواهی بکن.
جدی می‌گویم. مایکروسافت هم احتمالاً همین کار را خواهد کرد.

---

> _ساخته‌شده با عشق، طعنه، و کلیدهای رجیستری._
