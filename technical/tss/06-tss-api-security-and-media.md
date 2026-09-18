# Technical Specification — API, Security & Media

## 1. API Architecture

Website Resmi PK IMM Kaizen V1.1 menggunakan API sebagai communication layer antara frontend, backend application logic, database, dan external services.

API berada di dalam full-stack application yang sama dengan frontend.

Secara konseptual:

    Client
      ↓
    HTTPS
      ↓
    Application / API Layer
      ↓
    Middleware
      ↓
    Business Logic
      ↓
    Database / Object Storage
      ↓
    Response

Pendekatan ini menjaga arsitektur tetap sederhana dan menghindari kebutuhan terhadap backend service terpisah pada V1.

---

## 2. API Boundary

API dibagi menjadi dua boundary utama:

- Public API
- Admin API

### Public API

Public API digunakan untuk:

- membaca content yang memang bersifat public;
- mengambil data yang berstatus Published/Active;
- menerima anonymous aspiration submission.

Public API tidak boleh mengembalikan data internal atau content yang belum dipublikasikan.

### Admin API

Admin API digunakan untuk:

- authentication;
- content management;
- CRUD;
- status management;
- membaca aspirasi;
- media management.

Admin API hanya dapat digunakan oleh authenticated Super Admin.

---

## 3. Public API

Endpoint public secara konseptual meliputi:

    GET /api/public/pengurus

Digunakan untuk mengambil data kepengurusan yang aktif.

    GET /api/public/products

Digunakan untuk mengambil produk yang aktif.

    POST /api/public/aspirasi

Digunakan untuk menerima aspirasi anonim.

Untuk Kajian:

    GET /api/public/kajian

Digunakan untuk mengambil Kajian yang berstatus Published.

    GET /api/public/kajian/:slug

Digunakan untuk mengambil satu Kajian berdasarkan unique slug.

Public API Kajian tidak boleh mengembalikan Draft atau Unpublished content.

Endpoint lain untuk module seperti Profil, Bidang, Berita, Alumni, dan Ekowir mengikuti prinsip public visibility yang sama.

Detail endpoint final, request schema, response schema, validation rules, dan HTTP status code akan ditentukan dalam dokumen **API Specification**.

---

## 4. Admin API

Admin API digunakan oleh Super Admin.

Secara konseptual, resource utama meliputi:

    /api/admin/pengurus
    /api/admin/bidang
    /api/admin/berita
    /api/admin/kajian
    /api/admin/alumni
    /api/admin/ekowir
    /api/admin/products
    /api/admin/aspirasi

Operasi dapat mencakup:

- GET;
- POST;
- PUT/PATCH;
- DELETE;
- status update.

Semua endpoint di bawah:

    /api/admin/*

harus melalui authentication dan authorization.

---

## 5. API Request Flow

Request public:

    Public Client
         ↓
       HTTPS
         ↓
    Public API
         ↓
    Validation
         ↓
    Business Logic
         ↓
    Database / Storage
         ↓
    JSON Response

Request admin:

    Super Admin
         ↓
       HTTPS
         ↓
    Authentication
         ↓
    Authorization
         ↓
    Validation
         ↓
    Business Logic
         ↓
    Database / Storage
         ↓
    JSON Response

---

## 6. Authentication Security

Authentication hanya berlaku untuk area administratif.

V1 hanya memiliki:

    Super Admin

Tidak tersedia:

- public registration;
- public authentication;
- student account;
- alumni account;
- multi-role public account.

Authentication method masih merupakan technical open decision antara:

- Email + Password;
- Magic Link.

TSS Revised merekomendasikan:

    Email + Password

---

## 7. Session Security

Session strategy yang direkomendasikan:

    Encrypted JWT
          +
    HTTP-Only Cookie
          +
    Secure Cookie

HTTP-Only digunakan untuk mengurangi akses session cookie dari client-side JavaScript.

Secure Cookie memastikan cookie dikirim melalui HTTPS pada production environment.

Session validation harus dilakukan pada protected admin routes dan API.

---

## 8. Authorization

Authorization memastikan bahwa hanya Super Admin yang dapat melakukan operasi administratif.

Secara konseptual:

    Request
       ↓
    Valid Session?
       ├── No → 401 Unauthorized
       └── Yes
             ↓
       Super Admin?
             ├── No → 403 Forbidden
             └── Yes
                    ↓
                Admin API

Karena V1 hanya menggunakan satu administrative role, tidak diperlukan permission matrix kompleks.

---

## 9. Admin Route Protection

Area:

    /admin/*

dan:

    /api/admin/*

harus protected.

Jika user public mencoba membuka halaman admin tanpa session valid:

    Public User
        ↓
    /admin/*
        ↓
    Authentication Check
        ↓
    No Session
        ↓
    Redirect to Authentication

Jika request menuju Admin API tidak memiliki session valid:

    /api/admin/*
        ↓
    Authentication Check
        ↓
    Unauthorized

---

## 10. Server-side Validation

Semua input dari client harus divalidasi pada server.

Frontend validation hanya digunakan untuk meningkatkan user experience dan bukan sebagai security boundary.

Validasi dapat mencakup:

- required fields;
- string length;
- URL format;
- slug format;
- status;
- numeric values;
- image format;
- image size;
- content format;
- field relationships.

Request invalid harus ditolak sebelum masuk ke business logic atau database.

---

## 11. Input Sanitization

Input yang akan dirender kembali kepada user harus melalui sanitization yang sesuai.

Area yang membutuhkan perhatian khusus:

- Kajian content;
- rich text;
- text input;
- external URL;
- admin-generated content.

Raw HTML tidak boleh dirender secara langsung tanpa sanitization.

Untuk rich text, sanitizer seperti **DOMPurify** dapat digunakan sesuai kebutuhan implementasi.

Tujuan utama adalah mencegah:

- Cross-Site Scripting (XSS);
- malicious HTML;
- malicious script injection.

---

## 12. Kajian Content Security

Kajian merupakan native content dan dapat memiliki rich text.

Karena content berasal dari CMS/admin input, application harus memperlakukan content sebagai untrusted input.

Flow:

    Admin Input
        ↓
    Server Validation
        ↓
    Sanitization
        ↓
    Database
        ↓
    Safe Renderer
        ↓
    Public Page

Jika menggunakan Markdown, renderer harus membatasi syntax atau HTML yang diperbolehkan.

Jika menggunakan WYSIWYG/HTML, sanitization menjadi mandatory sebelum rendering.

---

## 13. Draft & Unpublished Protection

Public API harus memfilter content berdasarkan status.

Untuk Kajian:

    Draft
       ↓
    Not Public

    Unpublished
       ↓
    Not Public

    Published
       ↓
    Public

Jika public user mencoba mengakses:

    /kajian/[draft-slug]

atau:

    /kajian/[unpublished-slug]

application harus memperlakukannya sebagai content yang tidak tersedia untuk public.

Response yang sesuai adalah:

    404 Not Found

Dengan demikian, status internal content tidak dibocorkan kepada public.

---

## 14. SQL / NoSQL Injection Protection

Application harus menggunakan parameterized queries atau ORM/query builder yang aman.

Input user tidak boleh digabungkan secara langsung ke query database.

Recommended approach:

    User Input
        ↓
    Validation
        ↓
    ORM / Parameterized Query
        ↓
    Database

Penggunaan ORM seperti Prisma atau Drizzle direkomendasikan untuk membantu menjaga query tetap terstruktur dan aman.

---

## 15. CSRF Protection

Endpoint yang melakukan state-changing operation harus mempertimbangkan protection terhadap Cross-Site Request Forgery.

Operasi yang termasuk:

- create;
- update;
- delete;
- publish;
- unpublish;
- aspiration submission.

Mekanisme CSRF harus disesuaikan dengan authentication/session architecture yang dipilih.

---

## 16. Rate Limiting

Rate limiting diterapkan terutama pada:

    POST /api/public/aspirasi

Tujuan:

- mengurangi spam;
- mengurangi automated submission;
- mencegah abuse;
- menjaga resource database.

Konsep:

    Request
       ↓
    Rate Limit Check
       ↓
    Limit Exceeded?
       ├── Yes → 429 Too Many Requests
       └── No
              ↓
          Validation
              ↓
          Process Request

IP address dapat digunakan sebagai temporary rate-limit key.

Namun:

**IP address tidak boleh disimpan dalam entity Aspirations.**

---

## 17. Honeypot Protection

Selain rate limiter, V1 merekomendasikan penggunaan honeypot field untuk membantu mendeteksi automated submission.

Honeypot field:

- tidak terlihat oleh normal user;
- tidak diisi oleh normal user;
- jika terisi, request dapat dianggap suspicious.

Kombinasi yang direkomendasikan:

    Honeypot
       +
    Rate Limiter

Penggunaan CAPTCHA seperti reCAPTCHA atau Turnstile dapat dipertimbangkan apabila spam masih menjadi masalah.

---

## 18. API Error Handling

API harus menggunakan error response yang konsisten.

Kategori status yang dapat digunakan:

    400 Bad Request
    401 Unauthorized
    403 Forbidden
    404 Not Found
    409 Conflict
    429 Too Many Requests
    500 Internal Server Error

Contoh struktur konseptual:

    {
      "error": {
        "code": "VALIDATION_ERROR",
        "message": "Invalid request data"
      }
    }

Format final response akan ditentukan pada API Specification.

---

## 19. Error Information Disclosure

API tidak boleh mengembalikan informasi internal kepada public.

Tidak boleh mengekspos:

- database stack trace;
- SQL query;
- internal file path;
- secret;
- environment variable;
- authentication secret;
- infrastructure information yang tidak diperlukan.

Production error response harus memberikan pesan yang aman dan relevan.

Detail error lengkap dapat dicatat pada server logging.

---

## 20. Media Architecture

Media digunakan terutama untuk image content.

Module yang menggunakan media:

- Kepengurusan;
- Berita;
- Kajian;
- Alumni;
- Ekowir;
- Kaizen Company.

Image tidak disimpan sebagai binary utama di relational database.

Media disimpan menggunakan:

    Object Storage

Database hanya menyimpan reference atau URL media.

---

## 21. Supported Image Formats

Format input yang diterima:

    PNG
    JPG
    JPEG
    WebP

WebP menjadi format preferred untuk production asset.

Automatic conversion ke WebP direkomendasikan.

Tujuannya:

- mengurangi ukuran file;
- meningkatkan loading performance;
- menjaga konsistensi media;
- mendukung image optimization.

---

## 22. Image Size Validation

Maximum recommended upload size:

    2 MB

File yang melebihi batas harus ditolak atau diproses sesuai kebijakan media implementation.

Validation dilakukan di server.

Frontend tidak boleh menjadi satu-satunya tempat untuk memvalidasi ukuran file.

---

## 23. Image Upload Flow

Flow konseptual:

    Admin
      ↓
    Select Image
      ↓
    Client Validation
      ↓
    Upload Request
      ↓
    Server Validation
      ↓
    File Type Check
      ↓
    File Size Check
      ↓
    Image Processing
      ↓
    WebP Conversion
      ↓
    Object Storage
      ↓
    Media URL
      ↓
    Database Reference

Jika proses upload gagal, database tidak boleh menyimpan reference terhadap media yang tidak tersedia.

---

## 24. Media Security

Media upload harus divalidasi untuk mencegah file berbahaya.

Minimal validation:

- extension;
- MIME type;
- file size;
- image validity.

Sistem tidak boleh mempercayai extension yang diberikan client tanpa melakukan validation.

File yang bukan image valid harus ditolak.

---

## 25. Media Storage

Object storage digunakan sebagai media layer.

Konseptual:

    Application
        ↓
    Object Storage
        ↓
    Image URL
        ↓
    Database Reference

Database menyimpan URL atau storage reference.

File binary tidak disimpan langsung pada relational database kecuali terdapat alasan teknis khusus pada tahap implementasi.

---

## 26. Media Access

Public image yang digunakan oleh content Published/Active dapat diakses melalui public media URL sesuai konfigurasi storage.

Media yang berhubungan dengan content internal harus mengikuti access policy storage.

Jika media hanya digunakan untuk content admin/internal, public access tidak boleh diberikan tanpa alasan yang jelas.

---

## 27. SEO Security Boundary

Public content dapat di-index oleh search engine sesuai status publikasinya.

Admin area:

    /admin/*

harus diberi:

    noindex
    nofollow

Selain metadata frontend, server dapat mengirim:

    X-Robots-Tag: noindex, nofollow

untuk resource administratif sesuai kebutuhan deployment.

---

## 28. Content Security Policy

Basic Content Security Policy (CSP) direkomendasikan.

CSP dapat digunakan untuk membatasi:

- script sources;
- style sources;
- image sources;
- connect sources;
- frame sources.

Policy final harus disesuaikan dengan:

- framework;
- analytics;
- object storage;
- external services;
- WhatsApp;
- PWMU integration.

CSP tidak boleh dibuat terlalu ketat hingga memutus fungsi utama website.

---

## 29. External URL Security

External URL digunakan terutama untuk:

- PWMU;
- WhatsApp;
- external resources.

URL harus divalidasi sebelum disimpan melalui admin interface.

Untuk external links yang dibuka pada tab baru, frontend harus menggunakan konfigurasi yang sesuai untuk mengurangi risiko reverse tabnabbing.

Konsep:

    target="_blank"
    rel="noopener noreferrer"

---

## 30. WhatsApp Integration Security

Kaizen Company menggunakan WhatsApp sebagai external communication channel.

Website tidak memproses transaksi.

Flow:

    Product Detail
         ↓
    WhatsApp CTA
         ↓
    Encoded Message
         ↓
    WhatsApp

Tidak ada:

- payment processing;
- card data;
- order data;
- checkout session;
- transaction database.

Nomor WhatsApp dan template message harus dikontrol melalui application configuration atau content management sesuai hasil implementation design.

---

## 31. API & Media Environment Variables

Secret dan credential tidak boleh disimpan langsung di source code.

Environment variables yang direncanakan meliputi:

    DATABASE_URL
    AUTH_SECRET
    STORAGE_API_KEY

Environment variables harus:

- disimpan di environment configuration;
- tidak di-commit ke Git;
- dipisahkan antara development dan production;
- dikelola oleh owner organisasi pada tahap handover.

File seperti:

    .env
    .env.local

tidak boleh dimasukkan ke repository apabila berisi secret.

---

## 32. API Logging

Server-side logging digunakan untuk membantu troubleshooting.

Minimal event yang dapat dicatat:

- failed login;
- failed API request;
- unexpected server error;
- media upload failure;
- security-related rejection.

Logging harus menghindari penyimpanan data sensitif yang tidak diperlukan.

Untuk Aspirasi, anonymous content tetap harus diperlakukan sebagai data sensitif dari sisi privacy dan tidak boleh diperkaya dengan identity information yang tidak diperlukan.

---

## 33. API Security Responsibilities

Security responsibility dibagi sebagai berikut:

| Layer | Security Responsibility |
|---|---|
| Frontend | UX validation, safe client interaction |
| API | Request validation and response control |
| Middleware | Authentication, authorization, rate limiting |
| Application | Business rule enforcement |
| ORM | Safe database access |
| Database | Data integrity and persistence |
| Object Storage | Media access and storage |
| Deployment | HTTPS, environment secrets, infrastructure configuration |

Tidak ada satu layer yang boleh dianggap sebagai satu-satunya security control.

---

## 34. Security Checklist

Sebelum production, API dan media architecture harus memastikan:

- [ ] Admin authentication aktif.
- [ ] Admin authorization aktif.
- [ ] Public registration tidak tersedia.
- [ ] Admin API protected.
- [ ] Server-side validation aktif.
- [ ] Rich text disanitasi.
- [ ] Draft content tidak dapat diakses public.
- [ ] Unpublished content tidak dapat diakses public.
- [ ] SQL/NoSQL injection protection diterapkan.
- [ ] CSRF protection diperhitungkan.
- [ ] Aspirasi memiliki rate limiting.
- [ ] Aspirasi memiliki honeypot atau spam protection.
- [ ] IP address tidak disimpan dalam data aspirasi.
- [ ] Image upload divalidasi.
- [ ] Image size dibatasi.
- [ ] Image conversion ke WebP diterapkan atau tersedia.
- [ ] Secret menggunakan environment variables.
- [ ] Database error tidak diekspos ke client.
- [ ] Admin area tidak di-index.
- [ ] HTTPS digunakan pada production.
- [ ] External links menggunakan konfigurasi yang aman.

---

## 35. Technical Decisions

| Decision | Status | Current Direction |
|---|---|---|
| API Architecture | Decided | API Routes dalam full-stack application |
| Public API | Decided | Public read + anonymous aspiration submission |
| Admin API | Decided | Protected Super Admin API |
| Authentication | Open Decision | Email + Password / Magic Link |
| Session | Recommended | Encrypted JWT + HTTP-Only Secure Cookie |
| Rate Limiting | Recommended | Aspiration endpoint |
| Spam Protection | Recommended | Honeypot + Rate Limiter |
| Rich Text Security | Decided | Sanitization required |
| Rich Text Library | Open Decision | Markdown recommended |
| Database Query Protection | Recommended | ORM / Parameterized Query |
| Media Storage | Decided | Object Storage |
| Image Format | Decided | WebP preferred |
| Maximum Image Size | Recommended | 2 MB |
| Automatic WebP Conversion | Recommended | Yes |
| CSP | Recommended | Basic CSP |
| Analytics | Open Decision | Tool TBD |
| Error Monitoring | Open Decision | Tool TBD |

---

## 36. Relationship with Database Design

API dan security architecture membutuhkan database structure yang jelas.

Database Design berikutnya akan menentukan:

- table structure;
- field types;
- primary keys;
- foreign keys;
- indexes;
- constraints;
- status fields;
- relationships;
- migration strategy.

Khusus untuk API, Database Design harus mendukung kebutuhan:

- public visibility;
- admin CRUD;
- Kajian slug;
- content lifecycle;
- anonymous aspirations;
- media references.

---

## 37. Relationship with API Specification

API Specification akan menerjemahkan arsitektur ini menjadi contract yang lebih detail.

API Specification akan menentukan:

- endpoint;
- HTTP method;
- authentication requirement;
- request parameters;
- request body;
- validation;
- response body;
- status codes;
- error format;
- pagination apabila diperlukan;
- filtering;
- sorting;
- CRUD behavior.

TSS ini tidak menggantikan API Specification.

---

## 38. Final Security Boundary

Arsitektur security V1 menggunakan prinsip:

    Validate
        ↓
    Authenticate
        ↓
    Authorize
        ↓
    Sanitize
        ↓
    Process
        ↓
    Persist
        ↓
    Respond Safely

Untuk public content:

    Public Request
         ↓
    Visibility Check
         ↓
    Published / Active?
         ├── No → 404 / Not Available
         └── Yes
                ↓
            Public Response

Untuk admin content:

    Admin Request
         ↓
    Authentication
         ↓
    Authorization
         ↓
    Validation
         ↓
    Business Logic
         ↓
    Database / Storage

Pendekatan ini menjaga security boundary tetap berada pada server dan tidak bergantung pada frontend semata.

---

## Navigation

- [← TSS Content & Module Architecture](./05-tss-content-and-module-architecture.md)
- [TSS Deployment, Performance & Handover →](./07-tss-deployment-performance-and-handover.md)
