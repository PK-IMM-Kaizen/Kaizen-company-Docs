# Product Requirement Document — Business Rules

> Website Resmi PK IMM Kaizen V1.0

---

# 1. Business Rules

Business Rules mendefinisikan aturan bisnis yang harus menjadi dasar perilaku sistem Website Resmi PK IMM Kaizen.

---

## 1.1 BR-001 — Single Super Admin

Sistem V1 hanya memiliki satu application role:

> **Super Admin**

### Rules

- Hanya Super Admin yang dapat mengakses Dashboard Admin.
- Super Admin bertanggung jawab terhadap pengelolaan konten website.
- Pengurus atau bidang lain tidak memiliki akses administratif langsung pada V1.
- Permintaan perubahan data dari pengurus dilakukan melalui Super Admin.

---

## 1.2 BR-002 — Anonymous Aspiration

Aspirasi mahasiswa harus dapat dikirim secara anonim.

### Rules

Form Aspirasi:

- Tidak membutuhkan login.
- Tidak meminta nama.
- Tidak meminta email.
- Tidak meminta nomor HP.
- Tidak menyediakan public tracking.
- Menyimpan isi aspirasi dan timestamp.

### Boundary

Sistem tidak boleh mengubah fitur aspirasi menjadi sistem identitas atau akun pengguna pada V1.

---

## 1.3 BR-003 — Public Aspiration Restriction

Aspirasi yang telah dikirim hanya dapat diakses melalui area administratif.

### Rules

- Aspirasi tidak ditampilkan kepada publik.
- Tidak tersedia halaman daftar aspirasi publik.
- Tidak tersedia fitur tracking aspirasi oleh pengirim.
- Super Admin dapat melihat aspirasi melalui Dashboard.

---

## 1.4 BR-004 — Content Visibility

Konten hanya dapat ditampilkan kepada publik apabila memenuhi status publikasi yang ditentukan.

### Rules

~~~text
Content
   ↓
Status Check
   ├── Published / Active → Tampil kepada publik
   └── Draft / Inactive → Tidak tampil kepada publik
~~~

### Applicable Content

Aturan ini berlaku terhadap:

- Kepengurusan
- Alumni
- Produk
- Berita
- Kajian
- Konten organisasi lainnya

---

## 1.5 BR-005 — Historical Data Preservation

Perubahan status suatu data tidak selalu berarti data harus dihapus.

### Example

Ketika seorang pengurus sudah tidak aktif:

~~~text
Pengurus Aktif
      ↓
Status = Inactive
      ↓
Tidak tampil di website publik
      ↓
Data tetap tersimpan
~~~

### Rules

- Data historis dapat dipertahankan.
- Status aktif/inaktif digunakan untuk mengatur visibility.
- Penghapusan data hanya dilakukan apabila memang diperlukan.

---

## 1.6 BR-006 — No Digital Payment

Kaizen Company pada V1 bukan sistem e-commerce penuh.

### Rules

Website tidak menyediakan:

- Shopping Cart
- Checkout
- Payment Gateway
- Sistem pembayaran internal
- Order management kompleks

### Transaction Flow

~~~text
User
  ↓
Melihat Produk
  ↓
Klik "Beli" / "Hubungi Penjual"
  ↓
WhatsApp
  ↓
Transaksi dilakukan di luar website
~~~

---

## 1.7 BR-007 — Kaizen Company as Ekowir Program

Kaizen Company merupakan bagian dari program Ekowir.

### Rules

- Kaizen Company berfungsi sebagai etalase produk dan jasa.
- Produk/jasa dikelola melalui Super Admin.
- Produk dengan status aktif dapat ditampilkan kepada publik.
- Komunikasi transaksi diarahkan ke WhatsApp.

---

# 2. Content Lifecycle Rules

Konten yang dikelola melalui Dashboard mengikuti lifecycle:

~~~text
Draft
  ↓
Publish
  ↓
Unpublish
  ↓
Delete
~~~

---

## 2.1 Draft

Konten yang masih dalam proses pengelolaan.

### Rules

- Tidak ditampilkan kepada publik.
- Dapat diperbarui oleh Super Admin.
- Dapat dipublikasikan setelah data dianggap siap.

---

## 2.2 Publish

Konten yang telah dinyatakan siap ditampilkan.

### Rules

- Dapat ditampilkan kepada publik.
- Data harus memenuhi validasi yang diperlukan.

---

## 2.3 Unpublish

Konten yang sebelumnya telah dipublikasikan kemudian dinonaktifkan.

### Rules

- Tidak ditampilkan kepada publik.
- Data tetap dapat dipertahankan.
- Dapat dipublikasikan kembali apabila diperlukan.

---

## 2.4 Delete

Konten dihapus dari sistem.

### Rules

- Delete merupakan tindakan destruktif.
- Sistem harus meminta confirmation sebelum penghapusan.
- Data yang dihapus tidak boleh dianggap sebagai sekadar perubahan visibility.

---

# 3. Business Rules by Module

## 3.1 Kepengurusan

- Pengurus aktif ditampilkan kepada publik.
- Pengurus tidak aktif disembunyikan dari tampilan publik.
- Data pengurus tidak harus dihapus ketika masa kepengurusan berakhir.
- Super Admin menjadi pihak yang mengubah status data.

---

## 3.2 Alumni

- Alumni dapat memiliki status aktif/inaktif sesuai kebutuhan pengelolaan konten.
- Data yang tidak aktif tidak ditampilkan kepada publik.
- Data dapat dipertahankan sebagai bagian dari historical data.

---

## 3.3 Kaizen Company

- Hanya produk aktif yang ditampilkan.
- Stok bersifat display only.
- Website tidak menangani pembayaran.
- Website tidak menangani checkout.
- CTA pembelian mengarahkan pengguna ke WhatsApp.

---

## 3.4 Berita

- Berita berfungsi sebagai direktori.
- Website tidak menduplikasi artikel PWMU secara penuh.
- Artikel lengkap tetap berada di PWMU.
- Link PWMU dibuka pada tab baru.
- Setiap berita harus memiliki URL sumber.

---

## 3.5 Kajian

- Kajian merupakan native content website.
- Konten Kajian dapat memiliki halaman detail.
- Kajian berbeda dari Berita.
- Berita mengarahkan pengguna ke PWMU.
- Kajian dibaca langsung pada website.

### Open Decision

Hal berikut masih memerlukan keputusan:

- Model atribusi penulis.
- Workflow approval Kajian.
- Prioritas Kajian terhadap V1.

---

## 3.6 Aspirasi

- Aspirasi dapat dikirim tanpa login.
- Identitas tidak diminta melalui form.
- Isi aspirasi dan timestamp disimpan.
- Aspirasi hanya dapat dilihat melalui Dashboard.
- Tidak ada public tracking.
- Sistem harus memiliki perlindungan terhadap spam.

---

# 4. Access Rules

## 4.1 Public User

Publik dapat:

- Melihat konten yang dipublikasikan.
- Mengakses Kaizen Company.
- Melihat produk aktif.
- Mengakses detail produk.
- Menggunakan CTA WhatsApp.
- Membaca berita.
- Membaca Kajian.
- Mengirim Aspirasi.

Publik tidak dapat:

- Mengakses Dashboard.
- Mengelola konten.
- Melihat aspirasi pengguna lain.
- Mengakses data administratif.

---

## 4.2 Super Admin

Super Admin dapat:

- Login ke Dashboard.
- Mengelola konten.
- Melakukan CRUD.
- Mengunggah gambar.
- Mengubah status konten.
- Melihat aspirasi.
- Mengelola produk Kaizen Company.
- Mengelola informasi organisasi.

---

# 5. Authentication Rules

### Rules

- V1 hanya menyediakan authentication untuk Super Admin.
- Public user tidak membutuhkan authentication.
- Dashboard harus dilindungi dari akses tanpa authentication.
- Metode authentication masih merupakan open decision.
- Dashboard tidak boleh diindeks oleh search engine.

---

# 6. Media Rules

## 6.1 Image Format

Format utama gambar:

> **WebP**

### Rules

- Upload gambar harus divalidasi.
- Ukuran file harus divalidasi.
- Gambar publik harus memiliki alt text.
- Optimasi gambar harus diterapkan untuk mendukung performa.

---

## 6.2 Video

Website V1 tidak menyediakan local video hosting.

Jika diperlukan, video harus menggunakan layanan eksternal.

---

# 7. Data Management Rules

## 7.1 Backup

Database harus memiliki mekanisme backup secara berkala.

## 7.2 Aspirasi Export

Data Aspirasi dapat diekspor dalam format CSV.

### Purpose

- Backup tambahan.
- Dokumentasi.
- Pengolahan data oleh pengurus.

---

# 8. Security Rules

Sistem harus mempertimbangkan perlindungan terhadap:

- XSS
- CSRF
- SQL Injection
- NoSQL Injection
- Spam pada Aspirasi
- Unauthorized access pada Dashboard

### Aspiration Protection

Form Aspirasi harus memiliki mekanisme untuk mengurangi spam atau abuse.

Mekanisme spesifik masih dapat ditentukan pada tahap technical specification.

---

# 9. Business Rule Summary

| ID | Business Rule | Priority |
|---|---|---|
| BR-001 | Single Super Admin | Must Have |
| BR-002 | Anonymous Aspiration | Must Have |
| BR-003 | Public Aspiration Restriction | Must Have |
| BR-004 | Content Visibility | Must Have |
| BR-005 | Historical Data Preservation | Must Have |
| BR-006 | No Digital Payment | Must Have |
| BR-007 | Kaizen Company as Ekowir Program | Must Have |

---

# 10. Open Business Decisions

Beberapa keputusan bisnis/produk belum ditetapkan secara final.

| Decision | Status |
|---|---|
| Metode authentication Super Admin | TBD |
| Prioritas Kajian pada V1 | TBD |
| Model atribusi penulis Kajian | TBD |
| Workflow approval Kajian | TBD |
| Integrasi PWMU | TBD |
| Mekanisme proteksi spam Aspirasi | TBD |

Keputusan yang belum final harus ditetapkan sebelum requirement tersebut dianggap final untuk tahap technical specification.

---

# Navigation

- [← Product Requirement Document — Functional Requirements](./04-prd-functional-requirements.md)
- [Product Requirement Document — Module Requirements →](./06-prd-module-requirements.md)
