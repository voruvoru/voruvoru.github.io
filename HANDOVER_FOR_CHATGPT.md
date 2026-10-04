# 🌸 CHIBI WIBU ART — PROJECT HANDOVER DOC
> Dibuat dari sesi Claude Code. Bawa dokumen ini ke ChatGPT sebagai konteks awal.

---

## 1. IDENTITAS PROYEK

| Field | Value |
|---|---|
| Nama Bisnis | Chibi Wibu Art |
| Owner email | rrudiawan@gmail.com |
| Hosting | GitHub Pages (static) |
| Stack | HTML + CSS + JS murni (no backend, no PHP, no DB) |
| Currency | USD via PayPal Business |
| Target audiens | VTuber, streamer, anime fans (pasar internasional, bahasa Inggris) |

---

## 2. FILE YANG ADA SEKARANG

```
chibi-wibu-v4/
├── index.html        ← SATU FILE UTAMA (all-in-one: HTML + CSS + JS)
│                        2500+ baris, ~120KB
├── tos.html          ← Terms of Service
├── privacy.html      ← Privacy Policy
├── license.html      ← License terms
└── README.md         ← Panduan setup PayPal + Formspree
```

> **Output final:** `index.html` adalah file yang dibawa ke ChatGPT / GitHub Pages.

---

## 3. DESAIN SISTEM (Design System)

### Palet Warna
```css
--pink:      #FF6B9D   /* aksen utama */
--pink-hot:  #E8457A   /* hover/aktif */
--pink-soft: #FFB7C5
--lavender:  #C9B8FF
--sky:       #A1C4FD
--gold:      #FFD166
--txt:       #4A3550   /* teks utama */
--txt-soft:  #6B5073
--txt-muted: #9B89A0
--white:     #FFFFFF
```

### Font
- **Display/Heading:** Nunito 900 (Google Fonts)
- **Body:** Quicksand (Google Fonts)

### Background
- 4 animated blobs (`drift1`–`drift4` CSS keyframes)
- Noise SVG overlay untuk tekstur halus

### Glassmorphism
```css
.glass-card {
  background: rgba(255,255,255,.55);
  backdrop-filter: blur(16px) saturate(160%);
  border-radius: 20px;
}
```

### Scroll Reveal
- Class `.reveal` + `.is-visible` via IntersectionObserver JS
- Stagger delay via CSS variable `--d`

---

## 4. STRUKTUR SECTION (urutan dari atas ke bawah)

```
1. Hero
2. Gallery Slideshow (horizontal scroll-snap, panah prev/next, dots, swipe)
3. Commissions + Order Form
4. Digital Shop
5. Tools / Affiliate Strip
6. Affiliates (12-card grid, 6 kategori, filter tab)
7. Support (Ko-fi, Patreon, KaryaKarsa, sosmed)
8. Partner Spotlight (3 slot branded partnership)
9. News (Rosuuri style, 4-col grid, load more "...")
10. Articles / SEO (3 artikel, tag system)
11. Footer
```

---

## 5. FITUR YANG SUDAH DIIMPLEMENTASIKAN

### ✅ Gallery Slideshow
- Horizontal scroll-snap (`scroll-snap-type: x mandatory`)
- Tombol panah `#slidePrev` / `#slideNext`
- Dot indicators `#slideDots`
- Keyboard arrows support
- Touch swipe support
- Card width: `clamp(280px, 40vw, 420px)`

### ✅ Commission Form (`#commissionForm`)
Fields:
- Name / Discord Handle
- Email Address
- **WhatsApp Number** (field baru, dengan WA-styled prefix hijau, pattern digits only)
- Commission Tier (select)
- Character Description (textarea)
- Reference Image upload (max 25MB)
- Extra Notes

Action: `https://formspree.io/f/YOUR_FORM_ID` (TODO: ganti)

JS: AJAX via `fetch()`, tampilkan `.fstatus` success/error

### ✅ Notifikasi WhatsApp Owner (CallMeBot)
Setelah form submit berhasil → kirim WA ke nomor owner via CallMeBot API.
**Setup:**
1. WhatsApp ke `+34 644 59 78 71` → kirim: `I allow callmebot to send me messages`
2. Tunggu reply berisi API KEY
3. Isi di `index.html`:
   - `OWNER_WA = '6281234567890'` (nomor WA owner)
   - `CALLMEBOT_APIKEY = 'XXXXXX'`

Format pesan yang diterima owner:
```
🎨 NEW ORDER — Chibi Wibu Art
👤 Name   : [nama pemesan]
📦 Tier   : [tier yang dipilih]
📱 WA     : [nomor WA pemesan]
✉️ Email  : [email pemesan]
⏰ Time   : [waktu WIB]
👉 Check Formspree inbox for details.
```

### ✅ Email Notif Owner (Formspree)
- Otomatis dari Formspree ke `rrudiawan@gmail.com`
- Aktifkan di dashboard formspree.io → Settings → Notifications

### ✅ PayPal Smart Buttons
7 tombol total:
| ID | Harga |
|---|---|
| `#paypal-headshot` | $30 |
| `#paypal-halfbody` | $50 |
| `#paypal-fullbody` | $70 |
| `#paypal-shop1` | $12 |
| `#paypal-shop2` | $5 |
| `#paypal-shop3` | $8 |
| `#paypal-shop4` | $10 |

Style: `color:'pink', shape:'pill', label:'buynow', height:38`

### ✅ Affiliate System (4 lapisan)
1. Section `#affiliates` — 12 card, 6 kategori, filter tabs
2. Featured hero banner (Wacom)
3. Inline strip di sidebar order form
4. Footer quick links

### ✅ Partner Spotlight (`#partner-spotlight`)
- 3 card sejajar (grid 3 kolom)
- Semua masih `.empty` (slot tersedia)
- **Cara aktifkan:** ganti `<div class="ps-card empty">` → `<a href="..." class="ps-card live">`, hapus `.ps-slot-label`

### ✅ News Section (`#news`)
- Rosuuri style: 4-col photo grid, tanggal kecil, judul clean
- Gold italic "News" wordmark kanan atas
- 8 cards: 4 visible, 4 `.hidden-news` (reveal via "..." button)
- JS: toggle show/collapse

### ✅ Articles SEO (`#articles`)
- 3 artikel dengan multi-tag: `.a-tag.geo` / `.cat` / `.tip` / `.news`
- Judul SEO-optimized untuk keyword VTuber/chibi

### ✅ Fitur Lainnya
- Proteksi gambar: `oncontextmenu`, `dragstart` prevention
- Lightbox: `#lightbox`, keyboard Esc, click-outside close
- Tip Jar: fixed bottom-right `☕ Tip Me` → ko-fi
- Toast notification: `showToast()` untuk PayPal success/error
- Mobile nav: hamburger `#navBurger`
- Custom scrollbar: pink→lavender gradient
- Scroll reveal: IntersectionObserver
- Print-on-Demand banner → Redbubble

---

## 6. TODO — SEMUA PLACEHOLDER YANG HARUS DIGANTI

| Placeholder di index.html | Ganti dengan |
|---|---|
| `YOUR_CLIENT_ID` | PayPal Live Client ID dari developer.paypal.com |
| `YOUR_FORM_ID` | Formspree form ID dari formspree.io |
| `YOUR_CALLMEBOT_APIKEY` | API key dari CallMeBot (gratis) |
| `6281234567890` (OWNER_WA) | Nomor WA owner sebenarnya |
| `YOUR_WACOM_AFFILIATE_LINK` | Amazon Associates link Wacom |
| `YOUR_CLIPSTUDIO_AFFILIATE_LINK` | Clip Studio affiliate link |
| `YOUR_IPAD_AFFILIATE_LINK` | Amazon iPad link |
| `YOUR_PROCREATE_AFFILIATE_LINK` | Apple affiliate Procreate |
| `YOUR_AMAZON_GENERAL_LINK` | Amazon art supplies list |
| `YOUR_REDBUBBLE` | Username Redbubble |
| Semua handle `chibiwibuart` di sosmed | URL sosmed yang sebenarnya |
| Partner Spotlight 3 slots | Aktifkan saat partnership dikonfirmasi |

---

## 7. TODO — ASET YANG BELUM ADA

- [ ] Semua `.art-placeholder` div → ganti dengan `<img data-src="assets/...">` format WebP
- [ ] `og-preview.webp` 1200×630px untuk social sharing meta
- [ ] Folder `assets/` dengan artwork nyata
- [ ] `favicon.ico` di root
- [ ] Halaman artikel individu di folder `articles/`
- [ ] Halaman berita individu di folder `news/`

---

## 8. PANDUAN SETUP (untuk ChatGPT / developer lanjutan)

### A. Setup Formspree
1. Daftar di formspree.io
2. Create new form → copy Form ID (format: `xyzabcde`)
3. Ganti `YOUR_FORM_ID` di `index.html` dengan ID tersebut
4. Di dashboard Formspree → Settings → Notifications → aktifkan email ke rrudiawan@gmail.com

### B. Setup PayPal
1. Login ke developer.paypal.com
2. My Apps & Credentials → Create App
3. Copy Client ID (live, bukan sandbox)
4. Ganti `YOUR_CLIENT_ID` di script tag PayPal SDK

### C. Setup WhatsApp Notif Owner (CallMeBot — GRATIS)
1. Simpan nomor `+34 644 59 78 71` di kontak WA
2. Kirim pesan: `I allow callmebot to send me messages`
3. Tunggu balasan berisi APIKEY
4. Isi `OWNER_WA` dan `CALLMEBOT_APIKEY` di blok JS Formspree di `index.html`

### D. Deploy ke GitHub Pages
1. Buat repo baru di github.com (nama: `chibiwibuart` atau sesuai domain)
2. Upload semua file (index.html, tos.html, privacy.html, license.html)
3. Settings → Pages → Branch: main, folder: / (root)
4. Aktif di `https://USERNAME.github.io/REPO/`
5. Custom domain: Settings → Pages → Custom domain → masukkan domain .com/.art

---

## 9. MONETISASI PASIF — STATUS

| Stream | Status |
|---|---|
| Google AdSense | Slot HTML sudah ada (`.ad-slot`), belum diisi kode AdSense |
| Affiliate Amazon/Wacom | Slot sudah ada, link masih placeholder |
| Partner Spotlight | 3 slot siap, semua masih kosong |
| Digital Shop PayPal | Sudah aktif (4 produk), harga perlu disesuaikan |
| Ko-fi Tip Jar | Link mengarah ke `ko-fi.com/chibiwibuart` (perlu konfirmasi handle) |
| Patreon | Link mengarah ke `patreon.com/chibiwibuart` (perlu konfirmasi) |
| KaryaKarsa | Link mengarah ke `karyakarsa.com/chibiwibu` (perlu konfirmasi) |
| Redbubble PoD | Banner ada, username masih `YOUR_REDBUBBLE` |

---

## 10. PROMPT UNTUK CHATGPT

Salin prompt berikut sebagai pesan pertama ke ChatGPT, lalu lampirkan `index.html`:

---

```
Halo ChatGPT. Saya sedang memindahkan proyek "Chibi Wibu Art" ke sini.
Saya memiliki situs portofolio + e-commerce statis (GitHub Pages, HTML/CSS/JS murni).

KONTEKS BISNIS:
- Nama: Chibi Wibu Art | Owner: rrudiawan@gmail.com
- Target: VTuber, streamer, anime fans (pasar internasional, bahasa Inggris)
- Monetisasi: komisi custom, digital shop, affiliate, AdSense, tip jar
- Pembayaran: PayPal USD
- Form: Formspree
- Notif: CallMeBot WhatsApp + Formspree email

FILE TERLAMPIR: index.html (2500+ baris, all-in-one HTML+CSS+JS)

STRUKTUR SECTION (atas ke bawah):
Hero → Gallery Slideshow → Commissions+Form → Digital Shop
→ Tools/Affiliate → Affiliates 12-card → Support
→ Partner Spotlight 3 slot → News → Articles → Footer

DESIGN SYSTEM:
- Warna utama: --pink:#FF6B9D, --lavender:#C9B8FF, --sky:#A1C4FD, --gold:#FFD166
- Font: Nunito 900 (heading) + Quicksand (body)
- Efek: glassmorphism (rgba(255,255,255,.55) + backdrop-filter:blur(16px))
- Animasi: 4 blob SVG melayang + scroll reveal IntersectionObserver

PLACEHOLDER YANG BELUM DIISI (ganti sebelum deploy):
- YOUR_CLIENT_ID → PayPal Live Client ID
- YOUR_FORM_ID → Formspree form ID
- YOUR_CALLMEBOT_APIKEY + OWNER_WA → untuk notif WA ke pemilik
- Semua YOUR_*_AFFILIATE_LINK → link affiliasi
- YOUR_REDBUBBLE → username Redbubble
- chibiwibuart handles → URL sosmed yang benar

YANG BELUM SELESAI / PERLU DIKERJAKAN:
1. Semua gambar masih placeholder div — perlu ganti dengan <img data-src="assets/..."> WebP
2. Halaman artikel (articles/) dan berita (news/) individual belum dibuat
3. favicon.ico belum ada
4. og-preview.webp 1200x630px belum ada
5. [Tambahkan permintaan spesifik Anda di sini]

Bertindaklah sebagai Expert Static Web Developer. Lanjutkan pengembangan dari kondisi ini.
```

---

*Dokumen ini dibuat otomatis dari sesi Claude Code pada 2026-10-03.*
