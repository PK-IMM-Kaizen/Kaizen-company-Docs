# Database Design — Website Resmi PK IMM Kaizen V1.2 (Revised)

## 1. Document Information

* **Document Title:** Database Design — Website Resmi PK IMM Kaizen
* **Product:** Website Resmi PK IMM Kaizen V1.0
* **Version:** 1.2 (Revised)
* **Status:** Final Draft
* **Date:** September 2026
* **Author:** Senior Database Architect
* **Source Document:** PRD V1.1 Revised, TSS V1.1 Revised

---

## 2. Revision History

| Version | Date     | Change                                                                                                                                                 |
| ------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1.0     | Sep 2026 | Initial Database Design                                                                                                                                |
| 1.1     | Sep 2026 | Revised database design (Kajian & Pemikiran incorporation)                                                                                             |
| 1.2     | Sep 2026 | Technical revision: Supabase Auth integration, RLS strictness, relationships, indexing, product stock (numeric), timestamps, and security constraints. |

---

## 3. Executive Summary

Dokumen Database Design ini merumuskan struktur penyimpanan data untuk Website Resmi PK IMM Kaizen V1.1.

Desain ini menggunakan PostgreSQL (melalui Supabase) sebagai penyedia Database-as-a-Service (DaaS).

Revisi V1.2 ini berfokus pada penguatan keamanan (RLS yang lebih ketat), penghapusan penyimpanan password manual di basis data aplikasi dengan mengandalkan `auth.users` dari Supabase, perbaikan strategi indexing, konsistensi timestamp, dan penegasan relasi antar entitas yang berorientasi pada maintainability dan kemudahan handover.

---

## 4. Database Architecture

Sistem menggunakan **PostgreSQL (Supabase)**.

### Alasan

* Mendukung relasional yang kuat.
* Row Level Security (RLS) terintegrasi untuk otorisasi akses di level database.
* Open-source (mencegah vendor-lock-in murni).
* Free-tier yang efisien.

### Portability

Skema dirancang murni menggunakan fitur standar PostgreSQL (seperti CHECK constraints, FK) sehingga mudah di-dump dan di-migrasi ke penyedia VPS mandiri jika diperlukan di masa depan.

---

## 5. Design Principles

* **Normalization yang Wajar:** Tidak menormalisasi berlebihan (misalnya, author pada kajian dibiarkan sebagai teks bebas sesuai kebutuhan organisasi yang dinamis).
* **Referential Integrity:** Penggunaan `ON DELETE RESTRICT` pada relasi penting untuk mencegah hilangnya data secara tidak sengaja.
* **Minimal Complexity:** Tidak membuat tabel yang tidak diminta PRD (tidak ada tabel `orders`, `cart`, `comments`, `public_users`).
* **Handover-Friendly:** Struktur jelas, penamaan kolom baku, dan tidak menggunakan fitur proprietari yang menyulitkan migrasi.

---

## 6. Entity Overview

* **`super_admins`:** Tabel identitas/admin (relasi ke `auth.users`).
* **`organization_profile`:** Identitas dan kontak organisasi (single-row).
* **`divisions`:** Data bidang (termasuk Ekowir).
* **`management_members`:** Personalia pengurus.
* **`kajian`:** Konten tulisan/artikel native.
* **`news`:** Direktori redirect ke berita PWMU.
* **`alumni`:** Data alumni berprestasi.
* **`products`:** Katalog Kaizen Company.
* **`aspirations`:** Wadah masukan publik secara anonim.

---

## 7. ERD (Entity Relationship Diagram)

### Conceptual

* **`auth_users`:** `id (PK)`, `email`
* **`super_admins`:** `id (PK, FK to auth_users)`, `email`, `created_at`
* **`organization_profile`:** `id (PK)`, `name`, `history`, `vision`, `mission`, `address`, `email`, `social_links`
* **`divisions`:** `id (PK)`, `name`, `description`, `display_order`
* **`management_members`:** `id (PK)`, `division_id (FK)`, `name`, `photo_url`, `position`, `status`, `display_order`
* **`kajian`:** `id (PK)`, `title`, `slug (UK)`, `thumbnail_url`, `excerpt`, `content`, `author`, `status`, `published_at`
* **`news`:** `id (PK)`, `title`, `excerpt`, `thumbnail_url`, `pwmu_url`, `status`, `published_at`
* **`alumni`:** `id (PK)`, `name`, `photo_url`, `achievement`, `status`
* **`products`:** `id (PK)`, `name`, `description`, `stock`, `price`, `category`, `image_url`, `whatsapp_number`, `status`
* **`aspirations`:** `id (PK)`, `content`

---

## 8. Authentication & Admin Identity

* **Supabase Auth (`auth.users`):** Berperan sebagai sumber otentikasi tunggal. Sistem **TIDAK** menyimpan `password_hash` secara manual di tabel aplikasi.
* **Admin Identity (`super_admins`):** Tabel ekstensi dari `auth.users`. Tabel ini berfungsi sebagai Allowlist. Jika UUID pengguna yang login ada di tabel ini, maka ia adalah Super Admin dan diberikan akses CMS penuh melalui RLS.
* **Role Setup:** Hanya ada 1 role logis, yaitu `SUPER_ADMIN`. Tidak ada role staf, editor, atau penulis bidang.

---

# 9. Table Specifications

## 9.1. `super_admins` (Admin Identity)

| Column       | Data Type    | Nullable | Default | Key    | Description                       |
| ------------ | ------------ | -------- | ------- | ------ | --------------------------------- |
| `id`         | UUID         | No       | —       | PK, FK | Relasi 1:1 ke `auth.users.id`.    |
| `email`      | VARCHAR      | No       | —       | UK     | Duplikasi untuk kemudahan UI CMS. |
| `created_at` | TIMESTAMP TZ | No       | `NOW()` | —      | —                                 |

---

## 9.2. `organization_profile` (Single Row)

| Column         | Data Type    | Nullable | Default | Key | Description                   |
| -------------- | ------------ | -------- | ------- | --- | ----------------------------- |
| `id`           | INT          | No       | `1`     | PK  | Selalu 1.                     |
| `name`         | VARCHAR      | No       | —       | —   | Nama organisasi.              |
| `history`      | TEXT         | Yes      | —       | —   | Sejarah organisasi.           |
| `vision`       | TEXT         | Yes      | —       | —   | Visi.                         |
| `mission`      | TEXT         | Yes      | —       | —   | Misi.                         |
| `address`      | TEXT         | Yes      | —       | —   | Alamat.                       |
| `email`        | VARCHAR      | Yes      | —       | —   | Email publik organisasi.      |
| `social_links` | JSONB        | Yes      | —       | —   | Array/Objek social media.     |
| `created_at`   | TIMESTAMP TZ | No       | `NOW()` | —   | —                             |
| `updated_at`   | TIMESTAMP TZ | No       | `NOW()` | —   | Diperbarui saat Admin update. |

---

## 9.3. `divisions`

| Column          | Data Type    | Nullable | Default              | Key | Description           |
| --------------- | ------------ | -------- | -------------------- | --- | --------------------- |
| `id`            | UUID         | No       | `uuid_generate_v4()` | PK  | —                     |
| `name`          | VARCHAR      | No       | —                    | —   | Nama Bidang.          |
| `description`   | TEXT         | Yes      | —                    | —   | —                     |
| `display_order` | INT          | No       | `0`                  | —   | Urutan tampil publik. |
| `created_at`    | TIMESTAMP    | No       | `NOW()`              | —   | —                     |
| `updated_at`    | TIMESTAMP TZ | No       | `NOW()`              | —   | —                     |

---

## 9.4. `management_members`

| Column          | Data Type    | Nullable | Default              | Key | Description             |
| --------------- | ------------ | -------- | -------------------- | --- | ----------------------- |
| `id`            | UUID         | No       | `uuid_generate_v4()` | PK  | —                       |
| `division_id`   | UUID         | No       | —                    | FK  | Relasi ke `divisions`.  |
| `name`          | VARCHAR      | No       | —                    | —   | —                       |
| `photo_url`     | VARCHAR      | Yes      | —                    | —   | URL WebP foto profil.   |
| `position`      | VARCHAR      | No       | —                    | —   | Jabatan (misal: Ketua). |
| `status`        | VARCHAR      | No       | `'active'`           | —   | `active` / `inactive`.  |
| `display_order` | INT          | No       | `0`                  | —   | —                       |
| `created_at`    | TIMESTAMP TZ | No       | `NOW()`              | —   | —                       |
| `updated_at`    | TIMESTAMP TZ | No       | `NOW()`              | —   | —                       |

---

## 9.5. `kajian`

| Column          | Data Type    | Nullable | Default              | Key | Description                            |
| --------------- | ------------ | -------- | -------------------- | --- | -------------------------------------- |
| `id`            | UUID         | No       | `uuid_generate_v4()` | PK  | —                                      |
| `title`         | VARCHAR      | No       | —                    | —   | —                                      |
| `slug`          | VARCHAR      | No       | —                    | UK  | URL-safe identifier (unik).            |
| `thumbnail_url` | VARCHAR      | Yes      | —                    | —   | Cover image URL.                       |
| `excerpt`       | VARCHAR      | No       | —                    | —   | Deskripsi singkat SEO/Card.            |
| `content`       | TEXT         | No       | —                    | —   | Full text (direkomendasikan Markdown). |
| `author`        | VARCHAR      | Yes      | —                    | —   | Teks bebas (Free text).                |
| `status`        | VARCHAR      | No       | `'draft'`            | —   | `draft` / `published` / `unpublished`. |
| `published_at`  | TIMESTAMP TZ | Yes      | —                    | —   | Tanggal rilis tayang.                  |
| `created_at`    | TIMESTAMP TZ | No       | `NOW()`              | —   | —                                      |
| `updated_at`    | TIMESTAMP TZ | No       | `NOW()`              | —   | —                                      |

---

## 9.6. `news`

| Column          | Data Type    | Nullable | Default              | Key | Description                            |
| --------------- | ------------ | -------- | -------------------- | --- | -------------------------------------- |
| `id`            | UUID         | No       | `uuid_generate_v4()` | PK  | —                                      |
| `title`         | VARCHAR      | No       | —                    | —   | —                                      |
| `excerpt`       | VARCHAR      | No       | —                    | —   | —                                      |
| `thumbnail_url` | VARCHAR      | Yes      | —                    | —   | —                                      |
| `pwmu_url`      | VARCHAR      | No       | —                    | —   | Link redirect eksternal.               |
| `status`        | VARCHAR      | No       | `'draft'`            | —   | `draft` / `published` / `unpublished`. |
| `published_at`  | TIMESTAMP TZ | Yes      | —                    | —   | Tanggal berita asli di PWMU.           |
| `created_at`    | TIMESTAMP TZ | No       | `NOW()`              | —   | —                                      |
| `updated_at`    | TIMESTAMP TZ | No       | `NOW()`              | —   | —                                      |

---

## 9.7. `alumni`

| Column        | Data Type    | Nullable | Default              | Key | Description                  |
| ------------- | ------------ | -------- | -------------------- | --- | ---------------------------- |
| `id`          | UUID         | No       | `uuid_generate_v4()` | PK  | —                            |
| `name`        | VARCHAR      | No       | —                    | —   | —                            |
| `photo_url`   | VARCHAR      | Yes      | —                    | —   | —                            |
| `achievement` | TEXT         | No       | —                    | —   | —                            |
| `status`      | VARCHAR      | No       | `'published'`        | —   | `published` / `unpublished`. |
| `created_at`  | TIMESTAMP TZ | No       | `NOW()`              | —   | —                            |
| `updated_at`  | TIMESTAMP TZ | No       | `NOW()`              | —   | —                            |

---

## 9.8. `products`

| Column            | Data Type    | Nullable | Default              | Key | Description                       |
| ----------------- | ------------ | -------- | -------------------- | --- | --------------------------------- |
| `id`              | UUID         | No       | `uuid_generate_v4()` | PK  | —                                 |
| `name`            | VARCHAR      | No       | —                    | —   | —                                 |
| `description`     | TEXT         | Yes      | —                    | —   | —                                 |
| `stock`           | INT          | No       | `0`                  | —   | Numeric stock (`0 = Habis`).      |
| `price`           | BIGINT       | No       | `0`                  | —   | Harga produk (Rp).                |
| `category`        | VARCHAR      | Yes      | —                    | —   | misal: Barang/Jasa.               |
| `image_url`       | VARCHAR      | Yes      | —                    | —   | —                                 |
| `whatsapp_number` | VARCHAR      | No       | —                    | —   | Nomor HP untuk flow pembelian WA. |
| `status`          | VARCHAR      | No       | `'active'`           | —   | `active` / `inactive`.            |
| `created_at`      | TIMESTAMP TZ | No       | `NOW()`              | —   | —                                 |
| `updated_at`      | TIMESTAMP TZ | No       | `NOW()`              | —   | —                                 |

---

## 9.9. `aspirations`

| Column       | Data Type    | Nullable | Default              | Key | Description                    |
| ------------ | ------------ | -------- | -------------------- | --- | ------------------------------ |
| `id`         | UUID         | No       | `uuid_generate_v4()` | PK  | —                              |
| `content`    | TEXT         | No       | —                    | —   | Teks kritik/saran dari publik. |
| `created_at` | TIMESTAMP TZ | No       | `NOW()`              | —   | —                              |

---

## 10. Relationships & Referential Integrity

* **`divisions` → `management_members`:** 1:N. Seorang pengurus terikat pada 1 bidang (kolom `division_id`).
* **Deletion Action:** `FOREIGN KEY (division_id) REFERENCES divisions(id) ON DELETE RESTRICT`.
* **Alasan:** Mencegah Admin tidak sengaja menghapus "Bidang Ekowir" jika di dalamnya masih ada anggota kepengurusan.
* **Kajian Author:** Dipertahankan sebagai teks bebas (`VARCHAR`) agar penulis kajian yang bukan merupakan struktur kepengurusan aktif tetap bisa dicantumkan.

---

## 11. Constraints

* `kajian.slug`: `UNIQUE`
* `super_admins.email`: `UNIQUE`
* `organization_profile.id`: `CHECK (id = 1)`
* `products.stock`: `CHECK (stock >= 0)`
* `products.price`: `CHECK (price >= 0)`

---

## 12. Index Strategy

Indeks dibuat khusus untuk kolom yang di-query secara masif oleh pengunjung publik:

* `idx_kajian_slug`: Pada `kajian(slug)`
* `idx_kajian_status_date`: Pada `kajian(status, published_at DESC)`
* `idx_news_status`: Pada `news(status, published_at DESC)`
* `idx_products_status`: Pada `products(status)`
* `idx_members_division`: Pada `management_members(division_id)`
* `idx_divisions_order`: Pada `divisions(display_order)`

---

## 13. Status & Visibility

Status menggunakan CHECK constraints eksplisit untuk validitas data:

* **Kajian & News:** `CHECK (status IN ('draft', 'published', 'unpublished'))`
* **Management Members:** `CHECK (status IN ('active', 'inactive'))`
* **Products:** `CHECK (status IN ('active', 'inactive'))`
* **Alumni:** `CHECK (status IN ('published', 'unpublished'))`

---

## 14. Media & Storage Strategy

Sistem **TIDAK** memiliki tabel media mandiri (`media_table`).

* Database hanya menyimpan URL direct path dalam bentuk string.
* File fisik disimpan di Supabase Storage (sebuah bucket bernama `public_assets`).
* **Aturan Akses Storage:**

  * Publik memiliki hak akses `SELECT` (download).
  * Hanya Super Admin yang dapat melakukan `INSERT`, `UPDATE`, `DELETE`.

---

## 15. Row Level Security (RLS)

Desain keamanan menggunakan pendekatan Allowlist yang sangat spesifik:

### Identifikasi Super Admin

Verifikasi apakah:

```sql
auth.uid() IN (SELECT id FROM super_admins)
```

### Akses Publik

* `SELECT` diizinkan pada semua tabel konten hanya jika kondisi status terpenuhi (misal: `status = 'published'` atau `status = 'active'`).
* `INSERT` hanya diizinkan pada tabel `aspirations`.
* Akses lain secara tegas **DITOLAK**.

### Akses Super Admin

* Diizinkan `SELECT`, `INSERT`, `UPDATE`, `DELETE` pada semua tabel operasional.
* **Pengecualian:** Pada tabel `aspirations`, Super Admin hanya diizinkan `SELECT` dan `DELETE`.

---

## 16. Supabase Service Role Security Note

Supabase Service Role Key memiliki privilese bypass RLS.

Key ini **WAJIB** dijaga kerahasiaannya (Server-side only).

Tidak boleh direkatkan (hardcode) dalam kode frontend atau diakses melalui browser.

---

## 17. Backup & Recovery

* **Database Backup:** Mengandalkan sistem cadangan harian terotomatisasi (Automated Daily Backups) dari Supabase.
* **Aspiration Recovery:** Disediakan fungsionalitas Export CSV di aplikasi dashboard bagi Super Admin sebagai manual backup.

---

## 18. Migration Strategy

Skema didefinisikan menggunakan ORM berbasis migrasi (seperti Prisma).

Setiap perubahan struktur akan dicatat sebagai file SQL `.migration`.

---

## 19. Seed Data Strategy

* **`organization_profile`:** Diinjeksi dengan `id = 1` dan nama `"PK IMM Kaizen"` sebagai placeholder awal.
* **`super_admins`:** Data Admin pertama akan diinjeksi via skrip migrasi awal.

---

## 20. Handover Considerations

* Struktur basis data sangat linier dan menggunakan standar penamaan bahasa Inggris (`snake_case`).
* Pemilik (Owner) project Supabase **WAJIB** dialihkan ke email resmi organisasi (`admin@kaizen.org.id`) pada saat deployment final.

---

## 21. Traceability

| PRD / TSS Requirement          | Database Representation           | Note                                                 |
| ------------------------------ | --------------------------------- | ---------------------------------------------------- |
| Manajemen Identitas & CMS Auth | `auth.users` & `super_admins`     | Supabase terintegrasi, tak ada password lokal.       |
| Organization Profile (Single)  | `organization_profile`            | ID 1 tetap, timestamp aktif.                         |
| Kepengurusan & Bidang (1:N)    | `divisions`, `management_members` | FK Restrict.                                         |
| Kajian & Pemikiran             | `kajian`                          | Full content (Markdown), slug UK, Status kontrol.    |
| Berita (External PWMU)         | `news`                            | `pwmu_url` sebagai redirect, tanpa body content.     |
| Alumni Showcase                | `alumni`                          | Showcase selektif berbasis status.                   |
| Kaizen Company / Product       | `products`                        | stock INT, `whatsapp_number` dinamis.                |
| Aspirasi Mahasiswa             | `aspirations`                     | 100% anonim, tanpa IP/Email, rate limit (App layer). |

---

## 22. Open Decisions

| Decision Area    | Status   | Recommended                          | Impact                                               |
| ---------------- | -------- | ------------------------------------ | ---------------------------------------------------- |
| Kajian Author    | Resolved | Teks Bebas (`VARCHAR`).              | Mengakomodasi penulis di luar pengurus aktif.        |
| Product Contact  | Resolved | `whatsapp_number` di tabel products. | Admin dapat menentukan nomor WA berbeda tiap produk. |
| Product Stock    | Resolved | Kolom `stock` (`INT`) + Check >= 0.  | Stok di-update manual. Habis = 0.                    |
| Rich Text Format | Open     | Markdown.                            | Butuh konfirmasi final tim Frontend.                 |

---

## 23. Definition of Done

Database Design ini dinyatakan selesai apabila:

* [x] Autentikasi diselaraskan murni dengan Supabase Auth.
* [x] Otorisasi diperketat melalui konsep Allowlist Super Admin dan batasan RLS publik.
* [x] Seluruh Timestamp (`updated_at`) didistribusikan konsisten ke tabel CMS.
* [x] Stock pada entitas produk dikonversi menjadi operasional numerik (`INTEGER`).
* [x] Relasi entitas didefinisikan dengan On Delete Restrict.
* [x] Modul Kajian vs Berita PWMU dibedakan secara tegas sesuai PRD.
* [x] Persyaratan anonimitas mutlak bagi Aspirasi Mahasiswa terjamin.

---

## 24. Final Validation

* **Requirement Validation:** PASS
* **Schema Completeness:** PASS
* **Data Integrity (Constraints & FK):** PASS
* **Security (RLS Strictness):** PASS
* **Kajian Support:** PASS
* **Anonymous Aspirations:** PASS
* **PWMU External Content Model:** PASS
* **Kaizen Company / Product (Stock & Contact):** PASS
* **Handover Readiness:** PASS
* **Overengineering Check:** PASS

---

## 25. Final Status

> **PASS — DATABASE DESIGN READY FOR API SPECIFICATION**
