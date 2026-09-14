# Product Requirement Document — Functional Requirements

> Website Resmi PK IMM Kaizen V1.0

---

# 1. Functional Requirements

Functional Requirements mendefinisikan perilaku dan kemampuan utama yang harus tersedia pada Website Resmi PK IMM Kaizen V1.

---

## 1.1 FR-001 — Main Navigation

### Description

Website harus menyediakan navigasi utama yang memungkinkan pengguna mengakses halaman informasi organisasi.

### Navigation Items

- Beranda
- Profil
- Kepengurusan
- Bidang
- Berita
- Ekowir
- Alumni
- Kontak

### Rules

- Navigasi tersedia pada website publik.
- Navigasi harus konsisten pada halaman publik.
- Kajian diakses melalui section pada Beranda.
- Aspirasi diakses melalui bagian FAQ pada Beranda.
- Kaizen Company diakses melalui CTA khusus dan bukan melalui navbar utama.

---

## 1.2 FR-002 — Kaizen Company CTA

### Description

Website harus menyediakan CTA khusus untuk mengakses Kaizen Company.

### Behavior

~~~text
User
  ↓
Klik CTA Kaizen Company
  ↓
Halaman Kaizen Company
~~~

### Rules

- Kaizen Company tidak menjadi item utama pada navbar.
- Halaman Kaizen Company menggunakan Dark Theme.
- Hanya produk dengan status Aktif yang ditampilkan.

---

## 1.3 FR-003 — Product Catalog

### Description

Sistem harus menampilkan katalog produk dan jasa Kaizen Company.

### Product Information

Setiap produk dapat memiliki:

- Nama produk
- Foto
- Harga
- Deskripsi
- Kategori
- Stok
- Status

### Rules

- Produk aktif dapat dilihat publik.
- Produk tidak aktif tidak ditampilkan kepada publik.
- Stok bersifat display only.
- Sistem tidak menangani transaksi secara langsung.

---

## 1.4 FR-004 — Product Detail

### Description

Pengguna harus dapat melihat informasi detail produk atau jasa.

### Behavior

~~~text
Kaizen Company
      ↓
Pilih Produk
      ↓
Detail Produk
      ↓
Informasi Produk
      ↓
CTA WhatsApp
~~~

### Expected Output

Halaman menampilkan informasi produk dan CTA untuk menghubungi penjual.

---

## 1.5 FR-005 — WhatsApp Redirect

### Description

Sistem harus mengarahkan pengguna ke WhatsApp ketika pengguna memilih CTA pembelian atau kontak penjual.

### Behavior

~~~text
User
  ↓
Klik "Beli" / "Hubungi Penjual"
  ↓
Generate WhatsApp URL
  ↓
WhatsApp
~~~

### Rules

- Sistem tidak memproses pembayaran.
- Sistem tidak menyediakan checkout.
- Pesan WhatsApp dapat menggunakan format pre-filled message.
- Tujuan akhir adalah komunikasi langsung dengan penjual.

---

## 1.6 FR-006 — Anonymous Aspiration Access

### Description

Sistem harus menyediakan akses ke form Aspirasi Mahasiswa tanpa membutuhkan authentication.

### Access Path

~~~text
Beranda
  ↓
FAQ
  ↓
Link Aspirasi
  ↓
Form Aspirasi
~~~

### Rules

- Tidak membutuhkan login.
- Tidak membutuhkan account.
- Tidak meminta nama.
- Tidak meminta email.
- Tidak meminta nomor HP.

---

## 1.7 FR-007 — Anonymous Aspiration Submission

### Description

Sistem harus memungkinkan pengguna mengirim aspirasi dalam bentuk teks.

### Input

- Teks aspirasi

### Stored Data

- Teks aspirasi
- Timestamp

### Behavior

~~~text
User
  ↓
Mengisi Aspirasi
  ↓
Submit
  ↓
Validasi
  ↓
Simpan
  ↓
Success Feedback
~~~

### Rules

- Aspirasi disimpan ke database.
- Pengguna menerima feedback setelah submit berhasil.
- Tidak tersedia public tracking.
- Sistem harus memiliki mekanisme perlindungan terhadap spam.

---

## 1.8 FR-008 — Public Content Display

### Description

Website harus menampilkan informasi organisasi yang telah dipublikasikan.

### Content

- Profil
- Kepengurusan
- Bidang
- Berita
- Ekowir
- Alumni
- Kontak
- Kajian

### Rules

- Hanya konten yang berstatus publik/aktif yang ditampilkan.
- Data yang dinonaktifkan tidak ditampilkan kepada publik.
- Data historis dapat tetap dipertahankan di sistem.

---

## 1.9 FR-009 — Kepengurusan Management

### Description

Sistem harus menyediakan informasi struktur kepengurusan organisasi.

### Data

- Nama
- Foto
- Jabatan
- Bidang
- Status

### Rules

- Pengurus aktif ditampilkan kepada publik.
- Pengurus yang dinonaktifkan tidak ditampilkan kepada publik.
- Data tidak harus dihapus ketika status berubah menjadi tidak aktif.
- Data historis tetap dapat dipertahankan.

---

## 1.10 FR-010 — Bidang Management

### Description

Sistem harus menampilkan informasi bidang dalam struktur organisasi.

### Expected Content

- Nama bidang
- Informasi/deskripsi bidang
- Informasi terkait kepengurusan bidang

### Rules

- Informasi yang dipublikasikan harus berasal dari data organisasi.
- Konten dapat dikelola oleh Super Admin.

---

## 1.11 FR-011 — Berita Directory

### Description

Sistem harus menyediakan direktori berita organisasi.

### News Card

Setiap card berita dapat menampilkan:

- Thumbnail
- Judul
- Deskripsi singkat
- Link artikel PWMU

### Rules

- Website tidak menduplikasi artikel PWMU secara penuh.
- Artikel lengkap tetap berada pada PWMU.
- Link PWMU dibuka pada tab baru.
- Berita yang tersedia harus memiliki URL sumber.

---

## 1.12 FR-012 — Berita Search

### Description

Sistem harus menyediakan pencarian sederhana pada daftar berita.

### Behavior

~~~text
User
  ↓
Memasukkan keyword
  ↓
Sistem melakukan filtering
  ↓
Menampilkan berita yang relevan
~~~

### Scope

Pencarian V1 bersifat sederhana dan hanya ditujukan untuk membantu pengguna menemukan berita yang tersedia.

---

## 1.13 FR-013 — Kajian Section

### Description

Beranda harus menyediakan section khusus untuk konten Kajian.

### Content

Section dapat menampilkan:

- Judul kajian
- Ringkasan
- Thumbnail
- CTA menuju detail

### Behavior

~~~text
Beranda
  ↓
Section Kajian
  ↓
Pilih Kajian
  ↓
Halaman Detail
~~~

---

## 1.14 FR-014 — Kajian Detail

### Description

Sistem harus menyediakan halaman detail untuk artikel Kajian.

### Data

Artikel Kajian dapat memiliki:

- Judul
- Slug
- Konten
- Thumbnail
- Informasi penulis/author apabila model atribusi telah ditetapkan

### Rules

- Kajian merupakan native content website.
- Kajian berbeda dengan Berita.
- Berita mengarahkan pengguna ke PWMU.
- Kajian dibaca langsung pada website.

### Open Decision

Model atribusi penulis dan workflow approval masih merupakan keputusan yang perlu ditetapkan.

---

## 1.15 FR-015 — Super Admin Authentication

### Description

Sistem harus menyediakan authentication khusus untuk Super Admin.

### Access

Hanya pengguna dengan hak akses Super Admin yang dapat mengakses dashboard.

### Behavior

~~~text
User
  ↓
Admin Login
  ↓
Authentication
  ↓
Valid
  ├── Yes → Dashboard
  └── No  → Error
~~~

### Rules

- V1 hanya memiliki satu application role.
- Public user tidak memiliki account.
- Metode authentication masih merupakan open decision.
- Halaman dashboard tidak ditujukan untuk akses publik.

---

## 1.16 FR-016 — Admin Dashboard

### Description

Sistem harus menyediakan dashboard terpusat untuk pengelolaan website.

### Dashboard Modules

- Profil
- Kepengurusan
- Bidang
- Berita
- Kajian
- Ekowir
- Kaizen Company
- Alumni
- Aspirasi

### Rules

- Dashboard hanya dapat diakses oleh Super Admin.
- Data yang dikelola melalui dashboard harus tercermin pada website publik sesuai status publikasinya.

---

## 1.17 FR-017 — Content CRUD

### Description

Super Admin harus dapat melakukan operasi CRUD terhadap konten yang dikelola sistem.

### Operations

- Create
- Read
- Update
- Delete

### Applicable Content

- Profil
- Kepengurusan
- Bidang
- Berita
- Kajian
- Ekowir
- Kaizen Company
- Alumni

### Rules

- Data harus divalidasi sebelum disimpan.
- Tindakan destruktif harus memiliki confirmation.
- Perubahan data harus menghasilkan feedback keberhasilan atau kegagalan.

---

## 1.18 FR-018 — Content Status Management

### Description

Super Admin harus dapat mengatur status konten.

### Status

~~~text
Draft
  ↓
Publish
  ↓
Unpublish
  ↓
Delete
~~~

### Rules

- Konten yang belum dipublikasikan tidak ditampilkan kepada publik.
- Konten yang di-unpublish tidak ditampilkan kepada publik.
- Delete merupakan tindakan destruktif dan harus membutuhkan konfirmasi.

---

## 1.19 FR-019 — Image Upload

### Description

Sistem harus mendukung upload gambar untuk konten yang membutuhkan media.

### Rules

- Format gambar yang digunakan adalah WebP.
- Sistem harus melakukan validasi terhadap file.
- Sistem harus melakukan validasi ukuran file.
- Gambar harus memiliki alt text jika digunakan pada konten publik.

### Applicable Content

- Profil
- Kepengurusan
- Bidang
- Berita
- Kajian
- Ekowir
- Kaizen Company
- Alumni

---

## 1.20 FR-020 — Aspiration Management

### Description

Super Admin harus dapat melihat aspirasi yang masuk melalui dashboard.

### Data Display

- Isi aspirasi
- Timestamp

### Rules

- Identitas pengguna tidak disimpan melalui field identitas pada form.
- Aspirasi hanya dapat diakses melalui dashboard.
- Aspirasi tidak memiliki public tracking.

---

## 1.21 FR-021 — Content Validation

### Description

Sistem harus melakukan validasi terhadap input sebelum data disimpan.

### Validation Areas

- Required fields
- Text input
- URL
- Image file
- Image size
- Status
- Product data
- Content data

### Expected Behavior

Jika validasi gagal:

~~~text
Input
  ↓
Validation
  ↓
Invalid
  ↓
Validation Error
  ↓
User memperbaiki input
~~~

Jika validasi berhasil:

~~~text
Input
  ↓
Validation
  ↓
Valid
  ↓
Save
  ↓
Success Feedback
~~~

---

## 1.22 FR-022 — Error & Success Feedback

### Description

Sistem harus memberikan feedback terhadap tindakan pengguna.

### Success State

Contoh:

- Data berhasil disimpan.
- Data berhasil diperbarui.
- Data berhasil dihapus.
- Aspirasi berhasil dikirim.

### Error State

Contoh:

- Input tidak valid.
- Upload gagal.
- Authentication gagal.
- Data gagal disimpan.
- Terjadi kesalahan sistem.

---

## 1.23 FR-023 — Destructive Action Confirmation

### Description

Tindakan yang dapat menghapus data atau menyebabkan perubahan signifikan harus memiliki confirmation.

### Example

~~~text
Super Admin
    ↓
Klik Delete
    ↓
Confirmation Dialog
    ↓
Konfirmasi
    ↓
Data dihapus
~~~

### Rules

- Delete tidak boleh dilakukan hanya melalui satu accidental click.
- Sistem harus memberikan kesempatan kepada Super Admin untuk membatalkan tindakan.

---

## 1.24 FR-024 — Admin Access Protection

### Description

Halaman dan endpoint administratif harus dilindungi dari akses publik.

### Rules

- Pengguna yang belum terautentikasi tidak dapat mengakses dashboard.
- Pengguna publik harus diarahkan keluar dari area admin.
- Dashboard tidak boleh diindeks oleh search engine.
- Authentication dan authorization harus diterapkan pada area administratif.

---

## 1.25 FR-025 — Content Visibility

### Description

Sistem harus mengontrol apakah sebuah konten dapat dilihat publik.

### Visibility Rules

~~~text
Content
   ↓
Check Status
   ├── Active / Published → Public
   └── Inactive / Draft → Hidden
~~~

### Applicable Content

- Kepengurusan
- Alumni
- Produk
- Berita
- Kajian
- Konten organisasi lainnya

---

# 2. Functional Requirement Summary

| ID | Requirement | Priority |
|---|---|---|
| FR-001 | Main Navigation | Must Have |
| FR-002 | Kaizen Company CTA | Must Have |
| FR-003 | Product Catalog | Must Have |
| FR-004 | Product Detail | Must Have |
| FR-005 | WhatsApp Redirect | Must Have |
| FR-006 | Anonymous Aspiration Access | Must Have |
| FR-007 | Anonymous Aspiration Submission | Must Have |
| FR-008 | Public Content Display | Must Have |
| FR-009 | Kepengurusan Management | Must Have |
| FR-010 | Bidang Management | Must Have |
| FR-011 | Berita Directory | Must Have |
| FR-012 | Berita Search | Must Have |
| FR-013 | Kajian Section | TBD / Open Decision |
| FR-014 | Kajian Detail | TBD / Open Decision |
| FR-015 | Super Admin Authentication | Must Have |
| FR-016 | Admin Dashboard | Must Have |
| FR-017 | Content CRUD | Must Have |
| FR-018 | Content Status Management | Must Have |
| FR-019 | Image Upload | Must Have |
| FR-020 | Aspiration Management | Must Have |
| FR-021 | Content Validation | Must Have |
| FR-022 | Error & Success Feedback | Must Have |
| FR-023 | Destructive Action Confirmation | Must Have |
| FR-024 | Admin Access Protection | Must Have |
| FR-025 | Content Visibility | Must Have |

---

# 3. Functional Scope Principles

Functional requirements V1 mengikuti prinsip:

1. **Public information first**  
   Fokus utama adalah menyediakan informasi resmi organisasi.

2. **Centralized content management**  
   Pengelolaan konten dilakukan melalui Super Admin.

3. **No unnecessary transaction system**  
   Kaizen Company hanya berfungsi sebagai katalog dan penghubung ke WhatsApp.

4. **Anonymous aspiration**  
   Aspirasi tidak membutuhkan identitas pengguna.

5. **Native Kajian, external Berita**  
   Kajian dipublikasikan pada website, sedangkan Berita mengarahkan pengguna ke PWMU.

6. **Status-based visibility**  
   Konten hanya ditampilkan ketika memenuhi status publikasi yang ditentukan.

7. **V1 simplicity**  
   Sistem tidak memasukkan fitur kompleks yang belum menjadi kebutuhan V1.

---

# Navigation

- [← Product Requirement Document — Users & Journeys](./03-prd-users-and-journeys.md)
- [Product Requirement Document — Business Rules →](./05-prd-business-rules.md)
