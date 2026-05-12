# Panduan Publish & Konfigurasi Iklan — Yahya Edu Farm

> Dokumen ini untuk **handover ke tim marketing** atau panduan mandiri saat HTML
> sudah siap di-publish dan akan dijalankan iklannya (Meta Ads, Google Ads, TikTok Ads, dll).

**Estimasi total waktu setup**: 2–4 jam (sekali setup, lifetime use).

---

## 📍 Daftar Isi

1. [Publish HTML ke Internet](#bagian-1--publish-html-ke-internet)
2. [Konfigurasi WAJIB sebelum iklan](#bagian-2--konfigurasi-wajib-sebelum-iklan)
3. [Pasang Tracking Pixels](#bagian-3--pasang-tracking-pixels)
4. [Track Conversion Klik WhatsApp](#bagian-4--track-conversion-klik-whatsapp)
5. [Handover ke Tim Marketing](#bagian-5--handover-ke-tim-marketing)
6. [Alternatif: Hosting di WordPress](#bagian-6--alternatif-hosting-di-wordpress)
7. [Checklist Pre-Launch](#-checklist-pre-launch)

---

## Bagian 1 — Publish HTML ke Internet

Sebelum iklan bisa jalan, HTML harus punya **URL publik** yang bisa diakses dari mana saja. Ada 3 opsi populer:

### Opsi A — Vercel (GRATIS, paling cepat — RECOMMEND)

**Kelebihan**: gratis, super cepat (CDN global), auto SSL, deploy via drag-drop.

**Tata cara**:
1. Buka [vercel.com](https://vercel.com) → daftar pakai akun GitHub/Google
2. Klik **Add New → Project**
3. Pilih **Deploy a static site** (atau drag folder `web_yahyaedufarm` ke halaman deploy)
4. Setelah deploy, kamu dapat URL gratis: `web-yahyaedufarm.vercel.app`
5. (Opsional) Hubungkan domain custom → Settings → Domains → Add `yahyaedufarm.com`

**Update konten**: edit `index.html` → drag ulang folder ke Vercel → live dalam 30 detik.

### Opsi B — Niagahoster / Hostinger (hosting Indonesia berbayar)

**Kelebihan**: support Indonesia, latency rendah dari Pontianak, custom domain langsung include.

**Tata cara**:
1. Beli paket hosting Personal/Bisnis (~Rp 30–50rb/bulan) + domain `yahyaedufarm.com`
2. Login ke **cPanel** → buka **File Manager**
3. Masuk folder `public_html/`
4. Upload `index.html` ke folder ini (atau zip dulu, upload, extract)
5. Akses `https://yahyaedufarm.com` — sudah live
6. Aktifkan **SSL gratis** dari menu Security → Let's Encrypt

### Opsi C — Cloudflare Pages (gratis, infrastruktur kelas enterprise)

**Tata cara**:
1. Daftar di [pages.cloudflare.com](https://pages.cloudflare.com)
2. **Create Project → Direct Upload**
3. Upload folder `web_yahyaedufarm`
4. Dapat URL gratis: `web-yahyaedufarm.pages.dev`

### Setelah live — test dulu

Buka URL di browser, pastikan:
- [x] Logo Yahya Edu Farm muncul
- [x] Foto-foto galeri muncul (cabe, ikan nila, mangga, dll)
- [x] Tombol "Daftar Kunjungan" klik → buka WhatsApp ke `+62 852-4973-1265`
- [x] Buka di HP — layout tetap rapi (responsive)
- [x] Test page speed di [pagespeed.web.dev](https://pagespeed.web.dev) → target hijau (≥85)

---

## Bagian 2 — Konfigurasi WAJIB sebelum iklan

Tambahkan kode-kode di bawah ini **di dalam tag `<head>` `index.html`** sebelum iklan jalan. Tanpa ini, iklan bisa jalan tapi performanya tidak optimal.

### 2.1 Meta tags SEO lengkap

Cari di `index.html`:

```html
<title>Yahya Edu Farm — Belajar dari Bumi, Tumbuh Bersama Alam</title>
<meta name="description" content="Yahya Edu Farm — ruang edukasi pertanian dan peternakan terpadu di Pontianak. Belajar langsung dari alam, halal, ramah anak." />
```

**Tambahkan tepat setelahnya**:

```html
<!-- SEO -->
<meta name="keywords" content="edu farm pontianak, wisata edukasi anak pontianak, pertanian organik kalimantan barat, kunjungan sekolah pontianak, peternakan edukasi" />
<meta name="author" content="Yahya Edu Farm" />
<meta name="robots" content="index, follow" />
<link rel="canonical" href="https://yahyaedufarm.com/" />

<!-- Geo tag untuk SEO lokal Pontianak -->
<meta name="geo.region" content="ID-KB" />
<meta name="geo.placename" content="Pontianak" />
<meta name="geo.position" content="-0.022;109.330" />
```

> **Ganti** `https://yahyaedufarm.com/` dengan URL final-mu (Vercel / Niagahoster / dll).

### 2.2 Open Graph (preview saat di-share di FB/WA/IG)

Saat iklan tayang atau orang share link landing page, preview yang muncul harus rapi (judul + deskripsi + thumbnail). Tambahkan setelah meta SEO di atas:

```html
<!-- Open Graph (Facebook, WhatsApp, LinkedIn) -->
<meta property="og:type" content="website" />
<meta property="og:url" content="https://yahyaedufarm.com/" />
<meta property="og:title" content="Yahya Edu Farm — Edukasi Pertanian di Pontianak" />
<meta property="og:description" content="Ruang belajar terbuka untuk anak, sekolah, dan keluarga. Halal, ramah anak, di Jl. Parit Baru Pontianak." />
<meta property="og:image" content="https://yahyaedufarm.com/og-image.jpg" />
<meta property="og:image:width" content="1200" />
<meta property="og:image:height" content="630" />
<meta property="og:locale" content="id_ID" />

<!-- Twitter Card -->
<meta name="twitter:card" content="summary_large_image" />
<meta name="twitter:title" content="Yahya Edu Farm — Edukasi Pertanian di Pontianak" />
<meta name="twitter:description" content="Ruang belajar terbuka untuk anak, sekolah, dan keluarga." />
<meta name="twitter:image" content="https://yahyaedufarm.com/og-image.jpg" />
```

> **PENTING**: siapkan file `og-image.jpg` ukuran **1200×630 px** (foto ladang + logo + tagline) → upload ke folder root yang sama dengan `index.html`. Bisa dibuat di Canva.

### 2.3 Schema.org `LocalBusiness` (untuk Google Maps & Rich Result)

Tambahkan tepat **sebelum `</head>`** — supaya muncul di Google Search dengan rating bintang & alamat:

```html
<!-- Schema.org LocalBusiness -->
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "LocalBusiness",
  "name": "Yahya Edu Farm",
  "image": "https://yahyaedufarm.com/og-image.jpg",
  "@id": "https://yahyaedufarm.com",
  "url": "https://yahyaedufarm.com",
  "telephone": "+6285249731265",
  "email": "yahyaedufarm@gmail.com",
  "priceRange": "Rp",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "Jl. Parit Baru",
    "addressLocality": "Pontianak",
    "addressRegion": "Kalimantan Barat",
    "addressCountry": "ID"
  },
  "geo": {
    "@type": "GeoCoordinates",
    "latitude": -0.022,
    "longitude": 109.330
  },
  "openingHoursSpecification": [{
    "@type": "OpeningHoursSpecification",
    "dayOfWeek": ["Monday","Tuesday","Wednesday","Thursday","Friday","Saturday"],
    "opens": "08:00",
    "closes": "16:30"
  }],
  "sameAs": [
    "https://wa.me/6285249731265"
  ]
}
</script>
```

> **Catatan**: ganti koordinat `latitude` & `longitude` dengan posisi farm yang sebenarnya. Buka [Google Maps](https://maps.google.com), klik kanan di lokasi farm → klik koordinat untuk copy.

### 2.4 Favicon

Generate favicon dari logo di [realfavicongenerator.net](https://realfavicongenerator.net):
1. Upload logo PNG (transparan lebih bagus)
2. Download paket favicon
3. Upload semua file ke folder root project
4. Tempel kode HTML yang dia berikan ke `<head>`

---

## Bagian 3 — Pasang Tracking Pixels

Pixel = kode kecil yang melacak siapa yang kunjungi website + apa yang mereka lakukan. **Wajib** untuk iklan supaya bisa retargeting & ukur ROAS.

### 3.1 Meta Pixel (Facebook + Instagram Ads)

Ini yang paling penting untuk iklan FB/IG.

**Cara dapat Pixel ID**:
1. Buka [business.facebook.com](https://business.facebook.com) → masuk ke **Events Manager**
2. **Connect Data Sources → Web → Create**
3. Beri nama "Yahya Edu Farm Pixel" → lanjut
4. Akan muncul **Pixel ID** (16-digit angka, contoh: `1234567890123456`)

**Cara pasang** — tambahkan kode ini di `<head>` `index.html`, ganti `YOUR_PIXEL_ID` dengan ID asli:

```html
<!-- Meta Pixel Code -->
<script>
!function(f,b,e,v,n,t,s)
{if(f.fbq)return;n=f.fbq=function(){n.callMethod?
n.callMethod.apply(n,arguments):n.queue.push(arguments)};
if(!f._fbq)f._fbq=n;n.push=n;n.loaded=!0;n.version='2.0';
n.queue=[];t=b.createElement(e);t.async=!0;
t.src=v;s=b.getElementsByTagName(e)[0];
s.parentNode.insertBefore(t,s)}(window, document,'script',
'https://connect.facebook.net/en_US/fbevents.js');
fbq('init', 'YOUR_PIXEL_ID');
fbq('track', 'PageView');
</script>
<noscript><img height="1" width="1" style="display:none"
src="https://www.facebook.com/tr?id=YOUR_PIXEL_ID&ev=PageView&noscript=1"/></noscript>
<!-- End Meta Pixel Code -->
```

**Test apakah berhasil**: install extension Chrome **Meta Pixel Helper** → buka website → harus muncul ✅ hijau.

### 3.2 Google Tag (Google Ads + Google Analytics 4)

**Cara dapat Measurement ID**:
1. Buka [analytics.google.com](https://analytics.google.com) → buat property baru → pilih "Web"
2. Setelah jadi, dapat **Measurement ID** format `G-XXXXXXXXXX`

**Cara pasang** — tambahkan di `<head>`, ganti `G-XXXXXXXXXX`:

```html
<!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX');
</script>
```

**Test**: install extension **Google Tag Assistant** atau buka GA Realtime → kunjungi website → harus muncul user.

### 3.3 TikTok Pixel (opsional, kalau mau iklan TikTok)

**Cara dapat Pixel Code**:
1. Buka [ads.tiktok.com](https://ads.tiktok.com) → Assets → Events → Web Events → Create Pixel
2. Pilih method **Manually Install Pixel Code**
3. Copy seluruh kode pixel yang TikTok berikan

Tempel di `<head>` sama seperti Meta Pixel.

### 3.4 [Cara lebih clean] Pakai Google Tag Manager (GTM)

Daripada tempel 3 pixel terpisah, lebih rapi pakai **GTM** — 1 script di website, semua pixel di-manage dari dashboard GTM.

Tutorial GTM: [tagmanager.google.com](https://tagmanager.google.com) → Create Container → ikuti panduan.

**Recommend untuk tim marketing yang mature** karena lebih flexible (mereka bisa tambah/edit pixel tanpa minta developer).

---

## Bagian 4 — Track Conversion Klik WhatsApp

Conversion utama landing page ini = **klik tombol WhatsApp**. Ini harus ditrack supaya tim marketing bisa ukur:
- Berapa banyak klik per iklan
- ROAS (return on ad spend)
- Audience yang convert untuk retargeting

**Tata cara**: tambahkan script ini **sebelum `</body>`** di `index.html`:

```html
<!-- Track WhatsApp Click -->
<script>
document.querySelectorAll('a[href*="wa.me"]').forEach(function(link){
  link.addEventListener('click', function(){
    // Meta Pixel - track sebagai Lead
    if (typeof fbq !== 'undefined') {
      fbq('track', 'Lead', {
        content_name: 'WhatsApp Click',
        content_category: 'Contact'
      });
    }
    // Google Analytics 4 - custom event
    if (typeof gtag !== 'undefined') {
      gtag('event', 'whatsapp_click', {
        'event_category': 'Contact',
        'event_label': 'WhatsApp CTA'
      });
    }
    // TikTok Pixel
    if (typeof ttq !== 'undefined') {
      ttq.track('Contact');
    }
  });
});
</script>
```

Script ini otomatis mendeteksi **semua tombol WhatsApp** di halaman (yang `href` mengandung `wa.me`) — jadi tidak perlu modifikasi tombol satu per satu.

**Setup di Meta Ads Manager**:
1. Events Manager → pilih Pixel → tab **Events**
2. Cari event **Lead** yang baru auto-detect → klik **Set Up**
3. Tandai sebagai **Conversion Event** (max 8 conversion event per Pixel — Lead = priority 1)

**Setup di Google Ads**:
1. Tools → Conversions → New Conversion
2. Pilih **Website**
3. Source: **Google Analytics 4 events**
4. Pilih event `whatsapp_click` → Import sebagai conversion

---

## Bagian 5 — Handover ke Tim Marketing

Setelah semua pixel terpasang, ini yang perlu kamu **kirim ke tim marketing**:

### Checklist data untuk tim marketing

```
✉️ KIRIM KE TIM MARKETING:

1. URL Landing Page         : https://yahyaedufarm.com  (atau URL Vercel/dll)
2. Meta Pixel ID            : 1234567890123456
3. GA4 Measurement ID       : G-XXXXXXXXXX
4. TikTok Pixel ID          : (kalau ada)
5. Google Ads Customer ID   : XXX-XXX-XXXX
6. Conversion event utama   : "Lead" (Meta) / "whatsapp_click" (GA4)
7. WhatsApp Bisnis          : +62 852-4973-1265
8. Email                    : yahyaedufarm@gmail.com
9. Akses Business Manager   : (assign Marketing role lewat business.facebook.com)
10. Akses GTM (kalau ada)   : (assign User di tagmanager.google.com)
```

### Best practices iklan untuk landing page ini

**Audience targeting yang masuk akal**:
- Lokasi: Pontianak + radius 30km (atau seluruh Kalimantan Barat)
- Demografi: parent (25–45 tahun), guru/pengajar
- Interest: parenting, pendidikan anak, homeschooling, organic farming, halal lifestyle, wisata edukasi anak

**Format iklan yang work**:
- **Carousel** dengan 5 foto galeri (cabe, ikan nila, mangga, dll) + headline per slide
- **Video ad** — 15 detik tour singkat farm (kalau ada)
- **Lead Form ad** (di Meta) — bisa langsung dapat kontak tanpa keluar dari FB/IG

**Naming convention campaign** (saran):
```
[Platform]_[Audience]_[Objective]_[Date]
contoh: META_OrtuPontianak_Lead_Mei2026
```

**Budget awal yang masuk akal**: Rp 50.000–100.000/hari untuk testing 1 minggu, lalu scale yang performanya bagus.

**KPI yang dipantau**:
- CTR (target: > 1.5%)
- CPC (target: < Rp 1.500)
- Conversion rate WhatsApp click (target: > 3%)
- ROAS (target: minimal 3x)

---

## Bagian 6 — Alternatif: Hosting di WordPress

Kalau memang nantinya ingin di-host di server WordPress yang sudah ada (`eduyahyafarm.com` di hosting cPanel), ada 3 cara:

### Cara A — Static HTML di subdomain

Pakai HTML sebagai-nya, tapi taruh di subdomain `landing.yahyaedufarm.com`:
1. cPanel → **Subdomains** → buat `landing` pointing ke folder `public_html/landing/`
2. Upload `index.html` ke folder `public_html/landing/`
3. Selesai. WordPress utama (kalau ada) tetap di domain utama.

**Kelebihan**: super cepat, tidak terganggu plugin WordPress, ideal untuk iklan.

### Cara B — Convert jadi WordPress page (pakai plugin "Insert HTML")

1. Install plugin **WPCode** atau **Insert HTML Snippet**
2. Buat halaman baru di WordPress → kosongkan editor
3. Tempel kode HTML yang sudah dimodifikasi (hapus tag `<html>`, `<head>`, `<body>`)
4. CSS dan JS dipindah ke header.php / functions.php

**Kekurangan**: ribet, performance turun karena WordPress overhead.

### Cara C — Convert jadi proper WordPress theme

Ini pekerjaan developer (bisa minta saya bantu di sesi terpisah). Pecah `index.html` jadi:
- `header.php`
- `front-page.php`
- `footer.php`
- `style.css`
- `functions.php`

**Saran**: untuk landing page iklan, **Cara A (subdomain)** paling worth it. Static HTML + tracking pixel = page speed maksimal = quality score iklan tinggi = CPC lebih murah.

---

## ✅ Checklist Pre-Launch

Print/centang manual sebelum iklan dijalankan:

**Konten & visual**
- [ ] Logo muncul di navbar & footer
- [ ] Semua foto loading sempurna (galeri tanaman + foto About)
- [ ] Foto Open Graph (`og-image.jpg`) sudah dibuat ukuran 1200×630
- [ ] Favicon sudah terpasang
- [ ] Test di HP (responsive)

**Kontak & link**
- [ ] Tombol "Daftar Kunjungan" klik → buka WhatsApp `+62 852-4973-1265`
- [ ] Link email → buka mail client dengan tujuan `yahyaedufarm@gmail.com`
- [ ] Tidak ada link rusak (404)

**SEO & Meta**
- [ ] `<title>` sudah pas
- [ ] Meta description sudah pas
- [ ] Open Graph tags lengkap (test di [opengraph.xyz](https://www.opengraph.xyz/))
- [ ] Schema.org LocalBusiness sudah ada (test di [search.google.com/test/rich-results](https://search.google.com/test/rich-results))
- [ ] URL canonical pointing ke domain final

**Tracking**
- [ ] Meta Pixel terpasang (test pakai Meta Pixel Helper)
- [ ] GA4 terpasang (test di Realtime)
- [ ] TikTok Pixel terpasang (kalau pakai)
- [ ] Event "WhatsApp Click" tracked di kedua platform
- [ ] Conversion sudah di-mark di Meta Events Manager & Google Ads

**Performance**
- [ ] PageSpeed Insights → mobile score ≥ 80, desktop ≥ 90
- [ ] First Contentful Paint < 2 detik
- [ ] Cumulative Layout Shift < 0.1

**Hosting**
- [ ] HTTPS aktif (gembok hijau di browser)
- [ ] Domain custom sudah aktif (kalau pakai)
- [ ] Backup file `index.html` tersimpan di tempat aman (Google Drive)

**Handover**
- [ ] Pixel ID, GA4 ID, akses Business Manager sudah dishare ke tim marketing
- [ ] Tim marketing sudah konfirmasi iklan siap dijalankan

---

## 🆘 Troubleshooting Cepat

| Masalah | Solusi |
|---|---|
| Foto Unsplash gak loading | Internet user lambat — host foto sendiri (download → upload ke folder `assets/`) |
| Meta Pixel tidak detect | Cek script di posisi `<head>`, bukan `<body>`. Disable Adblock saat test. |
| Open Graph preview kosong di FB | Re-fetch di [developers.facebook.com/tools/debug](https://developers.facebook.com/tools/debug/) |
| Page speed rendah | Convert foto JPG → WebP. Tambah `loading="lazy"` di tag `<img>`. |
| WhatsApp link gak buka di iOS | Format `https://wa.me/6285249731265` (tanpa `+` atau spasi) |

---

*Dokumen ini bisa di-update sesuai kebutuhan. Untuk pertanyaan teknis lebih lanjut, kontak Raffi (Griya IT Nusantara).*

*Last updated: 2026-05-10*
