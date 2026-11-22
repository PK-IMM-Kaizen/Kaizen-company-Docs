# 🔍 SQL Audit Report

Laporan audit terhadap SQL historis dan metadata database Supabase untuk Kaizen Company Platform.

## 1. Audit Objective

Audit dilakukan untuk:

- Menginventarisasi struktur database yang sedang digunakan.
- Mengidentifikasi konfigurasi RLS dan hak akses.
- Memisahkan SQL historis berdasarkan tujuan.
- Mengidentifikasi potensi konflik dan risiko.
- Menjadi dasar dokumentasi database dan pengelolaan perubahan berikutnya.

Audit ini tidak dimaksudkan untuk mengubah desain aplikasi yang sudah berjalan di production.

## 2. Database Inventory

| Component | Result |
|---|---:|
| Application tables | 12 |
| Application columns | 103 |
| Constraints | 60 |
| Indexes | 13 |
| Foreign keys (public + auth) | 27 |
| RLS-enabled application tables | 12 |
| Detected RLS policies | 47 |
| Custom application functions | 1 |
| Application triggers | 1 |
| Storage buckets | 6 |
| Application views | 0 |
| Application materialized views | 0 |

## 3. Confirmed Findings

### 3.1 Duplicate Historical Definitions

Arsip SQL historis memiliki beberapa definisi berulang, termasuk definisi tabel `news` dan `system_logs`.

**Impact:**

- Sulit menentukan definisi mana yang merepresentasikan kondisi terbaru.
- Menjalankan seluruh arsip dapat menyebabkan konflik.
- Riwayat perubahan tidak dapat diperlakukan sebagai migration berurutan tanpa rekonstruksi.

**Documentation action:**

SQL historis disimpan sebagai arsip. Struktur terkini didokumentasikan berdasarkan metadata database aktual.

### 3.2 Broad RLS Policy Conditions

Beberapa policy ditemukan menggunakan:

```sql
USING (true)
```

atau:

```sql
WITH CHECK (true)
```

**Impact:**

Kondisi tersebut dapat memberikan akses luas untuk operasi dan target role yang ditentukan oleh policy.

**Review action:**

Periksa definisi lengkap setiap policy, termasuk:

- Table.
- Command.
- Target role.
- `USING`.
- `WITH CHECK`.
- Policy permissive atau restrictive.

Jangan menilai keamanan policy hanya dari satu kondisi tanpa melihat keseluruhan konfigurasi.

### 3.3 User Provisioning Function

Fungsi `handle_new_user()` memberikan role awal `admin` kepada setiap user baru yang diproses oleh trigger `on_auth_user_created`.

**Impact:**

Perilaku ini harus dipahami sebagai bagian dari alur provisioning akun yang digunakan aplikasi.

**Review action:**

Pastikan proses pembuatan akun dan pengelolaan role sesuai dengan alur operasional production yang berlaku.

### 3.4 Storage Bucket Exposure

Enam bucket ditemukan memiliki status `public = true`.

Bucket yang ditemukan:

- `organization-assets`
- `pengurus_photos`
- `ekowir_images`
- `dad_photos`
- `dad_payments`
- `news_images`

**Impact:**

File pada bucket public dapat diakses melalui URL publik.

Bucket `dad_payments` perlu menjadi prioritas evaluasi karena berkaitan dengan bukti pembayaran.

### 3.5 Destructive SQL

Arsip historis memuat perintah:

```sql
TRUNCATE TABLE public.divisions;
```

**Impact:**

Perintah tersebut menghapus seluruh baris pada tabel yang dituju.

**Review action:**

- Jangan menjalankan ulang perintah tersebut sebagai bagian dari setup database.
- Simpan sebagai bagian dari arsip historis.
- Periksa konteks dan tujuan awal perintah sebelum mempertimbangkan penggunaannya kembali.

### 3.6 Database Privileges

Ketiga role `anon`, `authenticated`, dan `service_role` ditemukan memiliki tujuh jenis privilege pada seluruh 12 tabel aplikasi.

Privilege tersebut termasuk `TRUNCATE`, `TRIGGER`, dan `REFERENCES`.

**Impact:**

Konfigurasi ini perlu dievaluasi berdasarkan kebutuhan operasional dan jalur akses aplikasi.

Keberadaan privilege tidak dengan sendirinya membuktikan bahwa seluruh operasi tersedia melalui API publik.

## 4. Application Access Model

Model akses aplikasi yang telah ditetapkan:

| Permission | Superadmin | Admin |
|---|:---:|:---:|
| Mengelola modul aplikasi | Ya | Ya |
| Membuat akun Admin | Ya | Tidak |
| Mengedit akun Admin | Ya | Tidak |
| Menghapus akun Admin | Ya | Tidak |

Superadmin dan Admin memiliki hak operasional yang sama. Perbedaan hanya terdapat pada pengelolaan akun Admin.

Role aplikasi tersebut tidak boleh disamakan dengan role PostgreSQL.

## 5. SQL Archive Classification

SQL historis perlu dikelompokkan berdasarkan tujuan:

| Category | Content |
|---|---|
| Schema | CREATE TABLE, ALTER TABLE |
| Constraints | PRIMARY KEY, FOREIGN KEY, UNIQUE, CHECK |
| Indexes | CREATE INDEX |
| RLS | ENABLE/DISABLE RLS, CREATE POLICY |
| Functions | CREATE OR REPLACE FUNCTION |
| Triggers | CREATE TRIGGER |
| Storage | Bucket dan Storage policies |
| Seeds | INSERT data awal |
| Destructive | TRUNCATE, DROP, DELETE massal |
| Archive | Query historis dan eksperimen |

## 6. Risk Register

| ID | Finding | Priority | Status |
|---|---|---|---|
| DB-001 | Policy dengan kondisi terbuka | High | Perlu review policy per tabel |
| DB-002 | Bucket `dad_payments` public | High | Perlu evaluasi akses file |
| DB-003 | Default role `admin` pada provisioning | Review | Perlu verifikasi alur akun |
| DB-004 | Privilege `TRUNCATE` pada role aplikasi | Review | Perlu evaluasi kebutuhan |
| DB-005 | SQL historis mengandung duplikasi | Medium | Arsip, jangan dijalankan massal |
| DB-006 | Perintah TRUNCATE pada `divisions` | High | Tandai sebagai destruktif |

Prioritas menunjukkan urutan pemeriksaan, bukan bukti bahwa sistem telah berhasil dieksploitasi.

## 7. Recommended Documentation Workflow

1. Gunakan metadata database aktual sebagai referensi kondisi terkini.
2. Simpan SQL lama di `sql/archive/`.
3. Pisahkan migration, seed, dan query audit.
4. Dokumentasikan setiap perubahan skema.
5. Tinjau RLS dan Storage policies sebelum perubahan hak akses.
6. Uji perubahan pada lingkungan non-production jika tersedia.
7. Lakukan perubahan production secara terkontrol.

## 8. Audit Limitations

Audit ini didasarkan pada hasil metadata dan SQL yang telah diperiksa.

Hal yang belum dapat dinyatakan final tanpa pemeriksaan definisi lengkap:

- Matriks akses setiap policy RLS per tabel dan operasi.
- Seluruh definisi index.
- Detail tipe data seluruh 103 kolom.
- Isi lengkap setiap bucket dan struktur folder Storage.
- Konteks historis setiap query destruktif.
- Implementasi aplikasi yang memanggil setiap tabel dan Storage bucket.

## 9. Conclusion

Database Kaizen Company Platform telah memiliki struktur aplikasi yang terdiri dari 12 tabel, relasi ke Supabase Auth, RLS pada seluruh tabel aplikasi, fungsi provisioning user, serta enam bucket Storage.

Temuan audit utama berpusat pada evaluasi policy RLS, akses Storage untuk data pembayaran, privilege database, dan pemisahan SQL historis dari migration yang digunakan untuk pengelolaan database.

Dokumentasi ini menjadi baseline untuk pemeliharaan database berikutnya. Setiap pembaruan harus mencerminkan kondisi aktual database dan tidak boleh mengasumsikan bahwa seluruh SQL historis masih berlaku.

---

**Project:** Kaizen Company Platform  
**Database:** Supabase PostgreSQL  
**Audit Type:** Schema, Security, Storage, and SQL Review  
**Environment:** Production
