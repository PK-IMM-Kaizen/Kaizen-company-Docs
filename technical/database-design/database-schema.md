
# Database Schema

Dokumen ini menjelaskan struktur database Kaizen Company, termasuk tabel, kolom, tipe data, relasi, dan fungsi setiap entitas.

## 1. Database Overview

Database menggunakan PostgreSQL melalui Supabase.

Struktur database dikembangkan untuk mendukung kebutuhan aplikasi Kaizen Company, termasuk pengelolaan pengguna, berita, kegiatan, pendaftaran, pembayaran, divisi, dan aktivitas sistem.

## 2. Table Documentation

Daftar berikut merupakan inventaris awal tabel yang ditemukan dalam kumpulan query historis. Detail kolom dan relasi perlu diverifikasi terhadap schema database Supabase yang sedang aktif.

| Table | Description | Verification |
|---|---|---|
| `news` | Menyimpan informasi berita dan publikasi | Perlu verifikasi |
| `system_logs` | Menyimpan catatan aktivitas sistem | Perlu verifikasi |
| `divisions` | Menyimpan informasi bidang atau divisi organisasi | Perlu verifikasi |
| `dad_registrations` | Menyimpan data pendaftaran DAD | Perlu verifikasi |
| `agendas` | Menyimpan informasi agenda atau kegiatan | Perlu verifikasi |
| `profiles` | Menyimpan informasi profil pengguna | Perlu verifikasi |

> Catatan: Daftar ini bukan representasi final seluruh tabel database. Struktur aktual harus diperiksa melalui Supabase sebelum dokumentasi dianggap final.

## 3. Schema Details

Detail setiap tabel akan didokumentasikan menggunakan format berikut.

### 3.1 Table: `news`

**Purpose:** Menyimpan informasi berita dan publikasi.

| Column | Data Type | Description |
|---|---|---|
| `id` | UUID | Primary key |
| `title` | TEXT | Judul berita |
| `slug` | TEXT | Identitas URL berita |
| `category` | TEXT | Kategori berita |
| `content` | TEXT | Isi berita |
| `thumbnail` | TEXT | Referensi gambar thumbnail |
| `status` | TEXT | Status publikasi |
| `publish_date` | TIMESTAMPTZ | Waktu publikasi |
| `author` | TEXT | Penulis berita |
| `news_type` | TEXT | Jenis berita |
| `created_at` | TIMESTAMPTZ | Waktu pembuatan |

**Verification Notes:**
- Pastikan seluruh kolom telah tersedia pada schema aktif.
- Periksa apakah `slug` memiliki constraint UNIQUE.
- Periksa konsistensi definisi tabel dari query historis.
- Pastikan kolom `author` dan `news_type` telah diterapkan.

### 3.2 Table: `system_logs`

**Purpose:** Menyimpan catatan aktivitas sistem.

Kolom yang ditemukan dalam query historis meliputi:

- `id`
- `admin_name`
- `action`
- `target`
- `type`
- `user_email`
- `module`
- `details`
- `created_at`

Detail tipe data, constraint, dan nullable setiap kolom perlu diverifikasi terhadap schema aktif.

### 3.3 Table: `divisions`

**Purpose:** Menyimpan informasi bidang atau divisi organisasi.

Kolom yang ditemukan dalam query historis meliputi:

- `id`
- `name`
- `description`
- `color`
- `photo`
- `created_at`

### 3.4 Table: `dad_registrations`

**Purpose:** Menyimpan informasi pendaftaran Darul Arqam Dasar (DAD).

Query historis menunjukkan adanya perubahan pada informasi pendaftar, termasuk:

- `nim`
- `nomor_hp`
- `alamat_sekarang`
- `foto_url`
- `bukti_pembayaran_path`
- `status_pembayaran`

Detail struktur lengkap perlu diverifikasi terhadap schema aktif.

## 4. Relationships

Relasi antartabel belum ditetapkan dalam dokumentasi ini karena perlu diverifikasi dari foreign key dan struktur database aktual.

Format dokumentasi relasi:

| Source Table | Column | Referenced Table | Referenced Column | Relationship |
|---|---|---|---|---|
| To be verified | - | To be verified | - | To be verified |

## 5. Constraints and Indexes

Constraint dan index harus didokumentasikan berdasarkan struktur database aktual.

Hal-hal yang perlu diperiksa:
- Primary key
- Foreign key
- Unique constraint
- Not null constraint
- Default value
- Check constraint
- Index

## 6. Schema Change History

Setiap perubahan struktur database harus dicatat dan memiliki referensi ke file migration terkait.

| Date | Change | Migration File | Status |
|---|---|---|---|
| To be documented | Initial schema review | - | Pending |

## 7. Verification Status

Dokumen ini masih merupakan inventaris awal berdasarkan query pengembangan.

Status final baru dapat ditetapkan setelah dilakukan pemeriksaan terhadap:
1. Schema aktif Supabase.
2. Seluruh tabel dan kolom.
3. Foreign key dan constraint.
4. Index.
5. Trigger dan function.
6. RLS policies.
