# Product Discovery — Scope

> Website Resmi PK IMM Kaizen V1.0

---

## 1. Product Scope

Website Resmi PK IMM Kaizen V1.0 berfokus pada tiga fungsi utama:

1. **Official Organization Profile**
   Menjadi pusat informasi publik resmi PK IMM Kaizen.

2. **Kaizen Company Showcase**
   Menjadi etalase produk/jasa Kaizen Company tanpa transaksi langsung di website.

3. **Anonymous Aspiration Channel**
   Menyediakan wadah aspirasi anonim yang terhubung ke Super Admin Dashboard.

Website tidak mencakup:

* Forum komunitas.
* Komentar publik.
* Public user account.
* Shopping cart.
* Payment gateway.
* Transaksi langsung di dalam website.

Website berfungsi sebagai **pusat informasi, etalase bisnis, dan saluran umpan balik**, bukan sebagai platform komunitas atau e-commerce kompleks.

---

# 2. Information Architecture & Navigation

Struktur navigasi publik mengikuti struktur berikut:

```text
PK IMM Kaizen
└── Website Resmi PK IMM Kaizen
    │
    ├── Beranda
    │   └── FAQ
    │       └── Link Aspirasi
    │
    ├── Profil
    │
    ├── Kepengurusan
    │
    ├── Bidang
    │
    ├── Berita
    │
    ├── Ekowir
    │
    ├── Alumni
    │
    ├── Kontak
    │
    └── Kaizen Company
        └── Akses melalui CTA khusus
            (bukan navbar utama)
```

### Navigation Rules

| Navigation     | Scope                                       | Public Access |
| -------------- | ------------------------------------------- | ------------- |
| Beranda        | Landing page dan informasi utama organisasi | View          |
| FAQ            | Frequently Asked Questions                  | View          |
| Aspirasi       | Form aspirasi anonim yang diakses dari FAQ  | Submit        |
| Profil         | Informasi resmi organisasi                  | View          |
| Kepengurusan   | Struktur dan profil pengurus                | View          |
| Bidang         | Informasi bidang dalam organisasi           | View          |
| Berita         | Direktori berita/kegiatan                   | View          |
| Ekowir         | Informasi bidang ekonomi dan kewirausahaan  | View          |
| Alumni         | Showcase alumni berprestasi                 | View          |
| Kontak         | Informasi kontak organisasi                 | View          |
| Kaizen Company | Katalog produk/jasa                         | View          |

> **Catatan:** Kaizen Company memiliki visual direction **Dark Theme**, sedangkan area website organisasi menggunakan **Light Theme**.

---

# 3. Public Website Features

## 3.1 Beranda

### Purpose

Menjadi entry point utama website dan memberikan gambaran singkat mengenai PK IMM Kaizen.

### Scope

Beranda menjadi pusat navigasi menuju:

* Profil
* Kepengurusan
* Bidang
* Berita
* Ekowir
* Alumni
* Kontak
* Kaizen Company
* FAQ
* Link Aspirasi

### FAQ & Aspirasi

FAQ berada dalam area Beranda dan menyediakan akses menuju **Link Aspirasi**.

Flow:

```text
Beranda
   ↓
FAQ
   ↓
Link Aspirasi
   ↓
Form Aspirasi
```

---

## 3.2 Profil

### Purpose

Menyediakan informasi resmi mengenai identitas dan profil PK IMM Kaizen.

### Scope

* Informasi organisasi.
* Konten profil yang dapat dikelola melalui Admin Dashboard.

### Access

| Actor       | Access |
| ----------- | ------ |
| Publik      | View   |
| Super Admin | Manage |

---

## 3.3 Kepengurusan

### Purpose

Menampilkan struktur dan informasi kepengurusan PK IMM Kaizen.

### Scope

* Daftar pengurus.
* Informasi/profil pengurus.
* Status pengurus Aktif/Inaktif.

### Business Rule

Pengurus dengan status **Aktif** ditampilkan pada website publik.

Pengurus dengan status **Inaktif** tidak ditampilkan pada tampilan publik, tetapi datanya tetap tersimpan.

### Access

| Actor       | Access        |
| ----------- | ------------- |
| Publik      | View          |
| Super Admin | CRUD / Status |

---

## 3.4 Bidang

### Purpose

Menampilkan informasi mengenai bidang-bidang yang terdapat dalam struktur PK IMM Kaizen.

### Scope

* Nama bidang.
* Informasi/deskripsi bidang.
* Konten bidang yang dikelola melalui Admin Dashboard.

### Access

| Actor       | Access |
| ----------- | ------ |
| Publik      | View   |
| Super Admin | Manage |

---

## 3.5 Berita

### Purpose

Menjadi direktori rekam jejak kegiatan organisasi.

### Scope

Website menampilkan daftar berita dalam bentuk card yang berisi:

* Thumbnail.
* Judul.
* Deskripsi singkat.
* Link artikel.

Website **tidak menduplikasi konten artikel secara penuh**.

Artikel lengkap tetap berada di PWMU.

### Functional Requirements

* Daftar berita.
* Search sederhana khusus halaman Berita.
* Link ke artikel PWMU.
* Link dibuka pada tab baru.
* Status konten dapat dikelola oleh Super Admin.

### User Flow

```text
Berita
   ↓
Pilih berita
   ↓
Lihat thumbnail + judul + deskripsi
   ↓
Klik "Lihat selengkapnya di PWMU"
   ↓
Artikel PWMU terbuka di tab baru
```

### Access

| Actor       | Access        |
| ----------- | ------------- |
| Publik      | View          |
| Super Admin | CRUD / Manage |

---

## 3.6 Ekowir

### Purpose

Menampilkan informasi mengenai bidang ekonomi dan kewirausahaan organisasi.

### Scope

Ekowir menjadi area yang menaungi konteks bisnis **Kaizen Company**.

Informasi Ekowir dapat dikelola oleh Super Admin melalui Dashboard.

### Access

| Actor       | Access |
| ----------- | ------ |
| Publik      | View   |
| Super Admin | Manage |

---

# 4. Kaizen Company

## 4.1 Kaizen Company Catalog

### Purpose

Menjadi etalase produk dan jasa yang dijual oleh Ekowir untuk mendukung kemandirian ekonomi organisasi.

### Navigation

Kaizen Company **bukan bagian dari navbar utama**.

Akses diberikan melalui CTA khusus pada website.

```text
Website Utama
     ↓
CTA Kaizen Company
     ↓
Kaizen Company Catalog
```

### Visual Direction

Kaizen Company menggunakan:

> **Dark Theme**

### Scope

Katalog menampilkan:

* Produk/jasa.
* Foto.
* Nama.
* Harga.
* Deskripsi.
* Kategori.
* Stok display.
* Status.

### Functional Requirements

* Menampilkan grid produk.
* Menampilkan detail produk.
* Hanya produk berstatus **Aktif** yang tampil kepada publik.
* Tombol **Beli / Hubungi Penjual** mengarahkan pengguna ke WhatsApp.
* Pesan WhatsApp dapat menggunakan format *pre-filled*.

### Tidak Termasuk

* Shopping Cart.
* Checkout.
* Payment Gateway.
* Transaksi langsung di website.
* Inventory tracking dinamis pada V1.

### User Flow

```text
CTA Kaizen Company
        ↓
Daftar produk
        ↓
Pilih produk
        ↓
Detail produk
        ↓
Beli / Hubungi Penjual
        ↓
WhatsApp
```

### Access

| Actor       | Access |
| ----------- | ------ |
| Publik      | View   |
| Super Admin | CRUD   |

---

# 5. Alumni

## Purpose

Menampilkan showcase alumni PK IMM Kaizen yang memiliki prestasi atau relevansi untuk ditampilkan kepada publik.

### Scope

* Profil alumni pilihan.
* Informasi singkat alumni.
* Status publikasi.

### Business Rule

Alumni dapat memiliki status:

* Aktif ditampilkan.
* Inaktif tidak ditampilkan.

### Access

| Actor       | Access        |
| ----------- | ------------- |
| Publik      | View          |
| Super Admin | CRUD / Status |

> **Catatan:** Direktori alumni lengkap bukan bagian dari V1.

---

# 6. Kontak

## Purpose

Menyediakan informasi kontak resmi PK IMM Kaizen.

### Scope

* Informasi kontak organisasi.
* Informasi yang diperlukan publik untuk menghubungi organisasi.

### Access

| Actor       | Access |
| ----------- | ------ |
| Publik      | View   |
| Super Admin | Manage |

---

# 7. Aspirasi Mahasiswa

## 7.1 Purpose

Menyediakan wadah masukan anonim sebagai bahan evaluasi organisasi.

## 7.2 Entry Point

Aspirasi tidak menjadi item utama navbar.

Akses dilakukan melalui:

```text
Beranda
   ↓
FAQ
   ↓
Link Aspirasi
   ↓
Form Aspirasi
```

## 7.3 Target User

* Personalia.
* Kader.
* Masyarakat umum.

## 7.4 Functional Requirements

* Form text-area.
* Tidak membutuhkan login.
* Tidak meminta nama.
* Tidak meminta email.
* Tidak meminta nomor HP.
* Data masuk ke Admin Dashboard.
* Timestamp disimpan.
* Tidak tersedia public tracking.

## 7.5 Input

```text
Teks Aspirasi
```

## 7.6 Output

```text
Pesan sukses submit
```

## 7.7 Access

| Actor       | Access |
| ----------- | ------ |
| Publik      | Submit |
| Super Admin | View   |

## 7.8 User Flow

```text
Beranda
   ↓
FAQ
   ↓
Link Aspirasi
   ↓
Isi Aspirasi
   ↓
Submit
   ↓
Pesan Sukses
```

### Acceptance Criteria

> Given form aspirasi terbuka,
> When pengguna mengisi teks dan menekan submit tanpa login,
> Then data tersimpan ke database dan pengguna melihat pesan sukses.

---

# 8. Admin Dashboard

## 8.1 Purpose

Menjadi pusat pengelolaan seluruh konten website.

## 8.2 Application Role

V1 hanya memiliki satu role:

> **Super Admin**

Pengurus dari bidang lain melakukan pengkinian data melalui koordinasi dengan Super Admin.

## 8.3 Managed Content

Super Admin dapat mengelola konten untuk:

```text
Admin Dashboard
│
├── Profil
├── Kepengurusan
├── Bidang
├── Berita
├── Ekowir
├── Alumni
├── Kaizen Company
└── Aspirasi
```

## 8.4 Functional Requirements

* CRUD standar.
* Image upload.
* Mengubah status Aktif/Inaktif.
* Membaca data Aspirasi.
* Mengelola direktori berita.
* Mengelola katalog Kaizen Company.
* Mengelola konten organisasi.

## 8.5 User Flow

```text
Halaman Login
      ↓
Dashboard
      ↓
Pilih Modul
      ↓
Kelola / Baca Data
      ↓
Simpan
      ↓
Logout
```

### Contoh

```text
Login
  ↓
Dashboard
  ↓
Kepengurusan
  ↓
Ubah status pengurus
  ↓
Simpan
  ↓
Data publik diperbarui
```

---

# 9. Content Management Matrix

| Content        | Public Page    | Admin Management | Status |
| -------------- | -------------- | ---------------- | ------ |
| Beranda        | Beranda        | Yes              | V1     |
| FAQ            | Beranda        | Yes              | V1     |
| Aspirasi       | Link Aspirasi  | Yes              | V1     |
| Profil         | Profil         | Yes              | V1     |
| Kepengurusan   | Kepengurusan   | Yes              | V1     |
| Bidang         | Bidang         | Yes              | V1     |
| Berita         | Berita         | Yes              | V1     |
| Ekowir         | Ekowir         | Yes              | V1     |
| Alumni         | Alumni         | Yes              | V1     |
| Kontak         | Kontak         | Yes              | V1     |
| Kaizen Company | Kaizen Company | Yes              | V1     |

---

# 10. User Flows

## 10.1 Public Website Flow

```text
                    ┌── Profil
                    ├── Kepengurusan
                    ├── Bidang
                    ├── Berita
                    ├── Ekowir
Beranda ────────────┼── Alumni
                    ├── Kontak
                    │
                    ├── FAQ
                    │    └── Link Aspirasi
                    │
                    └── CTA Kaizen Company
                              └── WhatsApp
```

## 10.2 Aspirasi Flow

```text
Beranda
   ↓
FAQ
   ↓
Link Aspirasi
   ↓
Form
   ↓
Submit
   ↓
Database
   ↓
Super Admin Dashboard
```

## 10.3 Kaizen Company Flow

```text
Beranda / CTA
      ↓
Kaizen Company
      ↓
Product Catalog
      ↓
Product Detail
      ↓
Beli / Hubungi Penjual
      ↓
WhatsApp
```

## 10.4 Super Admin Flow

```text
Login
  ↓
Dashboard
  ↓
Pilih Modul
  ↓
CRUD / Update / View
  ↓
Database
  ↓
Live Website
  ↓
Logout
```

---

# 11. Content Strategy

## 11.1 Real Content First

Tidak ada dummy text atau Lorem Ipsum pada production.

Jika data belum tersedia:

```text
[Content Required]
```

dapat digunakan sebagai penanda konten yang belum tersedia.

## 11.2 Content Sources

| Content               | Source     |
| --------------------- | ---------- |
| Kepengurusan          | Sekretaris |
| Berita kegiatan       | PWMU       |
| Produk Kaizen Company | Ekowir     |

---

# 12. V1 Scope Boundary

## 12.1 Must Have

### Public Website

* Beranda.
* FAQ.
* Profil.
* Kepengurusan.
* Bidang.
* Berita.
* Ekowir.
* Alumni.
* Kontak.
* Kaizen Company.
* Link Aspirasi anonim.

### Functional System

* Super Admin Dashboard.
* CRUD konten.
* Image upload.
* Status Aktif/Inaktif.
* WhatsApp redirect untuk Kaizen Company.
* Penyimpanan aspirasi anonim.
* Search sederhana pada halaman Berita.

## 12.2 Should Have

* Integrasi/link berita ke PWMU.
* SEO dasar.
* Open Graph.
* Export CSV untuk Aspirasi.

## 12.3 Could Have

* Dashboard Analytics Summary untuk Super Admin.

## 12.4 Future / Out of Scope V1

* Shopping Cart.
* Payment Gateway.
* User Account.
* Kalender Kegiatan.
* Direktori Full Alumni.
* Auto-sync PWMU jika V1 menggunakan mekanisme manual.
* Inventory tracking dinamis.

---

# 13. Future Enhancements

Pengembangan setelah V1 dapat mencakup:

1. Integrasi otomatis feed berita dari PWMU.
2. Sistem inventory tracking dinamis apabila bisnis Kaizen Company berkembang.
3. Pengembangan fitur lain berdasarkan kebutuhan organisasi setelah V1 berjalan.

---

# 14. Success Metrics

V1 dianggap berhasil apabila:

* Website live dan stabil pada domain `.org.id`.
* Super Admin dapat mengubah konten tekstual dan gambar tanpa menyentuh source code.
* Navigasi publik berfungsi sesuai struktur IA.
* WhatsApp redirect Kaizen Company berfungsi tanpa error.
* Aspirasi dapat dikirim secara anonim.
* Data aspirasi masuk ke database Admin tanpa membocorkan identitas pelapor.
* Tidak terdapat critical issue atau downtime saat peluncuran.

---

# 15. Definition of Done

* Seluruh Must Have requirement selesai.
* Seluruh navigasi utama dapat diakses.
* Tidak ada dummy content pada production.
* Konten yang belum tersedia ditandai dengan `[Content Required]`.
* Website responsive pada Mobile, Tablet, dan Desktop.
* Kaizen Company menggunakan Dark Theme.
* Website utama menggunakan Light Theme.
* Dashboard Admin sepenuhnya fungsional.
* Akses Dashboard Admin aman.
* Seluruh fitur utama dapat digunakan tanpa error kritis.

---

# Navigation

* [← Product Discovery Overview](./01-product-discovery-overview.md)
* [Product Discovery Constraints →](./03-product-discovery-constraints.md)
