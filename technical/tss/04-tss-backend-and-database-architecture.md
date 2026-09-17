# Technical Specification — Backend & Database Architecture

## 1. Backend / Application Architecture

Backend Website Resmi PK IMM Kaizen V1.1 menggunakan pendekatan **Full-stack Monolithic Application**.

Frontend dan backend berada dalam satu codebase serta menggunakan framework full-stack yang sama. API dan application logic dijalankan melalui server-side application layer.

Pendekatan ini dipilih untuk menjaga:

- kesederhanaan arsitektur;
- kemudahan deployment;
- kemudahan maintenance;
- kemudahan handover;
- rendahnya operational complexity;
- konsistensi antara frontend dan backend.

Arsitektur backend tidak menggunakan microservices atau distributed services pada V1.

---

## 2. Application Layer

Application layer bertanggung jawab terhadap:

- menerima HTTP request;
- melakukan authentication dan authorization;
- melakukan validasi input;
- menjalankan business logic;
- berkomunikasi dengan database;
- berkomunikasi dengan object storage;
- mengembalikan response kepada frontend.

Business logic V1 dijaga tetap sederhana karena sebagian besar kebutuhan sistem berupa:

- CRUD konten;
- perubahan status konten;
- pengambilan data publik;
- pengelolaan data admin;
- penyimpanan aspirasi anonim;
- agregasi data sederhana.

Tidak diperlukan business process kompleks atau event-driven architecture pada V1.

---

## 3. API Architecture

API menggunakan API routes yang berada dalam application yang sama dengan frontend.

Secara konseptual, API dibagi menjadi:

### Public API

Digunakan untuk kebutuhan website publik, seperti:

- mengambil data kepengurusan;
- mengambil data bidang;
- mengambil berita;
- mengambil Kajian & Pemikiran;
- mengambil alumni;
- mengambil produk;
- mengirim aspirasi anonim.

### Admin API

Digunakan untuk kebutuhan Super Admin, seperti:

- authentication;
- CRUD data organisasi;
- CRUD kepengurusan;
- CRUD bidang;
- CRUD berita;
- CRUD Kajian;
- CRUD alumni;
- CRUD Ekowir;
- CRUD Kaizen Company;
- membaca aspirasi;
- mengubah status konten.

Endpoint admin harus dilindungi authentication dan authorization.

Detail endpoint, method, request/response schema, status code, dan API contract akan ditentukan pada dokumen **API Specification**.

---

## 4. Backend Middleware

Backend menggunakan middleware untuk menangani concern yang bersifat cross-cutting.

### 4.1 AuthMiddleware

`AuthMiddleware` bertanggung jawab untuk melindungi endpoint dan halaman admin.

Fungsi utama:

- memeriksa keberadaan session;
- memvalidasi session;
- memastikan user memiliki hak akses Super Admin;
- menolak request yang tidak terautentikasi;
- mencegah akses langsung terhadap resource admin.

Secara konseptual:

    Request
       ↓
    AuthMiddleware
       ↓
    Valid Session?
       ├── No  → Unauthorized / Redirect
       └── Yes
              ↓
          Admin API

Endpoint dengan pola:

    /api/admin/*

harus dilindungi oleh authentication middleware.

Halaman dengan pola:

    /admin/*

juga harus memiliki protection terhadap akses tanpa session yang valid.

---

### 4.2 RateLimitMiddleware

`RateLimitMiddleware` digunakan untuk membatasi request terhadap endpoint yang berpotensi disalahgunakan.

Prioritas utama V1 adalah endpoint:

    /api/aspirasi

Tujuannya untuk mengurangi:

- spam submission;
- automated submission;
- abuse terhadap endpoint;
- beban database yang tidak diperlukan.

IP dapat digunakan sebagai dasar rate limiting pada middleware.

Namun, IP address **tidak boleh disimpan sebagai data aspirasi**.

Rate limiting merupakan mekanisme proteksi request dan bukan bagian dari data bisnis aspirasi.

---

## 5. Server-side Input Validation

Semua data yang berasal dari client harus divalidasi kembali di server.

Validasi frontend tidak dianggap sebagai security boundary.

Server-side validation mencakup:

- required field;
- format data;
- panjang input;
- valid URL;
- status value;
- file type;
- file size;
- slug;
- content input;
- data yang diperlukan oleh masing-masing module.

Request yang tidak memenuhi validation harus ditolak sebelum data diteruskan ke database.

Secara konseptual:

    Client Request
          ↓
    Authentication / Authorization
          ↓
    Input Validation
          ↓
    Business Logic
          ↓
    Database / Storage

---

# 6. Database Architecture

Database menggunakan pendekatan **Relational Database**.

Relational database dipilih karena sebagian besar data sistem memiliki struktur yang jelas dan membutuhkan konsistensi antar-entitas.

Database harus mampu mendukung:

- CRUD content;
- relationship antar-data;
- status management;
- historical data;
- filtering;
- ordering;
- slug lookup;
- backup;
- portability terhadap database provider.

Detail tipe data, primary key, foreign key, index, constraint, dan struktur tabel lengkap tidak didefinisikan pada TSS ini.

Detail tersebut akan ditentukan pada dokumen **Database Design**.

---

## 7. Core Database Entities

Secara konseptual, database V1 memiliki beberapa entity utama.

### 7.1 Users

Digunakan untuk menyimpan akun sistem.

Pada V1 hanya terdapat:

    Super Admin

Data user digunakan untuk authentication dan system ownership.

Tidak terdapat public user account pada V1.

---

### 7.2 Organization Profile

Digunakan untuk menyimpan informasi utama organisasi.

Contohnya meliputi:

- informasi organisasi;
- informasi kontak;
- informasi profil;
- data resmi organisasi.

Struktur detail dapat menggunakan pendekatan key-value atau single-row organization profile sesuai keputusan pada tahap Database Design.

---

### 7.3 Management Members

Digunakan untuk menyimpan data kepengurusan.

Data konseptual meliputi:

- ID;
- nama;
- foto;
- posisi;
- bidang;
- status aktif/inaktif.

Data historis tidak langsung dihapus ketika seorang pengurus menjadi tidak aktif.

Status digunakan untuk mengontrol visibilitas data publik.

---

### 7.4 Divisions

Digunakan untuk menyimpan informasi bidang/divisi organisasi.

Data dapat digunakan untuk menampilkan:

- nama bidang;
- deskripsi;
- informasi bidang;
- status publikasi.

---

### 7.5 News

Digunakan sebagai directory/aggregator berita.

Data konseptual meliputi:

- ID;
- title;
- short description;
- thumbnail URL;
- PWMU URL;
- status.

Berita pada V1 tidak menyimpan full article PWMU sebagai native article.

Website berfungsi sebagai directory yang mengarahkan pengguna ke sumber PWMU.

---

### 7.6 Kajian

Digunakan untuk menyimpan konten **Kajian & Pemikiran** sebagai native content.

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

Status Kajian mencakup:

    Draft
    Published
    Unpublished

Kajian yang berstatus Draft atau Unpublished tidak boleh ditampilkan kepada public user.

Kajian yang berstatus Published dapat diakses melalui halaman detail dengan dynamic route:

    /kajian/[slug]

Relasi author terhadap entity management member masih merupakan technical open decision pada TSS Revised.

---

### 7.7 Alumni

Digunakan untuk menyimpan data alumni yang ditampilkan pada website.

Data harus memiliki mekanisme status publikasi agar data yang tidak aktif atau tidak dipublikasikan tidak ditampilkan kepada pengguna publik.

---

### 7.8 Products

Digunakan untuk menyimpan produk atau layanan yang ditampilkan pada Ekowir dan Kaizen Company.

Data konseptual meliputi:

- ID;
- nama produk;
- foto;
- harga;
- deskripsi;
- kategori;
- stock display;
- status.

Status digunakan untuk menentukan apakah produk aktif atau tidak aktif.

Tidak terdapat payment gateway, shopping cart, checkout, maupun order management pada V1.

---

### 7.9 Aspirations

Digunakan untuk menyimpan aspirasi mahasiswa secara anonim.

Entity ini memiliki prinsip privacy-by-design.

Data aspirasi tidak boleh memiliki:

    user_id
    name
    email
    phone
    ip_address

Data utama yang diperlukan adalah:

- ID;
- text/content aspirasi;
- timestamp.

IP address hanya boleh digunakan secara sementara oleh mekanisme rate limiting dan tidak disimpan sebagai bagian dari data aspirasi.

Aspirasi hanya dapat diakses melalui area internal Super Admin.

---

# 8. Database Visibility Rules

Database status digunakan sebagai salah satu mekanisme untuk mengontrol visibility data.

Secara umum:

    Admin Database
          ↓
      Status Check
          ↓
      Public API
          ↓
      Public Website

Contoh:

    Published / Active
            ↓
       Public Visible

Sedangkan:

    Draft / Unpublished / Inactive
            ↓
       Public Hidden

Data yang disembunyikan dari public tidak berarti harus dihapus dari database.

Hal ini penting untuk mempertahankan historical data dan memudahkan pengelolaan konten oleh Super Admin.

---

# 9. Database Access Layer

Application layer tidak sebaiknya melakukan query database secara langsung dari setiap bagian frontend.

Database access dilakukan melalui backend/application layer.

Secara konseptual:

    Frontend
       ↓
    API / Application Layer
       ↓
    Business Logic
       ↓
    Database Access Layer / ORM
       ↓
    Relational Database

ORM atau query builder digunakan untuk membantu:

- struktur query yang konsisten;
- type safety apabila didukung;
- parameterized queries;
- migration;
- maintainability;
- portability.

Pilihan ORM atau query builder final ditentukan pada tahap technical decision dan Database Design.

TSS merekomendasikan penggunaan ORM seperti **Prisma** atau **Drizzle**.

---

# 10. Authentication & Authorization

## 10.1 Authentication Model

Authentication digunakan hanya untuk area administratif.

V1 tidak menyediakan:

- public registration;
- public login;
- student account;
- alumni account;
- multi-role public account.

Hanya terdapat satu role:

    Super Admin

Metode authentication masih merupakan technical open decision antara:

- Email + Password;
- Magic Link.

TSS Revised merekomendasikan **Email + Password** untuk V1.

---

## 10.2 Authorization Model

Authorization pada V1 dibuat sederhana.

    Authenticated Super Admin
            ↓
       Full Admin Access

Tidak terdapat role hierarchy atau permission matrix yang kompleks.

Super Admin memiliki akses terhadap seluruh module administrasi yang ditentukan dalam V1.

---

## 10.3 Session Strategy

TSS merekomendasikan session menggunakan:

    Encrypted JWT
    +
    HTTP-Only Cookie
    +
    Secure Cookie

Tujuan utama pendekatan ini adalah mengurangi exposure credential/session token terhadap client-side JavaScript dan menjaga authentication flow tetap sederhana.

Cookie authentication harus dikonfigurasi agar hanya dikirim melalui koneksi HTTPS pada production environment.

---

## 10.4 Admin Route Protection

Halaman admin:

    /admin/*

dan API admin:

    /api/admin/*

harus dilindungi.

Request tanpa session yang valid harus:

- ditolak pada API;
- diarahkan ke halaman authentication pada interface admin.

Admin interface juga harus diberi:

    noindex
    nofollow

agar tidak menjadi bagian dari public search indexing.

---

# 11. Public Data Boundary

Backend harus membedakan secara jelas antara:

    Public Data

dan:

    Internal Admin Data

Public API hanya boleh mengembalikan data yang memang diperbolehkan untuk ditampilkan kepada public.

Contohnya:

- Published Kajian → public;
- Draft Kajian → internal;
- Unpublished Kajian → internal;
- Active Product → public;
- Inactive Product → internal;
- Aspirasi → internal.

Dengan demikian, frontend bukan satu-satunya lapisan yang bertanggung jawab menyembunyikan data.

Visibility rule harus diterapkan pada server/API.

---

# 12. Backend Security Boundary

Backend menjadi security boundary utama untuk data dan operasi administratif.

Security responsibility mencakup:

- authentication;
- authorization;
- server-side validation;
- rate limiting;
- input sanitization;
- database query protection;
- protection terhadap unauthorized access;
- protection terhadap unpublished content;
- safe error response.

Backend tidak boleh mengembalikan database stack trace atau informasi internal server kepada public client.

---

# 13. Error Handling

API harus menggunakan response yang konsisten untuk kondisi error.

Contoh kategori:

    400 Bad Request
    401 Unauthorized
    403 Forbidden
    404 Not Found
    429 Too Many Requests
    500 Internal Server Error

Response error harus memberikan informasi yang cukup bagi client untuk menangani kondisi tersebut tanpa mengekspos informasi internal sistem.

Database error atau stack trace tidak boleh ditampilkan langsung kepada public user.

---

# 14. Backend & Database Responsibility Boundary

TSS membatasi tanggung jawab setiap layer sebagai berikut:

| Layer | Responsibility |
|---|---|
| Frontend | UI, interaction, presentation |
| API/Application | Request handling, authentication, business logic |
| Middleware | Cross-cutting security and request controls |
| Validation | Input validation and data integrity checks |
| ORM/Query Layer | Database access |
| Relational Database | Persistent structured data |
| Object Storage | Image/file storage |
| External Services | WhatsApp, PWMU, analytics/monitoring |

Pembagian ini dimaksudkan agar perubahan pada satu layer tidak menyebabkan coupling yang tidak diperlukan pada layer lainnya.

---

# 15. Database Design Boundary

TSS hanya mendefinisikan database secara konseptual.

Dokumen **Database Design** akan menjadi sumber detail untuk:

- table structure;
- column definitions;
- data types;
- primary keys;
- foreign keys;
- indexes;
- unique constraints;
- nullable rules;
- default values;
- relationships;
- migration strategy;
- seed data apabila diperlukan.

TSS tidak mendefinisikan detail tersebut agar technical specification tetap berada pada level arsitektur.

---

# 16. Backend & Database Constraints

Backend dan database harus mengikuti constraint berikut:

1. V1 menggunakan satu application utama.
2. Tidak menggunakan microservices.
3. Tidak menggunakan distributed event architecture.
4. Hanya terdapat satu role administratif, yaitu Super Admin.
5. Tidak ada public account.
6. Aspirasi harus tetap anonim.
7. IP address tidak disimpan dalam entity Aspirations.
8. Draft dan Unpublished content tidak boleh muncul melalui public API.
9. Semua admin API harus memiliki authentication dan authorization.
10. Semua input penting harus divalidasi server-side.
11. Database harus relational.
12. Detail schema ditentukan pada Database Design.
13. API contract detail ditentukan pada API Specification.

---

# 17. Technical Decisions Related to Backend & Database

| Decision | Status | Current Direction |
|---|---|---|
| Backend Architecture | Decided | Full-stack Monolithic |
| API Architecture | Decided | API Routes dalam full-stack framework |
| Database Type | Decided | Relational Database |
| ORM / Query Builder | Recommended | Prisma / Drizzle |
| Admin Role | Decided | Single Super Admin |
| Public Registration | Decided | Tidak tersedia |
| Authentication Method | Open Decision | Email + Password / Magic Link |
| Session Strategy | Recommended | Encrypted JWT + HTTP-Only Secure Cookie |
| Database Provider | Open Decision | Supabase / Firebase / VPS |
| Detailed Schema | Next Stage | Database Design |
| Detailed API Contract | Next Stage | API Specification |

---

# 18. Relationship with Next Technical Stages

Backend dan database architecture menjadi dasar untuk dua dokumen teknis berikutnya:

    TSS
     ↓
    Backend & Database Architecture
     ↓
    Database Design
     ↓
    API Specification

Database Design akan menerjemahkan entity konseptual menjadi struktur database konkret.

API Specification akan menerjemahkan kebutuhan application layer menjadi API contract yang dapat digunakan frontend dan backend.

---

## Navigation

- [← TSS Frontend Architecture](./03-tss-frontend-architecture.md)
- [TSS Content & Module Architecture →](./05-tss-content-and-module-architecture.md)
