# Product Discovery — Constraints

> Website Resmi PK IMM Kaizen V1.0

---

# 1. Functional Requirements

## 1.1 Content & Media

Sistem harus:

* Dapat menyimpan dan menampilkan gambar.
* Menggunakan format **WebP** untuk gambar.
* Mendukung image upload melalui Super Admin Dashboard.
* Mendukung pengelolaan status konten Aktif/Inaktif.

## 1.2 Berita

Sistem harus menyediakan:

* Daftar berita.
* Search sederhana pada halaman Berita.
* Thumbnail berita.
* Judul berita.
* Deskripsi singkat.
* Link menuju artikel asli di PWMU.

Website tidak melakukan duplikasi penuh terhadap artikel PWMU.

## 1.3 Content Status

Sistem harus dapat memberikan status:

* Aktif.
* Inaktif.

Status digunakan setidaknya pada:

* Kepengurusan.
* Alumni.
* Produk Kaizen Company.

Konten berstatus **Inaktif** tidak ditampilkan kepada publik.

---

# 2. Non-Functional Requirements

## 2.1 Design & UI

Website harus menggunakan pendekatan:

* Modern.
* Minimalistic.
* Responsive.

Font utama:

> **Plus Jakarta Sans**

Theme:

| Area           | Theme |
| -------------- | ----- |
| Website utama  | Light |
| Kaizen Company | Dark  |

## 2.2 Device Support

Website harus responsive pada:

* Mobile.
* Tablet.
* Desktop.

## 2.3 Performance

Image optimization merupakan requirement wajib.

Waktu muat halaman harus tetap optimal terutama pada:

* Halaman dengan banyak gambar.
* Katalog Kaizen Company.
* Daftar kepengurusan.
* Galeri.

---

# 3. SEO & Discoverability

Website harus memiliki SEO dasar yang mencakup:

* Meta Title.
* Meta Description.
* Meta tags yang relevan.

## Open Graph

Open Graph digunakan untuk meningkatkan tampilan ketika URL dibagikan melalui platform seperti WhatsApp.

Contoh konten yang perlu mendukung OG:

* Halaman website.
* Berita.
* Produk Kaizen Company.

---

# 4. Analytics & Monitoring

## 4.1 Basic Analytics

Sistem direncanakan memiliki tracking dasar untuk mengetahui:

* Trafik pengunjung.
* Halaman yang paling populer.

Platform analytics masih merupakan **Open Decision**.

Alternatif yang disebutkan:

* Google Analytics.
* Platform analytics ringan lainnya.
* Vercel Analytics.

## 4.2 Error Tracking

Sistem perlu memiliki mekanisme untuk mendeteksi error atau crash pada production.

Platform yang memungkinkan masih merupakan Open Decision.

Alternatif yang disebutkan:

* Sentry.
* Platform monitoring dari hosting provider.
* Tools sejenis.

---

# 5. Security Considerations

## 5.1 Admin Dashboard

Dashboard Admin:

* Tidak boleh terindeks oleh search engine.
* Harus memiliki mekanisme autentikasi.
* Hanya dapat diakses oleh Super Admin.

Metode autentikasi masih menjadi **Open Decision**.

## 5.2 Aspirasi Mahasiswa

Karena Aspirasi bersifat anonim dan tidak menggunakan login, sistem harus memiliki perlindungan terhadap spam.

Minimum consideration:

* Rate limiting.
* Proteksi bot seperti reCAPTCHA atau mekanisme sejenis.

## 5.3 Web Application Security

Sistem harus memiliki perlindungan terhadap serangan web dasar, termasuk:

* XSS.
* CSRF.
* SQL Injection.
* NoSQL Injection apabila teknologi tersebut digunakan.

---

# 6. Backup & Data Reliability

## 6.1 Database Backup

Database utama harus memiliki mekanisme backup berkala.

Tujuannya adalah mengurangi risiko kehilangan data akibat:

* Kesalahan sistem.
* Kesalahan pengelolaan data.
* Gangguan infrastructure.
* Perubahan atau penghapusan data yang tidak disengaja.

## 6.2 Manual Data Export

Dashboard Admin direncanakan menyediakan export data, khususnya:

> **CSV Export untuk Aspirasi**

Export CSV dapat menjadi lapisan backup manual tambahan.

---

# 7. Accessibility Considerations

## 7.1 Color Contrast

Kontras warna harus memadai untuk memastikan konten dapat dibaca dengan baik.

Perhatian khusus diperlukan pada transisi:

```text
Website Organisasi
Light Theme
       ↓
Kaizen Company
Dark Theme
```

## 7.2 Alternative Text

Semua gambar penting harus memiliki alt text yang sesuai.

Contoh:

* Logo organisasi.
* Foto pengurus.
* Foto alumni.
* Foto produk Kaizen Company.

---

# 8. Performance Considerations

## 8.1 CDN

Gambar sebaiknya disajikan melalui CDN yang tersedia dari infrastructure yang digunakan.

Contoh sumber:

* CDN hosting frontend.
* Supabase Storage/CDN.
* Infrastruktur sejenis.

## 8.2 Lazy Loading

Lazy loading perlu diterapkan terutama pada:

* Galeri produk.
* Daftar kepengurusan.
* Konten visual dalam jumlah besar.

Tujuannya untuk mengurangi initial page load.

---

# 9. Scalability Considerations

## 9.1 Frontend Architecture

Frontend diarahkan menggunakan framework modern yang mudah dikembangkan dan di-scale.

Alternatif yang masih terbuka:

* Next.js.
* Nuxt.

Pemilihan framework merupakan **Open Decision** dan akan ditentukan pada Technical Specification.

## 9.2 Database Structure

Struktur database harus dirancang agar tetap dapat digunakan ketika terjadi pergantian periode kepengurusan.

Pergantian pengurus tidak boleh menyebabkan struktur sistem harus dibangun ulang dari awal.

---

# 10. Constraints

## 10.1 Technology Constraint

Penggunaan:

> **PHP / Laravel**

tidak diperbolehkan untuk project ini.

## 10.2 Domain Constraint

Target domain:

> **`.org.id`**

Pemilihan domain mempertimbangkan efisiensi biaya dan identitas organisasi.

## 10.3 Storage Constraint

Storage difokuskan pada:

* Image.
* Format WebP.

Tidak terdapat sistem local video hosting pada V1.

## 10.4 Product Complexity Constraint

V1 harus tetap sederhana dan tidak berkembang menjadi platform e-commerce kompleks.

Tidak termasuk:

* Shopping Cart.
* Payment Gateway.
* User Account.
* Transaksi on-site.

---

# 11. Assumptions

## 11.1 WhatsApp Availability

Diasumsikan pengguna yang berinteraksi dengan Kaizen Company memiliki akses ke:

* WhatsApp Mobile, atau
* WhatsApp Web.

## 11.2 PWMU as Article Source

Diasumsikan artikel kegiatan lengkap telah tersedia di PWMU.

Website PK IMM Kaizen berfungsi sebagai:

> **Direktori / gateway menuju artikel PWMU**

bukan sebagai sistem publikasi ulang artikel secara penuh.

## 11.3 Content Availability

Diasumsikan organisasi dapat menyediakan data yang diperlukan untuk mengisi konten website, khususnya:

* Data kepengurusan.
* Data bidang.
* Data alumni.
* Data Ekowir.
* Data produk.
* Informasi kontak.
* Referensi berita.

Jika data belum tersedia, konten dapat ditandai:

```text
[Content Required]
```

---

# 12. Dependencies

## 12.1 PWMU

Website bergantung pada ketersediaan artikel di PWMU untuk konten berita.

Ketergantungan ini mencakup:

* Ketersediaan artikel.
* Validitas link.
* Aksesibilitas halaman PWMU.

## 12.2 Supabase

Apabila Supabase digunakan, sistem akan bergantung pada:

* Database uptime.
* Storage availability.
* Infrastruktur Supabase.

## 12.3 Organization Data

Website bergantung pada organisasi untuk menyediakan data dan dokumen yang diperlukan.

Sumber utama yang disebutkan:

> Sekretaris / Organisasi

---

# 13. Risks & Mitigations

## 13.1 Single Super Admin Dependency

### Risk

Ketergantungan terhadap satu Super Admin, terutama apabila Super Admin saat ini adalah developer.

Hal ini dapat menyebabkan kesulitan operasional ketika terjadi pergantian kepengurusan.

### Mitigation

* Dokumentasi operasional.
* Dokumentasi penggunaan Dashboard.
* Handover plan.
* Penggunaan akun organisasi.
* Repository berada pada GitHub Organization.

---

## 13.2 Aspirasi Spam

### Risk

Aspirasi bersifat anonim sehingga berpotensi disalahgunakan untuk:

* Spam.
* Bot submission.
* Flood request.

### Mitigation

Implementasi perlindungan seperti:

* Rate limiter.
* reCAPTCHA.
* Mekanisme anti-bot sejenis.

Tanpa mewajibkan login kepada pengguna.

---

## 13.3 PWMU Broken Link

### Risk

Artikel PWMU dapat:

* Dihapus.
* Dipindahkan.
* Mengalami perubahan URL.
* Tidak dapat diakses.

### Mitigation

Tidak terdapat mitigasi teknis otomatis yang ditetapkan pada tahap Product Discovery.

Super Admin dapat:

1. Memeriksa link.
2. Menghapus atau memperbarui direktori berita apabila link terbukti tidak valid.

---

# 14. Open Decisions / TBD

Keputusan berikut belum difinalisasi pada Product Discovery dan ditunda ke tahap Technical Specification.

## 14.1 Super Admin Authentication

Pilihan yang masih terbuka:

* Magic Link.
* Email/Password standard.
* Metode autentikasi lain yang sesuai.

## 14.2 PWMU Integration

Masih perlu diputuskan apakah berita dikelola melalui:

* Manual CRUD oleh Super Admin.
* RSS Feed.
* Scraping.
* Mekanisme integrasi lainnya.

V1 tetap dapat berjalan dengan pendekatan manual.

## 14.3 Frontend Framework

Pilihan:

* Next.js.
* Nuxt.

## 14.4 Hosting & Domain Provider

Vendor spesifik belum ditentukan.

## 14.5 Analytics & Monitoring

Platform belum ditentukan.

Alternatif:

* Google Analytics.
* Sentry.
* Vercel Analytics.
* Tools sejenis.

## 14.6 Handover Ownership

Masih perlu ditentukan secara teknis dan administratif:

* Kepemilikan GitHub Organization.
* Kepemilikan domain.
* Kepemilikan hosting.
* Kepemilikan database.
* Billing cloud infrastructure.
* Akun email organisasi yang digunakan untuk layanan pihak ketiga.

---

# 15. Handover & Maintainability

Sistem harus dirancang agar dapat diwariskan kepada kepengurusan periode berikutnya.

## 15.1 Repository Ownership

Dokumentasi dan source code harus berada pada:

> **GitHub Organization**

bukan akun personal developer.

## 15.2 Operational Guide

Harus tersedia panduan khusus untuk pengurus non-teknis:

> **Cara Mengubah Data Web**

Panduan tersebut harus membantu pengurus melakukan perubahan konten melalui Dashboard tanpa perlu memahami source code.

## 15.3 Organization Account

Layanan pihak ketiga sebaiknya menggunakan akun/email organisasi terpusat.

Contoh:

```text
admin@kaizen.org.id
```

Digunakan untuk layanan seperti:

* Supabase.
* Hosting.
* Domain.
* Infrastruktur cloud lainnya.

Tujuannya adalah mencegah hilangnya akses ketika developer berganti atau demisioner.

---

# 16. Product Discovery Conclusion

Product Discovery ini menetapkan batasan, kebutuhan, dan pertimbangan utama untuk Website Resmi PK IMM Kaizen V1.0.

Produk diposisikan sebagai:

```text
Official Organization Website
        +
Kaizen Company Showcase
        +
Anonymous Aspiration Channel
        +
Centralized Super Admin Dashboard
```

Produk **bukan**:

```text
E-Commerce Platform
        atau
Community Platform
```

Batasan tersebut menjadi prinsip utama agar V1 tetap:

* Sederhana.
* Efisien.
* Maintainable.
* Mudah di-handover.
* Tidak over-engineered.

Seluruh keputusan teknis yang masih terbuka akan dibahas pada tahap **Technical Specification** tanpa mengubah batasan produk yang telah ditetapkan pada Product Discovery.

Dengan selesainya Product Discovery, tahap berikutnya adalah penyusunan:

> **Product Requirement Document (PRD)**

PRD akan menerjemahkan hasil Product Discovery menjadi requirement produk yang lebih terstruktur dan menjadi dasar bagi dokumen teknis berikutnya.

---

# Product Discovery Navigation

* [← Product Discovery Scope](./02-product-discovery-scope.md)
* [Next: Product Requirement Document →](../requirements/prd-pk-imm-kaizen-v1.md)
