# Product Requirement Document (PRD) — Website Resmi PK IMM Kaizen

**V1.0 — Revised**

## 1. Document Information

* **Product Name:** Website Resmi PK IMM Kaizen
* **Document Owner:** Senior Product Manager / Product Owner / Business Analyst
* **Version:** 1.1 (Revised)
* **Status:** Draft
* **Date:** September 2026
* **Source of Truth:** Product Discovery — Website Resmi PK IMM Kaizen V1.0 + Requirement Update (Kajian & Pemikiran)

## 2. Product Overview

Website Resmi PK IMM Kaizen adalah representasi dan wajah digital resmi Pimpinan Komisariat Ikatan Mahasiswa Muhammadiyah (PK IMM) Kaizen Universitas Muhammadiyah Surabaya.

Sistem ini berfungsi sebagai pusat informasi publik organisasi, etalase katalog bisnis untuk program Kaizen Company, serta menyediakan fasilitas penerimaan Aspirasi Mahasiswa secara anonim.

Selain itu, website ini juga menjadi media publikasi pemikiran kritis melalui modul Kajian & Pemikiran.

Website ini dilengkapi dengan Admin Dashboard tunggal yang dioperasikan oleh Super Admin untuk pengelolaan konten secara mandiri (CMS).

## 3. Product Background

PK IMM Kaizen membutuhkan identitas digital yang dapat merepresentasikan organisasi secara profesional kepada publik.

Program Ekowir melalui Kaizen Company membutuhkan wadah katalog, dan program Link Aspirasi membutuhkan sarana digital anonim.

Di samping itu, bidang seperti Hikmah/Politik membutuhkan wadah literasi digital (Kajian & Pemikiran) untuk mempublikasikan tulisan dan kajian isu terkini yang dapat dibagikan ke masyarakat luas secara langsung tanpa bergantung pada portal eksternal.

## 4. Problem Statement

* Tidak adanya pusat informasi resmi yang terstruktur mengenai profil, kepengurusan, bidang, berita, dan alumni berprestasi PK IMM Kaizen.
* Kaizen Company belum memiliki etalase digital yang profesional dan terpusat.
* Evaluasi organisasi membutuhkan wadah penyampaian aspirasi (Link Aspirasi) yang benar-benar anonim.
* Belum adanya media publikasi mandiri (artikel/tulisan penuh) untuk menampung gagasan, kajian, dan pemikiran kader (khususnya Bidang Hikmah/Politik).
* Produk digital organisasi sebelumnya atau pada umumnya sering terbengkalai saat pergantian pengurus (masalah handover).

## 5. Product Vision

Menjadi wajah digital resmi PK IMM Kaizen yang profesional, terbuka, dan berkelanjutan; mendukung transparansi informasi, kemandirian ekonomi organisasi melalui Kaizen Company, budaya literasi melalui Kajian & Pemikiran, serta budaya evaluasi yang sehat melalui Link Aspirasi.

## 6. Product Goals

* Menyediakan pusat informasi publik resmi (Profil, Kepengurusan, Bidang).
* Menampilkan highlight berita kegiatan yang terintegrasi dengan portal PWMU.
* Memfasilitasi penerimaan aspirasi anonim secara aman dan terpusat.
* Menyediakan media katalog publikasi produk/jasa untuk Kaizen Company.
* Menyediakan media publikasi tulisan/artikel internal (Kajian & Pemikiran) yang memiliki tautan mandiri.
* Menyediakan CMS dashboard yang intuitif untuk Super Admin.
* Merancang sistem yang production-ready dan siap diwariskan kepada kepengurusan berikutnya.

## 7. Target Users

* Mahasiswa (UM Surabaya maupun masyarakat umum)
* Kader IMM Kaizen
* Personalia / Pengurus IMM Kaizen
* Alumni IMM Kaizen
* Masyarakat umum
* Calon konsumen / mitra Kaizen Company

## 8. User Personas

### Persona 1 — Mahasiswa / Pengunjung Umum

Membutuhkan informasi tentang PK IMM Kaizen, membaca berita kegiatan, membaca tulisan/kajian isu terkini, melihat profil alumni, melihat katalog produk, dan ingin mengirimkan kritik/saran secara anonim.

### Persona 2 — Kader / Personalia

Membutuhkan informasi struktur kepengurusan yang up-to-date, membagikan tautan kajian ke media sosial, mendapatkan informasi resmi organisasi, dan menggunakan website sebagai referensi kegiatan.

### Persona 3 — Calon Konsumen / Mitra

Membutuhkan akses cepat ke katalog Kaizen Company, melihat detail produk/jasa, dan menghubungi pihak penjual (Ekowir) untuk melakukan transaksi.

### Persona 4 — Super Admin

Membutuhkan dashboard yang mudah digunakan untuk memperbarui konten (berita, pengurus, produk, alumni, kajian) dan membaca aspirasi tanpa perlu menyentuh source code.

## 9. User Needs

* Akses informasi organisasi yang terstruktur dan cepat.
* Katalog produk Kaizen Company yang jelas dengan jalur komunikasi langsung (WhatsApp).
* Saluran literasi untuk membaca hasil kajian intelektual organisasi.
* Rasa aman dan jaminan anonimitas saat mengirimkan aspirasi.
* Kemudahan pengelolaan data dari backend tanpa keahlian pemrograman bagi pengurus.

## 10. Value Proposition

Website resmi yang menggabungkan company profile organisasi, media literasi intelektual (Kajian), etalase bisnis (Kaizen Company), dan saluran aspirasi anonim dalam satu ekosistem yang modern, cepat, terstruktur, dan mudah dikelola melalui satu pintu (Super Admin Dashboard).

## 11. Product Scope

PRD ini mendefinisikan kebutuhan (requirement) untuk:

### Public Website

* Beranda (termasuk section Kajian & Pemikiran)
* Profil
* Kepengurusan
* Bidang
* Berita
* Ekowir
* Alumni
* Kontak
* Halaman Detail Kajian
* Kaizen Company (via CTA)
* Form Aspirasi Mahasiswa

### Admin Dashboard

* Autentikasi Super Admin
* Manajemen Konten:

  * Profil
  * Pengurus
  * Bidang
  * Berita
  * Kajian & Pemikiran
  * Alumni
  * Ekowir
  * Kaizen Company
  * Produk
  * Aspirasi
  * Media

## 12. Out of Scope

Fitur berikut **TIDAK** termasuk dalam V1:

* Payment gateway / transaksi online.
* Shopping cart / checkout system terintegrasi.
* Akun pengguna publik (Public User Account).
* Kalender organisasi / Event management system.
* Direktori seluruh alumni (hanya showcase alumni pilihan).
* Forum / Sistem komentar publik.
* Duplikasi artikel kegiatan lengkap (Full article duplication) dari PWMU.
* Multi-role authentication (misal: login khusus ketua bidang / penulis kajian). Penulis bidang harus berkoordinasi dengan Super Admin untuk publikasi kajian.
* Public tracking untuk status penyelesaian aspirasi.

## 13. Information Architecture

```text
PK IMM Kaizen
└── Website Resmi PK IMM Kaizen
    ├── Beranda
    │   ├── Section: Kajian & Pemikiran
    │   │   └── Halaman Detail Kajian (URL terpisah)
    │   ├── FAQ
    │   └── Aspirasi Mahasiswa
    ├── Profil
    ├── Kepengurusan
    ├── Bidang
    ├── Berita
    ├── Ekowir
    ├── Alumni
    ├── Kontak
    └── Kaizen Company (Diakses melalui CTA khusus)
```

## 14. User Journeys

### Public Journey

Beranda → Navigasi ke Halaman (misal: Kepengurusan) → Melihat daftar pengurus → Navigasi ke Berita → Klik CTA menuju PWMU.

### Kajian Journey

Beranda → Scroll ke section Kajian & Pemikiran → Melihat daftar card kajian terbaru → Klik "Baca Selengkapnya" → Masuk ke halaman Detail Kajian → Membaca isi penuh dan membagikan URL (share).

### Kaizen Company Journey

Beranda → Klik CTA Kaizen Company → Halaman Katalog (Dark Theme) → Pilih Produk → Lihat Detail → Klik CTA Beli → Redirect ke WhatsApp dengan template pesan.

### Aspirasi Journey

Beranda → Scroll ke bagian FAQ → Klik Link Aspirasi Mahasiswa → Isi text area → Submit form → Sistem menampilkan pesan sukses (tanpa login).

### Super Admin Journey

Halaman Login → Masukkan kredensial → Dashboard utama → Pilih modul (misal: Kajian & Pemikiran) → Tambah Kajian Baru (Isi judul, ringkasan, konten penuh, penulis, thumbnail) → Simpan sebagai Draft / Publish → Data live di public website → Logout.

## 15. Feature Overview

1. **Public Website Content:** Halaman statis/dinamis untuk menyajikan informasi organisasi.
2. **Kajian & Pemikiran Module:** Modul pembuatan dan penampilan artikel internal lengkap dengan halaman detail mandiri (URL khusus).
3. **Kaizen Company Catalog:** Katalog bisnis digital (Light to Dark theme transition) dengan CTA WhatsApp.
4. **Aspirasi Mahasiswa:** Form submission anonim dengan proteksi SPAM dasar.
5. **PWMU Integration:** Direktori berita yang bertindak sebagai jembatan (redirect) ke portal berita PWMU.
6. **Super Admin Dashboard:** Sistem CMS single-role untuk operasi CRUD seluruh data website.

## 16. Functional Requirements

* **FR-001 (Navigation):** Sistem harus menampilkan navbar utama berisi: Beranda, Profil, Kepengurusan, Bidang, Berita, Ekowir, Alumni, Kontak.
* **FR-002 (Kaizen CTA):** Sistem harus menyediakan tombol/CTA khusus (bukan di navigasi utama sejajar) untuk masuk ke halaman Kaizen Company.
* **FR-003 (Aspirasi Access):** Sistem harus menyediakan akses ke form Aspirasi Mahasiswa melalui bagian FAQ di halaman Beranda.
* **FR-004 (Aspirasi Submission):** Sistem harus memungkinkan pengguna mengirim teks aspirasi tanpa proses autentikasi (login).
* **FR-005 (Kaizen Catalog):** Sistem harus menampilkan daftar produk dan jasa Kaizen Company yang berstatus "Aktif".
* **FR-006 (WhatsApp Redirect):** Sistem harus mengarahkan pengguna ke aplikasi WhatsApp (via URL `wa.me`) saat menekan tombol beli/hubungi pada detail produk Kaizen Company.
* **FR-007 (Dashboard Access):** Sistem harus menyediakan halaman login aman khusus untuk Super Admin.
* **FR-008 (Dashboard CRUD):** Sistem harus memungkinkan Super Admin membuat, membaca, memperbarui, dan menghapus (CRUD) data untuk seluruh modul konten dinamis.
* **FR-009 (Beranda - Kajian Section):** Sistem harus menampilkan daftar/card kajian terbaru di halaman Beranda.
* **FR-010 (Kajian Detail Page):** Sistem harus menyediakan halaman rute spesifik (detail page) untuk membaca konten penuh dari masing-masing Kajian.

## 17. Business Rules

* **BR-001:** Hanya Super Admin yang memiliki akses ke dashboard pengelolaan. Tidak ada role lain (Bidang Hikmah/Politik memberikan draft secara offline/external ke Super Admin untuk diunggah).
* **BR-002:** Form Aspirasi Mahasiswa bersifat anonim dan tidak mengumpulkan identitas personal (nama, email, no HP).
* **BR-003:** Data aspirasi tidak boleh dipublikasikan atau dapat dilihat oleh publik di bagian manapun di website.
* **BR-004:** Entitas dengan fitur status (Pengurus, Alumni, Produk Kaizen, Kajian) yang berstatus "Inaktif", "Unpublished", atau "Draft" tidak boleh ditampilkan di halaman publik.
* **BR-005:** Website tidak memproses pembayaran digital apapun. Segala transaksi Kaizen Company ditangani di luar sistem (melalui WhatsApp).
* **BR-006 (Pemisahan Tipe Konten):** Modul Berita hanya berfungsi sebagai aggregator/redirect yang menyimpan ringkasan dan link menuju artikel eksternal di portal PWMU. Sebaliknya, modul Kajian & Pemikiran adalah artikel native internal yang seluruh isi teks (body) disajikan dan disimpan secara penuh di database website resmi ini.
* **BR-007:** Kaizen Company diposisikan dan diakui sebagai program di bawah bidang Ekonomi & Kewirausahaan (Ekowir), bukan sebagai entitas terpisah dari PK IMM Kaizen.

## 18. Content Requirements

* Seluruh halaman harus menggunakan data dan konten riil (Real Content) saat perilisan (production-ready).
* Jika terdapat bagian yang kontennya belum disediakan oleh organisasi, sistem harus menggunakan placeholder eksplisit `[Content Required]` dan bukan dummy text (Lorem Ipsum).
* Konten memiliki lifecycle dasar: Draft → Publish (tampil publik) / Unpublish (sembunyi dari publik) → Delete (hapus permanen dari database).

## 19. Admin Dashboard Requirements

* **Navigasi Dashboard:** Harus mencakup menu untuk Profil, Kepengurusan, Bidang, Berita, Kajian & Pemikiran, Alumni, Produk & Jasa Kaizen Co, Aspirasi, dan Pengaturan Kontak/Media.
* **Validation & State:** Sistem harus memvalidasi input pada form dashboard (misal: judul wajib diisi). Harus ada success state dan error state yang jelas (Toast/Alert).
* **Destructive Action:** Tindakan penghapusan data (Delete) wajib memunculkan modal konfirmasi.
* **Aspirasi View:** Dashboard harus menampilkan daftar aspirasi masuk beserta timestamp (waktu pengiriman).

## 20. Authentication & Authorization Requirements

* **Autentikasi:** Hanya entitas Super Admin yang dapat melakukan proses login.
* **Status Implementasi:** Metode autentikasi spesifik (misal: Email/Password, Magic Link) berstatus `[Open Decision]` dan akan ditetapkan pada Technical Specification.
* **Authorization:** Publik yang mencoba mengakses URL dashboard harus di-redirect secara paksa ke halaman Beranda atau halaman 403 Forbidden / 401 Unauthorized.

## 21. Kajian & Pemikiran Requirements

* **Penempatan Publik:** Ditampilkan sebagai section di Beranda (bukan di navbar utama).
* **Card Data (Beranda):** Thumbnail/Gambar, Judul, Ringkasan Singkat (Excerpt), Tanggal Publikasi, Penulis/Bidang, dan tombol "Baca Selengkapnya".
* **Detail Page Data:** Menyajikan struktur lengkap meliputi Judul, Penulis, Tanggal, Gambar Utama (Hero Image), dan Konten (Body teks artikel penuh) yang mendukung pemformatan dasar (paragraf, bold, italic, list).
* **URL/Routing:** Memiliki slug mandiri (contoh: `/kajian/judul-kajian-pemikiran`) yang dapat dibagikan (shareable).
* **Admin CRUD:** Super Admin dapat mengelola Title, Thumbnail, Excerpt, Content (Rich Text/Markdown), Author Info, Publish Date, dan Status (Draft / Publish / Unpublish).
* **Workflow Persetujuan:** `[OPEN DECISION]` (Saat ini diasumsikan tidak ada workflow approval kompleks di dalam sistem; proses kurasi dilakukan di luar sistem oleh pimpinan sebelum diserahkan ke Super Admin).

## 22. Aspirasi Mahasiswa Requirements

* **Input Form:** Terdiri dari komponen textarea panjang tanpa field identitas.
* **Storage:** Data yang di-submit langsung masuk ke database dan diurutkan berdasarkan waktu terbaru di Dashboard Admin.
* **Spam Protection:** Sistem harus memiliki mekanisme dasar penangkal spam (misal: Rate limiting berbasis IP atau honeypot/reCAPTCHA - Detail: `[Technical Decision Required]`).
* **Feedback:** Pesan "Aspirasi berhasil dikirim" setelah submit sukses.

## 23. Berita & PWMU Requirements

* **Data Berita:** Sistem menyimpan Gambar (Thumbnail), Judul Berita, Deskripsi Singkat/Kutipan, dan URL menuju artikel PWMU.
* **CTA Redirect:** Tombol berbunyi "Lihat selengkapnya di PWMU" yang membuka tab baru (`target="_blank"`).

## 24. Kepengurusan Requirements

* **Data Pengurus:** Nama Lengkap, Foto Profile, Jabatan, Bidang, Status (Aktif/Inaktif).
* **Fleksibilitas:** Super Admin dapat menonaktifkan pengurus (misal: reshuffle atau demisioner) tanpa menghapus data historisnya.

## 25. Kaizen Company Requirements

* **Visual Direction:** Harus menggunakan Dark Theme.
* **Data Produk:** Mencakup Nama Produk, Foto, Harga, Deskripsi, Stok (Tampil sebagai info, bukan inventory tracker rumit), Kategori, Status (Aktif/Inaktif).
* **Data Jasa:** Mendukung entri "Website Development" dengan format data serupa produk yang disederhanakan.
* **CTA Beli (WhatsApp):** Tombol aksi utama pada produk. URL WhatsApp harus men-generate teks pre-filled.

## 26. Media & Image Requirements

* Semua gambar yang diunggah harus dikonversi atau disajikan menggunakan format modern (WebP).
* Mendukung fitur penambahan Alt Text pada unggahan gambar penting (untuk SEO & Accessibility).
* Modul Admin Dashboard harus memvalidasi ekstensi dan membatasi ukuran file gambar (file size limit wajar).

## 27. SEO Requirements

* **Metadata:** Setiap halaman publik utama (Beranda, Profil, Halaman Detail Kajian, dll.) harus memiliki Page Title dan Meta Description yang relevan dan dinamis.
* **Open Graph (OG):** Harus memiliki konfigurasi OG Tags agar saat URL di-share ke WhatsApp/Media Sosial, muncul preview gambar, judul, dan deskripsi dengan baik (Sangat krusial untuk URL Detail Kajian dan Produk Kaizen).
* **Indexability:** Halaman Admin Dashboard dilarang di-indeks (`noindex, nofollow` / `robots.txt disallow`).

## 28. Security Requirements

* Proteksi terhadap kerentanan XSS (Cross-Site Scripting) terutama pada input form Aspirasi dan pengisian teks body Kajian di CMS.
* Proteksi CSRF (Cross-Site Request Forgery) pada proses submit data.
* Mencegah eksploitasi SQL/NoSQL Injection.

## 29. Performance Requirements

* Lazy Loading harus diterapkan pada gambar dan daftar panjang (seperti galeri produk, list berita, daftar kajian, daftar pengurus).
* Aset statis harus dioptimasi agar waktu load wajar, menyeimbangkan estetika (Modern Minimalistic) dan efisiensi bandwidth.

## 30. Backup & Handover Requirements

* Database utama di production harus dikonfigurasi untuk memiliki backup berkala.
* Seluruh source code dan dokumentasi harus disimpan pada GitHub Organization.
* Akun pihak ketiga wajib didaftarkan menggunakan alamat email sentral organisasi.

## 31. Acceptance Criteria

### AC-001 (Kaizen Company WhatsApp Redirection)

* **Given:** pengguna publik berada di halaman Detail Produk Kaizen Company.
* **When:** pengguna menekan tombol "Hubungi Penjual / Beli via WA".
* **Then:** sistem membuka tab aplikasi WhatsApp dengan template pesan terisi.

### AC-002 (Aspirasi Submission)

* **Given:** pengguna publik melihat form Link Aspirasi di bagian FAQ Beranda.
* **When:** pengguna mengisi teks dan menekan tombol Submit (tanpa login).
* **Then:** sistem menyimpan teks ke database dan menampilkan notifikasi keberhasilan.

### AC-003 (Admin CRUD & Visibility - General)

* **Given:** Super Admin berada di Dashboard.
* **When:** Super Admin mengubah status entitas (Kajian/Pengurus) dari "Publish/Aktif" menjadi "Draft/Inaktif" lalu menyimpannya.
* **Then:** data tersebut langsung tidak terlihat pada halaman publik, namun data historisnya tetap ada di Dashboard Admin.

### AC-004 (PWMU Redirection)

* **Given:** pengguna publik melihat kartu Berita.
* **When:** pengguna mengklik "Lihat selengkapnya di PWMU".
* **Then:** sistem membuka tautan asli artikel PWMU pada tab browser baru (`_blank`).

### AC-005 (Kajian & Pemikiran - Public Detail)

* **Given:** pengguna publik berada di Beranda dan melihat section Kajian & Pemikiran.
* **When:** pengguna mengklik tombol "Baca Selengkapnya" pada sebuah kartu kajian.
* **Then:** pengguna diarahkan ke halaman detail Kajian yang memuat konten artikel secara penuh dengan URL mandiri yang unik.

## 32. V1 Prioritization

| Feature                      | Priority        | Rationale                                                                                    |
| ---------------------------- | --------------- | -------------------------------------------------------------------------------------------- |
| Kaizen Company               | Must Have       | Prioritas bisnis / Ekowir                                                                    |
| Admin Dashboard              | Must Have       | Pusat Pengelolaan website                                                                    |
| Aspirasi Mahasiswa           | Must Have       | Wadah evaluasi & program organisasi                                                          |
| Beranda                      | Must Have       | Entry point & kesan pertama digital                                                          |
| Profil, Kepengurusan, Bidang | Must Have       | Identitas & transparansi struktur                                                            |
| Kajian & Pemikiran           | [OPEN DECISION] | Ditambahkan sebagai requirement baru, perlu konfirmasi apakah menjadi blocker peluncuran V1. |
| Berita (PWMU link)           | Must Have       | Publikasi aktivitas/rekam jejak                                                              |
| Alumni Showcase              | Must Have       | Representasi & Inspirasi publik                                                              |
| Kontak                       | Must Have       | Komunikasi publik ke organisasi                                                              |

## PRD Revision Summary

| Area                      | Revision                                                                                   | Impact                                                                                                                                            |
| ------------------------- | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| Product Overview & Vision | Penambahan entitas "Kajian & Pemikiran".                                                   | Mengakomodasi kebutuhan Bidang Hikmah/Politik untuk mempublikasikan pemikiran/artikel orisinal.                                                   |
| Information Architecture  | Penambahan Section "Kajian & Pemikiran" di Beranda yang mengarah ke Halaman Detail Kajian. | Kajian memiliki halaman detail/single post tersendiri agar URL dapat dibagikan, tanpa mengubah susunan navbar utama.                              |
| Business Rules            | Penambahan BR-006 untuk memisahkan logika konten "Berita" dan "Kajian".                    | Mempertegas bahwa Berita merujuk ke PWMU (link), sedangkan Kajian adalah artikel native yang seluruh isinya disimpan di database lokal.           |
| Admin Dashboard           | Penambahan Modul Kajian pada CMS.                                                          | Super Admin harus dapat mengelola (CRUD) artikel Kajian, termasuk atribut thumbnail, author, dan publish state.                                   |
| SEO Requirements          | Penambahan fokus spesifik Open Graph (OG) untuk URL Detail Kajian.                         | Karena kajian akan sering dibagikan ke platform sosmed/WhatsApp, preview link (OG tags) wajib dikonfigurasi dengan baik.                          |
| Acceptance Criteria       | Penambahan AC-005.                                                                         | Menjamin skenario routing pengguna dari Beranda menuju detail kajian dapat diuji (testable).                                                      |
| V1 Prioritization         | Memasukkan "Kajian & Pemikiran" dengan prioritas ditandai sebagai [OPEN DECISION].         | Diperlukan diskusi lebih lanjut apakah fitur ini masuk cakupan Must Have yang menahan perilisan V1, atau dapat dikerjakan secara paralel/susulan. |

## Open Decisions

1. **Prioritas V1 (Kajian & Pemikiran):** Apakah penyelesaian modul Kajian menjadi blocker (syarat mutlak / Must Have) untuk peluncuran V1.0, atau berstatus Should Have?
2. **Atribusi Penulis Kajian:** Apakah kolom penulis cukup diisi dengan string teks bebas (misal: "Oleh: Fulan / Bidang Hikmah") oleh Super Admin, atau memerlukan tabel relasi referensi ke struktur/nama Pengurus yang sudah ada di database?
3. **Mekanisme Persetujuan (Approval Workflow):** PRD V1 mengasumsikan tidak ada workflow persetujuan di dalam aplikasi.

## PRD Readiness Assessment

* **Status:** READY FOR TSS
* **Alasan:** Perubahan dan integrasi requirement Kajian & Pemikiran telah dilakukan tanpa menimbulkan konflik arsitektural dengan fitur existing lainnya. Perbedaan antara konten Berita (Redirect) dan Kajian (Native Content) telah didefinisikan dengan jelas (Business Rule 006). Secara technical architecture data model dan fungsionalitas CMS-nya sangat identik dengan operasi CRUD konvensional, sehingga siap untuk Technical Specification (TSS).
