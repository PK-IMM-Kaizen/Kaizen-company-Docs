# Product Requirement Document — Non-Functional Requirements

> Website Resmi PK IMM Kaizen V1.0

---

# 1. Non-Functional Requirements

Non-Functional Requirements (NFR) mendefinisikan kualitas, batasan teknis, keamanan, performa, aksesibilitas, dan karakteristik operasional yang harus dipenuhi oleh Website Resmi PK IMM Kaizen V1.

---

# 2. NFR-001 — Design & Visual Quality

Website harus memiliki tampilan yang:

- Modern.
- Minimalistic.
- Profesional.
- Konsisten dengan identitas PK IMM Kaizen.
- Responsif pada berbagai ukuran layar.

### Typography

Font utama yang digunakan:

> **Plus Jakarta Sans**

### Theme

Website utama:

> **Light Theme**

Kaizen Company:

> **Dark Theme**

---

# 3. NFR-002 — Responsive Design

Website harus dapat digunakan pada berbagai ukuran perangkat.

### Target

- Desktop
- Laptop
- Tablet
- Mobile

### Requirements

- Layout harus menyesuaikan ukuran viewport.
- Navigasi harus tetap dapat digunakan pada layar kecil.
- Konten tidak boleh mengalami overflow yang mengganggu.
- Gambar dan media harus menyesuaikan container.

---

# 4. NFR-003 — Image Optimization

Sistem harus mengoptimalkan penggunaan gambar untuk menjaga performa website.

### Requirements

- Format gambar utama: WebP.
- Gambar harus divalidasi sebelum upload.
- Ukuran file harus divalidasi.
- Gambar harus dioptimasi sebelum atau saat ditampilkan.
- Gambar pada daftar panjang harus mendukung lazy loading.
- Gambar publik harus memiliki alt text.

### Applicable Content

- Kepengurusan
- Berita
- Kajian
- Alumni
- Ekowir
- Kaizen Company
- Galeri atau media lainnya

---

# 5. NFR-004 — Performance

Website harus memiliki waktu loading yang wajar dengan tetap mempertahankan kualitas visual.

### Requirements

- Lazy loading diterapkan pada gambar.
- Lazy loading diterapkan pada daftar panjang apabila diperlukan.
- Aset statis harus dioptimasi.
- Ukuran aset harus diperhatikan untuk mengurangi penggunaan bandwidth.
- CDN dapat digunakan untuk mendukung distribusi aset.

### Target Areas

Optimasi terutama berlaku pada:

- Galeri produk.
- Daftar berita.
- Daftar Kajian.
- Daftar pengurus.
- Media website lainnya.

---

# 6. NFR-005 — Security

Sistem harus menerapkan perlindungan terhadap ancaman keamanan umum.

### Required Protection

Sistem harus mempertimbangkan perlindungan terhadap:

- Cross-Site Scripting (XSS).
- Cross-Site Request Forgery (CSRF).
- SQL Injection.
- NoSQL Injection.
- Unauthorized access.
- Spam atau abuse pada form Aspirasi.

### Input Security

Perhatian khusus diberikan pada:

- Input Aspirasi.
- Content body Kajian.
- Form Dashboard.
- URL eksternal.
- File upload.

---

# 7. NFR-006 — Admin Security

Dashboard Admin harus dilindungi dari akses yang tidak sah.

### Requirements

- Hanya Super Admin yang dapat melakukan login.
- Public user tidak memiliki akses Dashboard.
- Area Dashboard harus menggunakan authentication dan authorization.
- URL Dashboard tidak boleh diindeks oleh search engine.
- Akses langsung ke URL Dashboard tanpa authorization harus ditolak atau diarahkan sesuai mekanisme keamanan yang ditentukan.

### Authentication

Metode authentication spesifik masih berstatus:

> **Open Decision**

Pilihan implementasi akan ditentukan pada Technical Specification.

---

# 8. NFR-007 — Anonymous Aspiration Privacy

Sistem harus mempertahankan karakter anonim pada fitur Aspirasi Mahasiswa.

### Requirements

Form tidak meminta:

- Nama.
- Email.
- Nomor HP.
- Akun pengguna.

### Data

Data yang dibutuhkan untuk fitur Aspirasi:

- Isi aspirasi.
- Timestamp.

### Public Access

Aspirasi tidak boleh:

- Ditampilkan kepada publik.
- Dapat dicari oleh publik.
- Memiliki public tracking.

---

# 9. NFR-008 — Accessibility

Website harus memperhatikan aksesibilitas dasar.

### Requirements

- Kontras warna harus mencukupi.
- Gambar publik harus memiliki alt text.
- Elemen interaktif harus dapat dikenali pengguna.
- Navigasi harus tetap usable pada perangkat dengan ukuran layar berbeda.

---

# 10. NFR-009 — SEO

Halaman publik harus memiliki metadata dasar untuk mendukung discoverability.

### Requirements

Setiap halaman yang relevan harus dapat memiliki:

- Meta Title.
- Meta Description.
- Metadata SEO yang relevan.
- Open Graph tags.

### Kajian

Halaman detail Kajian memiliki kebutuhan khusus untuk Open Graph karena URL Kajian dapat dibagikan melalui:

- WhatsApp.
- Media sosial.
- Platform komunikasi lainnya.

### Admin

Dashboard tidak boleh diindeks oleh search engine.

---

# 11. NFR-010 — External Link Handling

Website menggunakan beberapa layanan eksternal.

### PWMU

Link berita PWMU harus:

- Mengarah ke URL artikel asli.
- Dibuka pada tab baru.

### WhatsApp

CTA Kaizen Company harus:

- Mengarah ke URL WhatsApp.
- Menggunakan URL `wa.me`.
- Dapat membawa template pesan.

---

# 12. NFR-011 — Data Integrity

Sistem harus menjaga konsistensi data yang digunakan oleh website publik.

### Requirements

- Input Dashboard harus divalidasi.
- Required field harus diperiksa.
- Data yang tidak valid tidak boleh disimpan.
- Perubahan status harus tercermin pada visibility publik.
- Data historis yang tidak perlu dihapus harus tetap dapat dipertahankan.

---

# 13. NFR-012 — Content Lifecycle

Sistem harus mendukung lifecycle dasar konten:

~~~text
Draft
  ↓
Publish
  ↓
Unpublish
  ↓
Delete
~~~

### Requirements

- Draft tidak tampil kepada publik.
- Published tampil kepada publik.
- Unpublished tidak tampil kepada publik.
- Delete merupakan tindakan permanen.
- Delete harus memiliki confirmation.

---

# 14. NFR-013 — Error Handling

Sistem harus memberikan feedback yang jelas ketika terjadi kegagalan.

### Error State

Contoh:

- Authentication gagal.
- Input tidak valid.
- Upload gagal.
- Data gagal disimpan.
- URL tidak valid.
- Terjadi kesalahan sistem.

### Success State

Contoh:

- Data berhasil dibuat.
- Data berhasil diperbarui.
- Data berhasil dihapus.
- Status berhasil diperbarui.
- Aspirasi berhasil dikirim.

### UX Requirement

Feedback dapat menggunakan:

- Toast.
- Alert.
- Validation message.
- Confirmation dialog.

---

# 15. NFR-014 — Backup

Database production harus memiliki mekanisme backup berkala.

### Requirements

- Database utama memiliki backup berkala.
- Backup harus dapat digunakan untuk recovery apabila terjadi kehilangan atau kerusakan data.
- Strategi backup teknis akan ditentukan pada tahap Technical Specification.

### Additional Backup

Data Aspirasi memiliki opsi:

> **CSV Export**

CSV dapat digunakan sebagai backup tambahan dan kebutuhan dokumentasi/pengolahan data.

---

# 16. NFR-015 — Handover & Maintainability

Sistem harus dirancang agar dapat diwariskan kepada kepengurusan berikutnya.

### Requirements

- Source code disimpan pada GitHub Organization.
- Dokumentasi teknis disimpan bersama project.
- Dokumentasi non-teknis harus tersedia untuk pengelola.
- Pengelolaan website tidak boleh bergantung sepenuhnya pada developer saat ini.
- Data dan konfigurasi penting harus dapat diteruskan kepada pengurus berikutnya.

### Operational Guide

Harus tersedia panduan:

> **Cara Mengubah Data Web**

Panduan ditujukan untuk pengguna non-teknis.

---

# 17. NFR-016 — Centralized Ownership

Akun layanan pihak ketiga harus menggunakan identitas organisasi.

### Requirements

Akun yang berkaitan dengan production infrastructure sebaiknya menggunakan:

> **Email sentral organisasi**

### Applicable Services

- Hosting.
- Database.
- Domain.
- Storage.
- Layanan pihak ketiga lainnya.

### Purpose

Mengurangi risiko kehilangan akses ketika terjadi pergantian pengurus atau developer.

---

# 18. NFR-017 — Scalability

Sistem harus memiliki struktur yang memungkinkan pengembangan setelah V1 tanpa mengharuskan perubahan total terhadap fondasi sistem.

### Requirements

- Arsitektur frontend menggunakan teknologi modern.
- Pilihan framework berada pada keputusan teknis.
- Kandidat yang disebutkan dalam Product Discovery/PRD adalah Next.js atau Nuxt.
- Database harus dapat bertahan digunakan melewati pergantian periode kepengurusan.
- Struktur data tidak boleh terlalu bergantung pada satu periode kepengurusan.

### Boundary

Scalability V1 berfokus pada maintainability dan keberlanjutan sistem, bukan pada kebutuhan traffic berskala besar.

---

# 19. NFR-018 — Media Storage

### Image

Format utama:

> WebP

### Video

Website V1 tidak menyediakan local video hosting.

Jika video diperlukan, media harus menggunakan layanan eksternal.

---

# 20. NFR-019 — Browser & Device Compatibility

Website harus dapat digunakan pada browser modern dan perangkat yang umum digunakan oleh target pengguna.

### Minimum Expectation

- Desktop browser modern.
- Mobile browser modern.
- Tablet browser modern.

Implementasi detail compatibility matrix ditentukan pada tahap Technical Specification apabila diperlukan.

---

# 21. NFR-020 — Monitoring & Analytics

Website dapat menggunakan basic analytics dan error tracking.

### Analytics

Informasi yang dapat dipantau:

- Traffic website.
- Popularitas halaman.
- Penggunaan fitur utama.

### Error Tracking

Sistem dapat menggunakan mekanisme untuk mendeteksi:

- Runtime error.
- Application error.
- Error pada proses penting.

### Status

Platform analytics dan monitoring masih:

> **Open Decision**

---

# 22. NFR-021 — Domain & Deployment

Target domain production:

> **`.org.id`**

### Requirements

- Domain harus menggunakan identitas resmi organisasi.
- Deployment production harus menggunakan environment yang dapat dikelola organisasi.
- Credential dan billing tidak boleh bergantung pada akun personal developer untuk jangka panjang.

### Open Decision

Masih perlu ditentukan:

- Vendor domain.
- Vendor hosting.
- Infrastruktur deployment.

---

# 23. NFR Summary

| ID | Requirement | Priority |
|---|---|---|
| NFR-001 | Design & Visual Quality | Must Have |
| NFR-002 | Responsive Design | Must Have |
| NFR-003 | Image Optimization | Must Have |
| NFR-004 | Performance | Must Have |
| NFR-005 | Security | Must Have |
| NFR-006 | Admin Security | Must Have |
| NFR-007 | Anonymous Aspiration Privacy | Must Have |
| NFR-008 | Accessibility | Must Have |
| NFR-009 | SEO | Should Have |
| NFR-010 | External Link Handling | Must Have |
| NFR-011 | Data Integrity | Must Have |
| NFR-012 | Content Lifecycle | Must Have |
| NFR-013 | Error Handling | Must Have |
| NFR-014 | Backup | Must Have |
| NFR-015 | Handover & Maintainability | Must Have |
| NFR-016 | Centralized Ownership | Must Have |
| NFR-017 | Scalability | Must Have |
| NFR-018 | Media Storage | Must Have |
| NFR-019 | Browser & Device Compatibility | Must Have |
| NFR-020 | Monitoring & Analytics | Could Have / TBD |
| NFR-021 | Domain & Deployment | Must Have |

---

# 24. Open Technical Decisions

Requirement berikut belum menentukan implementasi teknis final:

| Decision | Status |
|---|---|
| Metode authentication Super Admin | Open Decision |
| Framework frontend: Next.js / Nuxt | Open Decision |
| Hosting provider | Open Decision |
| Domain provider | Open Decision |
| Analytics platform | Open Decision |
| Error tracking platform | Open Decision |
| Mekanisme backup | Technical Decision |
| Mekanisme spam protection Aspirasi | Technical Decision |
| Media storage provider | Technical Decision |

Keputusan teknis tersebut tidak boleh dianggap final hanya berdasarkan PRD.

Detail implementasi harus ditetapkan pada dokumen technical specification.

---

# Navigation

- [← Product Requirement Document — Module Requirements](./06-prd-module-requirements.md)
- [Product Requirement Document — Acceptance & Prioritization →](./08-prd-acceptance-and-prioritization.md)
