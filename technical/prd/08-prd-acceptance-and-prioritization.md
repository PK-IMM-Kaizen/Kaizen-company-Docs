# Product Requirement Document — Acceptance & Prioritization

## Document Information

| Field | Value |
|---|---|
| Product | Website Resmi PK IMM Kaizen |
| Organization | Pimpinan Komisariat Ikatan Mahasiswa Muhammadiyah Kaizen Universitas Muhammadiyah Surabaya |
| Document Type | Product Requirement Document |
| Version | 1.1 Revised |
| Status | Draft |
| Stage | Product Requirements |
| Next Stage | Technical Specification |
| Last Updated | September 2026 |

---

## 1. Overview

Dokumen ini mendefinisikan kriteria penerimaan (*acceptance criteria*), prioritas V1, *Definition of Done*, kesiapan rilis, serta keputusan terbuka yang masih perlu diselesaikan sebelum masuk ke tahap Technical Specification.

Acceptance criteria digunakan sebagai acuan untuk memastikan requirement utama telah memenuhi perilaku yang diharapkan dari sisi pengguna maupun sistem.

Prioritization digunakan untuk menjaga batas V1 agar pengembangan tetap fokus pada tujuan utama produk.

---

# 2. Acceptance Criteria

## AC-001 — Kaizen Company WhatsApp Redirection

### Objective

Memastikan pengguna dapat menghubungi pihak terkait melalui WhatsApp dari katalog Kaizen Company tanpa adanya sistem transaksi atau pembayaran di dalam platform.

### Given

Pengguna publik sedang berada pada halaman detail produk atau layanan Kaizen Company.

### When

Pengguna menekan tombol:

- `Hubungi Penjual`
- atau `Beli via WA`

### Then

Sistem harus:

1. Membuka WhatsApp.
2. Mengarahkan pengguna ke nomor WhatsApp yang telah dikonfigurasi.
3. Menyertakan template pesan yang relevan dengan produk atau layanan yang dipilih.
4. Tidak membuat transaksi atau pembayaran di dalam website.

### Expected Result

Pengguna dapat melanjutkan komunikasi dan proses transaksi melalui WhatsApp.

---

## AC-002 — Anonymous Aspiration Submission

### Objective

Memastikan mahasiswa atau pengguna publik dapat menyampaikan aspirasi secara anonim tanpa harus membuat akun atau memberikan identitas pribadi.

### Given

Pengguna publik mengakses fitur `Aspirasi Mahasiswa` melalui bagian FAQ atau akses yang telah disediakan pada website.

### When

Pengguna:

1. Mengisi teks aspirasi.
2. Menekan tombol submit.
3. Tidak melakukan login.
4. Tidak memberikan nama, email, atau nomor telepon.

### Then

Sistem harus:

1. Menerima aspirasi.
2. Menyimpan isi aspirasi ke database.
3. Menyimpan timestamp submission.
4. Tidak meminta identitas pribadi.
5. Menampilkan feedback bahwa aspirasi berhasil dikirim.

### Expected Result

Aspirasi tersimpan dan dapat dilihat oleh Super Admin tanpa mengungkap identitas pengirim.

---

## AC-003 — Admin CRUD & Content Visibility

### Objective

Memastikan Super Admin dapat mengelola konten dan mengontrol apakah suatu data ditampilkan pada website publik.

### Given

Super Admin telah berhasil masuk ke dashboard administrasi.

### When

Super Admin mengubah status suatu entitas dari:

- `Publish` menjadi `Draft`
- atau `Aktif` menjadi `Inaktif`

### Then

Sistem harus:

1. Menyimpan perubahan status.
2. Menghilangkan data tersebut dari tampilan publik jika status tidak lagi aktif/published.
3. Tetap mempertahankan data dalam sistem administrasi.
4. Tidak menghapus data historis hanya karena status berubah.

### Expected Result

Konten yang tidak aktif tidak muncul di website publik, tetapi tetap tersedia bagi Super Admin untuk pengelolaan dan kebutuhan historis.

---

## AC-004 — PWMU Redirection

### Objective

Memastikan berita yang bersumber dari PWMU tetap merujuk ke artikel asli tanpa menduplikasi keseluruhan konten artikel pada website.

### Given

Pengguna publik melihat kartu berita pada halaman `Berita`.

### When

Pengguna menekan tombol atau link:

`Lihat selengkapnya di PWMU`

### Then

Sistem harus:

1. Membuka URL artikel PWMU asli.
2. Membuka artikel pada browser tab baru.
3. Tidak menduplikasi keseluruhan artikel PWMU sebagai artikel native pada platform.

### Expected Result

Pengguna dapat membaca artikel lengkap pada sumber aslinya di PWMU.

---

## AC-005 — Kajian & Pemikiran Public Detail

### Objective

Memastikan konten Kajian & Pemikiran dapat dibaca sebagai konten native pada platform apabila modul tersebut disetujui untuk V1.

### Given

Pengguna publik berada pada halaman Beranda dan melihat section `Kajian & Pemikiran`.

### When

Pengguna menekan tombol:

`Baca Selengkapnya`

### Then

Sistem harus:

1. Mengarahkan pengguna ke halaman detail Kajian.
2. Menggunakan URL detail yang unik.
3. Menampilkan konten artikel secara penuh.
4. Tidak hanya menampilkan ringkasan atau preview.

### Expected Result

Pengguna dapat membaca artikel Kajian & Pemikiran pada halaman detail standalone.

### Decision Dependency

Requirement ini bergantung pada keputusan apakah modul `Kajian & Pemikiran` menjadi bagian dari V1 atau ditunda ke fase berikutnya.

---

# 3. V1 Prioritization

Prioritas V1 digunakan untuk menentukan fitur yang wajib tersedia pada saat peluncuran dan fitur yang masih dapat ditunda.

## 3.1 Priority Categories

| Priority | Meaning |
|---|---|
| Must Have | Wajib tersedia untuk V1 dan menjadi bagian dari release baseline |
| Should Have | Penting tetapi dapat ditunda apabila terdapat keterbatasan waktu atau resource |
| Could Have | Nilai tambah dan tidak menjadi blocker V1 |
| Future | Tidak termasuk V1 dan direncanakan untuk fase pengembangan berikutnya |
| Open Decision | Belum dapat ditetapkan sebelum keputusan produk dibuat |

---

# 4. V1 Feature Prioritization

| Feature / Module | Priority | Rationale |
|---|---|---|
| Kaizen Company | Must Have | Prioritas bisnis/Ekowir dan salah satu fokus utama produk |
| Admin Dashboard | Must Have | Menjadi pusat pengelolaan seluruh konten dinamis |
| Aspirasi Mahasiswa | Must Have | Mendukung fungsi evaluasi dan penyampaian aspirasi |
| Beranda | Must Have | Entry point utama dan membentuk first impression |
| Profil | Must Have | Menyediakan identitas resmi organisasi |
| Kepengurusan | Must Have | Mendukung transparansi struktur organisasi |
| Bidang | Must Have | Menjelaskan struktur dan bidang organisasi |
| Kajian & Pemikiran | Open Decision | Requirement baru yang perlu dipastikan statusnya terhadap launch V1 |
| Berita | Must Have | Menjadi media dokumentasi dan publikasi aktivitas organisasi |
| Alumni Showcase | Must Have | Mendukung representasi dan inspirasi alumni |
| Kontak | Must Have | Menyediakan kanal komunikasi publik |

---

# 5. Must Have — V1 Baseline

Fitur berikut menjadi baseline utama V1.

## 5.1 Kaizen Company

Harus tersedia:

- katalog produk/layanan;
- informasi produk;
- status aktif/inaktif;
- detail produk;
- CTA WhatsApp;
- template pesan WhatsApp;
- dark theme khusus Kaizen Company;
- pengelolaan produk melalui Super Admin.

Tidak termasuk:

- shopping cart;
- checkout;
- payment gateway;
- transaksi internal website.

---

## 5.2 Admin Dashboard

Harus tersedia:

- autentikasi Super Admin;
- dashboard administrasi;
- pengelolaan konten;
- CRUD;
- status publish/draft atau aktif/inaktif;
- image upload;
- validasi input;
- feedback success/error;
- konfirmasi tindakan destruktif;
- pengelolaan aspirasi.

---

## 5.3 Aspirasi Mahasiswa

Harus tersedia:

- akses publik;
- submission tanpa login;
- input teks;
- anonim;
- penyimpanan timestamp;
- perlindungan terhadap spam;
- feedback setelah submission;
- akses aspirasi melalui Super Admin.

Tidak termasuk:

- public discussion;
- komentar;
- forum;
- public tracking;
- akun pengguna.

---

## 5.4 Beranda

Harus tersedia sebagai entry point utama website.

Beranda harus menjadi tempat untuk mengakses atau melihat informasi penting seperti:

- identitas organisasi;
- informasi utama;
- section Kajian & Pemikiran apabila disetujui untuk V1;
- FAQ;
- akses Aspirasi Mahasiswa;
- CTA menuju Kaizen Company.

---

## 5.5 Profil, Kepengurusan, dan Bidang

Harus tersedia untuk menyediakan:

- identitas organisasi;
- struktur kepengurusan;
- informasi bidang;
- informasi anggota/pengurus yang relevan;
- status aktif/inaktif.

Data yang tidak aktif dapat disembunyikan dari publik tanpa harus menghapus data historis.

---

## 5.6 Berita

Harus tersedia sebagai direktori publik.

Berita V1 menggunakan pendekatan:

> Directory / Highlight → Redirect to PWMU

Data yang ditampilkan dapat mencakup:

- thumbnail;
- judul;
- excerpt;
- URL PWMU.

Artikel lengkap tetap berada pada sumber PWMU.

---

## 5.7 Alumni Showcase

Harus tersedia sebagai bagian dari representasi organisasi.

Status alumni dapat digunakan untuk mengontrol visibilitas data publik.

---

## 5.8 Kontak

Harus tersedia sebagai kanal komunikasi publik organisasi.

---

# 6. Should Have

Fitur berikut memiliki nilai tambahan tetapi bukan blocker utama V1.

## 6.1 PWMU Integration Enhancement

Integrasi berita PWMU dapat dikembangkan lebih lanjut setelah mekanisme dasar redirect berjalan.

Contoh kemungkinan pengembangan:

- sinkronisasi konten;
- RSS;
- automation;
- scraping.

Namun mekanisme sinkronisasi otomatis masih merupakan keputusan terbuka.

---

## 6.2 SEO & Open Graph

Dapat mencakup:

- page title;
- meta description;
- Open Graph;
- optimasi metadata untuk halaman publik.

SEO dan OG tetap direkomendasikan untuk production readiness, tetapi prioritasnya berada setelah baseline fungsi utama.

---

## 6.3 CSV Export

CSV export dapat digunakan untuk kebutuhan:

- backup data tertentu;
- pengelolaan data;
- kebutuhan handover;
- migrasi sederhana.

---

# 7. Could Have

## 7.1 Admin Analytics Summary

Dashboard dapat memiliki ringkasan analytics dasar seperti:

- jumlah kunjungan;
- pembacaan official information;
- penggunaan Knowledge Hub;
- aktivitas tertentu pada website.

Fitur ini bukan blocker utama untuk V1.

---

# 8. Future Scope

Fitur berikut secara eksplisit tidak termasuk V1.

## 8.1 Shopping Cart

Sistem keranjang belanja.

---

## 8.2 Payment Gateway

Pembayaran langsung melalui website.

---

## 8.3 User Accounts

Akun publik atau akun mahasiswa untuk pengguna website.

---

## 8.4 Event Calendar

Sistem kalender/event management penuh.

---

## 8.5 Full Alumni Directory

Direktori alumni yang lebih lengkap dan terstruktur.

---

## 8.6 Automatic PWMU Synchronization

Sinkronisasi otomatis dengan PWMU apabila mekanisme manual dipilih untuk V1.

---

# 9. Open Decisions

Beberapa keputusan produk masih harus dikonfirmasi sebelum requirement dapat dianggap final.

## OD-001 — Kajian & Pemikiran V1 Priority

### Question

Apakah `Kajian & Pemikiran` merupakan launch blocker dan wajib masuk V1?

### Current Status

`OPEN DECISION`

### Impact

Keputusan ini akan memengaruhi:

- scope V1;
- functional requirements;
- content management;
- data model;
- admin dashboard;
- acceptance criteria;
- technical specification.

---

## OD-002 — Author Attribution

### Question

Bagaimana identitas penulis Kajian & Pemikiran akan ditampilkan?

Kemungkinan model:

- nama penulis;
- nama bidang;
- nama organisasi;
- tanpa attribution publik.

### Current Status

`OPEN DECISION`

### Impact

Akan memengaruhi struktur data Kajian dan tampilan artikel.

---

## OD-003 — Kajian Approval Workflow

### Question

Apakah artikel Kajian memerlukan approval workflow sebelum dapat dipublish?

### Current Status

`OPEN DECISION`

### Impact

Jika diperlukan, workflow dapat berkembang menjadi:

`Draft → Review → Publish`

Jika tidak diperlukan, workflow dapat tetap menggunakan:

`Draft → Publish → Unpublish → Delete`

---

# 10. Definition of Done — V1

V1 dapat dianggap selesai apabila seluruh requirement Must Have telah diimplementasikan dan memenuhi acceptance criteria yang relevan.

## 10.1 Functional Completion

- [ ] Seluruh fitur Must Have telah tersedia.
- [ ] Seluruh functional requirement yang relevan telah diimplementasikan.
- [ ] CRUD Super Admin berfungsi.
- [ ] Status publish/draft atau aktif/inaktif berfungsi.
- [ ] Aspirasi anonim dapat dikirim.
- [ ] Aspirasi dapat dikelola Super Admin.
- [ ] Kaizen Company dapat menampilkan produk/layanan aktif.
- [ ] CTA WhatsApp berfungsi.
- [ ] Berita dapat mengarah ke PWMU.
- [ ] Data organisasi dapat ditampilkan dengan benar.

---

## 10.2 Content Completion

- [ ] Tidak ada dummy content yang tersisa pada production.
- [ ] Data organisasi menggunakan data resmi.
- [ ] Informasi kepengurusan menggunakan data resmi.
- [ ] Produk/layanan Kaizen Company menggunakan data yang telah dikonfirmasi.
- [ ] Link eksternal telah diverifikasi.
- [ ] Image telah menggunakan format yang sesuai.

---

## 10.3 UX & Responsive Completion

- [ ] Website dapat digunakan pada desktop.
- [ ] Website dapat digunakan pada tablet.
- [ ] Website dapat digunakan pada mobile.
- [ ] Navigasi utama berfungsi.
- [ ] CTA utama dapat ditemukan dengan jelas.
- [ ] Feedback success/error tersedia pada interaksi penting.
- [ ] Tidak terdapat critical usability issue yang menghambat penggunaan.

---

## 10.4 Security Completion

- [ ] Dashboard tidak dapat diakses tanpa autentikasi.
- [ ] Dashboard tidak diindeks search engine.
- [ ] Input pengguna divalidasi.
- [ ] Aspirasi memiliki perlindungan terhadap spam.
- [ ] Perlindungan XSS diterapkan.
- [ ] Perlindungan CSRF diterapkan apabila relevan dengan mekanisme autentikasi.
- [ ] Perlindungan SQL/NoSQL injection diterapkan sesuai teknologi database.
- [ ] Hak akses Super Admin diterapkan dengan benar.

---

## 10.5 Production Completion

- [ ] Website telah di-deploy ke production.
- [ ] Domain target `.org.id` telah dikonfigurasi.
- [ ] HTTPS aktif.
- [ ] Asset/image loading berfungsi.
- [ ] External links telah diverifikasi.
- [ ] Tidak terdapat critical launch issue.
- [ ] Tidak terdapat critical downtime pada saat release validation.

---

# 11. Handover Readiness

Karena produk harus dapat diteruskan setelah masa pengembangan awal, V1 tidak hanya dinilai dari sisi functionality tetapi juga maintainability dan ownership.

## 11.1 Repository

- [ ] Source code berada pada GitHub Organization.
- [ ] Repository tidak bergantung pada personal account developer.
- [ ] Dokumentasi teknis tersedia.
- [ ] Struktur project dapat dipahami oleh developer lain.

---

## 11.2 Infrastructure Ownership

- [ ] Domain berada di bawah kepemilikan organisasi.
- [ ] Hosting menggunakan akun organisasi.
- [ ] Database menggunakan akun organisasi.
- [ ] Storage menggunakan akun organisasi.
- [ ] Service eksternal penting menggunakan email organisasi.
- [ ] Billing tidak bergantung pada akun personal developer.

---

## 11.3 Operational Documentation

Dokumentasi minimal harus mencakup:

- cara mengakses dashboard;
- cara mengubah data website;
- cara mengelola produk;
- cara mengelola berita;
- cara mengelola data organisasi;
- cara melihat aspirasi;
- prosedur dasar backup;
- informasi ownership layanan.

Dokumentasi non-teknis harus tersedia dalam bentuk panduan yang dapat digunakan oleh pengurus/admin.

---

# 12. Release Readiness Checklist

| Area | Requirement | Status |
|---|---|---|
| Core Function | Seluruh Must Have selesai | Required |
| Content | Tidak ada dummy content | Required |
| Admin | Dashboard berfungsi penuh | Required |
| Security | Critical security controls tersedia | Required |
| Responsive | Desktop, tablet, mobile | Required |
| WhatsApp | CTA berjalan sesuai acceptance criteria | Required |
| Aspirasi | Anonymous submission berjalan | Required |
| PWMU | Redirect berjalan | Required |
| SEO | Metadata dasar tersedia | Recommended |
| Backup | Backup mechanism tersedia | Required |
| Handover | Ownership & documentation siap | Required |
| Domain | Target `.org.id` siap | Required |
| Monitoring | Basic monitoring tersedia | Recommended |

---

# 13. V1 Release Principle

V1 tidak dinilai berdasarkan jumlah fitur sebanyak mungkin.

Prioritas release adalah:

1. **Official Identity**
2. **Public Information**
3. **Kaizen Company**
4. **Anonymous Aspiration**
5. **Centralized Super Admin Management**
6. **Production Stability**
7. **Handover Readiness**

Fitur tambahan tidak boleh mengorbankan stabilitas, keamanan, maintainability, atau kesiapan peluncuran V1.

---

# 14. Requirement Readiness

Berdasarkan requirement yang telah didefinisikan, sebagian besar scope V1 telah memiliki:

- product goals;
- user personas;
- user journeys;
- functional requirements;
- business rules;
- module requirements;
- non-functional requirements;
- acceptance criteria;
- prioritization.

Namun terdapat beberapa keputusan yang masih terbuka, khususnya terkait `Kajian & Pemikiran`.

Keputusan terbuka tersebut harus diselesaikan sebelum requirement yang terdampak dikunci untuk tahap Technical Specification.

---

# 15. Transition to Technical Specification

Setelah seluruh keputusan produk yang bersifat blocker diselesaikan, PRD dapat digunakan sebagai baseline untuk tahap Technical Specification.

Technical Specification selanjutnya harus menerjemahkan requirement yang telah disetujui ke dalam spesifikasi teknis tanpa mengubah batasan produk V1 secara sepihak.

Alur pengembangan dokumentasi:

    Product Discovery
           ↓
          PRD
           ↓
    Technical Specification
           ↓
        SDS / SRS
           ↓
    Development / Implementation
           ↓
    Testing & Validation
           ↓
       Production

---

# 16. Final Status

| Item | Status |
|---|---|
| PRD Status | Draft — Ready for Technical Planning |
| V1 Baseline | Defined |
| Acceptance Criteria | Defined |
| Prioritization | Defined |
| Open Decisions | Kajian & Pemikiran, Author Attribution, Approval Workflow |
| Next Stage | Technical Specification |

---

## Navigation

- [← Product Requirement Document — Non-Functional Requirements](./07-prd-non-functional-requirements.md)
- [Product Requirement Document — README →](./README.md)
