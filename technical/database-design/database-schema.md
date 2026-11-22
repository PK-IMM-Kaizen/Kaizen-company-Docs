# 🧱 Database Schema

Dokumen ini berisi inventarisasi tabel aplikasi pada schema `public` dalam database Kaizen Company Platform.

## 1. Schema Overview

Hasil pemeriksaan menunjukkan terdapat 12 tabel aplikasi dengan total 103 kolom.

| No. | Table | Deskripsi |
|---:|---|---|
| 1 | `profiles` | Profil dan role pengguna aplikasi |
| 2 | `organization_profile` | Informasi profil organisasi |
| 3 | `news` | Informasi berita dan publikasi |
| 4 | `aspirations` | Data aspirasi |
| 5 | `pengurus` | Data pengurus organisasi |
| 6 | `alumni` | Data alumni |
| 7 | `products` | Data produk organisasi |
| 8 | `dad_registrations` | Data pendaftaran DAD |
| 9 | `site_settings` | Pengaturan website |
| 10 | `system_logs` | Catatan aktivitas sistem |
| 11 | `divisions` | Data bidang atau divisi organisasi |
| 12 | `agendas` | Data agenda kegiatan |

> Deskripsi tabel merupakan pengelompokan berdasarkan nama dan konteks penggunaannya. Detail fungsi setiap kolom harus mengacu pada definisi tabel aktual.

## 2. Table Details

### 2.1 `profiles`

Menyimpan profil pengguna aplikasi yang terhubung dengan Supabase Auth.

Informasi struktur yang telah teridentifikasi:

| Column | Keterangan |
|---|---|
| `id` | UUID, primary key, sekaligus foreign key ke `auth.users.id` |
| `email` | Email pengguna |
| `full_name` | Nama lengkap |
| `superadmin` | Kolom teks dengan default `'admin'` |
| `role` | Role aplikasi dengan default `'admin'` |
| `is_active` | Status aktif, default `true` |

Kolom lainnya mengikuti hasil introspeksi database.

### 2.2 `organization_profile`

Menyimpan informasi profil organisasi yang digunakan pada website.

### 2.3 `news`

Menyimpan data berita atau publikasi organisasi.

Kolom yang telah teridentifikasi:

| Column | Keterangan |
|---|---|
| `slug` | Slug unik |
| `gallery` | Kolom galeri |
| `date` | Informasi tanggal |
| `publish_date` | Informasi tanggal publikasi |
| `author` | Penulis, default `'RPK IMM Kaizen'` |
| `news_type` | Jenis berita, default `'pwmu'` |
| `created_at` | Waktu pembuatan |
| `updated_at` | Waktu pembaruan |

Tipe data dan seluruh kolom lainnya mengikuti definisi aktual pada database.

### 2.4 `aspirations`

Menyimpan data aspirasi yang dikirimkan melalui aplikasi.

### 2.5 `pengurus`

Menyimpan data pengurus organisasi.

### 2.6 `alumni`

Menyimpan informasi alumni.

### 2.7 `products`

Menyimpan informasi produk organisasi.

### 2.8 `dad_registrations`

Menyimpan data pendaftaran kegiatan Darul Arqam Dasar (DAD).

Kolom yang telah teridentifikasi:

| Column | Keterangan |
|---|---|
| `bukti_pembayaran_path` | Path file bukti pembayaran pada Storage |

Tabel ini memuat data pendaftaran yang bersifat personal. Pengelolaan akses dan file terkait perlu memperhatikan kebijakan privasi.

### 2.9 `site_settings`

Menyimpan konfigurasi website.

### 2.10 `system_logs`

Menyimpan catatan aktivitas sistem.

### 2.11 `divisions`

Menyimpan data bidang atau divisi organisasi.

### 2.12 `agendas`

Menyimpan data agenda kegiatan organisasi.

## 3. Database Constraints

Hasil inventarisasi menemukan 60 constraints:

| Jenis Constraint | Jumlah |
|---|---:|
| Primary Key | 12 |
| Foreign Key | 1 |
| Unique | 1 |
| Check | 46 |
| **Total** | **60** |

Jumlah tersebut merupakan hasil query metadata. Nama, kolom, dan definisi masing-masing constraint perlu dilihat pada hasil inventarisasi constraints.

## 4. Indexes

Ditemukan 13 indexes pada database yang diperiksa.

Daftar nama dan definisi index perlu mengacu pada metadata index aktual. Tidak semua index otomatis merupakan index yang dibuat secara manual; beberapa dapat berkaitan dengan constraint.

## 5. Views

Pemeriksaan terhadap `pg_views` dan `pg_matviews` tidak menemukan application view maupun materialized view pada cakupan query yang dijalankan.

## 6. Maintenance Notes

- Perubahan skema harus dicatat sebagai migration.
- Hindari perubahan langsung pada tabel production tanpa pemeriksaan dampak.
- Constraint dan index perlu diperiksa sebelum mengubah struktur kolom.
- SQL historis tidak boleh dianggap sebagai representasi tunggal kondisi database terkini.

---

**Source:** Supabase database metadata inspection.
