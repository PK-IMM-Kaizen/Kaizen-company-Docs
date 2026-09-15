# Product Discovery — PK IMM Kaizen

> Product Discovery untuk **Website Resmi PK IMM Kaizen** sebagai dasar untuk memahami masalah, tujuan, scope, constraint, risiko, keputusan, dan arah produk sebelum diterjemahkan ke Product Requirement Document (PRD).

---

## 📋 Document Information

| Field | Value |
|---|---|
| Product | Website Resmi PK IMM Kaizen |
| Organization | Pimpinan Komisariat Ikatan Mahasiswa Muhammadiyah Kaizen Universitas Muhammadiyah Surabaya |
| Document Type | Product Discovery |
| Version | 1.0 |
| Status | Draft — Approved for Technical Planning |
| Stage | Product Discovery |
| Next Stage | Product Requirement Document |
| Last Updated | September 2026 |

---

# 🎯 Purpose

Product Discovery ini digunakan untuk mendokumentasikan pemahaman awal dan keputusan produk sebelum masuk ke tahap Product Requirement Document.

Dokumen ini menjadi dasar untuk memahami:

- masalah yang ingin diselesaikan;
- tujuan produk;
- target pengguna;
- kebutuhan utama;
- product scope;
- information architecture;
- fitur utama;
- business rules tingkat produk;
- constraints;
- dependencies;
- risks;
- open decisions;
- V1 prioritization;
- success metrics;
- handover requirements.

Product Discovery berfungsi sebagai **product-level foundation** dan bukan sebagai spesifikasi teknis implementasi.

---

# 🧭 Product Discovery Structure

Product Discovery dibagi menjadi beberapa dokumen agar informasi dapat dipelihara secara terstruktur.

| No. | Document | Description |
|---|---|---|
| 01 | [Product Discovery Overview](./01-product-discovery-overview.md) | Product context, problem, vision, goals, users, value proposition, success metrics, dan product direction |
| 02 | [Product Discovery Scope](./02-product-discovery-scope.md) | Product scope, information architecture, navigation, feature scope, V1 boundary, dan scope principles |
| 03 | [Product Discovery Constraints](./03-product-discovery-constraints.md) | Constraints, dependencies, risks, security considerations, scalability, ownership, handover, dan open decisions |

---

# 🗺️ Discovery Flow

Dokumen Product Discovery dibaca melalui alur berikut:

    01 — Overview
          ↓
    02 — Scope
          ↓
    03 — Constraints
          ↓
    Product Requirement Document

---

# 📖 Product Discovery Overview

Dokumen Overview menjelaskan konteks dasar produk dan alasan produk ini dibangun.

Fokus utama meliputi:

- identitas produk;
- organisasi;
- product context;
- problem statement;
- product vision;
- product goals;
- target users;
- user needs;
- value proposition;
- success metrics;
- product direction.

Dokumen:

[01 — Product Discovery Overview](./01-product-discovery-overview.md)

---

# 📐 Product Discovery Scope

Dokumen Scope mendefinisikan batasan produk dari sisi fungsi dan pengalaman pengguna.

Fokus utama meliputi:

- product scope;
- scope boundary;
- information architecture;
- navigation structure;
- public website;
- admin dashboard;
- theme scope;
- content scope;
- V1 scope;
- scope principles.

Dokumen:

[02 — Product Discovery Scope](./02-product-discovery-scope.md)

---

# ⚙️ Product Discovery Constraints

Dokumen Constraints mendokumentasikan kondisi yang membatasi atau memengaruhi keputusan produk.

Fokus utama meliputi:

- technical constraints;
- product constraints;
- media constraints;
- infrastructure dependencies;
- external dependencies;
- security considerations;
- scalability;
- risks;
- ownership;
- handover;
- open decisions.

Dokumen:

[03 — Product Discovery Constraints](./03-product-discovery-constraints.md)

---

# 🎯 Product Direction

Website Resmi PK IMM Kaizen diarahkan sebagai **official digital face** organisasi.

Produk tidak hanya berfungsi sebagai company profile sederhana, tetapi menjadi platform publik yang menyediakan:

1. identitas resmi organisasi;
2. informasi organisasi;
3. struktur kepengurusan;
4. informasi bidang;
5. berita dan dokumentasi;
6. alumni showcase;
7. Ekowir;
8. Kaizen Company;
9. kanal Aspirasi Mahasiswa;
10. konten Kajian & Pemikiran apabila disetujui untuk V1;
11. kanal komunikasi publik.

---

# 🧩 Core Product Priorities

Product Discovery mengidentifikasi beberapa prioritas utama.

## 1. Official Digital Presence

Website harus menjadi representasi digital resmi organisasi.

Tujuan utamanya adalah menyediakan sumber informasi yang terstruktur, profesional, dan dapat diakses publik.

---

## 2. Kaizen Company

Kaizen Company menjadi salah satu prioritas utama produk sebagai bagian dari Ekowir.

Platform menyediakan:

- katalog produk/layanan;
- informasi produk;
- status aktif/inaktif;
- detail produk;
- CTA WhatsApp.

V1 tidak mencakup:

- shopping cart;
- checkout;
- payment gateway;
- transaksi internal website.

---

## 3. Anonymous Student Aspiration

Platform menyediakan kanal aspirasi yang dapat digunakan tanpa login dan tanpa memberikan identitas pribadi.

Prinsip utama:

- anonymous;
- text-based;
- public submission;
- tidak membutuhkan akun;
- tidak menyediakan public tracking;
- dapat dikelola oleh Super Admin.

---

## 4. Centralized Super Admin Management

Seluruh data dinamis dikelola melalui dashboard terpusat.

Pada V1 hanya terdapat:

> **Super Admin**

Super Admin menjadi pengelola utama terhadap:

- konten;
- gambar;
- produk;
- data organisasi;
- aspirasi;
- status publikasi;
- data lain yang termasuk dalam scope.

---

# 🧭 Information Architecture

Struktur navigasi utama yang telah ditetapkan:

    Beranda
    Profil
    Kepengurusan
    Bidang
    Berita
    Ekowir
    Alumni
    Kontak

Fitur tambahan:

    Beranda
      ├── FAQ
      │     └── Aspirasi Mahasiswa
      │
      └── Kajian & Pemikiran
            └── Detail Kajian

Kaizen Company diakses melalui:

    Special CTA
         ↓
    Kaizen Company

Kaizen Company tidak menjadi item utama pada navbar utama.

---

# 🎨 Theme Direction

Produk menggunakan dua pendekatan visual utama.

## Main Website

Menggunakan:

> **Light Theme**

Tujuan:

- official;
- clean;
- professional;
- readable;
- approachable.

---

## Kaizen Company

Menggunakan:

> **Dark Theme**

Tujuan:

- memberikan identitas visual berbeda;
- memperkuat positioning Kaizen Company;
- memberikan pengalaman yang lebih distinctive.

---

# 🏗️ Product Scope

## In Scope

### Public Website

- Beranda;
- Profil;
- Kepengurusan;
- Bidang;
- Berita;
- Ekowir;
- Alumni;
- Kontak;
- Kaizen Company;
- Aspirasi Mahasiswa;
- Kajian & Pemikiran apabila disetujui untuk V1.

### Admin

- Super Admin authentication;
- dashboard;
- content CRUD;
- image upload;
- status management;
- aspiration management.

---

# 🚫 Out of Scope

Fitur berikut tidak menjadi bagian dari V1:

- payment gateway;
- shopping cart;
- checkout;
- public user accounts;
- event calendar;
- full alumni directory;
- forum;
- public comments;
- public aspiration tracking;
- full duplication of PWMU articles;
- multi-role authentication.

---

# 🔐 Core Product Rules

Beberapa aturan utama yang telah ditetapkan:

| Rule | Description |
|---|---|
| Single Admin | V1 menggunakan satu role Super Admin |
| Anonymous Aspiration | Aspirasi tidak memerlukan identitas pengguna |
| No Public Tracking | Pengguna tidak dapat melacak aspirasi melalui sistem publik |
| No Internal Payment | Tidak ada payment gateway atau checkout |
| WhatsApp Transaction | Komunikasi/transaksi Kaizen Company diarahkan melalui WhatsApp |
| Content Visibility | Konten dapat diaktifkan/nonaktifkan atau publish/draft |
| Historical Data | Perubahan visibility tidak otomatis menghapus data historis |
| PWMU Redirect | Berita PWMU diarahkan ke sumber artikel asli |
| Kaizen Company | Kaizen Company merupakan bagian dari Ekowir |

---

# 📊 V1 Prioritization

## Must Have

- Beranda;
- Profil;
- Kepengurusan;
- Bidang;
- Berita;
- Alumni Showcase;
- Kontak;
- Kaizen Company;
- Aspirasi Mahasiswa;
- Super Admin Dashboard.

## Should Have

- PWMU integration enhancement;
- SEO & Open Graph;
- CSV export.

## Could Have

- Admin Analytics Summary.

## Future

- Shopping Cart;
- Payment Gateway;
- User Accounts;
- Event Calendar;
- Full Alumni Directory;
- Automatic PWMU Synchronization.

## Open Decision

- Kajian & Pemikiran V1 priority;
- author attribution;
- approval workflow.

---

# ⚠️ Constraints

Product Discovery mengidentifikasi beberapa constraint utama.

## Technical Constraints

- Tidak menggunakan PHP/Laravel.
- Modern frontend stack menjadi arah pengembangan.
- Database harus mampu bertahan terhadap pergantian kepengurusan.
- Image storage menggunakan WebP.
- Tidak melakukan local video hosting.

---

## Domain & Infrastructure Constraints

Target domain:

> `.org.id`

Ownership infrastructure harus diarahkan kepada organisasi dan tidak bergantung pada akun personal developer.

---

## Content Constraints

Data resmi organisasi harus berasal dari sumber yang dapat dipertanggungjawabkan.

Production tidak boleh menggunakan dummy content.

---

## Media Constraints

Image harus:

- dioptimalkan;
- menggunakan WebP;
- memiliki alt text;
- memenuhi validasi ukuran dan ekstensi.

Video tidak disimpan secara lokal pada platform.

---

# 🔗 Dependencies

Produk memiliki beberapa dependency eksternal dan organisasi.

## PWMU

Digunakan sebagai sumber eksternal untuk berita.

Ketergantungan meliputi:

- URL artikel;
- availability artikel;
- kemungkinan perubahan struktur sumber;
- kemungkinan pengembangan integrasi otomatis di masa depan.

---

## Supabase

Digunakan sebagai salah satu dependency yang direncanakan untuk kebutuhan backend/data/infrastructure.

Konfigurasi ownership harus menggunakan account/email organisasi.

---

## Organization Data

Produk bergantung pada data resmi organisasi, termasuk:

- data kepengurusan;
- data bidang;
- data alumni;
- informasi organisasi;
- data Ekowir;
- informasi Kaizen Company.

---

# 🛡️ Security Direction

Product Discovery menetapkan security sebagai bagian penting dari production readiness.

Perlindungan yang dibutuhkan meliputi:

- dashboard access protection;
- XSS protection;
- CSRF protection apabila relevan;
- SQL/NoSQL injection protection;
- rate limiting untuk aspirasi;
- input validation;
- admin noindex;
- data privacy untuk aspirasi anonim.

---

# ⚡ Performance Direction

Performance menjadi bagian dari product quality.

Arah yang ditetapkan:

- lazy loading;
- image optimization;
- CDN;
- optimized assets;
- responsive experience;
- modern frontend architecture.

---

# 📈 Scalability Direction

Produk harus dirancang agar dapat bertahan melewati pergantian kepengurusan.

Scalability tidak hanya berarti kemampuan menangani traffic, tetapi juga:

- maintainability;
- ownership transfer;
- data continuity;
- infrastructure continuity;
- documentation;
- future content expansion.

---

# ⚠️ Product Risks

## Risk 1 — Single Super Admin

Ketergantungan terhadap satu administrator dapat menjadi single point of failure.

### Mitigation Direction

- dokumentasi;
- ownership organisasi;
- handover procedure;
- backup;
- centralized organization account.

---

## Risk 2 — Aspiration Spam

Form anonim berpotensi disalahgunakan.

### Mitigation Direction

- rate limiting;
- input validation;
- anti-spam mechanism;
- admin monitoring.

---

## Risk 3 — PWMU Link Dependency

Perubahan atau kerusakan external URL dapat membuat link berita tidak berfungsi.

### Mitigation Direction

- URL validation;
- periodic checking;
- clear source attribution;
- future automation apabila diperlukan.

---

# 🔄 Ownership & Handover

Handover menjadi requirement penting sejak Product Discovery.

## Repository

Source code diarahkan ke:

> GitHub Organization

Bukan personal repository developer.

---

## Infrastructure

Service penting harus berada pada ownership organisasi, termasuk:

- domain;
- hosting;
- database;
- storage;
- external services;
- billing.

---

## Organization Email

Service utama diarahkan menggunakan centralized organization email.

---

## Documentation

Harus tersedia dokumentasi:

- technical documentation;
- deployment information;
- basic maintenance;
- content management;
- data management;
- non-technical admin guide.

---

# 📈 Success Metrics

Product success tidak hanya diukur dari jumlah fitur.

Indikator keberhasilan utama:

1. Website live dan stabil pada domain `.org.id`.
2. Super Admin dapat mengubah 100% dynamic text/image yang termasuk scope tanpa mengubah source code.
3. CTA WhatsApp berfungsi.
4. Aspirasi anonim dapat dikirim dengan aman.
5. Tidak terdapat critical issue pada launch.
6. Website dapat dipelihara setelah handover.

---

# 🚦 Launch Definition

V1 dianggap siap diluncurkan apabila:

- seluruh Must Have selesai;
- tidak ada dummy content;
- website responsive;
- admin berfungsi penuh;
- security baseline diterapkan;
- aspirasi anonim berfungsi;
- Kaizen Company berfungsi;
- WhatsApp CTA berfungsi;
- data organisasi telah diverifikasi;
- deployment production siap;
- ownership organisasi siap;
- dokumentasi handover tersedia;
- tidak terdapat critical launch issue.

---

# 📌 Open Decisions

Beberapa keputusan masih terbuka dan harus diselesaikan sebelum requirement yang terdampak dikunci.

| ID | Decision | Status |
|---|---|---|
| OD-001 | Apakah Kajian & Pemikiran masuk V1 | Open |
| OD-002 | Model author attribution Kajian | Open |
| OD-003 | Approval workflow Kajian | Open |
| OD-004 | Super Admin authentication method | Open |
| OD-005 | PWMU integration: manual vs RSS/scraping | Open |
| OD-006 | Next.js vs Nuxt | Open |
| OD-007 | Hosting dan domain vendor | Open |
| OD-008 | Analytics dan error tracking tools | Open |
| OD-009 | Handover ownership dan billing | Open |

Keputusan yang bersifat technical implementation tidak boleh dibuat secara sepihak apabila dapat mengubah product scope atau business requirement.

---

# 🧠 Discovery Principles

Product Discovery ini mengikuti prinsip:

1. **Problem before Solution**  
   Masalah dan kebutuhan harus dipahami sebelum solusi teknis ditetapkan.

2. **Scope Control**  
   V1 harus memiliki batas yang jelas.

3. **User Value First**  
   Fitur harus memiliki alasan bisnis atau user value yang jelas.

4. **No Premature Technical Commitment**  
   Detail implementasi teknis tidak dikunci sebelum tahap Technical Specification.

5. **Explicit Decisions**  
   Keputusan yang belum final harus ditandai sebagai Open Decision.

6. **Handover by Design**  
   Sistem dirancang sejak awal agar dapat diteruskan oleh organisasi.

7. **Production Readiness**  
   V1 harus dipandang sebagai produk production-ready, bukan sekadar prototype.

---

# 🔄 Transition to PRD

Setelah Product Discovery selesai, hasil discovery diterjemahkan ke dalam:

> **Product Requirement Document**

PRD akan mendefinisikan secara lebih detail:

- product requirements;
- user journeys;
- functional requirements;
- business rules;
- module requirements;
- non-functional requirements;
- acceptance criteria;
- prioritization;
- release readiness.

Product Discovery menjawab:

> **Mengapa produk ini dibangun, masalah apa yang diselesaikan, siapa penggunanya, dan apa batasannya?**

PRD menjawab:

> **Apa yang harus dibangun agar tujuan tersebut dapat dicapai?**

---

# 🗺️ Documentation Lifecycle

Keseluruhan alur dokumentasi produk:

    Product Discovery
           ↓
    Product Requirement Document
           ↓
    Technical Specification
           ↓
        SDS / SRS
           ↓
       Development
           ↓
    Testing & Validation
           ↓
       Production
           ↓
    Maintenance & Handover

---

# 📚 Related Documentation

## Product Discovery

- [01 — Product Discovery Overview](./01-product-discovery-overview.md)
- [02 — Product Discovery Scope](./02-product-discovery-scope.md)
- [03 — Product Discovery Constraints](./03-product-discovery-constraints.md)

## Next Stage

- [Product Requirement Document](../prd/README.md)

---

# ✅ Final Status

| Item | Status |
|---|---|
| Product Context | Defined |
| Problem Statement | Defined |
| Product Vision | Defined |
| Product Goals | Defined |
| Target Users | Defined |
| Product Scope | Defined |
| Information Architecture | Defined |
| V1 Boundary | Defined |
| Constraints | Defined |
| Dependencies | Defined |
| Risks | Identified |
| Success Metrics | Defined |
| Handover Direction | Defined |
| Open Decisions | Identified |
| Next Stage | Product Requirement Document |

---

## Navigation

- [← Previous Stage — Project Documentation](../../README.md)
- [Product Discovery Overview →](./01-product-discovery-overview.md)
- [Product Discovery Scope](./02-product-discovery-scope.md)
- [Product Discovery Constraints](./03-product-discovery-constraints.md)
- [Next Stage — Product Requirement Document →](../prd/README.md)
