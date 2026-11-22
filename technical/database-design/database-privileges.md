# 🛡️ Database Privileges

Dokumen ini menjelaskan hak akses PostgreSQL yang ditemukan pada database Kaizen Company Platform.

## 1. Database Roles

Terdapat tiga role utama yang diperiksa pada tabel aplikasi:

| Role | Description |
|---|---|
| `anon` | Database role untuk request tanpa autentikasi |
| `authenticated` | Database role untuk request dengan autentikasi |
| `service_role` | Database role dengan hak istimewa layanan |

Role tersebut berbeda dari role aplikasi `Superadmin` dan `Admin`.

## 2. Application Table Privileges

Pemeriksaan menunjukkan bahwa ketiga role memiliki privilege berikut pada seluruh 12 tabel aplikasi:

- `DELETE`
- `INSERT`
- `REFERENCES`
- `SELECT`
- `TRIGGER`
- `TRUNCATE`
- `UPDATE`

| Role | Tables | Detected Privileges |
|---|---:|---|
| `anon` | 12 | 7 jenis privilege |
| `authenticated` | 12 | 7 jenis privilege |
| `service_role` | 12 | 7 jenis privilege |

Tabel yang diperiksa:

1. `agendas`
2. `alumni`
3. `aspirations`
4. `dad_registrations`
5. `divisions`
6. `news`
7. `organization_profile`
8. `pengurus`
9. `products`
10. `profiles`
11. `site_settings`
12. `system_logs`

## 3. Storage Privileges

Ringkasan privilege yang ditemukan pada schema `storage`:

| Table | anon | authenticated | service_role |
|---|---|---|---|
| `bucket_lifecycle_states` | - | - | Full set |
| `buckets` | DELETE, INSERT, SELECT, UPDATE | DELETE, INSERT, SELECT, UPDATE | Full set |
| `buckets_analytics` | DELETE, INSERT, SELECT, UPDATE | DELETE, INSERT, SELECT, UPDATE | Full set |
| `buckets_vectors` | SELECT | SELECT | SELECT |
| `lifecycle_abandoned_artifacts` | - | - | Full set |
| `objects` | DELETE, INSERT, SELECT, UPDATE | DELETE, INSERT, SELECT, UPDATE | Full set |
| `s3_multipart_uploads` | SELECT | SELECT | Full set |
| `s3_multipart_uploads_parts` | SELECT | SELECT | Full set |
| `vector_indexes` | SELECT | SELECT | SELECT |

`Full set` merujuk pada privilege yang dikembalikan oleh query metadata untuk role terkait, bukan klaim bahwa seluruh operasi dapat dilakukan melalui API publik.

## 4. GRANT and RLS

GRANT dan RLS merupakan dua mekanisme yang berbeda.

- **GRANT** menentukan operasi database yang diizinkan pada tingkat privilege.
- **RLS** membatasi baris data yang dapat dibaca atau dimodifikasi berdasarkan policy.
- **Application role** menentukan kewenangan pengguna di dalam aplikasi.

Keberadaan GRANT tidak otomatis membuktikan bahwa operasi tersebut dapat dilakukan melalui endpoint aplikasi. Jalur akses dan mekanisme API yang digunakan juga perlu diperhitungkan.

## 5. Privilege Review

Privilege berikut perlu mendapatkan perhatian saat evaluasi konfigurasi:

| Privilege | Review |
|---|---|
| `SELECT` | Periksa bersama policy SELECT |
| `INSERT` | Periksa bersama policy INSERT |
| `UPDATE` | Periksa bersama policy UPDATE |
| `DELETE` | Periksa bersama policy DELETE |
| `TRUNCATE` | Periksa kebutuhan privilege karena operasi ini tidak dibatasi oleh RLS |
| `TRIGGER` | Evaluasi kebutuhan untuk role aplikasi |
| `REFERENCES` | Evaluasi kebutuhan untuk role aplikasi |

Khusus `TRUNCATE`, RLS tidak memberikan pembatasan baris untuk operasi tersebut. Namun, hasil pemeriksaan GRANT saja tidak membuktikan bahwa endpoint PostgREST menyediakan akses untuk menjalankan perintah TRUNCATE.

## 6. Security Notes

- Jangan membagikan secret `service_role` kepada frontend.
- Jangan menyamakan role PostgreSQL dengan role aplikasi.
- Periksa privilege dan RLS secara bersamaan.
- Evaluasi privilege yang tidak diperlukan sebelum melakukan perubahan.
- Jangan melakukan pencabutan privilege secara langsung pada production tanpa menguji dampaknya.

---

**Source:** `information_schema.role_table_grants` inspection.
