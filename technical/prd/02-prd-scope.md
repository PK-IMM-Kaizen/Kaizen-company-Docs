# Product Requirement Document — Scope

> Website Resmi PK IMM Kaizen V1.0

---

## 1. Product Scope

PRD ini mendefinisikan kebutuhan untuk dua area utama:

1. **Public Website**
2. **Admin Dashboard**

### 1.1 Public Website

Public Website mencakup:

- Beranda
- Profil
- Kepengurusan
- Bidang
- Berita
- Ekowir
- Alumni
- Kontak
- Section **Kajian & Pemikiran** pada Beranda
- Halaman Detail Kajian
- Kaizen Company melalui CTA khusus
- Form Aspirasi Mahasiswa

### 1.2 Admin Dashboard

Admin Dashboard mencakup:

- Autentikasi Super Admin
- Manajemen Profil
- Manajemen Kepengurusan
- Manajemen Bidang
- Manajemen Berita
- Manajemen Kajian & Pemikiran
- Manajemen Alumni
- Manajemen Ekowir
- Manajemen Kaizen Company
- Manajemen Produk
- Manajemen Aspirasi
- Manajemen Media

---

## 2. Scope Boundary

Website V1 berfokus pada:

- Identitas digital resmi PK IMM Kaizen.
- Pusat informasi publik organisasi.
- Publikasi aktivitas organisasi.
- Media publikasi Kajian & Pemikiran.
- Katalog produk dan jasa Kaizen Company.
- Saluran aspirasi anonim.
- Pengelolaan konten melalui satu Super Admin.

Website V1 **bukan** merupakan:

- Sistem e-commerce penuh.
- Platform komunitas.
- Sistem manajemen organisasi yang kompleks.
- Platform dengan akun pengguna publik.
- Sistem transaksi online.

---

## 3. Out of Scope

Fitur berikut tidak termasuk dalam V1:

### 3.1 E-Commerce

- Payment Gateway.
- Shopping Cart.
- Checkout system terintegrasi.
- Transaksi online di dalam website.

Transaksi Kaizen Company dilakukan di luar sistem melalui WhatsApp.

### 3.2 Public Account

- Registrasi akun publik.
- Login pengguna umum.
- User profile publik.

### 3.3 Organization Event Management

- Kalender organisasi.
- Event management system.
- Sistem pendaftaran event.

### 3.4 Alumni System

- Direktori seluruh alumni.

V1 hanya menyediakan **showcase alumni pilihan**.

### 3.5 Community Features

- Forum.
- Komentar publik.
- Social interaction system.

### 3.6 PWMU Full Article Duplication

Website tidak melakukan duplikasi artikel kegiatan lengkap dari PWMU.

Modul Berita hanya menyimpan informasi ringkas dan URL menuju artikel asli PWMU.

### 3.7 Multi-Role Authentication

V1 hanya menggunakan satu application role:

> **Super Admin**

Tidak terdapat login khusus untuk:

- Ketua bidang.
- Penulis Kajian.
- Pengurus bidang lainnya.

Penulis atau bidang yang ingin mempublikasikan Kajian & Pemikiran harus berkoordinasi dengan Super Admin.

### 3.8 Public Aspiration Tracking

Pengguna tidak dapat melihat atau melacak status penyelesaian aspirasi yang telah dikirim.

---

## 4. Information Architecture

Struktur informasi utama website:

```text
PK IMM Kaizen
│
└── Website Resmi PK IMM Kaizen
    │
    ├── Beranda
    │   ├── Section: Kajian & Pemikiran
    │   │   └── Halaman Detail Kajian
    │   ├── FAQ
    │   └── Aspirasi Mahasiswa
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
        └── Diakses melalui CTA khusus
````

## 5. Navigation Structure

### 5.1 Main Navbar

Navbar utama berisi:

* Beranda
* Profil
* Kepengurusan
* Bidang
* Berita
* Ekowir
* Alumni
* Kontak

### 5.2 Kajian & Pemikiran

Kajian & Pemikiran tidak menjadi item pada navbar utama.

Modul ini ditampilkan sebagai section pada Beranda.

Flow:

```text
Beranda
   ↓
Section Kajian & Pemikiran
   ↓
Card Kajian
   ↓
Baca Selengkapnya
   ↓
Halaman Detail Kajian
```

Setiap Kajian memiliki URL mandiri yang dapat dibagikan.

Contoh:

```text
/kajian/judul-kajian-pemikiran
```

### 5.3 Aspirasi Mahasiswa

Akses Aspirasi Mahasiswa tersedia melalui bagian FAQ pada Beranda.

Flow:

```text
Beranda
   ↓
FAQ
   ↓
Link Aspirasi Mahasiswa
   ↓
Form Aspirasi
```

### 5.4 Kaizen Company

Kaizen Company tidak ditempatkan sebagai item navbar utama.

Akses dilakukan melalui CTA khusus.

Flow:

```text
Website Utama
   ↓
CTA Kaizen Company
   ↓
Kaizen Company
```

Halaman Kaizen Company menggunakan Dark Theme.

## 6. Public Website Scope

### 6.1 Beranda

Beranda menjadi entry point utama website.

Beranda menyediakan:

* Informasi utama organisasi.
* Section Kajian & Pemikiran.
* FAQ.
* Akses menuju Aspirasi Mahasiswa.
* CTA menuju Kaizen Company.

### 6.2 Profil

Menampilkan informasi resmi mengenai PK IMM Kaizen.

### 6.3 Kepengurusan

Menampilkan struktur kepengurusan organisasi.

Data pengurus memiliki status:

* Aktif
* Inaktif

### 6.4 Bidang

Menampilkan informasi bidang yang terdapat dalam organisasi.

### 6.5 Berita

Berita berfungsi sebagai direktori aktivitas organisasi.

Konten berita tidak diduplikasi secara penuh dari PWMU.

Website menyimpan:

* Thumbnail.
* Judul.
* Deskripsi singkat / kutipan.
* URL artikel PWMU.

### 6.6 Ekowir

Menampilkan informasi terkait program Ekonomi & Kewirausahaan.

Kaizen Company diposisikan sebagai program di bawah bidang Ekonomi & Kewirausahaan (Ekowir).

### 6.7 Alumni

Menampilkan showcase alumni pilihan yang memiliki nilai representasi dan inspirasi bagi publik.

V1 tidak menyediakan direktori seluruh alumni.

### 6.8 Kontak

Menyediakan informasi dan jalur komunikasi publik dengan organisasi.

### 6.9 Kajian & Pemikiran

Menjadi media publikasi artikel atau tulisan orisinal organisasi.

Konten Kajian:

* Disimpan penuh di database website.
* Memiliki halaman detail mandiri.
* Memiliki URL yang dapat dibagikan.
* Dapat dibaca secara penuh oleh publik.

## 7. Admin Dashboard Scope

Admin Dashboard merupakan CMS terpusat untuk pengelolaan konten website.

### 7.1 Role

Hanya terdapat satu application role:

Super Admin

### 7.2 Dashboard Modules

Dashboard mencakup menu:

```text
Dashboard
├── Profil
├── Kepengurusan
├── Bidang
├── Berita
├── Kajian & Pemikiran
├── Alumni
├── Produk & Jasa Kaizen Company
├── Aspirasi
└── Pengaturan Kontak / Media
```

### 7.3 Content Management

Super Admin dapat melakukan operasi:

* Create
* Read
* Update
* Delete

terhadap data yang tersedia pada modul CMS.

### 7.4 Content Lifecycle

Konten memiliki lifecycle dasar:

```text
Draft
  ↓
Publish
  ↓
Unpublish
  ↓
Delete
```

### 7.5 Visibility Rule

Data dengan status:

* Inaktif
* Unpublished
* Draft

tidak boleh ditampilkan kepada publik.

Data historis tetap tersedia di Dashboard selama belum dihapus secara permanen.

## 8. Theme Scope

### 8.1 Main Website

Website utama menggunakan:

Light Theme

### 8.2 Kaizen Company

Kaizen Company menggunakan:

Dark Theme

Perbedaan tema ini merupakan bagian dari visual direction V1.

## 9. Content Scope

Seluruh halaman pada saat production release harus menggunakan real content.

Tidak diperbolehkan menggunakan:

* Lorem Ipsum
* Dummy Text
* Dummy Content

Jika konten belum tersedia dari organisasi, sistem menggunakan placeholder eksplisit:

[Content Required]

### 9.1 Content Sources

| Content               | Source                             |
| --------------------- | ---------------------------------- |
| Kepengurusan          | Sekretaris                         |
| Berita kegiatan       | PWMU                               |
| Produk Kaizen Company | Ekowir                             |
| Kajian & Pemikiran    | Bidang terkait melalui Super Admin |

## 10. Scope Principles

Pengembangan V1 mengikuti prinsip berikut:

* **Official First**
  Website menjadi sumber informasi resmi organisasi.

* **Simple by Design**
  Fitur yang tidak diperlukan untuk tujuan V1 tidak dimasukkan.

* **Single Point of Management**
  Seluruh pengelolaan konten dilakukan melalui Super Admin.

* **No Unnecessary Transaction Complexity**
  Kaizen Company tidak memiliki sistem pembayaran atau checkout internal.

* **Privacy by Default**
  Aspirasi Mahasiswa tidak mengumpulkan identitas personal.

* **Real Content First**
  Production release harus menggunakan konten nyata.

* **Handover Ready**
  Sistem harus dapat dilanjutkan oleh kepengurusan berikutnya.

## Navigation

- [← Product Requirement Document — Overview](./01-prd-overview.md)
- [Product Requirement Document — Users & Journeys →](./03-prd-users-and-journeys.md)
