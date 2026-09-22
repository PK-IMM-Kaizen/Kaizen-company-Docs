# Technical Specification (TSS) — Website Resmi PK IMM Kaizen V1.1 (Revised)

## 1. Document Information

* **Document Title:** Technical Specification (TSS) — Website Resmi PK IMM Kaizen
* **Product:** Website Resmi PK IMM Kaizen V1.0
* **Version:** 1.1 (Revised)
* **Status:** Draft
* **Date:** September 2026
* **Author:** Senior Technical Product Manager / Lead Developer
* **Source Document:** Product Requirement Document (PRD) — Website Resmi PK IMM Kaizen V1.0 — Revised
* **Related Documents:** Product Discovery V1.0

---

## 2. Purpose

Dokumen Technical Specification (TSS) ini bertujuan untuk menerjemahkan kebutuhan bisnis dan fungsional dari PRD (yang fokus pada What dan Why) menjadi rancangan teknis (How).

Dokumen ini menjadi panduan utama bagi developer dalam membangun, menguji, dan melakukan deployment sistem. TSS dirancang untuk memastikan sistem V1.0 bersifat production-ready, aman, mudah dipelihara, dan siap diwariskan (handover).

---

## 3. Technical Scope

Berdasarkan PRD Revised V1.1, scope teknis dibagi menjadi area berikut:

* **Public Website [REQUIRED]:** Beranda, Profil, Kepengurusan, Bidang, Berita, Ekowir, Alumni, Kontak.
* **Kajian & Pemikiran [REQUIRED]:** Section list di Beranda dan Halaman Detail mandiri (URL/slug dinamis). Konten dikelola oleh Bidang Hikmah/Politik (melalui Super Admin) dan disajikan secara native di dalam website.
* **Kaizen Company [REQUIRED]:** Katalog produk/jasa (Dark Theme), halaman detail, redirect URL WhatsApp.
* **Aspirasi Mahasiswa [REQUIRED]:** Form submission publik anonim, rate limiting/spam protection.
* **Admin Authentication [REQUIRED]:** Sistem login single-role (Super Admin).
* **Super Admin Dashboard (CMS) [REQUIRED]:** Antarmuka CRUD data (Profil, Pengurus, Bidang, Berita, Kajian, Alumni, Ekowir, Kaizen Co, Aspirasi).
* **Media Management [REQUIRED]:** Upload, validasi, konversi WebP.

---

## 4. System Architecture

Untuk memenuhi target V1 yang mengutamakan simplicity dan biaya rendah, arsitektur yang direkomendasikan adalah **Monolithic / Full-stack Framework** (Frontend dan Backend API berada dalam satu codebase/deployment).

```text
[ Public Users & Super Admin ]
              |
           (HTTPS)
              |
              v
+-------------------------------+
|       Web Application         |
|     (e.g., Next.js / Nuxt.js) |
|                               |
|  +-------------------------+  |
|  |      Client (UI)        |  |
|  +-------------------------+  |
|                               |
|  +-------------------------+  |
|  |     API / App Layer     |  |
|  +-------------------------+  |
+-------------------------------+
              |
       +------+------+
       |             |
       v             v
 [ Database ]   [ Object Storage ]
 (Relational)     (WebP Images)

+--------------------------------+
|       External Services        |
| - WhatsApp (URL API)           |
| - PWMU (Redirection)           |
| - Analytics/Monitoring         |
+--------------------------------+
```

### Alasan Pendekatan Full-stack

Mencegah over-engineering. Memisahkan frontend dan backend secara fisik di repository dan server berbeda untuk aplikasi CMS standar akan meningkatkan kompleksitas deployment dan menyulitkan handover.

Arsitektur ini juga secara native mendukung Dynamic Routing dan SSR/SSG/ISR yang krusial untuk SEO halaman Kajian.

---

## 5. Architecture Principles

* **Simplicity [REQUIRED]:** Kode harus lugas. Hindari pola desain kompleks (microservices, event-driven) yang tidak sesuai skala V1.
* **Maintainability & Handover [REQUIRED]:** Penggunaan standar industri dan dokumentasi kode (clean code) agar mudah dipahami pengurus/developer selanjutnya.
* **Security-First Admin [REQUIRED]:** Area dashboard terisolasi sepenuhnya dari akses publik.
* **Low Operational Complexity [RECOMMENDED]:** Menggunakan managed services (seperti BaaS/PaaS) untuk meminimalkan beban maintenance server Linux secara manual.

---

## 6. Frontend Architecture

* **Framework Layer:** Berbasis komponen (Component-based UI). SSR (Server-Side Rendering) atau SSG/ISR (Static Site Generation) sangat [RECOMMENDED] untuk SEO halaman publik, terutama halaman Kajian.

### Layout & Theming [REQUIRED]

* **LightLayout:** Untuk halaman organisasi utama.
* **DarkLayout:** Dikhususkan untuk area Kaizen Company.
* **AdminLayout:** Dikhususkan untuk dashboard Super Admin.

### Dynamic Routing [REQUIRED]

Dibutuhkan implementasi rute dinamis (contoh: `/kajian/[slug]`) untuk memfasilitasi halaman detail Kajian.

Rute ini bertugas mengambil data berdasarkan slug dan mengembalikan status 404 jika slug tidak ditemukan atau berstatus Unpublished/Draft.

### Rich Text Rendering [REQUIRED]

Komponen khusus (misal: `RichTextRenderer` atau `MarkdownRenderer`) yang mampu me-render konten body Kajian secara aman tanpa mengeksekusi script berbahaya.

### State Management & Data Fetching

Harus menangani:

* Loading state
* Error state
* Empty state (`[Content Required]`)

### Image Optimization [REQUIRED]

Menggunakan komponen image optimization bawaan framework untuk lazy loading dan format WebP.

---

## 7. Backend / Application Architecture

Karena menggunakan arsitektur Full-stack, Backend Layer bertindak sebagai API Routes dalam satu framework.

* **Business Logic:** Sangat berpusat pada operasi CRUD sederhana dan agregasi data.

### Middleware [REQUIRED]

* **AuthMiddleware:** Memblokir akses ke rute `/api/admin/*` dan halaman `/admin/*` jika session tidak valid.
* **RateLimitMiddleware:** Membatasi permintaan khusus pada rute `/api/aspirasi` untuk mencegah SPAM.

### Input Validation [REQUIRED]

Wajib dilakukan di sisi server (Server-side validation) sebelum menyentuh database.

---

## 8. Database Architecture

Sistem menggunakan Relational Database [RECOMMENDED].

### Entity

* `users` (Hanya untuk Super Admin. Ownership: Sistem).
* `organization_profile` (Bentuk key-value atau single-row).
* `management_members`
* `divisions`
* `news` (Atribut: ID, judul, deskripsi_singkat, thumbnail_url, pwmu_url, status).
* `kajian` [NEW] (Atribut konseptual: id, title, slug (unique), excerpt, thumbnail_url, author, content (body), published_at, status (Draft/Published/Unpublished), created_at, updated_at).
* `alumni`
* `products`
* `aspirations`

Detail skema tabel, relasi FK, dan tipe data akan dijabarkan pada Database Design terpisah.

Relasi field `author` pada entitas kajian berstatus **OPEN DECISION**.

---

## 9. Authentication & Authorization

* **Metode Authentication:** [OPEN DECISION] (Kandidat: Magic Link via email, atau Email/Password standar).
* **Role [REQUIRED]:** Hanya 1 Role (Super Admin). Tidak ada role khusus untuk penulis/Bidang Hikmah; pembuatan artikel dikoordinasikan ke Super Admin.
* **Session Strategy [RECOMMENDED]:** JWT terenkripsi yang disimpan dalam HTTP-Only, Secure Cookies.
* **Protection [REQUIRED]:** Tidak ada fitur registrasi publik (Sign Up dimatikan).

---

## 10. Content Management Architecture

Tabel strategi pengelolaan konten berdasarkan PRD:

| Konten              | Admin CRUD     | Visibility                      |
| ------------------- | -------------- | ------------------------------- |
| Organisasi & Kontak | Yes            | N/A (Always Live)               |
| Kepengurusan        | Yes            | Aktif / Inaktif                 |
| Bidang & Ekowir     | Yes            | Published / Unpublished         |
| Berita              | Yes            | Published / Unpublished         |
| Kajian & Pemikiran  | Yes            | Draft / Published / Unpublished |
| Alumni              | Yes            | Published / Unpublished         |
| Produk Kaizen       | Yes            | Aktif / Inaktif                 |
| Aspirasi            | Yes (Read/Del) | Internal Only                   |

Mekanisme workflow persetujuan (approval) sebelum publish masih berstatus **OPEN DECISION** di PRD, sehingga secara teknis V1 akan langsung dikontrol oleh Super Admin tanpa status state machine yang kompleks.

---

## 11. Kaizen Company Technical Architecture

### Flow Pembelian [REQUIRED]

Klien merender data dari database → Pengguna klik **"Hubungi Penjual"** → FE membangun URL:

```text
https://wa.me/{nomor_admin}?text={pesan_pre_filled_ter-encode}
```

→ Redirect.

### No Payment/Cart [REQUIRED]

Tidak ada implementasi:

* tabel `orders`
* `cart`
* integrasi payment gateway server-side

---

## 12. Aspirasi Mahasiswa Technical Architecture

### Anonimitas [REQUIRED]

Skema database `aspirations` TIDak boleh memiliki kolom:

* `user_id`
* `name`
* `email`
* `ip_address`

IP hanya boleh dicek di level middleware/memory untuk rate limit, tidak disimpan.

### Spam Protection [OPEN DECISION]

Kandidat:

1. Rate limiter per IP
2. Honeypot field
3. reCAPTCHA/Turnstile

**[RECOMMENDED]** menggunakan Honeypot + Rate Limiter untuk efisiensi dan menjaga anonimitas mutlak.

---

## 13. Berita & Kajian Integration

Terdapat perbedaan arsitektural yang tegas antara Berita dan Kajian:

### Berita (External Redirect)

Hanya menyimpan:

* thumbnail
* title
* excerpt
* `pwmu_url`

Website bertindak sebagai agregator yang mengarahkan pengguna (`target="_blank"`) ke artikel lengkap di PWMU.

Metode sinkronisasi PWMU: **OPEN DECISION**, rekomendasi V1: **Manual Entry**.

### Kajian (Native Content)

Menyimpan keseluruhan isi teks (`content`), memiliki URL/slug sendiri di dalam aplikasi (misal `/kajian/[slug]`), dan di-render secara native pada halaman detail.

---

## 14. Media & File Storage

* **File Strategy [REQUIRED]:** Dibatasi hanya untuk tipe image. File thumbnail / hero image Kajian mengikuti arsitektur media yang sama.
* **Validation:** Ekstensi `.png`, `.jpg`, `.jpeg`, `.webp`. Ukuran maks 2MB per gambar [RECOMMENDED].
* **Transformation [RECOMMENDED]:** Konversi gambar otomatis ke WebP di sisi client sebelum diunggah, atau via layanan storage.

---

## 15. API Architecture

### Konseptual

#### Public Endpoints

```text
GET  /api/public/pengurus
GET  /api/public/products
POST /api/public/aspirasi
```

#### Kajian Endpoints (Public)

```text
GET /api/public/kajian
GET /api/public/kajian/:slug
```

Hanya status `Published` yang dapat diakses.

#### Admin Endpoints

Dilindungi oleh middleware.

Meliputi:

```text
CRUD /api/admin/pengurus
CRUD /api/admin/products
CRUD /api/admin/kajian
```

CRUD Kajian menyertakan operasi Update Status ke:

* Draft
* Publish

---

## 16. Security Architecture

### Rich Text Security [REQUIRED]

Karena modul Kajian memiliki artikel dengan full content, sistem wajib mengimplementasikan sanitasi rich-text.

HTML tidak boleh di-render secara mentah (Raw HTML) tanpa dilewati library sanitizer (misal: DOMPurify) baik di sisi client maupun server untuk mencegah eksekusi script berbahaya dan serangan XSS.

### Unpublished Content Protection [REQUIRED]

API Publik harus memvalidasi agar Kajian berstatus Draft atau Unpublished merespons dengan `404/Not Found` jika diakses dari URL publik.

### SQL/NoSQL Injection [REQUIRED]

Penggunaan ORM/Query Builder.

### Security Headers [RECOMMENDED]

Implementasi Content Security Policy (CSP) dasar.

---

## 17. Performance Architecture

* **Rendering Strategy [RECOMMENDED]:** Memanfaatkan Static Generation (SSG) atau Incremental Static Regeneration (ISR) untuk merender halaman detail Kajian secara optimal agar HTML sudah ter-build untuk mesin pencari.
* **Lazy Loading [REQUIRED]:** Komponen `<Image>` untuk foto pengurus, katalog produk, dan thumbnail kajian agar LCP optimal.
* **Efficient Query:** Pengambilan data Kajian menggunakan indeks pada kolom `slug` di tingkat database.

---

## 18. SEO & URL Architecture

### Dynamic Metadata (Kajian) [REQUIRED]

Halaman `/kajian/[slug]` harus secara dinamis men-generate meta tag berdasarkan data kajian terkait:

* **title:** Menggunakan judul kajian.
* **description:** Menggunakan excerpt.
* **canonical URL:** Spesifik per slug.

### Dynamic Open Graph (OG) [REQUIRED]

Tag OG (`og:title`, `og:description`, `og:image`) wajib disediakan agar ketika link Kajian dibagikan ke media sosial atau WhatsApp, preview link muncul dengan benar.

### Indexability [REQUIRED]

Halaman Kajian berstatus Published harus di-indeks.

Sebaliknya, rute `/admin/*` harus mengembalikan header:

```text
X-Robots-Tag: noindex, nofollow
```

---

## 19. Analytics & Monitoring

* **Analytics [OPEN DECISION]:** Untuk memantau traffic.
* **Monitoring [OPEN DECISION]:** Untuk mencatat unhandled exceptions di production.

---

## 20. Backup & Recovery

* **Database Backup [REQUIRED]:** Bergantung pada konfigurasi provider cloud database. Entitas Kajian otomatis ter-cover dalam backup utama ini.
* **Export Manual [REQUIRED]:** Fitur Export CSV khusus untuk modul Aspirasi Mahasiswa sebagai supplementary backup.

---

## 21. Deployment Architecture

* **Domain [REQUIRED]:** `.org.id` (Membutuhkan verifikasi dokumen legal organisasi).
* **Environment [RECOMMENDED]:** Development dan Production.
* **Deployment Platform [OPEN DECISION]:** Platform berbasis serverless sangat dipertimbangkan (Vercel/Netlify).

---

## 22. Environment Configuration

Variabel Environment harus dipisahkan dari source code.

Contoh:

```text
DATABASE_URL
AUTH_SECRET
STORAGE_API_KEY
```

---

## 23. Error Handling

### Public UI

Menggunakan:

* Error Boundary (500)
* Not Found (404)

Terutama saat slug kajian tidak valid.

### API [REQUIRED]

Response API mengembalikan format standar JSON tanpa membocorkan stack trace database.

---

## 24. Logging & Observability

**[RECOMMENDED]:** Pencatatan log sederhana di server untuk:

* failed login attempts
* API failure

---

## 25. Scalability & Future Migration

* **Portability [RECOMMENDED]:** Gunakan ORM standar agar jika database provider berubah, kode tidak perlu dirombak total.

---

## 26. Maintainability & Handover

* **Ownership [REQUIRED]:** HARUS mendaftar GitHub, Domain, Hosting, dan Database menggunakan email resmi (contoh: `admin@kaizen.org.id`).
* **Documentation [REQUIRED]:** `README.md` mencakup setup dan deployment. Developer berikutnya harus dapat memahami Content Model Kajian dan Publishing Flow yang dijalankan oleh Super Admin.

---

## 27. Technical Risks

| Risk                        | Impact | Likelihood | Mitigasi                                                                        |
| --------------------------- | ------ | ---------- | ------------------------------------------------------------------------------- |
| XSS dari Rich Text Editor   | High   | Medium     | Wajib sanitasi ketat (sanitization boundary) sebelum render HTML ke DOM Publik. |
| Handover developer macet    | High   | High       | Enforce aturan Centralized Email Ownership & Dokumentasi standar.               |
| Spam pada Aspirasi (Anonim) | Medium | High       | Implementasi Honeypot (kolom tak terlihat) & Rate Limit.                        |

---

## 28. Open Technical Decisions

### TBD-01 Frontend/Backend Framework

* Next.js
* Nuxt.js
* SvelteKit

**Rekomendasi:** Next.js / Nuxt.js.

### TBD-02 Database & Storage Provider

* Supabase
* Firebase
* VPS

**Rekomendasi:** Supabase (PostgreSQL).

### TBD-03 Hosting / Deployment

* Vercel
* Netlify
* VPS

**Rekomendasi:** Vercel / Netlify.

### TBD-04 Admin Auth Method

* Email + Password
* Magic Link

**Rekomendasi:** Email + Password.

### TBD-05 Format Rich-Text Kajian

* Markdown
* WYSIWYG (HTML)

**Rekomendasi:** Markdown (Lebih aman dari celah XSS dan struktur database lebih bersih).

**Status:** OPEN.

### TBD-06 Relasi Author Kajian

* Teks Bebas
* ID Relasi Pengurus

**Rekomendasi:** Teks Bebas (Fleksibilitas V1).

**Status:** OPEN.

### TBD-07 Approval Workflow Kajian

* In-app State
* Offline Coord

**Rekomendasi:** Offline Coord (Menyederhanakan V1).

**Status:** OPEN.

---

## 29. Technology Recommendation

Berdasarkan constraint PRD (Dilarang PHP, Handover mudah, Production-ready):

* **Core Framework:** Next.js (App Router) atau Nuxt.js. Keduanya sempurna untuk menangani dynamic routing & SEO metadata Kajian.
* **Database & Storage:** Supabase.
* **ORM:** Prisma atau Drizzle.
* **Hosting:** Vercel.
* **Analytics:** Vercel Web Analytics.

---

## 30. Traceability

| Requirement                   | Technical Coverage                                                                |
| ----------------------------- | --------------------------------------------------------------------------------- |
| FR-009 Kajian di Homepage     | UI, API — `GET /api/public/kajian`, Homepage Section                              |
| FR-010 Kajian Detail & Slug   | UI, API, SEO — Dynamic route `/kajian/[slug]`, Dynamic Meta/OG                    |
| CMS-Kajian CRUD & Lifecycle   | Admin API, Security — Tabel `kajian`, `POST/PUT /api/admin/kajian`, XSS Sanitizer |
| FR-005 Kaizen Company Catalog | UI, API — DarkLayout, `GET /products`                                             |
| FR-004 Aspirasi Anonim        | API, DB, Security — Form UI, `POST /aspirasi`, Honeypot, Tabel `aspirations`      |

---

## 31. Technical Definition of Done

Sistem dianggap siap memasuki tahap eksekusi kode (Development) apabila:

1. Architecture & Tech Stack (TBD-01 s/d TBD-07) telah disetujui secara final.
2. Modul Kajian & Pemikiran sudah tercakup secara teknis (Database konseptual, Routing, API, Rich-Text Security, dan SEO) tanpa konflik dengan PRD Revised V1.1.
3. Dokumen Database Design dan API Specification selesai.
4. Security & Backup Strategy (termasuk perlindungan unpublished content) diakui.

---

# C. Final Validation

* **PRD <-> TSS consistency:** PASS
* **Kajian requirement coverage:** PASS (Tercakup dalam DB, Routing, CMS, Security, SEO, UI).
* **Architecture consistency:** PASS (Tetap Monolithic/Full-stack, selaras dengan kebutuhan baru).
* **Database readiness:** PASS (Entitas kajian terdefinisi high-level).
* **API readiness:** PASS (Endpoint API konseptual tersedia).
* **Security readiness:** PASS (Rich-text sanitization & unpublished protection terdefinisi).
* **SEO readiness:** PASS (Dynamic OG & metadata terdefinisi).
* **Deployment & Handover readiness:** PASS (Tidak terganggu oleh perubahan ini).

> **STATUS: PASS — TSS READY FOR DATABASE DESIGN & API SPECIFICATION**
