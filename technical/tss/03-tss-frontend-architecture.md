# Technical Specification — Frontend Architecture

> Definisi arsitektur frontend untuk Website Resmi PK IMM Kaizen V1.1 Revised.

---

# 1. Frontend Architecture

## 1.1 Architecture Approach

Frontend menggunakan pendekatan:

> **Component-Based UI**

Antarmuka dibangun menggunakan komponen yang dapat digunakan kembali untuk menjaga:

- konsistensi;
- maintainability;
- scalability;
- kemudahan pengembangan;
- kemudahan handover.

Frontend menjadi bagian dari full-stack application dan berada dalam codebase yang sama dengan backend/API layer.

---

# 2. Rendering Strategy

## 2.1 Public Website

Untuk halaman publik, penggunaan:

- SSR (Server-Side Rendering);
- SSG (Static Site Generation);
- ISR (Incremental Static Regeneration);

sangat direkomendasikan untuk kebutuhan SEO.

Status:

> **RECOMMENDED**

---

## 2.2 Kajian & Pemikiran

Halaman Kajian menjadi salah satu bagian yang membutuhkan perhatian khusus terhadap rendering karena setiap Kajian memiliki:

- URL dinamis;
- slug unik;
- content body;
- metadata SEO;
- Open Graph metadata.

Rendering strategy harus mendukung pengambilan content berdasarkan slug dan menghasilkan halaman yang dapat diindeks oleh search engine ketika status content adalah Published.

SSR atau SSG/ISR direkomendasikan terutama untuk halaman detail Kajian.

---

# 3. Application Layout Architecture

Frontend menggunakan beberapa layout berdasarkan area aplikasi.

## 3.1 LightLayout

`LightLayout` digunakan untuk halaman utama organisasi.

Cakupan:

- Beranda;
- Profil;
- Kepengurusan;
- Bidang;
- Berita;
- Ekowir;
- Alumni;
- Kontak;
- Kajian & Pemikiran.

Status:

> **REQUIRED**

---

## 3.2 DarkLayout

`DarkLayout` digunakan khusus untuk area:

> **Kaizen Company**

Layout ini menjadi boundary visual untuk katalog produk dan layanan Kaizen Company.

Status:

> **REQUIRED**

---

## 3.3 AdminLayout

`AdminLayout` digunakan khusus untuk:

> **Super Admin Dashboard**

Area ini terpisah dari public website dan membutuhkan authentication yang valid.

Status:

> **REQUIRED**

---

# 4. Layout Separation

Struktur layout frontend secara konseptual:

    Web Application
    |
    +-- Public Area
    |   |
    |   +-- LightLayout
    |       |
    |       +-- Beranda
    |       +-- Profil
    |       +-- Kepengurusan
    |       +-- Bidang
    |       +-- Berita
    |       +-- Ekowir
    |       +-- Alumni
    |       +-- Kontak
    |       +-- Kajian
    |
    +-- Kaizen Company
    |   |
    |   +-- DarkLayout
    |       |
    |       +-- Catalog
    |       +-- Product Detail
    |
    +-- Admin Area
        |
        +-- AdminLayout
            |
            +-- Super Admin Dashboard

Pemisahan layout digunakan untuk menjaga perbedaan konteks antara:

- website organisasi;
- Kaizen Company;
- sistem administrasi.

---

# 5. Dynamic Routing

## 5.1 Kajian Detail Route

Frontend harus menyediakan dynamic route untuk halaman detail Kajian.

Contoh:

`/kajian/[slug]`

Route bertugas:

1. menerima parameter `slug`;
2. mengambil data Kajian berdasarkan slug;
3. memeriksa status content;
4. menampilkan halaman detail jika content valid;
5. mengembalikan `404 Not Found` jika content tidak ditemukan;
6. mengembalikan `404 Not Found` jika content berstatus Draft;
7. mengembalikan `404 Not Found` jika content berstatus Unpublished.

Status:

> **REQUIRED**

---

## 5.2 Slug Requirement

Setiap Kajian harus memiliki slug yang unik.

Slug digunakan sebagai identifier pada public URL.

Contoh konseptual:

`/kajian/strategi-gerakan-mahasiswa`

Frontend tidak boleh menganggap slug yang tidak ditemukan sebagai content yang valid.

---

# 6. Kajian Content Rendering

## 6.1 Rich Text Rendering

Frontend membutuhkan komponen khusus untuk melakukan rendering body Kajian.

Contoh pendekatan:

- `RichTextRenderer`;
- `MarkdownRenderer`.

Komponen tersebut harus mampu menampilkan content secara aman.

Status:

> **REQUIRED**

---

## 6.2 Security Boundary

Content Kajian tidak boleh dirender dengan cara yang memungkinkan script berbahaya dieksekusi di browser.

Frontend harus memastikan bahwa rich-text content telah melalui mekanisme sanitization yang sesuai sebelum menghasilkan output ke DOM.

Tujuan utama:

> mencegah script execution dan XSS pada halaman publik.

Detail security dan sanitization architecture dibahas pada:

`06-tss-api-security-and-media.md`

---

# 7. State Management & Data Fetching

Frontend harus menangani kondisi data secara eksplisit.

Minimal terdapat tiga kondisi utama:

## 7.1 Loading State

Digunakan ketika frontend sedang:

- mengambil data;
- menunggu API response;
- memuat content.

---

## 7.2 Error State

Digunakan ketika terjadi kegagalan seperti:

- API failure;
- network error;
- server error;
- content retrieval failure.

Frontend harus menampilkan feedback yang sesuai kepada pengguna tanpa mengekspos informasi internal sistem.

---

## 7.3 Empty State

Digunakan ketika request berhasil tetapi tidak terdapat content yang dapat ditampilkan.

Contoh:

- belum ada Kajian Published;
- belum ada produk aktif;
- belum ada data content tertentu.

Untuk content yang bersifat wajib tersedia, frontend dapat menggunakan state:

> **Content Required**

Status handling:

> **REQUIRED**

---

# 8. Data Fetching Principles

Frontend mengambil data melalui application/API layer.

Secara konseptual:

    Frontend Component
            |
            v
      Data Fetching
            |
            v
       API / App Layer
            |
            v
         Database
            |
            v
        API Response
            |
            v
      Frontend State
            |
            v
      Rendered Content

Frontend tidak boleh bergantung pada data hardcoded untuk content yang telah ditetapkan sebagai dynamic content.

---

# 9. Public Content Visibility

Frontend hanya boleh menampilkan content yang memang tersedia untuk public.

Khusus Kajian:

| Content Status | Public Frontend |
|---|---|
| Draft | Tidak ditampilkan |
| Published | Ditampilkan |
| Unpublished | Tidak ditampilkan |
| Tidak ditemukan | 404 |

Frontend tidak boleh melakukan fallback ke Draft atau Unpublished content ketika public request menggunakan slug tertentu.

---

# 10. Image Optimization

Frontend harus menggunakan mekanisme image optimization yang tersedia pada framework.

Tujuan:

- mengurangi ukuran asset;
- meningkatkan loading performance;
- mendukung lazy loading;
- mendukung WebP;
- mengoptimalkan pengalaman pengguna.

Status:

> **REQUIRED**

---

# 11. Image Usage

Image optimization diterapkan terutama pada:

- foto pengurus;
- gambar produk;
- thumbnail Kajian;
- image content lainnya.

Framework image component direkomendasikan digunakan dibandingkan melakukan rendering image tanpa optimization.

---

# 12. Lazy Loading

Image yang tidak berada pada area awal viewport harus dapat menggunakan lazy loading sesuai kemampuan framework.

Contoh target:

- management photos;
- product catalog images;
- Kajian thumbnails.

Tujuannya adalah mengurangi initial page load dan membantu optimasi performance.

---

# 13. Frontend Component Responsibility

Komponen frontend harus memiliki responsibility yang jelas.

Secara konseptual:

| Component Area | Responsibility |
|---|---|
| Layout | Struktur halaman dan visual context |
| Navigation | Navigasi antar halaman |
| Content Component | Menampilkan dynamic content |
| Rich Text Renderer | Merender body Kajian secara aman |
| Image Component | Rendering image teroptimasi |
| Form Component | Input dan submission pengguna |
| State Component | Loading, error, dan empty state |

Detail visual component seperti:

- warna;
- typography;
- spacing;
- visual hierarchy;
- design tokens;
- interaction design;

tidak didefinisikan dalam TSS ini.

Detail tersebut menjadi bagian dari:

> **UI/UX Specification**

---

# 14. Frontend Error Handling

Frontend harus menyediakan handling untuk kondisi umum berikut:

- page not found;
- invalid Kajian slug;
- unavailable content;
- API failure;
- server error;
- network failure.

Minimal terdapat:

- `404 Not Found`;
- `500 Error`;
- loading state;
- error state;
- empty state.

---

# 15. Kajian Page Flow

Alur halaman Kajian:

    Beranda
       |
       v
    Kajian Section
       |
       v
    Kajian Card
       |
       v
    "Baca Selengkapnya"
       |
       v
    /kajian/[slug]
       |
       v
    Fetch Kajian
       |
       +-------------------+
       |                   |
       v                   v
    Published        Draft/Unpublished
       |                   |
       v                   v
    Render Detail        404
       |
       v
    Rich Text Renderer
       |
       v
    Public Content

---

# 16. Frontend Architecture Boundaries

Frontend architecture memiliki batas tanggung jawab sebagai berikut:

### Frontend Responsible For

- page rendering;
- component rendering;
- routing;
- layout;
- client interaction;
- data fetching;
- loading/error/empty state;
- image optimization;
- safe content rendering.

### Frontend Not Responsible For

- database schema definition;
- database migration;
- persistent data storage;
- server-side authorization;
- API contract definition;
- final authentication provider configuration;
- detailed visual design specification.

Responsibility tersebut berada pada layer atau dokumen teknis masing-masing.

---

# 17. Relationship With Backend Architecture

Frontend berkomunikasi dengan Backend/Application Layer melalui API atau application interface yang disediakan oleh full-stack framework.

Konseptual flow:

    User Interaction
          |
          v
    Frontend Component
          |
          v
    API Request
          |
          v
    Backend / Application Layer
          |
          v
    Validation & Business Logic
          |
          v
    Database
          |
          v
    API Response
          |
          v
    Frontend State
          |
          v
    UI Rendering

Detail middleware, validation, authentication, dan business logic berada pada Backend/Application Architecture.

---

# 18. Frontend Architecture Constraints

Frontend V1 harus mempertahankan batasan berikut:

- menggunakan component-based architecture;
- public website menggunakan LightLayout;
- Kaizen Company menggunakan DarkLayout;
- Super Admin menggunakan AdminLayout;
- Kajian menggunakan dynamic routing;
- Draft/Unpublished Kajian tidak boleh tersedia pada public route;
- rich-text harus dirender secara aman;
- loading, error, dan empty state harus ditangani;
- image harus dioptimalkan;
- WebP digunakan sebagai format image;
- frontend tidak mengimplementasikan transaksi pembayaran Kaizen Company;
- frontend tidak mengubah batasan business rules yang telah ditetapkan PRD.

---

# 19. Frontend Technical Decisions

| Decision | Direction | Status |
|---|---|---|
| UI Architecture | Component-Based | Required |
| Public Layout | LightLayout | Required |
| Kaizen Company Layout | DarkLayout | Required |
| Admin Layout | AdminLayout | Required |
| Kajian Routing | `/kajian/[slug]` | Required |
| Rich Text Renderer | Dedicated Safe Renderer | Required |
| Rendering Strategy | SSR / SSG / ISR | Recommended |
| Image Optimization | Framework Image Optimization | Required |
| Image Format | WebP | Required |
| Data States | Loading / Error / Empty | Required |
| Final Framework | Next.js / Nuxt.js | Open Decision |

---

# 20. Frontend Readiness

Frontend architecture telah memiliki baseline teknis untuk dilanjutkan ke:

- backend/application architecture;
- database architecture;
- API specification;
- UI/UX specification.

Detail implementasi frontend dapat dilakukan setelah keputusan framework dan technical contract yang diperlukan telah ditetapkan.

---

## Navigation

- [← TSS System Architecture](./02-tss-system-architecture.md)
- [TSS Backend & Database Architecture →](./04-tss-backend-and-database-architecture.md)
