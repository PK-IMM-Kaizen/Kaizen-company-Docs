# API Specification — Website Resmi PK IMM Kaizen V1.1 (Revised)

## 1. Document Information

* **Document Title:** API Specification — Website Resmi PK IMM Kaizen
* **Product:** Website Resmi PK IMM Kaizen V1.0
* **Version:** 1.1 (Revised)
* **Date:** September 2026
* **Author:** Senior Backend/API Architect
* **Source Documents:** Product Discovery, PRD V1.1 Revised, TSS V1.1 Revised, Database Design V1.2 Revised

---

## 2. Revision History

| Version | Date     | Change                                                                                                                                                                                                                                                                                                                                                                                                 |
| ------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1.0     | Sep 2026 | Initial API Specification creation based on Database Design V1.2 Revised.                                                                                                                                                                                                                                                                                                                              |
| 1.1     | Sep 2026 | Controlled revision: resource-specific public visibility, endpoint/operation matrix completeness, resource-specific search, HTTP status code clarification, framework-neutral caching, Supabase Auth authorization clarification, rich text security/open decision clarification, delete policy clarification, product/news/kajian/aspiration contract alignment, wording and validation improvements. |

---

## 3. Purpose

Dokumen ini menetapkan kontrak API (API Contract) antara client (Frontend/UI) dan server (Backend). Tujuannya adalah memastikan kedua sisi pengembangan memiliki acuan yang sama terkait endpoint, format request/response, validasi, dan otorisasi sebelum implementasi atau mocking UI/UX dilakukan.

Dokumen ini merupakan jembatan teknis yang konsisten dengan Database Design V1.2 Revised.

---

## 4. API Scope

API mencakup operasi data untuk:

1. Organization Profile (Single-row)
2. Divisions (Bidang Ekowir, Hikmah, dll)
3. Management Members (Personalia)
4. Kajian & Pemikiran (Native Content)
5. News (PWMU Redirects)
6. Alumni (Showcase)
7. Products (Kaizen Company Catalog)
8. Aspirations (Anonymous Feedback)
9. Media/Storage (Upload to Supabase Bucket)

---

## 5. API Architecture

* **Style:** RESTful
* **Communication:** JSON over HTTPS
* **Database/BaaS:** Supabase (PostgreSQL, Auth, Storage)
* **Client-Server Flow:** Stateless, mengandalkan JWT (JSON Web Token) dari Supabase Auth.

---

## 6. API Conventions

* **Base Path:** `/api/v1`
* **Path Separation:** `/public` untuk akses tanpa autentikasi, `/admin` untuk akses Super Admin.
* **Format Data:** `application/json` (Kecuali upload file menggunakan `multipart/form-data`).
* **Naming Convention:** `snake_case` untuk request/response payload.
* **Response Wrapper:**

```json
{
  "success": true,
  "data": {},
  "meta": {},
  "error": null
}
```

---

## 7. Authentication & Authorization Architecture

API memisahkan konsep Authentication dan Authorization secara tegas:

* **Authentication (Supabase Auth):** "Apakah user valid?". API mengandalkan session/JWT dari Supabase Auth. UUID user adalah identitas utama. Sistem tidak menyimpan `password_hash` lokal.
* **Authorization (Application Layer & RLS):** "Apakah user ini adalah Super Admin?". Otorisasi dilakukan dengan memverifikasi UUID dari JWT terhadap tabel allowlist `super_admins`.
* **Role Logis Tunggal:** Aplikasi hanya memiliki satu role yaitu `SUPER_ADMIN`. Tidak ada role Editor, Staff, atau Bidang lainnya. Jika UUID terautentikasi tidak ada di allowlist, API merespons dengan `403 Forbidden`.
* **Service Role Warning:** Jika Backend menggunakan Service Role Key Supabase, key tersebut HANYA beroperasi di lingkungan server yang aman (server-side). Service role key TIDAK BOLEH diekspos ke client, repository, atau frontend browser. Otorisasi aplikasi tetap harus dijalankan sebelum mengeksekusi operasi privileged.

---

## 8. Public API Visibility Rules

Endpoint Public (`/api/v1/public/...`) tidak membutuhkan token. Visibilitas data didefinisikan secara spesifik per resource sesuai dengan skema Database Design:

* **Organization Profile:** Public dapat membaca field profil yang ditujukan untuk publik.
* **Divisions:** Public dapat membaca daftar bidang organisasi.
* **Management Members:** Public HANYA mendapatkan anggota yang berstatus `active`.
* **Kajian:** Public HANYA mendapatkan kajian yang berstatus `published`. Draft dan Unpublished tidak dapat diakses melalui public endpoint.
* **News:** Public HANYA mendapatkan metadata berita yang berstatus `published`.
* **Alumni:** Public HANYA mendapatkan alumni yang berstatus `published`.
* **Products:** Public HANYA mendapatkan produk yang berstatus `active`.
* **Aspirations:** Public HANYA memiliki akses `POST /aspirations` (Submit). TIDAK ADA akses public GET.
* **Media:** Public mengakses media statis yang berada di `public_assets` bucket langsung melalui URL.

---

## 9. Operation Matrix

| Resource             | Public Operation         | Super Admin Operation                                 |
| -------------------- | ------------------------ | ----------------------------------------------------- |
| Organization Profile | GET                      | READ / UPDATE                                         |
| Divisions            | GET                      | CREATE / READ / UPDATE / DELETE                       |
| Management Members   | GET (active)             | CREATE / READ / UPDATE / DELETE                       |
| Kajian               | GET (published)          | CREATE / READ / UPDATE / DELETE / PUBLISH / UNPUBLISH |
| News                 | GET (published metadata) | CREATE / READ / UPDATE / DELETE                       |
| Alumni               | GET (published)          | CREATE / READ / UPDATE / DELETE                       |
| Products             | GET (active)             | CREATE / READ / UPDATE / DELETE                       |
| Aspirations          | POST only                | READ / DELETE                                         |
| Media                | Public asset access      | Upload (POST)                                         |

**Catatan Delete Policy:** Apabila resource tidak secara spesifik mensyaratkan soft delete pada PRD/Database Design, API akan melakukan hard delete. Pengecualian pada foreign key (misal: Division ke Management) menggunakan RESTRICT untuk mencegah penghapusan jika masih terdapat dependensi.

---

## 10. Organization Profile API

* **Public:** `GET /api/v1/public/organization`
* **Admin:** `GET /api/v1/admin/organization`, `PUT /api/v1/admin/organization` (Update data statis).

---

## 11. Divisions API

* **Public:** `GET /api/v1/public/divisions`
* **Admin:** `GET, POST, PUT, DELETE /api/v1/admin/divisions`

---

## 12. Management Members API

* **Public:** `GET /api/v1/public/management` (Hanya status `active`).
* **Admin:** `GET, POST, PUT, DELETE /api/v1/admin/management` (CRUD penuh).

---

## 13. Kajian API

* **Public:** `GET /api/v1/public/kajian` (Listing `published`), `GET /api/v1/public/kajian/{slug}` (Detail native `published`).
* **Admin:** `GET, POST, PUT, DELETE /api/v1/admin/kajian`.
* **Business Rule:** Validasi slug unique. Author berupa free-text (sesuai Database Design). Content adalah native (bukan redirect).

---

## 14. News / PWMU API

* **Public:** `GET /api/v1/public/news` (Metadata `published`).
* **Admin:** `GET, POST, PUT, DELETE /api/v1/admin/news`.
* **Business Rule:** API hanya menyimpan dan mengembalikan metadata (title, excerpt, thumbnail) serta `pwmu_url`. PWMU tetap menjadi source of truth untuk isi berita penuh.

---

## 15. Alumni API

* **Public:** `GET /api/v1/public/alumni` (Status `published`).
* **Admin:** `GET, POST, PUT, DELETE /api/v1/admin/alumni`.

---

## 16. Products / Kaizen Company API

* **Public:** `GET /api/v1/public/products` (Status `active`).
* **Admin:** `GET, POST, PUT, DELETE /api/v1/admin/products`.
* **Business Rule:** numeric price (`>=0`), numeric stock (`>=0`), `whatsapp_number` tersedia. Tidak ada cart, payment, atau transaction order API.

---

## 17. Aspirasi API

* **Public:** HANYA `POST /api/v1/public/aspirations`. Murni anonim. API tidak akan menerima/menyimpan field `name`, `email`, `account`, `phone`, atau IP address secara permanen di database.
* **Admin:** `GET` (Baca aspirasi), `DELETE` (Hapus aspirasi). Tidak ada `PUT/UPDATE` untuk menjaga orisinalitas aspirasi.

---

## 18. Media / Storage API

* **Public:** Akses melalui public URL Supabase Storage.
* **Admin:** `POST /api/v1/admin/media/upload`. Validasi image only (png, jpg, jpeg, webp) dengan ukuran sekitar ~2MB.

---

## 19. Validation Rules

Validasi dilakukan di tingkat API sebelum menyentuh database:

* **Slug:** URL-safe regex `^[a-z0-9-]+$`.
* **String Lengths:** Maksimal 255 karakter untuk kolom VARCHAR (Title, Name).
* **Numeric Constraints:** `products.price >= 0` dan `products.stock >= 0`.
* **Status Enums:** Harus sesuai CHECK constraint di DB (misal: `draft`, `published`, `unpublished`).
* **Sanitization:** Input string harus di-trim.

---

## 20. Error Handling

Format standar Error Response:

```json
{
  "success": false,
  "data": null,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Field 'title' is required.",
    "details": [
      "title cannot be empty"
    ]
  }
}
```

---

## 21. Pagination / Search / Filter / Sort

* **Pagination:** Page-based (Menggunakan `page` dan `limit`). Output meta ada di objek `meta`.
* **Search:** Diarahkan berdasarkan field relevan tiap resource (Bukan full-text generic engine).
* **Management Members:** `search=name`
* **Divisions:** `search=name`
* **Kajian:** `search=title, excerpt, author`
* **News:** `search=title`
* **Products:** `search=name`
* **Alumni:** `search=name`
* **Filter/Sort:** `?status=active` atau `?sort=published_at&order=desc` sesuai skema.

---

## 22. Caching & Performance

* API didesain netral terhadap framework (Framework-Neutral). Backend tidak mengunci implementasi spesifik Vercel/Next.js.
* Public API merekomendasikan penggunaan HTTP Headers seperti `Cache-Control` (contoh: `public, s-maxage=60, stale-while-revalidate=300`) yang dapat ditangkap oleh layer Frontend (SSR/SSG/ISR).
* Admin data/Unpublished content TIDAK BOLEH terkena public cache.

---

## 23. Security & Rich Text Protection

* **RLS Enforcement:** Backend berjalan sebagai klien terautentikasi (meneruskan JWT) agar Row Level Security di database berlaku konsisten.
* **Rich Text Sanitization:** API mengirim konten markdown/rich text (Status Format: OPEN DECISION) sesuai yang tersimpan. Namun, API Specification menegaskan bahwa Content Renderer di Frontend wajib melakukan sanitization (misal: DOMPurify) untuk mencegah XSS.
* **Rate Limiting:** Implementasi Rate Limit untuk `POST Aspirasi` merupakan kebutuhan keamanan (status implementasi: OPEN DECISION).

---

## 24. SEO Support

API Public Kajian Detail (`GET /api/v1/public/kajian/{slug}`) mengembalikan properties (Title, Excerpt, Thumbnail, Author, Published Date) yang memadai agar Frontend dapat merender tag HTML `<meta>` dan Open Graph (OG) spesifik.

---

## 25. HTTP Status Code Matrix

| Code  | Meaning               | Usage                                                                      |
| ----- | --------------------- | -------------------------------------------------------------------------- |
| `200` | OK                    | Request GET, PUT, DELETE berhasil.                                         |
| `201` | Created               | Request POST (Resource baru) berhasil dibuat.                              |
| `400` | Bad Request           | Request malformed / sintaks JSON tidak valid.                              |
| `401` | Unauthorized          | JWT tidak ada, invalid, atau expired.                                      |
| `403` | Forbidden             | JWT valid tetapi user BUKAN Super Admin yang berada di allowlist.          |
| `404` | Not Found             | Resource tidak ditemukan / Resource (draft) tidak tersedia untuk public.   |
| `409` | Conflict              | Validasi Unique Constraint gagal (misal: duplicate slug).                  |
| `422` | Unprocessable Entity  | Validation/Business-rule error (Data sintaks valid tapi melanggar aturan). |
| `429` | Too Many Requests     | Rate limit / Spam protection (contoh pada POST Aspirasi).                  |
| `500` | Internal Server Error | Unexpected server-side error.                                              |

---

## 26. API Endpoint Matrix

| Method | Endpoint                  | Access      | Purpose                                  |
| ------ | ------------------------- | ----------- | ---------------------------------------- |
| GET    | `/public/organization`    | Public      | Mendapat info organisasi statis.         |
| GET    | `/public/divisions`       | Public      | Daftar divisi/bidang.                    |
| GET    | `/public/management`      | Public      | Daftar pengurus (status active).         |
| GET    | `/public/kajian`          | Public      | List Kajian (status published).          |
| GET    | `/public/kajian/{slug}`   | Public      | Detail Kajian native (status published). |
| GET    | `/public/news`            | Public      | List Berita/Metadata (status published). |
| GET    | `/public/alumni`          | Public      | Showcase Alumni (status published).      |
| GET    | `/public/products`        | Public      | Katalog Ekowir/Products (status active). |
| POST   | `/public/aspirations`     | Public      | Submit aspirasi mahasiswa anonim.        |
| GET    | `/admin/organization`     | Super Admin | Baca profil organisasi (CMS).            |
| PUT    | `/admin/organization`     | Super Admin | Update profil organisasi.                |
| POST   | `/admin/kajian`           | Super Admin | Create Kajian baru.                      |
| GET    | `/admin/kajian`           | Super Admin | List Kajian (All statuses).              |
| PUT    | `/admin/kajian/{id}`      | Super Admin | Update Kajian (termasuk ganti status).   |
| DEL    | `/admin/kajian/{id}`      | Super Admin | Hard Delete Kajian.                      |
| GET    | `/admin/aspirations`      | Super Admin | Baca daftar aspirasi masuk.              |
| DEL    | `/admin/aspirations/{id}` | Super Admin | Hapus data aspirasi.                     |
| POST   | `/admin/media/upload`     | Super Admin | Upload asset ke Storage.                 |

> **Catatan:** Pola operasi GET (All), POST, PUT, DELETE konsisten pada rute `/admin` untuk Management, Divisions, News, Alumni, dan Products.

---

## 27. Detailed Endpoint Specifications (Example)

### Endpoint: Public Submit Aspirasi

* **Method:** `POST`
* **Path:** `/api/v1/public/aspirations`
* **Access:** Public (Anonymous)
* **Purpose:** Menerima masukan dari mahasiswa tanpa identitas.

**Request Body:**

```json
{
  "content": "Mohon perbanyak kegiatan diskusi."
}
```

**Validation:**

`content` (Required, string, min 10 chars, max 2000 chars).

API akan membuang field identitas apabila dikirim.

**Success Response (201):**

```json
{
  "success": true,
  "data": {
    "message": "Aspirasi berhasil dikirim."
  }
}
```

**Error Response (422):**

```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "..."
  }
}
```

**Error Response (429):**

`Too Many Requests` (Rate limited).

---

## 28. Traceability Matrix

| PRD/TSS Requirement       | Database Entity        | API Endpoint                                             |
| ------------------------- | ---------------------- | -------------------------------------------------------- |
| Organization Profile      | `organization_profile` | GET/PUT `/api/v1/.../organization`                       |
| Divisions Management      | `divisions`            | GET/POST/PUT/DEL `/api/v1/.../divisions`                 |
| Management Members        | `management_members`   | GET/POST/PUT/DEL `/api/v1/.../management`                |
| FR-009 Kajian Homepage    | `kajian`               | GET `/api/v1/public/kajian`                              |
| FR-010 Kajian Detail      | `kajian`               | GET `/api/v1/public/kajian/{slug}`                       |
| Kajian CRUD               | `kajian`               | GET/POST/PUT/DEL `/api/v1/admin/kajian`                  |
| News (PWMU Redirect)      | `news`                 | GET `/api/v1/.../news`                                   |
| Products (Kaizen Company) | `products`             | GET/POST/PUT/DEL `/api/v1/.../products`                  |
| Aspirasi Anonim           | `aspirations`          | POST `/public/aspirations`, GET/DEL `/admin/aspirations` |
| Showcase Alumni           | `alumni`               | GET/POST/PUT/DEL `/api/v1/.../alumni`                    |
| Media Storage             | N/A (Storage)          | POST `/api/v1/admin/media/upload`                        |
| Super Admin Authorization | `super_admins`         | Admin Route Validations                                  |

---

## 29. Open Decisions

### Decision 1: Rich Text Format untuk Kajian

* **Current Status:** OPEN DECISION. Database Design dan TSS mengindikasikan Markdown, tetapi implementasi final tergantung framework UI.
* **Impact on API:** API tetap menerima format sebagai string `TEXT`. Content renderer di frontend WAJIB menangani sanitasi XSS yang tepat.

### Decision 2: Rate Limiting Mechanism (Aspirasi)

* **Current Status:** OPEN DECISION. Konseptual disetujui untuk Spam Protection.
* **Impact on API:** Middleware diperlukan untuk memblokir IP temporer (merespons `429`) tanpa menyimpan IP tersebut ke dalam struktur data aspirasi permanen.

### Decision 3: Soft Delete vs Hard Delete Edge Cases

* **Current Status:** OPEN DECISION. Untuk entitas ringan API melakukan Hard Delete. Untuk foreign key digunakan RESTRICT. Soft Delete mechanism tidak diimplementasikan kecuali requirement bisnis di masa depan mengubahnya.

---

## 30. Implementation Readiness

* [x] Frontend Developer: Memiliki kontrak URL, payload, search params, dan response code yang jelas.
* [x] Backend Developer: Memiliki pedoman otorisasi allowlist, Supabase Auth integration, validasi 422, dan RLS consistency.
* [x] Database Developer: Skema data API sesuai 100% dengan Database Design V1.2.
* [x] UI/UX Developer: Memiliki acuan mengenai batasan data yang akan tampil ke publik (misalnya hanya status published/active).

---

## 31. Definition of Done

API Specification ini dianggap selesai apabila:

* [x] Semua resource dari Database Design telah diperiksa dan diselaraskan.
* [x] Public vs Super Admin authorization flow terdokumentasi akurat berbasis UUID allowlist.
* [x] Kajian (native) dan News (PWMU metadata) dipisahkan secara teknis.
* [x] Product API mencerminkan numeric stock dan whatsapp contact tanpa sistem e-commerce.
* [x] Aspirasi API memenuhi asas privasi anonimitas penuh.
* [x] Status code HTTP (terutama penambahan 422) diatur tepat sesuai best practices.
* [x] Tidak ada asumsi kerangka kerja (framework-neutral).

---

## 32. Final Validation

* **Requirement consistency:** PASS (Mengacu pada PRD V1.1)
* **Database consistency:** PASS (Mengacu pada Database Design V1.2)
* **Authentication consistency:** PASS (Supabase Auth, tanpa local password)
* **Authorization consistency:** PASS (1 Role Super Admin, Allowlist, Service Role rules)
* **RLS consistency:** PASS
* **Public API completeness:** PASS (Filter status eksplisit divalidasi)
* **Admin API completeness:** PASS
* **Kajian API completeness:** PASS
* **News/PWMU separation:** PASS
* **Kaizen Company API:** PASS (No checkout/cart)
* **Aspirasi privacy:** PASS (POST only untuk public, zero tracking)
* **Media/Storage:** PASS
* **Validation & Error handling:** PASS (Terstruktur, 422 Unprocessable Entity ditambahkan)
* **Security & Performance:** PASS (XSS warning, framework-neutral caching)
* **SEO:** PASS
* **Traceability & Implementation readiness:** PASS

### FINAL STATUS

> **PASS — API SPECIFICATION READY FOR UI/UX SPECIFICATION**
