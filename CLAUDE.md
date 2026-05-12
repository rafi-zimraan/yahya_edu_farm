# CLAUDE.md — Yahya Edu Farm Landing Page

> Instruksi untuk Claude saat membantu Raffi develop landing page **Yahya Edu Farm**.
> Letakkan file ini di **root folder project** agar Claude membacanya otomatis di setiap sesi.

---

## 📋 Tentang Project

**Yahya Edu Farm** adalah landing page edu farm (edukasi pertanian & peternakan) yang berlokasi di **Jl. Parit Baru, Pontianak, Kalimantan Barat**. Target audience: orang tua, sekolah, dan komunitas yang ingin mengajak anak-anak belajar langsung di lahan pertanian. Project ini berbasis Islami / muslim-friendly — semua aktivitas, makanan, dan fasilitas mengikuti prinsip halal.

### Status

Single-file landing page — **bukan WordPress**. Dibuka dan di-edit langsung di **VS Code**.

### Stack

| Layer | Tech |
|---|---|
| HTML | HTML5 semantic, single file (`index.html`) |
| CSS | Vanilla CSS dengan CSS Custom Properties (variables) di `:root` |
| JS | Vanilla JS minimal — hanya inisialisasi Lucide icons |
| Fonts | Google Fonts: **Fraunces** (display serif) + **Plus Jakarta Sans** (body) |
| Icons | **Lucide** (via CDN `unpkg.com/lucide@latest`) |
| Images | Unsplash (eksternal URLs, perlu diganti dengan foto asli farm) |

### Cara menjalankan

```bash
# Cukup buka file di browser
open index.html       # macOS
start index.html      # Windows

# Atau pakai live-server kalau mau auto-reload
npx live-server .
```

Tidak ada build step. Tidak ada dependencies yang perlu di-install.

---

## 🎨 Design System

Konsep desain: **"Refined Organic Editorial"** — profesional minimalis dengan sentuhan natural/earthy.

### Color tokens (CSS variables di `:root`)

```css
/* Primary green palette */
--green-900: #14361b;   /* primer / heading */
--green-800: #1e4a25;   /* CTA & footer accent */
--green-700: #2b6235;   /* link hover, eyebrow */
--green-600: #3d7a44;
--green-500: #5a8c3f;   /* aksen utama (mengikuti logo) */
--green-400: #84a85f;
--green-200: #c8d6b5;
--green-50:  #eef3e6;   /* badge background */

/* Neutrals */
--cream:     #f7f3ea;   /* CTA dark background pair */
--paper:     #fbf9f3;   /* page background — bukan putih flat! */
--ink-900:   #1a1f1a;   /* body text dark */
--ink-700:   #3a3f38;
--ink-500:   #6b7064;
```

**JANGAN** ganti dasar palet ini tanpa permintaan eksplisit. Kalau perlu warna baru, **tambahkan** ke palette ini, jangan ganti yang ada — banyak komponen referensi ke variable yang sama.

### Typography

```css
--font-display: "Fraunces", "Iowan Old Style", Georgia, serif;
--font-body:    "Plus Jakarta Sans", system-ui, ...;
```

- **Heading** (h1–h4): selalu pakai `Fraunces`, weight 400–500, letter-spacing -0.02em
- **Body**: `Plus Jakarta Sans`, weight 400 default, line-height 1.6
- **Eyebrow** (text kecil di atas heading): uppercase, letter-spacing 0.22em, font-weight 600

### Spacing & layout

- Container max-width: `1240px`, padding inline `28px`
- Section padding: `110px 0` (block sections), `80–100px` (hero)
- Border radius: `--radius-sm: 6px` / `--radius-md: 14px` / `--radius-lg: 24px`
- Shadow: 2 level — `--shadow-soft` (badge, card biasa) dan `--shadow-lift` (hover, hero visual)

### Komponen reusable

- `.btn .btn-primary` — solid hijau gelap
- `.btn .btn-ghost` — outline
- `.eyebrow` — text kecil dengan dash kiri (digunakan di setiap section head)
- `.section-head` — wrapper konsisten untuk eyebrow + h2 + p

---

## 📐 Struktur halaman (urut dari atas)

1. **Navbar** sticky + blur — logo + 5 menu + WhatsApp CTA
2. **Hero** — split 2 kolom, headline serif + italic accent di kata "Tumbuh"
3. **Partners bar** — list mitra sekolah/komunitas (background cream)
4. **About** — 2 kolom: foto bertumpuk di kiri, narasi + 4 checklist di kanan
5. **Programs** — grid 4 card (Wisata Edukasi, Workshop Organik, Kunjungan Sekolah, Pelatihan Peternakan)
6. **Why Us** — 4 kolom dengan italic number "— 01" sampai "— 04"
7. **Gallery** — section hijau gelap, 6 foto dengan caption pill (cabe, ikan nila, mangga, tomat, timun, selada)
8. **Testimonials** — 3 card dengan kutipan serif + avatar inisial
9. **CTA** — kartu hijau gelap rounded dengan WhatsApp button
10. **Footer** — 4 kolom: brand+sosmed, navigasi, program, kontak

---

## 📞 Data kontak (HARDCODED — jangan diubah tanpa instruksi)

| Field | Value |
|---|---|
| WhatsApp | `+62 852-4973-1265` → link: `https://wa.me/6285249731265` |
| Email | `yahyaedufarm@gmail.com` |
| Alamat | `Jl. Parit Baru, Pontianak, Kalimantan Barat` |
| Jam operasional | Sen–Sab, 08.00 – 16.30 WIB |

Semua tombol "Daftar Kunjungan" / "Hubungi via WhatsApp" / "Hubungi Kami" mengarah ke link WhatsApp yang sama. Email pakai `mailto:` link.

---

## 🖼️ Aset Image

### Logo
Logo `Yahya Edu Farm` di-embed sebagai **base64 data URI** langsung di HTML (di tag `<img src="data:image/jpeg;base64,...">`). Ada **2 lokasi**: navbar + footer. Kalau perlu ganti logo, ganti **kedua-duanya** dengan data URI yang sama.

Cara generate base64 dari file logo baru:
```bash
# macOS / Linux
base64 -i logo.png | pbcopy   # otomatis ke clipboard

# atau pakai online: https://www.base64-image.de/
```
Lalu replace pattern `data:image/jpeg;base64,...` di kedua tag `<img>`.

### Foto-foto (Unsplash placeholder)

Saat ini semua foto pakai Unsplash. **Sangat disarankan untuk ganti dengan foto asli farm** (lebih authentic + SEO-friendly). Daftar foto yang dipakai:

| Lokasi | Konteks | URL pattern |
|---|---|---|
| Hero | Pemandangan ladang hijau organik | `photo-1574323347407-f5e1ad6d020b` |
| About 1 (besar) | Tangan anak menyiram tanaman | `photo-1591857177580-dc82b9ac4e1e` |
| About 2 (kecil) | Petani muda memegang bibit | `photo-1593113646773-028c64a8f1b8` |
| Gallery 1 | Cabe | `photo-1583596906651-cf28e1c5e3a3` |
| Gallery 2 | Kolam ikan nila | `photo-1583209814683-c023dd293cc6` |
| Gallery 3 | Mangga | `photo-1553279768-865429fa0078` |
| Gallery 4 | Tomat | `photo-1592924357228-91a4daadcfea` |
| Gallery 5 | Timun | `photo-1604977042946-1eecc30f269e` |
| Gallery 6 | Selada | `photo-1556801712-76c8eb07bbc9` |

Cara ganti dengan foto sendiri: simpan foto di folder `assets/`, lalu ubah `src` jadi `assets/nama-file.jpg`.

---

## ✅ Konvensi yang HARUS dipatuhi

### Bahasa & tone
- **Semua copy dalam Bahasa Indonesia** (yang baku & ringkas, bukan formal kaku)
- Sapaan ke pengunjung pakai "Anda" untuk konteks profesional
- Headline boleh italic accent (kayak `<span class="accent">Tumbuh</span>`) untuk emphasis

### Muslim-friendly / halal
- **Tidak boleh** menampilkan foto orang tanpa pakaian tertutup (lengan/celana panjang minimal)
- Foto anak-anak: prioritaskan POV yang fokus pada **tangan + aktivitas + tanaman** (bukan close-up wajah)
- Kata "halal" boleh disebut di hero badge dan section "Why Us"
- Hindari konten yang berkonotasi non-halal (musik latar, animasi yang berlebihan, dll)

### Aksesibilitas
- Setiap `<img>` wajib punya `alt` text yang deskriptif (Bahasa Indonesia)
- Heading hierarchy: 1 × `h1` (di hero), `h2` di setiap section, `h3` untuk card
- Color contrast green-900 di paper → ratio aman ≥7:1

### Kode
- Indentation: **2 spaces** (sesuai existing)
- CSS class naming: kebab-case (`hero-grid`, `about-features`)
- Tidak boleh inline style — semua styling lewat class & CSS variables
- JS minimal — kalau perlu interaktivitas, vanilla JS dulu, jangan tarik framework

### JANGAN lakukan
- ❌ Tambah dependency npm / framework (React, Vue, dll)
- ❌ Pakai Tailwind CDN — design system sudah konsisten dengan custom CSS
- ❌ Tambah credit "made with ❤️ by ..." di footer
- ❌ Pakai font selain Fraunces & Plus Jakarta Sans tanpa alasan kuat
- ❌ Ganti palet hijau ke skema warna lain
- ❌ Hardcode foto orang tanpa pakaian tertutup

---

## 🛠️ Pola request yang umum

Saat Raffi minta perubahan, anggap pola umum berikut:

| Permintaan | Yang Claude harus lakukan |
|---|---|
| "Tambah section X" | Ikut struktur `.block` + `.section-head` + container yang ada |
| "Ganti foto Y" | Cari Unsplash photo ID yang relevan, atau tunjukkan caranya pakai foto lokal |
| "Ubah copy section Z" | Ganti konten saja, jangan ubah struktur HTML |
| "Bikin lebih ramai/sepi" | Tweak spacing & shadow dulu, jangan ganti palet warna |
| "Tambah animasi" | Pakai CSS-only solutions (transition, animation, scroll-driven), bukan JS library |
| "Bikin halaman baru (mis: tentang.html)" | Buat file baru pakai shared CSS — bisa extract style ke `style.css` jika sudah > 1 halaman |
| "Optimasi SEO" | Update `<title>`, `<meta description>`, tambah Open Graph tags, schema.org JSON-LD untuk LocalBusiness |

---

## 📦 File yang ada di project

```
yahya-edu-farm/
├── index.html        # Single-file landing page (logo embedded sebagai base64)
└── CLAUDE.md         # File ini
```

Kalau project berkembang (lebih dari 1 halaman), struktur yang disarankan:
```
yahya-edu-farm/
├── index.html
├── tentang.html
├── program.html
├── kontak.html
├── assets/
│   ├── logo.png
│   ├── hero.jpg
│   └── gallery/
└── css/
    └── style.css     # extract dari <style> di-page kalau sudah multi-halaman
```

---

## 🚀 Roadmap (saran pengembangan ke depan)

Bukan urgent, tapi bisa dipertimbangkan kalau Raffi minta extend:

- [ ] Section **Harga Paket** (table 3 paket: Reguler / Sekolah / Custom)
- [ ] Form **Daftar Kunjungan** (HTML form → integrasi Fonnte WhatsApp Bot atau Google Forms)
- [ ] Halaman **Blog/Artikel** edukasi pertanian
- [ ] Schema.org JSON-LD `LocalBusiness` + `Organization` untuk SEO lokal Pontianak
- [ ] Multi-language (ID + EN switch) untuk turis/expat di Pontianak
- [ ] Lazy-load images dengan `loading="lazy"` di tag `<img>`
- [ ] Open Graph + Twitter Card meta tags untuk shareability
- [ ] Favicon dari logo (generate via realfavicongenerator.net)

---

*Last updated: 2026-05-10*
