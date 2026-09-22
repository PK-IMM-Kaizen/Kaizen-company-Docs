# Product Discovery — Website Resmi PK IMM Kaizen V1.0

## 1. Document Information

* **Product Name:** Website Resmi PK IMM Kaizen
* **Document Owner:** Senior Product Manager / Business Analyst
* **Version:** 1.0
* **Status:** Draft (Approved for Technical Planning)
* **Date:** September 2026

## 2. Executive Summary

Proyek ini bertujuan untuk merancang dan membangun Website Resmi Pimpinan Komisariat Ikatan Mahasiswa Muhammadiyah (PK IMM) Kaizen Universitas Muhammadiyah Surabaya dari awal. Website ini dirancang sebagai source of truth digital untuk publik dan internal, dengan target production-ready V1.0.

Tiga prioritas utama pengembangan adalah integrasi program unggulan Kaizen Company sebagai katalog bisnis (di bawah bidang Ekowir), sistem Aspirasi Mahasiswa yang anonim, dan Admin Dashboard tersentralisasi untuk pengelolaan konten secara mandiri oleh Super Admin.

Sistem ini dirancang untuk mudah diwariskan (handover) ke kepengurusan periode selanjutnya.

## 3. Product Identity

* **Nama Organisasi:** Pimpinan Komisariat Ikatan Mahasiswa Muhammadiyah Kaizen Universitas Muhammadiyah Surabaya
* **Nama Produk:** Website Resmi PK IMM Kaizen
* **Status Produk:** Production-ready V1.0, dioptimalkan untuk periode 2026–2027 dan siap diwariskan secara berkelanjutan.

## 4. Background

Sebagai organisasi mahasiswa yang aktif dan terus berkembang, PK IMM Kaizen membutuhkan wajah digital resmi. Saat ini, kebutuhan akan pusat informasi terpadu, etalase program bisnis (Kaizen Company), serta wadah aspirasi yang aman sangat mendesak.

Website ini dibangun untuk memenuhi kebutuhan representasi digital yang mandiri, modern, dan tidak bergantung pada platform pihak ketiga semata.

## 5. Problem Statement

* Organisasi tidak memiliki pusat informasi publik resmi yang terstruktur.
* Prestasi alumni dan rekam jejak kepengurusan belum terdokumentasi dan terpublikasi dengan baik dalam satu platform.
* Program ekonomi dan kewirausahaan (Kaizen Company) membutuhkan etalase/katalog digital yang profesional untuk menjangkau pasar di luar organisasi.
* Dibutuhkan sistem penerimaan umpan balik (Link Aspirasi) yang benar-benar anonim untuk menghindari bias dan "fatamorgana dalam refleksi" organisasi.
* Sistem digital organisasi mahasiswa seringkali terbengkalai saat berganti kepengurusan karena tidak dirancang untuk diwariskan (handover).

## 6. Product Vision

Menjadi wajah digital resmi PK IMM Kaizen yang profesional, terbuka, dan berkelanjutan; mendukung transparansi informasi, kemandirian ekonomi organisasi melalui Kaizen Company, serta budaya evaluasi yang sehat melalui Link Aspirasi.

## 7. Product Goals

* Menjadi pusat informasi publik resmi (Profil, Kepengurusan, Bidang).
* Menampilkan highlight berita kegiatan (terhubung ke PWMU) dan prestasi alumni pilihan.
* Memfasilitasi penerimaan aspirasi anonim secara aman dan terpusat.
* Menyediakan media katalog publikasi produk/jasa untuk Kaizen Company.
* Menyediakan dashboard manajemen konten yang mudah digunakan oleh Super Admin.
* Memastikan sistem dirancang sedemikian rupa sehingga mudah dimaintain dan diwariskan ke pengurus periode berikutnya.

## 8. Target Users

* Mahasiswa (UM Surabaya maupun umum)
* Kader IMM
* Personalia/Pengurus IMM Kaizen
* Alumni IMM Kaizen
* Masyarakat umum
* Calon mitra organisasi / konsumen Kaizen Company

## 9. User Needs

* **Publik/Mahasiswa:** Mencari informasi tentang IMM Kaizen, membaca berita, melihat katalog produk Kaizen Company, mengirimkan aspirasi anonim.
* **Pengurus/Kader:** Melihat struktur organisasi, mengarahkan mitra ke website resmi, menjadikan web sebagai referensi kegiatan.
* **Super Admin:** Memperbarui data kepengurusan, menambah produk Kaizen Company, membaca aspirasi masuk, dan mengatur konten tanpa perlu menyentuh kode.

## 10. Value Proposition

Website yang menggabungkan company profile organisasi dengan etalase bisnis (Kaizen Company) dan saluran aspirasi anonim dalam satu ekosistem yang modern, cepat, terstruktur, dan dikelola melalui satu pintu (Super Admin Dashboard).

## 11. Product Scope

Fokus pada penyediaan informasi satu arah (Company Profile), katalog bisnis tanpa sistem transaksi on-site (diarahkan ke WhatsApp), dan form aspirasi anonim satu arah (tanpa public tracking).

Tidak mencakup fitur komunitas seperti forum, komentar, atau user account untuk publik.

## 12. Information Architecture

```text
PK IMM Kaizen
└── Website Resmi PK IMM Kaizen
    ├── Beranda
    │   ├── FAQ
    │   └── Aspirasi Mahasiswa
    ├── Profil
    ├── Kepengurusan
    ├── Bidang
    ├── Berita
    ├── Ekowir
    ├── Alumni
    ├── Kontak
    └── Kaizen Company (Akses via CTA khusus, bukan navbar utama)
```

**Catatan:** Kaizen Company memiliki Visual Direction Dark Theme, sementara halaman utama menggunakan Light Theme.

## 13. Feature Overview

1. **Kaizen Company Catalog:** Etalase produk dan jasa (Website Development).
2. **Aspirasi Mahasiswa (Link Aspirasi):** Form pengiriman kritik/saran anonim di Beranda (FAQ).
3. **Admin Dashboard:** CMS terpusat untuk Super Admin.
4. **Organigram & Alumni Showcase:** Manajemen status pengurus aktif/inaktif dan profil alumni berprestasi.
5. **Berita Terintegrasi:** Direktori berita yang mengarahkan pembaca ke artikel lengkap di PWMU.

## 14. Detailed Feature Requirements

### Feature 1: Kaizen Company Catalog

* **Purpose:** Menampilkan produk/jasa yang dijual oleh Ekowir untuk kemandirian ekonomi.
* **Target User:** Masyarakat umum, Mahasiswa, Kader.
* **Business Value:** Meningkatkan reach penjualan dan kredibilitas usaha organisasi.
* **Description:** Halaman dengan dark theme berisi daftar produk dan jasa. Tidak ada shopping cart atau payment gateway.
* **Functional Requirements:** Menampilkan grid produk. Tombol "Beli" mengarahkan pengguna ke WhatsApp dengan pesan pre-filled.
* **User Flow:** User masuk ke Kaizen Company → Melihat daftar produk → Klik detail produk → Klik "Hubungi Penjual / Beli" → Dialihkan ke WhatsApp.
* **Input:** Klik pada CTA beli.
* **Output:** Redireksi ke URL WhatsApp (`wa.me/...`).
* **Business Rules:** Hanya produk dengan status "Aktif" yang ditampilkan ke publik.
* **Data Requirements:** Nama produk, Foto, Harga, Deskripsi, Kategori, Stok (display only), Status.
* **Access Requirements:** Publik (View), Super Admin (CRUD).
* **Dependencies:** WhatsApp URL API.

**Acceptance Criteria:**

* Given pengguna berada di halaman Kaizen Company, When pengguna mengklik produk, Then detail produk dan tombol WhatsApp muncul.
* Given pengguna mengklik tombol WhatsApp, When sistem memproses klik, Then pengguna dialihkan ke aplikasi/web WhatsApp dengan format pesan yang sudah disiapkan.

### Feature 2: Aspirasi Mahasiswa (Link Aspirasi)

* **Purpose:** Wadah masukan anonim sebagai bahan evaluasi Rapat Setengah Periode.
* **Target User:** Personalia, Kader, Masyarakat Umum.
* **Business Value:** Menciptakan budaya organisasi yang transparan, anti-fatamorgana refleksi.
* **Description:** Form text-area sederhana yang dapat diakses dari bagian FAQ di Beranda.
* **Functional Requirements:** Form pengiriman teks tanpa kewajiban login. Data masuk ke Dashboard Admin.
* **User Flow:** User ke Beranda → Scroll ke FAQ → Klik Link Aspirasi → Isi form → Submit → Selesai.
* **Input:** Teks aspirasi.
* **Output:** Pesan sukses submit.
* **Business Rules:** Tidak ada public tracking. Tidak meminta nama/email/nomor HP.
* **Data Requirements:** Teks Aspirasi, Timestamp.
* **Access Requirements:** Publik (Submit), Super Admin (View list).

**Acceptance Criteria:**

* Given form aspirasi terbuka, When pengguna mengisi teks dan menekan submit tanpa login, Then data tersimpan ke database dan pengguna melihat pesan sukses.

### Feature 3: Admin Dashboard (Super Admin)

* **Purpose:** Pusat kontrol konten website.
* **Target User:** Super Admin (Developer saat ini, Sekretaris/Pengurus di masa depan).
* **Business Value:** Memastikan website tetap up-to-date tanpa ketergantungan pada developer untuk mengubah hardcode.
* **Description:** CMS single-role untuk mengelola Profil, Kepengurusan, Bidang, Berita, Alumni, Ekowir, Kaizen Co, dan Aspirasi.
* **Functional Requirements:** CRUD standar, image upload, ubah status (Aktif/Inaktif).
* **User Flow:** Login → Lihat menu di sidebar → Pilih entitas → Lakukan perubahan → Simpan → Logout.
* **Input:** Kredensial login, Data form konten.
* **Output:** Perubahan data di database dan live website.
* **Business Rules:** Hanya satu role yang ada. Jika bidang lain ingin update, harus melalui Super Admin.
* **Data Requirements:** Kredensial Super Admin, Data seluruh entity website.

**Acceptance Criteria:**

* Given pengguna memiliki akses Super Admin, When pengguna memperbarui status kepengurusan dari aktif menjadi inaktif, Then profil pengurus tersebut hilang dari tampilan publik namun data tetap ada di database.

### Feature 4: Berita & PWMU Redirection

* **Purpose:** Menampilkan rekam jejak kegiatan organisasi.
* **Description:** Berisi daftar berita (Thumbnail, Judul, Deskripsi Singkat). Tidak duplikasi konten. Tombol "Lihat selengkapnya di PWMU".

**Acceptance Criteria:**

* Given pengguna melihat card berita, When mengklik judul atau CTA, Then pengguna dialihkan ke link asli PWMU di tab baru.

## 15. User Flows

* **Public:** Beranda → Eksplorasi Navbar (Profil, Kepengurusan, Bidang, Berita, Ekowir, Alumni, Kontak) → Interaksi (WhatsApp Kaizen / Form Aspirasi).
* **Super Admin:** Halaman Login rahasia → Dashboard → Pilih Modul (misal: Aspirasi) → Baca Aspirasi → Logout.

## 16. Admin & Content Management

* Hanya terdapat 1 Application Role: Super Admin.
* Pengurus dari berbagai bidang harus berkoordinasi dengan Super Admin untuk pengkinian data (termasuk stok Kaizen Company).

## 17. Content Strategy

* **Real Content First:** Tidak ada dummy text (Lorem Ipsum) saat peluncuran. Jika data kosong, tampilkan placeholder `[Content Required]`.
* **Sumber Data:** Data kepengurusan dari Sekretaris, berita acara dari PWMU, produk dari Ekowir.

## 18. Functional Requirements

* Sistem harus dapat menyimpan dan menampilkan gambar dengan format WebP.
* Sistem harus memiliki fitur pencarian (search) sederhana khusus pada halaman Berita.
* Sistem harus dapat menandai pengurus/alumni/produk dengan status aktif/inaktif.

## 19. Non-Functional Requirements

* **Design & UI:** Modern + Minimalistic. Font: Plus Jakarta Sans. Website utama = Light Theme. Kaizen Company = Dark Theme.
* **Device Support:** Responsive untuk Desktop, Tablet, Mobile.
* **Performance:** Image optimization wajib diimplementasikan. Waktu muat halaman harus optimal.

## 20. SEO & Discoverability

* Implementasi tag Meta, Title, dan Description yang relevan.
* Open Graph (OG) tags untuk kemudahan sharing link (misal: saat membagikan link berita atau produk Kaizen Company ke grup WhatsApp).

## 21. Analytics & Monitoring

* Integrasi tracking dasar (misal: Google Analytics / platform ringan lainnya - Open Decision) untuk memantau trafik pengunjung dan halaman terpopuler.
* Error tracking untuk mendeteksi apabila terjadi crash di production.

## 22. Security Considerations

* Dashboard tidak boleh terindeks oleh mesin pencari.
* Rate limiting pada form Aspirasi Mahasiswa untuk mencegah SPAM (bot).
* Proteksi terhadap serangan dasar web (XSS, CSRF, SQLi/NoSQLi).

## 23. Backup & Data Reliability

* Database utama harus memiliki mekanisme backup berkala.
* Disediakan fitur export data (misal: CSV) di Dashboard Admin sebagai lapisan backup manual.

## 24. Accessibility Considerations

* Kontras warna yang cukup, terutama saat transisi dari Light Theme (Organisasi) ke Dark Theme (Kaizen Company).
* Alt text pada semua gambar (logo, foto pengurus, produk Kaizen Company).

## 25. Performance Considerations

* Penggunaan CDN (bawaan dari hosting provider FE / Supabase) untuk menyajikan gambar.
* Implementasi Lazy Loading pada galeri produk dan daftar kepengurusan.

## 26. Scalability Considerations

* Menggunakan arsitektur frontend modern (Next.js/Nuxt) yang mudah discale.
* Struktur database dirancang agar tidak breaking saat periode kepengurusan berganti.

## 27. Constraints

* **Tech Stack:** Dilarang menggunakan PHP/Laravel.
* **Domain:** Target penggunaan ekstensi `.org.id` (Budget efisien).
* **Storage:** Terbatas pada gambar (WebP), tidak ada sistem video hosting lokal.

## 28. Assumptions

* Pengguna publik sudah memiliki aplikasi WhatsApp mobile atau web terpasang saat berinteraksi dengan Kaizen Company.
* Semua artikel kegiatan panjang sudah terbit di portal PWMU, sehingga web ini hanya bertindak sebagai direktori tautan.

## 29. Dependencies

* Platform PWMU (ketersediaan artikel).
* Supabase (Database & Storage) uptime.
* Ketersediaan dokumen persyaratan dari Sekretaris/Organisasi untuk melengkapi Content Required.

## 30. Risks & Mitigations

* **Risiko:** Ketergantungan terhadap satu Super Admin (Developer).

  * **Mitigasi:** Pembuatan dokumentasi operasional dan handover plan yang jelas di akhir periode.

* **Risiko:** SPAM pada Aspirasi Mahasiswa (karena anonim).

  * **Mitigasi:** Implementasi proteksi reCAPTCHA / rate limiter sederhana (tanpa login).

* **Risiko:** Link PWMU broken / dihapus sepihak oleh PWMU.

  * **Mitigasi:** Tidak ada mitigasi teknis khusus, Super Admin dapat menghapus direktori berita di dashboard jika link terbukti mati.

## 31. Open Decisions / TBD

Berikut adalah daftar keputusan teknis yang ditunda ke fase Technical Specification:

* Metode Autentikasi Super Admin: (Magic link, Email/Password standard, dll).
* Mekanisme Sinkronisasi PWMU: Apakah manual (CRUD oleh Admin) atau otomatis (via RSS feed/Scraping).
* Frontend Framework: Next.js atau Nuxt.
* Hosting & Domain Provider: Vendor spesifik belum ditentukan.
* Analytics & Monitoring Tools: Pemilihan platform (Google Analytics, Sentry, Vercel Analytics, dll).
* Mekanisme Handover spesifik: Terkait kepemilikan repository GitHub dan penagihan cloud infrastructure.

## 32. V1 Scope Boundary

* **Must Have:** Halaman Beranda, Profil, Kepengurusan, Ekowir, Kaizen Company (Dark Theme + WhatsApp link), Link Aspirasi (Anonim), Admin Dashboard (Super Admin).
* **Should Have:** Integrasi berita ke PWMU, SEO & Open Graph dasar, Export CSV untuk Aspirasi.
* **Could Have:** Dashboard Analytics summary di halaman Admin.
* **Future (Out of Scope V1):** Shopping Cart, Payment Gateway, User Account, Kalender Kegiatan, Direktori Full Alumni, Auto-sync PWMU (jika V1 diputuskan manual).

## 33. Future Enhancements

* Integrasi otomatis feed berita dari PWMU.
* Penambahan sistem inventory tracking dinamis jika bisnis Kaizen Company membesar.

## 34. Success Metrics

* Website sukses live di domain `.org.id` dan dapat diakses stabil oleh publik.
* Super Admin dapat mengubah 100% konten tekstual/gambar dinamis tanpa menyentuh source code.
* Fitur redireksi WhatsApp Kaizen Company berfungsi tanpa error.
* Aspirasi dapat terkirim secara anonim dan masuk ke database Admin tanpa kebocoran data pelapor.
* 0 critical issues/downtime saat peluncuran.

## 35. Definition of Done

* Seluruh Must Have requirement selesai dikembangkan.
* Tidak ada dummy content di production; seluruh informasi menggunakan data riil (atau ditandai Content Required yang disetujui untuk ditunda).
* Website lulus responsive test di Mobile, Tablet, Desktop.
* Dashboard Admin sepenuhnya fungsional dan aksesnya aman.

## 36. Handover & Maintainability Considerations

* Sistem harus didokumentasikan dalam GitHub Organization (Bukan akun personal developer).
* Pembuatan panduan "Cara Mengubah Data Web" khusus untuk pengurus non-teknis.
* Penggunaan akun email organisasi sentral (misal: [admin@kaizen.org.id](mailto:admin@kaizen.org.id)) untuk mendaftar layanan pihak ketiga (Supabase, Hosting, Domain) guna mencegah hilangnya akses jika developer lulus/demisioner.

## 37. Product Discovery Conclusion

Dokumen Product Discovery ini menetapkan scope, visi, dan batasan fungsional dari Website Resmi PK IMM Kaizen V1.0.

Dengan disetujuinya dokumen ini, pengembangan akan dilanjutkan ke tahap pembuatan Product Requirement Document (PRD) dan Technical Specification (yang akan menjawab seluruh Open Decisions).

Fiksasi batasan bahwa sistem ini adalah representasi informasi, etalase bisnis, dan wadah umpan balik (bukan e-commerce kompleks) merupakan kunci agar proyek V1.0 sukses, hemat biaya, dan maintainable.
