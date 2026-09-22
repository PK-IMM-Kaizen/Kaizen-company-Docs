# UI/UX Specification

## Website Resmi PK IMM Kaizen V1.0

## 1. Document Information

* **Document Title:** UI/UX Specification — Website Resmi PK IMM Kaizen
* **Product:** Website Resmi PK IMM Kaizen V1.0
* **Version:** 1.0
* **Date:** September 2026
* **Author:** Senior UI/UX Architect
* **Source Documents:** Product Discovery, PRD V1.1 Revised, TSS V1.1 Revised, Database Design V1.2 Revised, API Specification V1.1 Revised, Logo Resmi PK IMM Kaizen, Baseline CSS Palette.

---

## 2. Revision History

* **Controlled Minor Revision:** Memperbaiki kelengkapan struktur Admin Dashboard, konsistensi responsive product grid, kelengkapan semantic design tokens, pemisahan UX specification dari implementation detail, dan validasi penghapusan elemen map pada halaman Kontak agar 100% konsisten dengan requirement tanpa penambahan fitur baru.

---

## 3. Purpose

Dokumen ini berfungsi sebagai panduan komprehensif (blueprint) untuk pembuatan antarmuka (UI) dan pengalaman pengguna (UX) pada Website Resmi PK IMM Kaizen V1.0.

Spesifikasi ini dirancang agar siap digunakan sebagai acuan langsung dalam pembuatan desain di Figma (Figma Make) dan tahap implementasi frontend, memastikan konsistensi visual, interaksi, dan sinkronisasi dengan backend (API & Database).

---

## 4. UI/UX Goals

* **Representatif & Resmi:** Menampilkan identitas PK IMM Kaizen sebagai organisasi mahasiswa yang profesional, intelektual, dan aktif.
* **Modern & Clean:** Antarmuka yang bersih, tidak terlalu ramai, menghindari dekorasi berlebihan.
* **Fungsional & Jelas:** Pemisahan UX yang tegas antara konten native (Kajian), konten redirect (Berita PWMU), dan katalog bisnis (Kaizen Company).
* **Mobile-First & Accessible:** Nyaman digunakan di perangkat mobile dengan kontras yang mematuhi standar aksesibilitas dasar (WCAG).
* **Maintainable:** Menggunakan sistem komponen yang dapat dikelola dengan mudah oleh kepengurusan berikutnya.

---

## 5. Design Principles

* **Content is King:** Hierarki visual diarahkan untuk menonjolkan konten tulisan (Kajian) dan informasi (Profil/Pengurus).
* **Clarity over Cleverness:** Interaksi sederhana dan fungsional. Tidak ada animasi berlebihan.
* **Distinct Contexts:** Memberikan perlakuan visual yang sedikit berbeda (Dark Theme) khusus untuk area Kaizen Company agar terasa seperti "etalase produk", namun tetap berada dalam ekosistem IMM.
* **Frictionless Feedback:** Form Aspirasi anonim harus sangat mudah digunakan dengan umpan balik sukses/gagal yang instan.

---

## 6. Brand & Visual Identity

Identitas visual website berpusat pada warna kebesaran Ikatan Mahasiswa Muhammadiyah (Merah) yang melambangkan keberanian, dipadukan dengan aksen Emas/Kuning (melambangkan pencerahan/matahari Muhammadiyah), dan latar belakang monokrom yang bersih.

---

## 7. Logo Usage

* **Karakter Logo:** Resmi, berwibawa.
* **Light Background:** Menggunakan logo utama (warna full color).
* **Dark Background:** Menggunakan varian logo monochrome/white atau versi logo yang kontras jika tersedia.
* **Clear Space:** Minimal 1x tinggi huruf "K" pada logo di semua sisi.
* **Navbar Sizing:** Tinggi logo maksimal 40px pada desktop dan 32px pada mobile agar proporsional.
* **JANGAN** mendistorsi, meregangkan, atau mengubah warna default logo.

---

## 8. Color System

Palette lama (Baseline CSS) telah dinormalisasi menjadi sistem token semantik.

* **Primary (IMM Red):** Utama untuk tombol, tautan, elemen aktif.
* **Primary Dark/Light:** Variasi untuk hover states dan focus rings.
* **Accent (Gold/Yellow):** Untuk badge, highlight, elemen peringatan.
* **Neutral/Surface:** Skala dari putih hingga gelap untuk tipografi, borders, card, dan latar belakang.
* **Semantic:** Success (Hijau), Warning (Kuning/Emas), Error (Merah), Info (Biru spesifik).

---

## 9. Typography System

Tipografi dibatasi pada dua font family untuk konsistensi:

* **Heading Font:** Plus Jakarta Sans (Memberikan kesan modern, aktif, dan representatif untuk organisasi).
* **Body Font:** Inter (Sangat readable untuk artikel panjang seperti Kajian & Pemikiran).

### Hierarchy

| Element              |                         Size | Weight                                                   |
| -------------------- | ---------------------------: | -------------------------------------------------------- |
| h1                   | 48px / 36px (Desktop/Mobile) | Bold                                                     |
| h2                   |                  32px / 24px | SemiBold                                                 |
| h3                   |                  24px / 20px | SemiBold                                                 |
| Body Large           |                         18px | Regular                                                  |
| Body Base            |                         16px | Regular (1.5 - 1.6 line-height untuk readability Kajian) |
| Body Small / Caption |                         14px | Regular                                                  |
| Button / Label       |                  16px / 14px | Medium/SemiBold                                          |

---

## 10. Spacing & Layout

Sistem spasi menggunakan kelipatan 8px (8-point grid system).

* **xs:** 4px
* **sm:** 8px
* **md:** 16px
* **lg:** 24px
* **xl:** 32px
* **2xl:** 48px
* **3xl:** 64px

**Section Padding:** Umumnya 80px (Desktop) dan 48px (Mobile) vertikal (Top & Bottom).

---

## 11. Grid & Breakpoints (Responsive Product Grid)

Penerapan standar kolom responsif untuk Card Grid (terutama Product Cards Kaizen Company dan general grid):

* **Mobile (< 768px):** 1 column.
* **Tablet (768px - 1023px):** 2 columns.
* **Desktop (1024px - 1279px):** 3 columns.
* **Large Desktop (>= 1280px):** 4 columns.

Desain mengutamakan mobile-first. Max-width container pada desktop adalah 1200px (terpusat).

---

## 12. Design Tokens

Seluruh semantic color dari rancangan sebelumnya telah dipetakan secara eksplisit:

| Token                  | Value     |
| ---------------------- | --------- |
| `color.primary`        | `#CC1021` |
| `color.primary.dark`   | `#9B0D1A` |
| `color.primary.light`  | `#E8192C` |
| `color.accent`         | `#E07B1A` |
| `color.background`     | `#FFFFFF` |
| `color.surface`        | `#F7F6F5` |
| `color.surface.2`      | `#EEECEB` |
| `color.card`           | `#FFFFFF` |
| `color.text.primary`   | `#111111` |
| `color.text.secondary` | `#555555` |
| `color.text.muted`     | `#888888` |
| `color.border`         | `#E0DEDC` |
| `color.border.strong`  | `#CACAC8` |
| `color.success`        | `#2D7D46` |
| `color.warning`        | `#D4A017` |
| `color.error`          | `#C8102E` |
| `color.info`           | `#1A6FA8` |

---

## 13. Component System

* **Buttons:**

  * **Primary:** Solid `color.primary`, text putih. Rounded 6px.
  * **Secondary:** Outline `color.border`, text `color.text.primary`.
  * **Ghost:** Transparent, text `color.text.secondary`, hover `color.surface`.

* **Cards:** Background `color.card`, Border `1px solid color.border`, Shadow sm, Radius 8px.

* **Inputs:** Border `color.border`, Radius 6px, Focus ring `2px solid color.primary.light`.

* **Badges:** Kecil, padding `4px 8px`, membulat, digunakan untuk Status atau Kategori.

---

## 14. Navigation

* **Public Navbar:** Sticky top, latar background solid. Logo di kiri. Link di tengah/kanan (Desktop) atau Hamburger Menu (Mobile).
* **Menu Items:** Beranda, Profil, Kepengurusan, Bidang, Berita, Ekowir, Alumni, Kontak.
* **JANGAN** memasukkan Kajian, Kaizen Company, atau Aspirasi langsung sebagai item Navbar utama.

---

## 15. Public Website UX

Website publik berfokus pada navigasi penjelajahan informasi secara intuitif.

---

## 16. Homepage Specification

* **Hero Section:** Judul utama, sub-judul, primary CTA, secondary CTA ("Baca Kajian Terbaru").
* **Kajian & Pemikiran Section:** Menampilkan card Kajian terbaru dengan tombol "Lihat Semua Kajian".
* **Berita Highlight:** Menampilkan card Berita terbaru (CTA membuka sumber PWMU eksternal).
* **Ekowir / Kaizen Company CTA:** Banner yang stand-out mengarahkan ke etalase Kaizen Company.
* **FAQ & Aspirasi:** Accordion untuk FAQ dan CTA menuju Form Aspirasi Mahasiswa.

---

## 17. Profile Specification

* **Tujuan:** Menampilkan sejarah, visi, misi, dan identitas organisasi.
* **UI Layout:** Teks terpusat atau Split layout. Tipografi dominan, jarak antar paragraf longgar.

---

## 18. Kepengurusan Specification

* **Tujuan:** Transparansi struktur organisasi.
* **UI Layout:** Menampilkan pimpinan inti di atas, dan struktur anggota per bidang dalam Grid responsif di bawahnya.

---

## 19. Bidang Specification

* **Tujuan:** Menjelaskan fungsi tiap bidang kerja.
* **UI Layout:** Daftar bidang. Tiap card berisi nama bidang dan deskripsi.

---

## 20. Berita & PWMU Specification

* **Tujuan:** Mempromosikan aktivitas yang dimuat di portal eksternal.
* **UX Flow:** Menggunakan CTA eksplisit "Lihat selengkapnya di PWMU". CTA membuka sumber PWMU eksternal. TIDAK ADA halaman detail berita di internal website. Website tidak menduplikasi full article PWMU.

---

## 21. Kajian & Pemikiran Specification (Listing)

* **Tujuan:** Mempublikasikan tulisan native dari Bidang Hikmah/Politik.
* **UX Flow:** Menampilkan card dengan judul, excerpt, dan metadata. Klik "Baca Selengkapnya" mengarahkan ke halaman Detail Kajian native. Kajian bukan item navbar, melainkan section beranda.

---

## 22. Kajian Detail Specification

* **Tujuan:** Pengalaman membaca native content yang mendalam.
* **UI Layout:** Hero image, judul, dan metadata. Content Area max-width 800px.
* **UX Flow:** Hanya Kajian yang telah `published` yang tampil untuk umum.

---

## 23. Ekowir Specification

* **Tujuan:** Menjelaskan fungsi bidang Ekonomi Kewirausahaan.
* **UX Flow:** Halaman pengantar yang memuat CTA menuju katalog Kaizen Company.

---

## 24. Kaizen Company Specification

* **Tujuan:** Etalase bisnis. Kaizen Company tetap merupakan bagian dari Ekowir dan BUKAN navbar utama.
* **Visual Identity:** Menggunakan Dark Theme agar kontras, menonjolkan nuansa eksklusif.
* **UI Layout:** Grid Katalog Produk (1 col Mobile, 2 cols Tablet, 3 cols Desktop, 4 cols Large Desktop).

---

## 25. Product Detail Specification

* **Tujuan:** Informasi konversi produk.
* **Data:** Nama, Harga, Deskripsi, Stok.
* **UX Flow:** Tidak ada e-commerce checkout, shopping cart, atau payment gateway. CTA pembelian membuka WhatsApp eksternal dengan pesan pembelian yang telah dipersiapkan.

---

## 26. Alumni Specification

* **Tujuan:** Showcase profil alumni inspiratif (Bukan full alumni directory).
* **UI Layout:** Grid profil dengan area ekstra untuk teks kontribusi.

---

## 27. Kontak Specification

* **Tujuan:** Menampilkan kontak resmi organisasi.
* **UI Layout:** Alamat teks sekretariat, email, tombol-tombol media sosial, dan Contact CTA. Tidak ada fitur integrasi peta/map interaktif.

---

## 28. Aspirasi Specification

* **Tujuan:** Form masukan mahasiswa secara anonim penuh.
* **UX Rules:** Diakses dari area FAQ pada Beranda. TIDAK ADA field Nama, Email, Phone, atau Identitas (Text only). Tidak ada public aspiration listing. Feedback setelah submission berhasil harus jelas.

---

## 29. Admin Dashboard UX

* **Role Utama:** Hanya ada SATU application role: `SUPER ADMIN`. Role organisasi (Sekretaris, Medkom, Ekowir, dll) hanya penyedia data, BUKAN role aplikasi.
* **Struktur Area:** Overview, Profil, Kepengurusan, Bidang, Kajian, Berita, Ekowir, Kaizen Company, Produk, Alumni, Aspirasi, Media.
* **Pengelolaan Media:** Terintegrasi di dalam form content (misal saat unggah gambar kajian), namun spesifikasi teknis dan validasi upload tetap tercakup sebagai bagian dari fungsionalitas admin.

---

## 30. Admin CRUD UX

* **Listing:** Data tabel, Pagination, Search, Filter Status.
* **Forms:** Mandatory fields ditandai (`*`).
* **Destructive Action:** Tindakan Hapus memunculkan Modal Konfirmasi.

---

## 31. Responsive Design

* Semua halaman menerapkan Mobile-first design.
* Grid system menyesuaikan ukuran perangkat (1, 2, 3, 4 kolom) secara konsisten di seluruh aplikasi.

---

## 32. Accessibility (A11y)

* Kontras teks dan latar mematuhi standar.
* Keyboard navigation dengan outline focus yang jelas.
* Semantik HTML dan label form dipastikan mendukung screen reader.

---

## 33. Interaction & Motion

* Transisi hover halus pada card dan tombol.
* Loading state menggunakan skeleton atau spinner.
* Hindari animasi dekoratif berlebih.

---

## 34. Loading / Empty / Error States

* **Empty State:** Pesan visual ramah saat data kosong.
* **Error State:** Umpan balik jelas saat aksi gagal.
* **Success State:** Toast notification.

---

## 35. SEO & Social Sharing UX

* Spesifik untuk halaman Detail Kajian: UI menyertakan elemen yang mewakili metadata (Title, Excerpt, Hero image) untuk optimalisasi SEO dan preview Open Graph di media sosial.

---

## 36. Figma Make Implementation Guidance

* Gunakan Design Tokens (Colors, Typography) langsung.
* Implementasi Grid 1-2-3-4 kolom pada area card/produk.
* Pisahkan konsep Light Mode (Public/Admin) dan Dark Mode (Kaizen Company).

---

## 37. Requirement Traceability

* Desain merupakan translasi murni dari Product Discovery, PRD V1.1 Revised, TSS V1.1 Revised, Database Design V1.2 Revised, dan API Specification V1.1 Revised.
* Contoh: Ketiadaan keranjang belanja merefleksikan spesifikasi WhatsApp flow.

---

## 38. Open Decisions

* **Rich Text Format:** Pemilihan Markdown vs WYSIWYG HTML masih OPEN DECISION. UI harus mendukung form teks panjang dan memproyeksikan konten secara tersanitasi untuk mencegah XSS.
* **Rate Limiting/Spam Protection Aspirasi:** OPEN DECISION pada sisi infrastruktur, UI akan mengimplementasikan feedback penolakan ringan jika terkena limit.

---

## 39. UI/UX Acceptance Criteria

* Desain responsif secara konsisten.
* Tidak ada fitur baru di luar spesifikasi.
* Terdapat batas yang jelas antara UX Native content dan External content.
* Semantic tokens teraplikasi 100%.

---

## 40. Final Validation

* **Product scope konsisten:** PASS
* **Public navigation konsisten:** PASS
* **Admin scope konsisten (Seluruh 12 area tercakup):** PASS
* **Single Super Admin role:** PASS
* **Kajian section + detail page:** PASS
* **Kajian native content:** PASS
* **Berita/PWMU external flow (Tanpa full duplication):** PASS
* **Kaizen Company/Ekowir relationship:** PASS
* **Aspirasi anonymous (Tanpa public listing):** PASS
* **Product purchase via WhatsApp (Tanpa ecommerce checkout):** PASS
* **Responsive layout (1, 2, 3, 4 cols terstandardisasi):** PASS
* **Design tokens lengkap (Seluruh 17 tokens terdefinisi):** PASS
* **Accessibility:** PASS
* **Interaction states:** PASS
* **SEO:** PASS
* **Figma Make readiness:** PASS
* **No unauthorized feature additions:** PASS

### UI/UX Specification Status

> **PASS — UI/UX SPECIFICATION READY FOR FIGMA MAKE**
