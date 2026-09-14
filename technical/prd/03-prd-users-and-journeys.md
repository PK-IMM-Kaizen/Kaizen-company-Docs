# Product Requirement Document — Users & Journeys

> Website Resmi PK IMM Kaizen V1.0

---

## 1. Target Users

Produk memiliki beberapa kelompok pengguna dengan kebutuhan dan pola interaksi yang berbeda.

| Target User | Deskripsi | Kebutuhan Utama |
|---|---|---|
| Mahasiswa | Mahasiswa yang ingin mengetahui informasi PK IMM Kaizen | Informasi organisasi, berita, bidang, aspirasi, dan kajian |
| Kader | Anggota/kader IMM yang membutuhkan informasi internal dan aktivitas organisasi | Informasi kepengurusan, bidang, berita, kajian, dan aspirasi |
| Personalia / Pengurus | Pengurus yang terlibat dalam pengelolaan organisasi | Informasi organisasi yang terstruktur dan terbarui |
| Alumni | Alumni yang ingin mengetahui aktivitas dan perkembangan organisasi | Informasi organisasi dan alumni |
| Masyarakat Umum | Pengunjung di luar lingkungan organisasi | Profil organisasi, berita, kajian, produk, dan kontak |
| Konsumen / Partner | Pihak yang tertarik dengan produk atau jasa Kaizen Company | Katalog produk/jasa dan akses komunikasi melalui WhatsApp |
| Super Admin | Pengelola utama website | Pengelolaan seluruh konten dan data website |

---

# 2. User Personas

## 2.1 Persona — Public Visitor

### Profile

Pengunjung umum yang ingin mengetahui identitas dan aktivitas PK IMM Kaizen.

### Goals

- Mengetahui profil organisasi.
- Melihat struktur kepengurusan.
- Mengetahui bidang yang tersedia.
- Membaca berita organisasi.
- Melihat informasi alumni.
- Mengetahui produk dan jasa Kaizen Company.
- Membaca kajian.
- Menghubungi organisasi.

### Needs

- Navigasi sederhana.
- Informasi yang jelas.
- Konten yang mudah ditemukan.
- Tampilan profesional dan responsif.

### Main Interactions

- Beranda
- Profil
- Kepengurusan
- Bidang
- Berita
- Ekowir
- Alumni
- Kontak
- Kajian
- Kaizen Company

---

## 2.2 Persona — Kader / Mahasiswa

### Profile

Mahasiswa atau kader yang berinteraksi dengan organisasi dan membutuhkan akses terhadap informasi serta ruang penyampaian aspirasi.

### Goals

- Mendapatkan informasi organisasi.
- Mengikuti perkembangan kegiatan melalui berita.
- Membaca kajian.
- Mengetahui struktur kepengurusan.
- Menyampaikan aspirasi secara anonim.

### Needs

- Informasi yang terstruktur.
- Akses aspirasi tanpa login.
- Jaminan bahwa identitas tidak diminta melalui form aspirasi.
- Informasi organisasi yang selalu diperbarui.

### Main Interactions

- Beranda
- Kepengurusan
- Bidang
- Berita
- Kajian
- Aspirasi
- Profil

---

## 2.3 Persona — Consumer / Partner

### Profile

Pengunjung yang tertarik terhadap produk atau jasa yang ditawarkan melalui Kaizen Company.

### Goals

- Melihat produk atau jasa yang tersedia.
- Mengetahui harga dan deskripsi.
- Mengetahui status ketersediaan.
- Menghubungi penjual.

### Needs

- Katalog yang jelas.
- Informasi produk yang aktual.
- CTA pembelian yang mudah.
- Komunikasi langsung melalui WhatsApp.

### Main Interactions

- Kaizen Company
- Detail Produk
- WhatsApp

---

## 2.4 Persona — Super Admin

### Profile

Pengelola utama website yang bertanggung jawab terhadap konten dan data yang ditampilkan kepada publik.

### Goals

- Mengelola seluruh konten website.
- Menambah, mengubah, dan menghapus data.
- Mengubah status konten.
- Mengelola aspirasi mahasiswa.
- Menjaga informasi publik tetap aktual.
- Memungkinkan website dikelola tanpa mengubah source code.

### Needs

- Dashboard terpusat.
- Authentication yang aman.
- CRUD konten.
- Image upload.
- Status aktif/inaktif.
- Validasi input.
- Konfirmasi untuk tindakan destruktif.

### Main Interactions

- Login
- Dashboard
- Profil
- Kepengurusan
- Bidang
- Berita
- Kajian
- Ekowir
- Kaizen Company
- Alumni
- Aspirasi
- Logout

---

# 3. User Needs

## 3.1 Information Needs

Pengguna membutuhkan informasi organisasi yang:

- Resmi.
- Terstruktur.
- Mudah ditemukan.
- Mudah dipahami.
- Dapat diperbarui oleh pengelola.

---

## 3.2 Organizational Information

Pengguna membutuhkan akses terhadap:

- Profil organisasi.
- Struktur kepengurusan.
- Informasi bidang.
- Berita.
- Alumni.
- Kontak organisasi.

---

## 3.3 Literacy & Kajian

Pengguna membutuhkan ruang untuk:

- Membaca artikel kajian.
- Mengakses konten pemikiran organisasi.
- Menjelajahi artikel melalui bagian Kajian pada Beranda.
- Membuka halaman detail artikel.

---

## 3.4 Kaizen Company

Pengguna membutuhkan:

- Katalog produk dan jasa yang terpusat.
- Informasi produk yang jelas.
- Informasi harga.
- Informasi kategori.
- Informasi stok yang ditampilkan.
- Akses komunikasi langsung dengan penjual melalui WhatsApp.

---

## 3.5 Anonymous Aspiration

Pengguna membutuhkan mekanisme penyampaian aspirasi yang:

- Tidak membutuhkan login.
- Tidak meminta nama.
- Tidak meminta email.
- Tidak meminta nomor HP.
- Menyimpan waktu pengiriman.
- Memberikan feedback setelah berhasil dikirim.
- Tidak menyediakan public tracking.

---

## 3.6 Content Management

Super Admin membutuhkan kemampuan untuk:

- Mengelola konten tanpa mengubah kode.
- Mengunggah gambar.
- Mengubah data.
- Mengubah status aktif/inaktif.
- Melihat aspirasi yang masuk.
- Mengelola konten yang ditampilkan pada website.

---

# 4. User Journeys

## 4.1 Public Visitor Journey

### Goal

Menemukan informasi resmi mengenai PK IMM Kaizen.

### Flow

~~~text
Pengunjung
    ↓
Beranda
    ↓
Melihat informasi utama
    ↓
Eksplorasi Navbar
    ├── Profil
    ├── Kepengurusan
    ├── Bidang
    ├── Berita
    ├── Ekowir
    ├── Alumni
    └── Kontak
    ↓
Menemukan informasi yang dibutuhkan
~~~

### Expected Outcome

Pengunjung dapat memperoleh informasi organisasi tanpa membutuhkan akun.

---

## 4.2 Kajian Journey

### Goal

Membaca artikel kajian atau pemikiran organisasi.

### Flow

~~~text
Pengunjung
    ↓
Beranda
    ↓
Section Kajian
    ↓
Melihat daftar / card kajian
    ↓
Memilih kajian
    ↓
Halaman Detail Kajian
    ↓
Membaca artikel
~~~

### Expected Outcome

Pengguna dapat membaca konten kajian secara langsung pada website.

---

## 4.3 Kaizen Company Journey

### Goal

Menemukan produk atau jasa dan menghubungi penjual.

### Flow

~~~text
Pengunjung
    ↓
CTA Kaizen Company
    ↓
Kaizen Company
    ↓
Melihat katalog
    ↓
Memilih produk / jasa
    ↓
Melihat detail
    ↓
Klik "Beli" / "Hubungi Penjual"
    ↓
WhatsApp
~~~

### Expected Outcome

Pengguna memperoleh informasi produk/jasa dan dapat melanjutkan komunikasi melalui WhatsApp.

### Boundary

Proses transaksi tidak dilakukan di dalam website.

Tidak terdapat:

- Shopping Cart
- Checkout
- Payment Gateway

---

## 4.4 Aspirasi Mahasiswa Journey

### Goal

Menyampaikan aspirasi secara anonim.

### Flow

~~~text
Pengguna
    ↓
Beranda
    ↓
FAQ
    ↓
Link Aspirasi
    ↓
Form Aspirasi
    ↓
Menulis aspirasi
    ↓
Submit
    ↓
Pesan sukses
~~~

### Expected Outcome

Aspirasi berhasil disimpan dan dapat dilihat oleh Super Admin.

### Privacy Boundary

Form tidak meminta:

- Nama
- Email
- Nomor HP
- Login / Account

Tidak tersedia public tracking terhadap aspirasi yang telah dikirim.

---

## 4.5 Super Admin Journey

### Goal

Mengelola konten dan data website.

### Flow

~~~text
Super Admin
    ↓
Halaman Login
    ↓
Authentication
    ↓
Dashboard
    ↓
Memilih Modul
    ↓
Melihat / Menambah / Mengubah / Menghapus Data
    ↓
Validasi
    ↓
Simpan Perubahan
    ↓
Data diperbarui
    ↓
Logout
~~~

---

## 4.6 Super Admin — Content Update Journey

### Example

Pengurus memberikan data baru kepada Super Admin.

~~~text
Pengurus
    ↓
Memberikan data terbaru
    ↓
Super Admin
    ↓
Login Dashboard
    ↓
Memilih Modul
    ↓
Memasukkan / Mengubah Data
    ↓
Validasi
    ↓
Publish / Aktifkan
    ↓
Data tampil pada Website Publik
~~~

### Expected Outcome

Konten website dapat diperbarui tanpa perubahan source code.

---

# 5. Journey Principles

User journey V1 mengikuti prinsip berikut:

1. **Public-first**  
   Pengunjung dapat mengakses informasi utama tanpa login.

2. **Low Friction**  
   Interaksi publik dibuat sesederhana mungkin.

3. **Anonymous by Design**  
   Aspirasi tidak membutuhkan identitas pengguna.

4. **Direct Communication**  
   Kaizen Company mengarahkan komunikasi transaksi langsung ke WhatsApp.

5. **Centralized Management**  
   Pengelolaan konten dilakukan melalui satu Super Admin.

6. **No Unnecessary Account**  
   V1 tidak membutuhkan public user account.

7. **Clear Boundaries**  
   Website bukan marketplace, forum, atau social platform.

---

# Navigation

- [← Product Requirement Document — Scope](./02-prd-scope.md)
- [Product Requirement Document — Functional Requirements →](./04-prd-functional-requirements.md)
