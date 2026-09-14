# Product Requirement Document — Overview

> Website Resmi PK IMM Kaizen V1.0

---

## 1. Document Information

| Item | Detail |
|---|---|
| **Product Name** | Website Resmi PK IMM Kaizen |
| **Document Owner** | Senior Product Manager / Product Owner / Business Analyst |
| **Version** | 1.1 (Revised) |
| **Status** | Draft |
| **Date** | September 2026 |
| **Source of Truth** | Product Discovery — Website Resmi PK IMM Kaizen V1.0 + Requirement Update (Kajian & Pemikiran) |

---

## 2. Product Overview

**Website Resmi PK IMM Kaizen** adalah representasi dan wajah digital resmi **Pimpinan Komisariat Ikatan Mahasiswa Muhammadiyah (PK IMM) Kaizen Universitas Muhammadiyah Surabaya**.

Sistem ini berfungsi sebagai:

- Pusat informasi publik organisasi.
- Etalase katalog bisnis untuk program **Kaizen Company**.
- Fasilitas penerimaan **Aspirasi Mahasiswa** secara anonim.
- Media publikasi pemikiran kritis melalui modul **Kajian & Pemikiran**.
- CMS terpusat melalui **Admin Dashboard** yang dioperasikan oleh **Super Admin**.

---

## 3. Product Background

PK IMM Kaizen membutuhkan identitas digital yang dapat merepresentasikan organisasi secara profesional kepada publik.

Program Ekowir melalui **Kaizen Company** membutuhkan wadah katalog, sedangkan program **Link Aspirasi** membutuhkan sarana digital anonim.

Selain itu, bidang seperti **Hikmah/Politik** membutuhkan wadah literasi digital melalui **Kajian & Pemikiran** untuk mempublikasikan tulisan dan kajian isu terkini yang dapat dibagikan kepada masyarakat luas secara langsung tanpa bergantung pada portal eksternal.

Website juga perlu dirancang agar tidak mudah terbengkalai ketika terjadi pergantian kepengurusan.

---

## 4. Problem Statement

Website ini dikembangkan untuk menjawab beberapa permasalahan utama:

1. Tidak adanya pusat informasi resmi yang terstruktur mengenai:
   - Profil
   - Kepengurusan
   - Bidang
   - Berita
   - Alumni berprestasi PK IMM Kaizen

2. **Kaizen Company** belum memiliki etalase digital yang profesional dan terpusat.

3. Evaluasi organisasi membutuhkan wadah penyampaian aspirasi (**Link Aspirasi**) yang benar-benar anonim.

4. Belum adanya media publikasi mandiri untuk menampung:
   - Gagasan
   - Kajian
   - Pemikiran kader
   - Isu terkini

   khususnya dari **Bidang Hikmah/Politik**.

5. Produk digital organisasi berisiko terbengkalai ketika terjadi pergantian pengurus karena masalah **handover**.

---

## 5. Product Vision

> Menjadi wajah digital resmi PK IMM Kaizen yang profesional, terbuka, dan berkelanjutan; mendukung transparansi informasi, kemandirian ekonomi organisasi melalui Kaizen Company, budaya literasi melalui Kajian & Pemikiran, serta budaya evaluasi yang sehat melalui Link Aspirasi.

---

## 6. Product Goals

Product memiliki tujuan sebagai berikut:

### 6.1 Informasi Organisasi

Menyediakan pusat informasi publik resmi yang mencakup:

- Profil
- Kepengurusan
- Bidang

### 6.2 Publikasi Aktivitas

Menampilkan highlight berita kegiatan yang terintegrasi dengan portal **PWMU**.

### 6.3 Aspirasi Mahasiswa

Memfasilitasi penerimaan aspirasi secara anonim dengan aman dan terpusat.

### 6.4 Kaizen Company

Menyediakan media katalog publikasi produk dan jasa untuk **Kaizen Company**.

### 6.5 Kajian & Pemikiran

Menyediakan media publikasi tulisan atau artikel internal yang memiliki tautan mandiri dan dapat dibagikan.

### 6.6 Content Management

Menyediakan CMS Dashboard yang intuitif untuk **Super Admin**.

### 6.7 Sustainability & Handover

Merancang sistem yang:

- Production-ready.
- Dapat dikelola secara mandiri.
- Siap diwariskan kepada kepengurusan berikutnya.

---

## 7. Target Users

Target pengguna Website Resmi PK IMM Kaizen meliputi:

| Target User | Kebutuhan Utama |
|---|---|
| **Mahasiswa** | Mendapatkan informasi organisasi, berita, kajian, alumni, katalog, dan menyampaikan aspirasi |
| **Kader IMM Kaizen** | Mendapatkan informasi resmi dan mengikuti publikasi organisasi |
| **Personalia / Pengurus IMM Kaizen** | Mengakses informasi struktur dan menggunakan website sebagai referensi kegiatan |
| **Alumni IMM Kaizen** | Melihat informasi dan showcase alumni |
| **Masyarakat umum** | Mengenal organisasi dan mengakses informasi publik |
| **Calon konsumen / mitra Kaizen Company** | Melihat katalog dan menghubungi pihak penjual |

---

## 8. User Personas

### Persona 1 — Mahasiswa / Pengunjung Umum

Membutuhkan informasi tentang PK IMM Kaizen, membaca berita kegiatan, membaca tulisan atau kajian isu terkini, melihat profil alumni, melihat katalog produk, dan mengirimkan kritik atau saran secara anonim.

### Persona 2 — Kader / Personalia

Membutuhkan:

- Informasi struktur kepengurusan yang up-to-date.
- Kemampuan membagikan tautan kajian ke media sosial.
- Informasi resmi organisasi.
- Website sebagai referensi kegiatan.

### Persona 3 — Calon Konsumen / Mitra

Membutuhkan:

- Akses cepat ke katalog Kaizen Company.
- Detail produk atau jasa.
- Jalur komunikasi dengan pihak penjual atau Ekowir untuk melakukan transaksi.

### Persona 4 — Super Admin

Membutuhkan dashboard yang mudah digunakan untuk:

- Memperbarui berita.
- Mengelola pengurus.
- Mengelola produk.
- Mengelola alumni.
- Mengelola kajian.
- Membaca aspirasi.

Semua aktivitas tersebut harus dapat dilakukan tanpa perlu menyentuh source code.

---

## 9. User Needs

Kebutuhan utama pengguna adalah:

- Akses informasi organisasi yang terstruktur dan cepat.
- Katalog produk Kaizen Company yang jelas dengan jalur komunikasi langsung melalui WhatsApp.
- Saluran literasi untuk membaca hasil kajian intelektual organisasi.
- Rasa aman dan jaminan anonimitas saat mengirimkan aspirasi.
- Kemudahan pengelolaan data dari backend tanpa keahlian pemrograman bagi pengurus.

---

## 10. Value Proposition

> Website resmi yang menggabungkan **company profile organisasi, media literasi intelektual (Kajian), etalase bisnis (Kaizen Company), dan saluran aspirasi anonim** dalam satu ekosistem yang modern, cepat, terstruktur, dan mudah dikelola melalui satu pintu (**Super Admin Dashboard**).

---

# Navigation

- [← Product Discovery — Constraints](../product-discovery/03-product-discovery-constraints.md)
- [Product Requirement Document — Scope →](./02-prd-scope.md)
