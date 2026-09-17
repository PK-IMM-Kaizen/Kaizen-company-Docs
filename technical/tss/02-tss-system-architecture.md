# Technical Specification — System Architecture

> Definisi arsitektur sistem tingkat tinggi untuk Website Resmi PK IMM Kaizen V1.1 Revised.

---

# 1. System Architecture

## 1.1 Architecture Approach

Untuk memenuhi target V1 yang mengutamakan:

- simplicity;
- biaya operasional rendah;
- maintainability;
- kemudahan handover;

arsitektur sistem yang digunakan adalah:

> **Monolithic / Full-stack Framework**

Frontend dan Backend API berada dalam:

- satu codebase;
- satu application layer;
- satu deployment.

Pendekatan ini dipilih untuk menjaga sistem tetap sederhana dan menghindari kompleksitas teknis yang tidak diperlukan untuk skala V1.

---

## 1.2 High-Level Architecture

Arsitektur sistem secara konseptual:

    [ Public Users & Super Admin ]
                    |
                  HTTPS
                    |
                    v
        +-------------------------+
        |    Web Application      |
        |    Next.js / Nuxt.js    |
        |                         |
        |  +-------------------+  |
        |  |    Client (UI)    |  |
        |  +-------------------+  |
        |                         |
        |  +-------------------+  |
        |  |  API / App Layer  |  |
        |  +-------------------+  |
        +-------------------------+
                    |
              +-----+-----+
              |           |
              v           v
        [ Database ] [ Object Storage ]
        (Relational)  (WebP Images)
              |
              v
        +-------------------------+
        |   External Services     |
        |                         |
        | - WhatsApp (URL API)    |
        | - PWMU (Redirection)    |
        | - Analytics/Monitoring  |
        +-------------------------+

---

# 2. Architecture Components

## 2.1 Public Users

Public Users merupakan pengguna yang mengakses website tanpa membutuhkan akun.

Public Users dapat mengakses:

- Beranda;
- Profil;
- Kepengurusan;
- Bidang;
- Berita;
- Ekowir;
- Alumni;
- Kontak;
- Kajian & Pemikiran;
- Kaizen Company;
- Aspirasi Mahasiswa.

Public Users tidak memiliki akses ke area administrasi.

---

## 2.2 Super Admin

Super Admin merupakan satu-satunya role administrator pada V1.

Super Admin memiliki akses ke:

- Admin Dashboard;
- content management;
- management data;
- Kajian management;
- Kaizen Company management;
- Aspirasi management;
- media management.

Akses Super Admin dilindungi oleh authentication dan authorization.

---

## 2.3 Web Application

Web Application menjadi application layer utama sistem.

Web Application bertanggung jawab terhadap:

- rendering public website;
- rendering admin dashboard;
- routing;
- server-side application logic;
- API;
- authentication;
- authorization;
- content retrieval;
- content management;
- integrasi external services.

Framework yang dipertimbangkan:

- Next.js;
- Nuxt.js.

Pemilihan final framework masih merupakan technical decision yang harus diselesaikan.

---

## 2.4 Client UI

Client UI menangani:

- tampilan public website;
- interaksi pengguna;
- form submission;
- content presentation;
- responsive interface;
- navigasi;
- admin dashboard interface.

Detail desain interface dan interaction tidak didefinisikan dalam TSS ini dan menjadi bagian dari:

> **UI/UX Specification**

---

## 2.5 API / Application Layer

API / Application Layer menangani komunikasi antara client dan application logic.

Tanggung jawab utama:

- menerima request;
- melakukan validation;
- authentication;
- authorization;
- menjalankan business logic;
- membaca data;
- mengubah data;
- mengembalikan response.

Detail endpoint dan request/response schema akan didefinisikan pada:

> **API Specification**

---

## 2.6 Relational Database

Database digunakan sebagai penyimpanan data utama sistem.

Pendekatan:

> **Relational Database**

Database menjadi sumber data utama untuk content dan data operasional seperti:

- organization profile;
- management members;
- divisions;
- news;
- Kajian;
- alumni;
- products;
- aspirations;
- Super Admin users.

Detail schema database tidak didefinisikan pada TSS ini.

Detail tersebut akan menjadi bagian dari:

> **Database Design**

---

## 2.7 Object Storage

Object Storage digunakan untuk menyimpan file media, terutama image.

Media yang dapat disimpan mencakup:

- organization images;
- management photos;
- product images;
- Kajian thumbnails;
- media lain yang termasuk scope.

Format image yang digunakan diarahkan ke:

> **WebP**

Detail media management akan dijelaskan pada bagian teknis terkait dan specification berikutnya.

---

# 3. External Services

Sistem dapat berinteraksi dengan beberapa external services.

## 3.1 WhatsApp

WhatsApp digunakan untuk mengarahkan calon pembeli atau pengguna Kaizen Company kepada kontak yang telah ditentukan.

Flow bersifat redirect.

Tidak terdapat:

- payment gateway;
- cart;
- checkout;
- order management server-side.

---

## 3.2 PWMU

PWMU digunakan sebagai sumber eksternal untuk konten Berita.

Website Kaizen tidak menggandakan full article PWMU.

Berita berfungsi sebagai aggregator/directory yang mengarahkan pengguna ke artikel asli di PWMU.

---

## 3.3 Analytics & Monitoring

Analytics digunakan untuk kebutuhan pengukuran traffic website.

Monitoring digunakan untuk membantu mendeteksi error atau exception pada production.

Provider final untuk analytics dan monitoring masih merupakan open decision.

---

# 4. Architecture Flow

## 4.1 Public Content Flow

Alur public content:

    Public User
         |
         v
    Web Application
         |
         v
    API / Application Layer
         |
         v
    Relational Database
         |
         v
    Published Content
         |
         v
    Client UI
         |
         v
    Public User

Content yang belum dipublikasikan tidak boleh ditampilkan kepada public.

---

## 4.2 Admin Content Management Flow

Alur pengelolaan content:

    Super Admin
         |
         v
    Admin Dashboard
         |
         v
    Authentication
         |
         v
    API / Application Layer
         |
         v
    Validation
         |
         v
    Business Logic
         |
         v
    Relational Database
         |
         v
    Updated Content

Akses terhadap Admin Dashboard dan Admin API harus membutuhkan authentication yang valid.

---

## 4.3 Media Flow

Alur media:

    Super Admin
         |
         v
    Admin Dashboard
         |
         v
    Media Validation
         |
         v
    Image Processing
         |
         v
    Object Storage
         |
         v
    Media URL
         |
         v
    Database Reference
         |
         v
    Public / Admin UI

---

## 4.4 Kaizen Company Flow

Alur Kaizen Company:

    Public User
         |
         v
    Kaizen Company
         |
         v
    Product Detail
         |
         v
    Hubungi Penjual
         |
         v
    WhatsApp
         |
         v
    Pre-filled Message

Tidak ada proses transaksi internal di dalam aplikasi.

---

## 4.5 Aspirasi Flow

Alur Aspirasi:

    Public User
         |
         v
    Aspirasi Form
         |
         v
    Spam Protection
         |
         v
    Server-side Validation
         |
         v
    Aspirations Storage
         |
         v
    Super Admin Dashboard

Aspirasi harus tetap anonymous.

---

# 5. Architecture Principles

## 5.1 Simplicity

Kode harus dibuat lugas dan mudah dipahami.

Arsitektur tidak boleh menggunakan pola kompleks yang tidak sesuai dengan kebutuhan V1.

Hindari penggunaan:

- microservices;
- event-driven architecture;
- distributed architecture;

jika tidak terdapat kebutuhan nyata yang mengharuskannya.

**Status:** REQUIRED

---

## 5.2 Maintainability & Handover

Sistem harus menggunakan standar industri dan struktur kode yang dapat dipahami oleh developer berikutnya.

Prioritas:

- clean code;
- struktur project yang jelas;
- dokumentasi;
- standar implementasi;
- dependency yang wajar.

Tujuannya adalah memastikan sistem tidak bergantung pada pengetahuan personal developer saat ini.

**Status:** REQUIRED

---

## 5.3 Security-First Admin

Area administrasi harus sepenuhnya terisolasi dari akses publik.

Protection diterapkan pada:

- Admin Dashboard;
- Admin API;
- authentication;
- session;
- authorization.

Public User tidak boleh memperoleh akses ke resource administratif tanpa authentication yang valid.

**Status:** REQUIRED

---

## 5.4 Low Operational Complexity

Sistem direkomendasikan menggunakan managed services seperti:

- BaaS;
- PaaS;
- managed database;
- managed storage;
- serverless hosting.

Tujuannya adalah meminimalkan kebutuhan maintenance server Linux secara manual.

**Status:** RECOMMENDED

---

# 6. Monolithic Architecture Rationale

Arsitektur monolithic/full-stack dipilih untuk mencegah over-engineering.

Untuk aplikasi CMS dengan skala V1, memisahkan frontend dan backend secara fisik ke:

- repository berbeda;
- server berbeda;
- deployment berbeda;

dapat meningkatkan:

- deployment complexity;
- operational overhead;
- configuration complexity;
- maintenance complexity;
- handover difficulty.

Dengan satu full-stack application, frontend dan backend dapat dikelola dalam satu codebase dan deployment.

---

# 7. SEO & Rendering Consideration

Arsitektur full-stack juga mendukung kebutuhan SEO pada halaman public.

Khususnya untuk:

> **Kajian & Pemikiran**

sistem membutuhkan:

- dynamic routing;
- slug-based content retrieval;
- SEO metadata;
- Open Graph metadata;
- server rendering atau static generation.

Rendering strategy yang dipertimbangkan:

- SSR;
- SSG;
- ISR.

Detail implementasi rendering akan dijelaskan pada:

> `03-tss-frontend-architecture.md`

---

# 8. Architecture Boundaries

TSS menetapkan boundary berikut:

| Boundary | Responsibility |
|---|---|
| Public | Public website dan public content |
| Admin | Authentication dan content management |
| Application | Business logic dan request processing |
| Database | Persistent structured data |
| Object Storage | Image/media storage |
| External Services | WhatsApp, PWMU, Analytics, Monitoring |

Boundary tersebut bertujuan menjaga pemisahan tanggung jawab tanpa menambah kompleksitas arsitektur yang tidak diperlukan.

---

# 9. Architecture Constraints

Arsitektur V1 harus mempertimbangkan constraint berikut:

- tidak menggunakan arsitektur yang berlebihan untuk skala V1;
- frontend dan backend berada dalam satu full-stack application;
- public dan admin harus memiliki boundary yang jelas;
- database harus relational;
- image menggunakan WebP;
- external content PWMU tetap berada pada sumber aslinya;
- transaksi Kaizen Company tidak diproses di dalam sistem;
- Aspirasi harus anonymous;
- sistem harus mudah di-handover.

---

# 10. Architecture Decision Status

| Decision | Status |
|---|---|
| Monolithic / Full-stack Architecture | Recommended Direction |
| Separate Frontend Repository | Not Required |
| Separate Backend Repository | Not Required |
| Microservices | Out of Scope for V1 |
| Event-driven Architecture | Out of Scope for V1 |
| Relational Database | Recommended |
| Object Storage | Required |
| SSR / SSG / ISR | Recommended |
| Final Framework | Open Decision |
| Final Hosting Provider | Open Decision |
| Final Database Provider | Open Decision |

---

# 11. Relationship With Other Technical Documents

TSS System Architecture menjadi baseline untuk dokumen teknis berikutnya.

### Frontend Architecture

Detail mengenai:

- component architecture;
- layouts;
- dynamic routing;
- rich-text rendering;
- state/data fetching;
- image optimization;

akan didefinisikan pada:

`03-tss-frontend-architecture.md`

### Backend & Database Architecture

Detail mengenai:

- application layer;
- middleware;
- validation;
- database entities;
- authentication;

akan didefinisikan pada:

`04-tss-backend-and-database-architecture.md`

### Database Design

Detail schema database akan didefinisikan pada dokumen:

`database-design/`

### API Specification

Detail endpoint dan contract API akan didefinisikan pada dokumen:

`api-specification/`

### UI/UX Specification

Detail interface dan interaction akan didefinisikan pada dokumen:

`ui-ux-specification/`

---

# 12. Architecture Readiness

Arsitektur sistem telah memiliki arah yang cukup untuk dilanjutkan ke technical architecture berikutnya.

Baseline yang telah ditetapkan:

- Monolithic / Full-stack;
- public dan admin boundary;
- relational database;
- object storage;
- external service integration;
- security-first admin;
- low operational complexity;
- maintainability dan handover;
- SEO-oriented rendering untuk Kajian.

Technical decisions yang masih terbuka harus diselesaikan sebelum implementation final.

---

## Navigation

- [← TSS Overview](./01-tss-overview.md)
- [TSS Frontend Architecture →](./03-tss-frontend-architecture.md)
