# Product Requirement Document — Module Requirements

> Website Resmi PK IMM Kaizen V1.0

---

# 1. Module Requirements

Dokumen ini mendefinisikan kebutuhan masing-masing modul utama pada Website Resmi PK IMM Kaizen V1.

Modul dibagi menjadi:

- Public Website Modules
- Content & Organization Modules
- Business Modules
- Communication Modules
- Admin Modules

---

# 2. Public Website Modules

## 2.1 Module — Beranda

### Purpose

Menjadi entry point utama website dan memberikan gambaran singkat mengenai PK IMM Kaizen.

### Requirements

Beranda harus menyediakan akses atau informasi menuju:

- Informasi utama organisasi.
- Navigasi halaman publik.
- Section Kajian & Pemikiran.
- FAQ.
- Link Aspirasi Mahasiswa.
- CTA Kaizen Company.
- Informasi lain yang dianggap penting untuk identitas organisasi.

### Rules

- Beranda merupakan bagian Must Have V1.
- Kajian & Pemikiran ditampilkan sebagai section pada Beranda.
- Aspirasi diakses melalui bagian FAQ.
- Kaizen Company diakses melalui CTA khusus.

---

# 3. Organization Modules

## 3.1 Module — Profil

### Purpose

Menampilkan identitas resmi PK IMM Kaizen kepada publik.

### Requirements

Modul harus menyediakan informasi profil organisasi yang relevan dan bersumber dari data resmi organisasi.

### Access

| Actor | Access |
|---|---|
| Public | View |
| Super Admin | CRUD |

### Rules

- Konten harus menggunakan data riil.
- Tidak menggunakan Lorem Ipsum pada production.
- Jika data belum tersedia, gunakan placeholder `[Content Required]`.

---

## 3.2 Module — Kepengurusan

### Purpose

Menampilkan struktur kepengurusan PK IMM Kaizen.

### Data

Setiap pengurus dapat memiliki:

- Nama
- Foto
- Jabatan
- Bidang
- Status

### Access

| Actor | Access |
|---|---|
| Public | View active |
| Super Admin | CRUD |

### Rules

- Pengurus aktif ditampilkan kepada publik.
- Pengurus inaktif disembunyikan dari publik.
- Data historis tetap dapat dipertahankan.
- Perubahan status tidak otomatis berarti penghapusan data.

---

## 3.3 Module — Bidang

### Purpose

Menampilkan informasi bidang yang terdapat dalam struktur PK IMM Kaizen.

### Requirements

Modul harus memungkinkan informasi bidang ditampilkan secara terstruktur.

### Access

| Actor | Access |
|---|---|
| Public | View |
| Super Admin | CRUD |

### Rules

- Informasi harus berasal dari data organisasi.
- Super Admin menjadi pengelola data pada V1.

---

## 3.4 Module — Alumni

### Purpose

Menampilkan showcase alumni pilihan sebagai bagian dari representasi dan inspirasi publik.

### Scope Boundary

Modul Alumni V1 bukan merupakan direktori seluruh alumni.

### Data

Alumni dapat memiliki:

- Nama
- Foto
- Profil
- Informasi pencapaian atau kontribusi
- Status

### Access

| Actor | Access |
|---|---|
| Public | View active |
| Super Admin | CRUD |

### Rules

- Hanya alumni yang dipilih dan dipublikasikan yang ditampilkan.
- Alumni inaktif/unpublished tidak ditampilkan kepada publik.
- Direktori lengkap seluruh alumni berada di luar scope V1.

---

# 4. Content Modules

## 4.1 Module — Berita

### Purpose

Menampilkan rekam jejak dan highlight aktivitas PK IMM Kaizen.

### Content Model

Berita berfungsi sebagai direktori atau aggregator menuju PWMU.

### Data

Setiap berita dapat memiliki:

- Thumbnail
- Judul
- Deskripsi singkat
- URL artikel PWMU

### Public Behavior

~~~text
Berita
  ↓
News Card
  ↓
Klik "Lihat selengkapnya di PWMU"
  ↓
Artikel PWMU
~~~

### Rules

- Artikel lengkap tidak diduplikasi pada website.
- URL asli PWMU harus disimpan.
- Link dibuka pada tab baru.
- Berita yang tidak dipublikasikan tidak ditampilkan.

### Access

| Actor | Access |
|---|---|
| Public | View |
| Super Admin | CRUD |

---

## 4.2 Module — Kajian & Pemikiran

### Purpose

Menjadi media publikasi native untuk tulisan, kajian, dan pemikiran kader/organisasi.

### Public Placement

Kajian ditampilkan sebagai section pada Beranda.

Kajian tidak menjadi item pada navbar utama.

### Public Flow

~~~text
Beranda
  ↓
Section Kajian & Pemikiran
  ↓
Kajian Card
  ↓
"Baca Selengkapnya"
  ↓
Detail Kajian
~~~

### Data

Kajian dapat memiliki:

- Judul
- Slug
- Ringkasan
- Konten penuh
- Penulis
- Thumbnail
- Publish state

### Rules

- Kajian merupakan native content website.
- Konten artikel penuh disimpan pada sistem.
- Setiap Kajian memiliki URL mandiri yang unik.
- Kajian dengan status Draft atau Unpublished tidak ditampilkan kepada publik.
- URL detail harus dapat dibagikan.

### Admin Behavior

Super Admin dapat:

- Membuat Kajian.
- Membaca Kajian.
- Mengubah Kajian.
- Menghapus Kajian.
- Menyimpan sebagai Draft.
- Mempublikasikan Kajian.
- Meng-unpublish Kajian.

### Open Decision

Masih diperlukan keputusan mengenai:

- Prioritas Kajian terhadap peluncuran V1.
- Model atribusi penulis.
- Workflow approval.

---

# 5. Business Modules

## 5.1 Module — Ekowir

### Purpose

Menampilkan informasi dan aktivitas ekonomi/kewirausahaan organisasi.

### Relationship

Kaizen Company merupakan program di bawah:

> **Bidang Ekonomi & Kewirausahaan (Ekowir)**

Kaizen Company bukan entitas organisasi yang terpisah dari PK IMM Kaizen.

### Access

| Actor | Access |
|---|---|
| Public | View |
| Super Admin | CRUD |

---

## 5.2 Module — Kaizen Company

### Purpose

Menjadi etalase digital produk dan jasa Kaizen Company.

### Theme

Kaizen Company menggunakan:

> **Dark Theme**

### Data

Setiap produk/jasa dapat memiliki:

- Nama
- Foto
- Harga
- Deskripsi
- Kategori
- Stok
- Status

### Public Rules

- Hanya produk dengan status Aktif yang ditampilkan.
- Stok bersifat display only.
- Produk tidak diproses sebagai transaksi internal website.

### Product Flow

~~~text
Kaizen Company
  ↓
Katalog
  ↓
Pilih Produk
  ↓
Detail Produk
  ↓
"Beli" / "Hubungi Penjual"
  ↓
WhatsApp
~~~

### Transaction Boundary

V1 tidak menyediakan:

- Shopping Cart
- Checkout
- Payment Gateway
- Pembayaran digital
- Order management kompleks

### WhatsApp

CTA pembelian harus mengarahkan pengguna ke WhatsApp menggunakan URL `wa.me`.

Pesan dapat menggunakan template atau pre-filled message.

---

# 6. Communication Modules

## 6.1 Module — Aspirasi Mahasiswa

### Purpose

Menyediakan saluran penyampaian kritik dan saran secara anonim.

### Access

Form dapat diakses publik tanpa authentication.

### Public Flow

~~~text
Beranda
  ↓
FAQ
  ↓
Link Aspirasi Mahasiswa
  ↓
Form
  ↓
Isi Aspirasi
  ↓
Submit
  ↓
Success Feedback
~~~

### Input

- Teks aspirasi

### Stored Data

- Teks aspirasi
- Timestamp

### Rules

Form tidak meminta:

- Nama
- Email
- Nomor HP
- Login

### Privacy

- Aspirasi tidak boleh ditampilkan kepada publik.
- Tidak tersedia public tracking.
- Aspirasi hanya dapat dilihat oleh Super Admin melalui Dashboard.

### Protection

Sistem harus memiliki proteksi spam dasar.

### Access

| Actor | Access |
|---|---|
| Public | Submit |
| Super Admin | View |

---

## 6.2 Module — Kontak

### Purpose

Menyediakan informasi komunikasi resmi PK IMM Kaizen.

### Requirements

Modul harus menampilkan informasi kontak yang disediakan organisasi.

### Access

| Actor | Access |
|---|---|
| Public | View |
| Super Admin | Manage |

---

# 7. Admin Modules

## 7.1 Module — Admin Authentication

### Purpose

Membatasi akses Dashboard hanya kepada Super Admin.

### Flow

~~~text
Admin Login
  ↓
Masukkan Kredensial
  ↓
Authentication
  ├── Valid → Dashboard
  └── Invalid → Error
~~~

### Rules

- Hanya Super Admin yang dapat login.
- Public user tidak memiliki akun.
- Metode authentication masih merupakan Open Decision.
- URL Dashboard tidak boleh dapat diakses tanpa authorization.

---

## 7.2 Module — Admin Dashboard

### Purpose

Menjadi pusat pengelolaan seluruh konten website.

### Dashboard Navigation

Dashboard harus mencakup menu:

- Profil
- Kepengurusan
- Bidang
- Berita
- Kajian & Pemikiran
- Alumni
- Produk & Jasa Kaizen Company
- Aspirasi
- Pengaturan Kontak/Media

### Rules

- Dashboard menggunakan single-role access.
- Role yang tersedia pada V1 hanya Super Admin.
- Perubahan konten publik dilakukan melalui Dashboard.

---

## 7.3 Module — Content Management

### Purpose

Memungkinkan Super Admin mengelola data tanpa menyentuh source code.

### Operations

- Create
- Read
- Update
- Delete

### Applicable Modules

- Profil
- Kepengurusan
- Bidang
- Berita
- Kajian & Pemikiran
- Alumni
- Ekowir
- Kaizen Company
- Kontak
- Media

---

## 7.4 Module — Media Management

### Purpose

Mengelola media yang digunakan pada konten website.

### Requirements

Sistem harus mendukung upload gambar untuk modul yang membutuhkan media.

### Rules

- Format gambar utama: WebP.
- File harus melalui validasi.
- Ukuran file harus divalidasi.
- Gambar publik harus memiliki alt text.
- Aset gambar harus dioptimasi untuk performa.

---

## 7.5 Module — Aspirasi Management

### Purpose

Memberikan Super Admin akses terhadap aspirasi yang masuk.

### Dashboard View

Setiap aspirasi minimal menampilkan:

- Isi aspirasi
- Timestamp

### Rules

- Data aspirasi tidak dapat diakses publik.
- Super Admin dapat membaca daftar aspirasi.
- Public tracking tidak tersedia.

---

# 8. Module State & Visibility

Modul yang memiliki status publikasi harus mengikuti aturan visibility.

~~~text
Content
   ↓
Status
   ├── Published / Active
   │       ↓
   │    Public
   │
   └── Draft / Unpublished / Inactive
           ↓
        Hidden
~~~

### Applicable Modules

- Kepengurusan
- Alumni
- Kaizen Company
- Kajian & Pemikiran
- Berita
- Konten dinamis lainnya

---

# 9. Module Validation & Feedback

Setiap modul yang menyediakan input melalui Dashboard harus memiliki:

### Validation

- Required field validation.
- Format validation.
- URL validation jika diperlukan.
- Image validation.
- Status validation.

### Feedback

Sistem harus menyediakan:

- Success state.
- Error state.
- Validation error.
- Confirmation untuk tindakan destruktif.

### Example

~~~text
Super Admin
  ↓
Submit Form
  ↓
Validation
  ├── Invalid
  │     ↓
  │   Error Feedback
  │
  └── Valid
        ↓
      Save
        ↓
    Success Feedback
~~~

---

# 10. Module Relationship Summary

| Module | Public | Super Admin | Native Content | External Redirect |
|---|---:|---:|---:|---:|
| Beranda | ✓ | ✓ | ✓ | - |
| Profil | ✓ | ✓ | ✓ | - |
| Kepengurusan | ✓ | ✓ | ✓ | - |
| Bidang | ✓ | ✓ | ✓ | - |
| Berita | ✓ | ✓ | Ringkasan | PWMU |
| Kajian & Pemikiran | ✓ | ✓ | ✓ | - |
| Ekowir | ✓ | ✓ | ✓ | - |
| Kaizen Company | ✓ | ✓ | ✓ | WhatsApp |
| Alumni | ✓ | ✓ | ✓ | - |
| Kontak | ✓ | ✓ | ✓ | - |
| Aspirasi | Submit | View | ✓ | - |
| Admin Dashboard | - | ✓ | - | - |

---

# 11. Module Scope Boundary

Modul V1 tidak boleh berkembang menjadi fitur yang berada di luar scope berikut:

- Payment Gateway.
- Shopping Cart.
- Checkout.
- Public User Account.
- Kalender Organisasi.
- Event Management System.
- Full Alumni Directory.
- Forum.
- Public Comment System.
- Full Article Duplication dari PWMU.
- Multi-role Authentication.
- Public Aspiration Tracking.

---

# Navigation

- [← Product Requirement Document — Business Rules](./05-prd-business-rules.md)
- [Product Requirement Document — Non-Functional Requirements →](./07-prd-non-functional-requirements.md)
