
# Row Level Security (RLS) Policies

Dokumen ini menjelaskan pengaturan keamanan akses database menggunakan PostgreSQL Row Level Security (RLS) pada Supabase.

## 1. Overview

Row Level Security digunakan untuk mengontrol akses terhadap baris data berdasarkan role dan kondisi tertentu.

RLS harus diterapkan sesuai kebutuhan akses masing-masing modul dan jenis pengguna.

## 2. Policy Documentation

Setiap policy harus didokumentasikan dengan informasi berikut:

| Attribute | Description |
|---|---|
| Table | Tabel yang dilindungi |
| Policy Name | Nama policy |
| Operation | SELECT, INSERT, UPDATE, atau DELETE |
| Target Role | Role yang mendapatkan akses |
| USING | Kondisi untuk mengakses baris |
| WITH CHECK | Kondisi validasi data baru |
| Purpose | Tujuan policy |
| Review Status | Status pemeriksaan keamanan |

## 3. Security Review Findings

Berdasarkan kumpulan query historis, terdapat beberapa pola policy yang perlu ditinjau ulang sebelum digunakan pada production.

### 3.1 Unrestricted Access

Beberapa query menggunakan kondisi:

```sql
USING (true)
WITH CHECK (true)
```

Kondisi tersebut dapat memberikan akses luas terhadap data, tergantung operasi dan role yang menjadi target policy.

**Required Review:**
- Pastikan policy memiliki target role yang sesuai.
- Hindari memberikan akses penuh tanpa kebutuhan yang jelas.
- Batasi akses berdasarkan kepemilikan data atau hak pengguna.
- Tinjau ulang policy untuk operasi SELECT, INSERT, UPDATE, dan DELETE secara terpisah.

### 3.2 User Profile and Role Assignment

Query historis perlu diperiksa terkait mekanisme pembuatan profil dan pemberian role pengguna.

**Required Review:**
- Pastikan pengguna baru tidak otomatis memperoleh hak administrator.
- Validasi sumber pemberian role.
- Pastikan perubahan role hanya dapat dilakukan oleh pihak yang berwenang.
- Periksa trigger dan function yang berkaitan dengan Supabase Auth.

### 3.3 Storage Policies

Bucket yang ditemukan dalam query historis antara lain:

| Bucket | Purpose | Review |
|---|---|---|
| `dad_photos` | Penyimpanan foto pendaftar | Perlu pemeriksaan akses |
| `dad_payments` | Penyimpanan bukti pembayaran | Perlu pemeriksaan akses |
| `news_images` | Penyimpanan gambar berita | Perlu pemeriksaan akses |

**Required Review:**
- Periksa apakah bucket harus public atau private.
- Batasi akses upload berdasarkan kebutuhan pengguna.
- Batasi update dan delete kepada pihak berwenang.
- Pastikan file bukti pembayaran tidak dapat diakses publik.
- Periksa batas ukuran dan MIME type file.
- Pastikan policy tidak memberikan akses lintas bucket.

### 3.4 Payment Evidence

Query historis menunjukkan perubahan konfigurasi bucket `dad_payments` dari private menjadi public.

Hal ini harus menjadi prioritas pemeriksaan karena bucket tersebut menyimpan bukti pembayaran.

**Security Recommendation:**

Gunakan bucket private untuk dokumen pembayaran. Berikan akses baca hanya kepada pihak yang berwenang melakukan verifikasi.

## 4. Policy Review Checklist

- [ ] Seluruh tabel sensitif telah mengaktifkan RLS.
- [ ] Tidak terdapat akses publik yang tidak diperlukan.
- [ ] Role `anon` dan `authenticated` telah dibedakan.
- [ ] Operasi SELECT memiliki pembatasan yang sesuai.
- [ ] Operasi INSERT memiliki validasi `WITH CHECK`.
- [ ] Operasi UPDATE memiliki pembatasan `USING` dan `WITH CHECK` yang sesuai.
- [ ] Operasi DELETE hanya diberikan kepada pihak berwenang.
- [ ] Storage bucket memiliki konfigurasi akses yang tepat.
- [ ] Bukti pembayaran tidak dapat diakses secara publik.
- [ ] Trigger dan function telah diperiksa.
- [ ] Tidak ada policy duplikat atau policy lama yang masih aktif tanpa alasan.

## 5. Policy Change History

| Date | Table / Bucket | Change | Review Status |
|---|---|---|---|
| To be documented | - | - | Pending |

## 6. Security Notes

Kumpulan SQL historis tidak boleh langsung dianggap sebagai konfigurasi keamanan final.

Setiap policy perlu ditinjau berdasarkan kebutuhan akses aplikasi, role pengguna, dan sensitivitas data sebelum diterapkan pada production.
