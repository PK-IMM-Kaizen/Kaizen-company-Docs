# Technical Specification — Content & Module Architecture

## 1. Content Management Architecture

Website Resmi PK IMM Kaizen V1.1 menggunakan pendekatan **centralized content management** melalui satu area administrasi yang dikendalikan oleh Super Admin.

Seluruh konten dinamis yang membutuhkan perubahan tanpa modifikasi source code dikelola melalui dashboard.

Module utama yang dikelola meliputi:

- Organization Profile;
- Kepengurusan;
- Bidang;
- Berita;
- Kajian & Pemikiran;
- Alumni;
- Ekowir;
- Kaizen Company;
- Aspirasi.

Tujuan utama arsitektur content management adalah memastikan:

- konten publik dapat diperbarui tanpa perubahan source code;
- ownership konten tetap terpusat;
- data organisasi dapat bertahan melewati pergantian kepengurusan;
- status publikasi dapat dikontrol;
- konten internal tidak bocor ke public website.

---

# 2. Content Lifecycle

Content lifecycle V1 menggunakan state sederhana sesuai kebutuhan masing-masing module.

Secara umum:

    Create / Edit
         ↓
       Draft
         ↓
      Publish
         ↓
     Published
         ↓
    Unpublish
         ↓
    Unpublished

Content yang tidak lagi diperlukan dapat dihapus melalui dashboard sesuai hak akses Super Admin.

Tidak digunakan workflow approval multi-level pada V1.

Jika diperlukan approval workflow yang lebih kompleks, hal tersebut menjadi pengembangan di luar arsitektur V1.

---

# 3. Content Visibility

Visibility content ditentukan pada server-side dan bukan hanya pada frontend.

Secara konseptual:

    Content Database
          ↓
      Status Check
          ↓
      Public API
          ↓
      Public Website

Content yang berstatus:

    Published / Active

dapat ditampilkan kepada public sesuai aturan module.

Sedangkan content yang berstatus:

    Draft / Unpublished / Inactive

tidak boleh dikembalikan oleh public API.

Content yang tidak aktif tetap dapat disimpan untuk kebutuhan internal, historical data, atau pengelolaan berikutnya.

---

# 4. Organization Profile Module

## 4.1 Purpose

Module Organization Profile digunakan untuk mengelola informasi resmi organisasi.

Data digunakan oleh halaman:

- Profil;
- Kontak;
- bagian informasi organisasi lainnya.

## 4.2 Management

Super Admin dapat:

- melihat data;
- membuat data;
- mengubah data;
- memperbarui informasi;
- mengelola informasi kontak.

Informasi organisasi merupakan bagian dari official content sehingga perubahan harus dilakukan dengan mempertimbangkan validitas informasi resmi organisasi.

## 4.3 Public Visibility

Organization Profile yang aktif digunakan oleh public website.

Tidak diperlukan sistem Draft/Published yang kompleks apabila informasi organisasi menggunakan model single active profile.

---

# 5. Kepengurusan Module

## 5.1 Purpose

Module Kepengurusan digunakan untuk menampilkan struktur kepengurusan PK IMM Kaizen.

## 5.2 Data

Data konseptual anggota kepengurusan meliputi:

- nama;
- foto;
- posisi;
- bidang;
- status.

## 5.3 Status Management

Setiap anggota kepengurusan memiliki status aktif/inaktif.

Contoh:

    Active
    Inactive

Anggota aktif ditampilkan pada website publik.

Anggota yang menjadi tidak aktif tidak harus dihapus dari database.

Hal ini memungkinkan historical data tetap tersedia pada area administrasi.

## 5.4 Administrative Operations

Super Admin dapat:

- create;
- read;
- update;
- delete;
- activate;
- deactivate.

---

# 6. Bidang Module

## 6.1 Purpose

Module Bidang digunakan untuk menampilkan informasi bidang/divisi yang terdapat dalam organisasi.

## 6.2 Data

Data konseptual meliputi:

- nama bidang;
- deskripsi;
- informasi bidang;
- status publikasi.

## 6.3 Visibility

Bidang yang dipublikasikan dapat ditampilkan pada public website.

Bidang yang tidak dipublikasikan tidak boleh muncul pada public interface.

## 6.4 Administrative Operations

Super Admin dapat:

- create;
- read;
- update;
- delete;
- publish;
- unpublish.

---

# 7. Berita Module

## 7.1 Purpose

Module Berita berfungsi sebagai **directory/aggregator berita**.

Website tidak menduplikasi seluruh isi artikel dari PWMU.

Informasi berita yang disimpan pada sistem digunakan untuk membuat directory card yang mengarahkan pengguna ke sumber berita asli.

## 7.2 Data

Data konseptual meliputi:

- title;
- short description;
- thumbnail;
- PWMU URL;
- status.

## 7.3 Public Display

Berita ditampilkan dalam bentuk card atau directory item.

Card dapat berisi:

- thumbnail;
- judul;
- deskripsi singkat;
- action menuju sumber PWMU.

## 7.4 External Redirect

Ketika pengguna memilih berita:

    Website PK IMM Kaizen
             ↓
          PWMU

Link PWMU dibuka pada tab baru.

Website tidak menjadi canonical source dari full article PWMU.

## 7.5 Search

V1 menyediakan simple search pada module Berita.

Search dilakukan terhadap informasi berita yang tersedia pada sistem.

## 7.6 Synchronization

Integrasi PWMU masih merupakan technical decision.

V1 dapat menggunakan pendekatan manual entry.

Apabila di masa mendatang digunakan RSS atau scraping, perubahan tersebut tidak boleh mengubah prinsip bahwa artikel PWMU tetap merupakan external source.

---

# 8. Kajian & Pemikiran Module

## 8.1 Purpose

Module Kajian & Pemikiran digunakan untuk menyediakan konten pemikiran secara native pada platform.

Berbeda dengan Berita, konten Kajian disimpan dan ditampilkan langsung pada website.

TSS Revised menetapkan Kajian sebagai bagian teknis yang harus didukung oleh arsitektur.

## 8.2 Homepage Section

Kajian ditampilkan sebagai section pada halaman Beranda.

Section dapat menampilkan beberapa Kajian yang berstatus Published.

Setiap item dapat berisi:

- thumbnail;
- title;
- excerpt;
- author;
- action `Baca Selengkapnya`.

## 8.3 Detail Page

Setiap Kajian memiliki standalone detail page.

Dynamic route:

    /kajian/[slug]

Slug harus unique.

Contoh konseptual:

    /kajian/pemikiran-mahasiswa-dalam-perubahan-sosial

Detail page menampilkan konten lengkap Kajian.

## 8.4 Content Fields

Entity Kajian secara konseptual memiliki:

- ID;
- title;
- unique slug;
- excerpt;
- thumbnail URL;
- author;
- content;
- published_at;
- status;
- created_at;
- updated_at.

## 8.5 Content Status

Kajian menggunakan tiga status utama:

    Draft
    Published
    Unpublished

Rules:

- Draft tidak dapat diakses public;
- Published dapat diakses public;
- Unpublished tidak dapat diakses public.

Public API harus memastikan content visibility berdasarkan status.

## 8.6 Rich Text Content

Content Kajian dapat menggunakan format rich text atau Markdown sesuai keputusan technical implementation.

Jika rich text digunakan, content harus melalui sanitization sebelum dirender.

Raw HTML tidak boleh langsung dirender tanpa mekanisme sanitization yang sesuai.

## 8.7 Missing Content

Jika slug tidak ditemukan atau content tidak memenuhi visibility requirement, public application harus mengembalikan halaman:

    404 Not Found

Draft dan Unpublished tidak boleh dibocorkan melalui response public.

## 8.8 Author

Author attribution masih merupakan technical open decision.

Alternatif yang tercatat:

- free text author;
- relation terhadap management member.

Keputusan final dilakukan pada tahap Database Design.

## 8.9 Publishing Workflow

V1 tidak membutuhkan approval workflow multi-role.

Super Admin menjadi pihak yang melakukan pengelolaan dan publikasi Kajian.

Koordinasi dengan bidang terkait dapat dilakukan di luar sistem.

---

# 9. Alumni Module

## 9.1 Purpose

Module Alumni digunakan untuk menampilkan alumni inspiratif pada public website.

## 9.2 Data

Data alumni dikelola oleh Super Admin.

Data memiliki mekanisme status publikasi sehingga alumni yang tidak ingin atau tidak perlu ditampilkan dapat disembunyikan tanpa harus menghapus data secara permanen.

## 9.3 Visibility

Hanya alumni yang memenuhi status publikasi yang dapat ditampilkan pada public website.

Data yang tidak aktif tetap dapat disimpan sebagai historical/internal data.

## 9.4 Administrative Operations

Super Admin dapat:

- create;
- read;
- update;
- delete;
- publish;
- unpublish.

---

# 10. Ekowir Module

## 10.1 Purpose

Ekowir digunakan sebagai area yang menampilkan aktivitas atau produk kewirausahaan organisasi.

Kaizen Company menjadi bagian penting dari area economic/business showcase.

## 10.2 Content Management

Super Admin dapat mengelola:

- informasi Ekowir;
- produk;
- status produk;
- informasi pendukung.

## 10.3 Visibility

Produk atau content yang tidak aktif tidak ditampilkan kepada public.

---

# 11. Kaizen Company Module

## 11.1 Purpose

Kaizen Company merupakan catalog produk dan/atau layanan yang dapat ditampilkan kepada public.

Module ini tidak berfungsi sebagai e-commerce penuh.

Tujuan utama adalah:

- product showcase;
- service showcase;
- informasi produk;
- direct contact melalui WhatsApp.

## 11.2 Theme

Kaizen Company menggunakan **Dark Theme** yang berbeda dari main organization website yang menggunakan Light Theme.

Perbedaan theme harus ditangani melalui dedicated layout:

    DarkLayout

## 11.3 Product Data

Data konseptual produk meliputi:

- nama produk;
- foto;
- harga;
- deskripsi;
- kategori;
- stock display;
- status.

## 11.4 Product Status

Produk menggunakan status:

    Active
    Inactive

Produk Active dapat ditampilkan kepada public.

Produk Inactive tidak ditampilkan kepada public.

Data produk Inactive tetap dapat disimpan di database.

## 11.5 Product Detail

Public user dapat membuka detail produk untuk melihat informasi lengkap.

Detail product page harus menyediakan CTA untuk menghubungi penjual melalui WhatsApp.

## 11.6 WhatsApp Flow

Flow:

    Product Detail
         ↓
    Hubungi Penjual / Beli via WhatsApp
         ↓
    Pre-filled WhatsApp Message
         ↓
    WhatsApp

Frontend membangun URL WhatsApp menggunakan nomor admin/penjual dan pesan yang telah di-encode.

Tidak terdapat:

- shopping cart;
- checkout;
- payment gateway;
- order management;
- transaction processing.

## 11.7 Website Development Service

Kaizen Company juga dapat menampilkan **Website Development** sebagai service.

Service tetap mengikuti prinsip catalog/showcase.

Transaksi dilakukan di luar sistem melalui komunikasi langsung.

---

# 12. Aspirasi Module

## 12.1 Purpose

Module Aspirasi menyediakan mekanisme bagi mahasiswa untuk menyampaikan aspirasi secara anonim.

Aspirasi dirancang sebagai **one-way anonymous submission**.

## 12.2 Access

Aspirasi dapat diakses oleh public tanpa login.

Akses dapat ditemukan melalui:

    Beranda
       ↓
    FAQ / Aspirasi
       ↓
    Form Aspirasi

## 12.3 Form

Form hanya meminta content aspirasi.

Tidak meminta:

- nama;
- email;
- nomor telepon;
- akun pengguna;
- login.

## 12.4 Storage

Aspirasi disimpan ke database.

Data minimal meliputi:

- ID;
- text/content;
- timestamp.

Entity aspirasi tidak boleh menyimpan:

    user_id
    name
    email
    phone
    ip_address

## 12.5 Spam Protection

Endpoint aspirasi harus memiliki protection terhadap spam.

Mekanisme yang direkomendasikan:

- honeypot;
- rate limiter.

IP dapat digunakan oleh rate limiting middleware tetapi tidak disimpan sebagai bagian dari data aspirasi.

## 12.6 Submission Flow

Flow:

    Public User
        ↓
    Aspirasi Form
        ↓
    Server Validation
        ↓
    Spam Protection
        ↓
    Database
        ↓
    Success Response

## 12.7 Public Visibility

Aspirasi tidak dipublikasikan kepada public.

Tidak tersedia:

- public aspiration list;
- public comments;
- public replies;
- aspiration tracking.

Aspirasi hanya dapat dibaca oleh Super Admin melalui dashboard.

## 12.8 Administrative Operations

Super Admin dapat:

- melihat aspirasi;
- membaca aspirasi;
- menghapus aspirasi.

Tidak terdapat fitur public response pada V1.

---

# 13. Dashboard Module Architecture

Dashboard merupakan centralized management center untuk Super Admin.

Secara konseptual:

    Super Admin
         ↓
    Admin Dashboard
         ↓
    ┌───────────────┐
    │ Organization  │
    │ Kepengurusan  │
    │ Bidang        │
    │ Berita        │
    │ Kajian        │
    │ Alumni        │
    │ Ekowir        │
    │ Kaizen Co.    │
    │ Aspirasi      │
    └───────────────┘

Dashboard tidak menggunakan multi-role permission pada V1.

---

# 14. Dashboard Content Operations

Untuk module yang memiliki content lifecycle, dashboard harus menyediakan operasi yang sesuai.

Secara umum:

| Module | Create | Read | Update | Delete | Status |
|---|---:|---:|---:|---:|---|
| Organization Profile | Yes | Yes | Yes | Yes | Active/Live |
| Kepengurusan | Yes | Yes | Yes | Yes | Active/Inactive |
| Bidang | Yes | Yes | Yes | Yes | Published/Unpublished |
| Berita | Yes | Yes | Yes | Yes | Published/Unpublished |
| Kajian | Yes | Yes | Yes | Yes | Draft/Published/Unpublished |
| Alumni | Yes | Yes | Yes | Yes | Published/Unpublished |
| Ekowir | Yes | Yes | Yes | Yes | Published/Unpublished |
| Kaizen Company | Yes | Yes | Yes | Yes | Active/Inactive |
| Aspirasi | No | Yes | No | Yes | Internal |

Status dan operation detail dapat disempurnakan pada API Specification dan Database Design.

---

# 15. Media Handling per Content Module

Content yang menggunakan image harus mengikuti media architecture yang ditentukan pada TSS.

Image requirements:

- image only;
- supported format: PNG, JPG, JPEG, WebP;
- maximum recommended size: 2 MB;
- automatic WebP conversion recommended;
- optimized storage;
- lazy loading pada public interface.

Module yang dapat menggunakan image antara lain:

- Kepengurusan;
- Berita;
- Kajian;
- Alumni;
- Ekowir;
- Kaizen Company.

Image tidak disimpan sebagai binary utama di relational database.

Storage image menggunakan object storage.

Database menyimpan reference/URL terhadap media tersebut.

---

# 16. Module-to-Frontend Relationship

Setiap module memiliki frontend presentation layer masing-masing.

Secara konseptual:

    Database
        ↓
    API / Application Layer
        ↓
    Module Data
        ↓
    Frontend Component
        ↓
    Public Interface / Admin Interface

Frontend tidak boleh mengakses database secara langsung.

Frontend hanya menerima data melalui application/API layer.

---

# 17. Module-to-Database Relationship

Module content memiliki entity database masing-masing sesuai kebutuhan.

Konseptual mapping:

| Module | Primary Entity |
|---|---|
| Authentication | Users |
| Organization | Organization Profile |
| Kepengurusan | Management Members |
| Bidang | Divisions |
| Berita | News |
| Kajian | Kajian |
| Alumni | Alumni |
| Ekowir | Products / related content |
| Kaizen Company | Products |
| Aspirasi | Aspirations |

Struktur relasional detail dan hubungan antar-entity ditentukan pada dokumen **Database Design**.

---

# 18. Module-to-API Relationship

Setiap module yang membutuhkan dynamic data akan berkomunikasi melalui API/application layer.

Contoh konseptual:

    Public Website
         ↓
    Public API
         ↓
    Module Data
         ↓
    Database

Sedangkan dashboard menggunakan:

    Admin Dashboard
         ↓
    Protected Admin API
         ↓
    Authentication
         ↓
    Module Data
         ↓
    Database

Detail endpoint tidak ditentukan dalam dokumen ini dan akan dibahas pada **API Specification**.

---

# 19. Cross-Module Rules

Beberapa rules berlaku lintas module:

### Rule 1 — Server-side Visibility

Status content harus diperiksa di server.

### Rule 2 — Admin-only Mutation

Perubahan content hanya dapat dilakukan melalui authenticated Super Admin.

### Rule 3 — Historical Data

Data yang menjadi inactive/unpublished tidak otomatis dihapus.

### Rule 4 — Public API Filtering

Public API hanya mengembalikan data yang memenuhi public visibility rules.

### Rule 5 — Media Validation

Uploaded image harus divalidasi sebelum disimpan.

### Rule 6 — Security

User input harus divalidasi dan disanitasi sesuai jenis content.

### Rule 7 — No Unnecessary Complexity

Module V1 tidak boleh berkembang menjadi sistem yang memiliki workflow kompleks yang tidak diperlukan oleh product scope.

---

# 20. Content Security Considerations

Module yang menerima user-generated atau admin-generated content harus memperhatikan security.

Area dengan risiko paling tinggi adalah:

- Kajian rich text;
- Aspirasi text input;
- external URLs;
- image upload.

Security controls mencakup:

- server-side validation;
- sanitization;
- safe rendering;
- file validation;
- size validation;
- allowed extension;
- protected admin API;
- rate limiting;
- safe error response.

Raw HTML tidak boleh dirender tanpa sanitization yang sesuai.

---

# 21. Content Error States

Setiap module public harus memiliki state minimal:

    Loading
    Error
    Empty

Untuk content yang memang diperlukan agar halaman dapat berfungsi, empty state dapat memberikan pesan:

    Content Required

Contoh:

- tidak ada berita;
- tidak ada Kajian Published;
- tidak ada produk Active;
- tidak ada alumni Published.

Error state tidak boleh menampilkan informasi internal seperti database error atau server stack trace.

---

# 22. Module Architecture Constraints

Arsitektur module V1 mengikuti constraint berikut:

1. Semua content dikelola melalui centralized Super Admin dashboard.
2. Tidak ada multi-role content management.
3. Tidak ada public account.
4. Tidak ada public comments/forum.
5. Tidak ada payment processing.
6. Tidak ada shopping cart.
7. Tidak ada checkout.
8. Tidak ada order management.
9. Berita tetap mengarah ke PWMU sebagai external source.
10. Kajian disimpan sebagai native content.
11. Aspirasi tetap anonymous.
12. Draft dan Unpublished content tidak boleh tampil kepada public.
13. Inactive product tidak boleh tampil kepada public.
14. Historical data tidak harus dihapus ketika status berubah.
15. Detail API dan database schema didefinisikan pada dokumen berikutnya.

---

# 23. Technical Decisions Related to Content & Modules

| Decision | Status | Current Direction |
|---|---|---|
| Centralized CMS | Decided | Super Admin Dashboard |
| Public Accounts | Decided | Tidak tersedia |
| Multi-role CMS | Decided | Tidak tersedia pada V1 |
| Berita Model | Decided | External PWMU Directory |
| Kajian Model | Required by TSS Revised | Native Content |
| Kajian Detail Route | Decided | `/kajian/[slug]` |
| Kajian Author Relation | Open Decision | Free Text / Management Relation |
| Kajian Approval Workflow | Open Decision | Offline Coordination recommended |
| Kaizen Company | Decided | Product/Service Catalog |
| Kaizen Transaction | Decided | External WhatsApp |
| Payment Gateway | Out of Scope | Tidak tersedia |
| Aspirasi | Decided | Anonymous One-way Submission |
| Aspiration Public Tracking | Decided | Tidak tersedia |
| Spam Protection | Recommended | Honeypot + Rate Limiter |
| Image Storage | Decided | Object Storage |
| Image Format | Decided | WebP preferred |
| Rich Text Format | Open Decision | Markdown recommended |

---

# 24. Relationship with Next Technical Stages

Content & Module Architecture menjadi penghubung antara application architecture dengan detail implementation.

Alur teknis:

    TSS System Architecture
             ↓
    Frontend Architecture
             ↓
    Backend & Database Architecture
             ↓
    Content & Module Architecture
             ↓
    API / Security / Media Specification
             ↓
    Database Design
             ↓
    API Specification
             ↓
    UI/UX Specification
             ↓
    Development

Dokumen berikutnya akan membahas API, security, dan media secara lebih khusus.

---

## Navigation

- [← TSS Backend & Database Architecture](./04-tss-backend-and-database-architecture.md)
- [TSS API, Security & Media →](./06-tss-api-security-and-media.md)
