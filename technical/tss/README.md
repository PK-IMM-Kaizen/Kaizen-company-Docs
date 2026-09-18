# Technical Specification (TSS)

> **Project:** Website Resmi PK IMM Kaizen V1.0  
> **Document Version:** 1.1 Revised  
> **Status:** Draft — Technical Planning  
> **Stage:** Technical Specification  
> **Audience:** Technical Team / Developer / System Maintainer

---

## 1. Document Information

| Field | Value |
|---|---|
| Product | Website Resmi PK IMM Kaizen |
| Product Version | V1.0 |
| Document | Technical Specification (TSS) |
| Version | 1.1 Revised |
| Status | Draft — Technical Planning |
| Source | PRD — Website Resmi PK IMM Kaizen V1.0 Revised |
| Previous Stage | Product Requirement Document (PRD) |
| Current Stage | Technical Specification (TSS) |
| Next Stage | Database Design & API Specification |

---

# 2. Purpose

Folder ini berisi seluruh dokumen **Technical Specification (TSS)** untuk Website Resmi PK IMM Kaizen V1.0.

TSS berfungsi menerjemahkan:

    PRD
    What + Why
        ↓
    TSS
    How
        ↓
    Database Design
    API Specification
    UI/UX Specification
        ↓
    Development

Technical Specification digunakan sebagai technical baseline sebelum project masuk ke tahap desain database, API, UI/UX, dan development.

---

# 3. TSS Structure

Technical Specification dibagi menjadi beberapa dokumen berdasarkan area teknis.

| No. | Document | Description |
|---|---|---|
| 01 | [TSS Overview](./01-tss-overview.md) | Document information, purpose, dan technical scope |
| 02 | [System Architecture](./02-tss-system-architecture.md) | System architecture dan architecture principles |
| 03 | [Frontend Architecture](./03-tss-frontend-architecture.md) | Frontend structure, layout, routing, rendering, state, dan image optimization |
| 04 | [Backend & Database Architecture](./04-tss-backend-and-database-architecture.md) | Backend architecture, middleware, database architecture, authentication, dan authorization |
| 05 | [Content & Module Architecture](./05-tss-content-and-module-architecture.md) | Content management dan technical architecture setiap module |
| 06 | [API, Security & Media](./06-tss-api-security-and-media.md) | API architecture, security architecture, dan media/file storage |
| 07 | [Deployment, Performance & Handover](./07-tss-deployment-performance-and-handover.md) | Performance, SEO, deployment, backup, monitoring, environment, dan handover |
| 08 | [Decisions, Traceability & Readiness](./08-tss-decisions-traceability-and-readiness.md) | Technical risks, open decisions, traceability, validation, dan readiness |

---

# 4. Technical Documentation Flow

Technical Specification mengikuti alur:

    TSS Overview
          ↓
    System Architecture
          ↓
    Frontend Architecture
          ↓
    Backend & Database Architecture
          ↓
    Content & Module Architecture
          ↓
    API, Security & Media
          ↓
    Deployment, Performance & Handover
          ↓
    Decisions, Traceability & Readiness

Setelah seluruh TSS selesai:

    TSS
     ↓
    Database Design
     +
    API Specification
     ↓
    UI/UX Specification
     ↓
    Development

---

# 5. Technical Scope

Technical Specification mencakup technical planning untuk:

## 5.1 Public Website

Public website mencakup:

- Beranda;
- Profil;
- Kepengurusan;
- Bidang;
- Berita;
- Ekowir;
- Alumni;
- Kontak.

---

## 5.2 Kajian & Pemikiran

Kajian & Pemikiran pada Revised TSS mencakup:

- section Kajian pada homepage;
- standalone detail page;
- dynamic slug;
- native article content;
- CRUD melalui Super Admin;
- Draft;
- Published;
- Unpublished;
- rich text/content rendering;
- SEO metadata.

Route utama:

    /kajian/[slug]

---

## 5.3 Kaizen Company

Kaizen Company mencakup:

- product/service catalog;
- product detail;
- active/inactive status;
- dark theme;
- image;
- price;
- description;
- category;
- stock display;
- WhatsApp CTA.

Tidak terdapat:

- shopping cart;
- checkout;
- payment gateway;
- order management.

---

## 5.4 Aspirasi

Aspirasi mencakup:

- anonymous public submission;
- text-based submission;
- timestamp;
- public form;
- server-side validation;
- rate limiting;
- spam protection;
- Super Admin access.

Aspirasi tidak menyimpan identitas pengirim.

---

## 5.5 Admin Dashboard

Admin menggunakan satu role:

    Super Admin

Dashboard digunakan untuk:

- content management;
- CRUD;
- image upload;
- status management;
- Aspirasi management;
- Kajian management;
- Kaizen Company management;
- organization content management.

Tidak terdapat multi-role authorization pada V1.

---

# 6. System Architecture Summary

Architecture yang digunakan mengikuti pendekatan:

    Monolithic / Full-stack Framework

High-level architecture:

    Public Users
          │
    Super Admin
          │
          ▼
        HTTPS
          │
          ▼
    Web Application
          │
          ├── Client UI
          │
          ├── Admin UI
          │
          ├── API / App Layer
          │
          ├── Authentication
          │
          └── Business Logic
          │
          ├───────────────┐
          ▼               ▼
    Relational DB    Object Storage
          │
          └───────────────┐
                          ▼
                  External Services
                          │
                ├── WhatsApp
                ├── PWMU
                └── Analytics /
                    Monitoring

Pendekatan ini dipilih untuk menjaga:

- simplicity;
- maintainability;
- deployment simplicity;
- low operational complexity;
- handover readiness.

Microservices tidak diperlukan untuk V1.

---

# 7. Architecture Principles

Technical architecture mengikuti prinsip berikut.

## 7.1 Simplicity

Implementation harus tetap sederhana dan menghindari overengineering.

Tidak diperlukan:

- microservices;
- event-driven architecture;
- distributed systems;
- service mesh;
- infrastructure kompleks.

---

## 7.2 Maintainability

Codebase harus:

- mudah dipahami;
- mengikuti standard framework;
- memiliki struktur yang konsisten;
- memiliki separation of concern yang wajar;
- mudah dilanjutkan developer berikutnya.

---

## 7.3 Security First

Area admin harus dipisahkan dari public access.

Security boundary mencakup:

- authentication;
- authorization;
- input validation;
- XSS protection;
- CSRF protection;
- SQL/NoSQL injection protection;
- rate limiting;
- secure cookies;
- environment secrets.

---

## 7.4 Low Operational Complexity

Managed infrastructure dan PaaS/BaaS dipertimbangkan untuk mengurangi beban operasional.

---

## 7.5 Handover Friendly

Infrastructure harus dapat dipindahkan dari developer awal kepada organisasi.

Ownership harus diarahkan kepada:

    Organization
          ↓
    Official Email
          ↓
    GitHub
    Domain
    Hosting
    Database
    Storage

---

# 8. Frontend Architecture Summary

Frontend menggunakan component-based architecture.

Public website memiliki layout:

    LightLayout

Kaizen Company menggunakan:

    DarkLayout

Admin Dashboard menggunakan:

    AdminLayout

---

## 8.1 Rendering

Untuk public content, SSR atau SSG/ISR direkomendasikan terutama untuk Kajian karena kebutuhan SEO.

Kajian detail:

    /kajian/[slug]

harus mendukung:

- dynamic content;
- metadata;
- canonical URL;
- Open Graph;
- 404 handling;
- unpublished protection.

---

## 8.2 Content Rendering

Kajian membutuhkan safe content rendering.

Architecture:

    Stored Content
          ↓
    Validation
          ↓
    Sanitization
          ↓
    Safe Renderer
          ↓
    Public Page

Raw HTML tidak boleh dirender tanpa sanitization.

---

## 8.3 Image Optimization

Image handling mencakup:

- WebP;
- image validation;
- size validation;
- lazy loading;
- framework image optimization;
- object storage.

---

# 9. Backend Architecture Summary

Backend menggunakan API/App Layer dalam full-stack application.

Middleware utama:

    Authentication Middleware
            +
    Rate Limit Middleware
            +
    Server-side Validation

---

## 9.1 Authentication Middleware

Digunakan untuk melindungi:

    /admin/*
    /api/admin/*

User tanpa valid session harus ditolak atau diarahkan kembali ke public area/login sesuai implementation.

---

## 9.2 Rate Limit Middleware

Digunakan terutama untuk:

    /api/aspirasi

Tujuan:

- mengurangi spam;
- membatasi repeated requests;
- melindungi public endpoint.

---

## 9.3 Validation

Validation harus dilakukan di server sebelum data disimpan ke database.

---

# 10. Database Architecture Summary

Database menggunakan relational database.

Entity utama:

- users;
- organization_profile;
- management_members;
- divisions;
- news;
- kajian;
- alumni;
- products;
- aspirations.

Conceptual relationship:

    Users
      │
      └── Super Admin

    Organization Profile

    Divisions
      │
      └── Management Members

    News

    Kajian

    Alumni

    Products

    Aspirations

Detail schema, data type, foreign key, constraint, dan index akan didefinisikan pada tahap:

    Database Design

---

# 11. Authentication & Authorization

V1 menggunakan:

    Single Super Admin

Tidak terdapat:

- public registration;
- public login;
- multi-role authorization;
- special author account;
- special Bidang Hikmah account.

Authentication method masih merupakan technical open decision.

Options:

- Email + Password;
- Magic Link.

Recommended:

    Email + Password

---

# 12. Content Management Summary

Content lifecycle:

    Draft
      ↓
    Publish
      ↓
    Unpublish
      ↓
    Delete

Visibility principle:

    Published / Active
            ↓
      Public Website

    Draft / Unpublished / Inactive
            ↓
        Admin Only

---

# 13. Module Architecture Summary

## 13.1 Organization Profile

Super Admin dapat mengelola:

- organization information;
- contact information;
- relevant public content.

---

## 13.2 Kepengurusan

Data:

- name;
- photo;
- position;
- division;
- status.

Status dapat berupa active/inactive.

Data historis tidak harus dihapus ketika anggota dinonaktifkan.

---

## 13.3 Bidang

Bidang dapat dikelola melalui Super Admin.

Status public content menggunakan publish/unpublish atau status sesuai module requirement.

---

## 13.4 Berita

Berita berfungsi sebagai directory/highlight.

Data utama:

- title;
- short description/excerpt;
- thumbnail;
- PWMU URL;
- status.

Website tidak menduplikasi full article PWMU.

Flow:

    Website
       ↓
    News Card
       ↓
    PWMU URL
       ↓
    Original PWMU Article

---

## 13.5 Kajian

Kajian merupakan native content.

Data utama:

- title;
- unique slug;
- excerpt;
- thumbnail;
- author;
- content;
- published_at;
- status;
- created_at;
- updated_at.

Status:

    Draft
    Published
    Unpublished

---

## 13.6 Alumni

Alumni dapat dikelola oleh Super Admin.

Status inactive/unpublished digunakan jika profile tidak ingin ditampilkan pada public website.

---

## 13.7 Ekowir

Ekowir merupakan module business/product information.

---

## 13.8 Kaizen Company

Kaizen Company merupakan catalog khusus dengan:

    Dark Theme

Product/service memiliki:

- name;
- photo;
- price;
- description;
- category;
- stock display;
- status.

CTA:

    Hubungi Penjual
          ↓
      WhatsApp

Tidak terdapat native payment flow.

---

## 13.9 Aspirasi

Aspirasi bersifat:

    Anonymous
    Public Submission
    Internal Review

Data minimal:

- content;
- created_at.

Tidak menyimpan:

- user_id;
- name;
- email;
- phone;
- ip_address.

IP dapat digunakan secara temporary untuk rate limiting tetapi tidak disimpan sebagai permanent application data.

---

# 14. API Architecture Summary

Public API conceptual boundary:

    GET  /api/public/pengurus
    GET  /api/public/products
    GET  /api/public/kajian
    GET  /api/public/kajian/:slug
    POST /api/public/aspirasi

Admin API conceptual boundary:

    /api/admin/pengurus
    /api/admin/products
    /api/admin/kajian

Admin endpoints harus dilindungi authentication dan authorization.

Detail API akan didefinisikan pada:

    API Specification

---

# 15. Media Architecture

Media hanya mencakup image pada V1.

Accepted formats:

    .png
    .jpg
    .jpeg
    .webp

Maximum recommended upload size:

    2 MB

Processing:

    Original Image
          ↓
    Validation
          ↓
    WebP Conversion
          ↓
    Object Storage
          ↓
    Database URL Reference

Image storage tidak dilakukan sebagai binary langsung di relational database.

---

# 16. Security Architecture Summary

Security requirements:

- authentication;
- authorization;
- secure cookies;
- XSS protection;
- CSRF protection;
- SQL/NoSQL injection protection;
- input validation;
- rate limiting;
- rich text sanitization;
- CSP consideration;
- secure environment variables;
- protected admin routes;
- admin noindex.

---

# 17. Performance Architecture Summary

Performance strategy:

- SSR/SSG/ISR sesuai kebutuhan;
- static generation untuk content yang sesuai;
- lazy loading;
- image optimization;
- WebP;
- CDN;
- database indexing;
- efficient queries.

Kajian detail direkomendasikan menggunakan SSG/ISR jika framework yang dipilih mendukungnya dengan baik.

---

# 18. SEO Architecture Summary

Public website harus menyediakan:

- page title;
- meta description;
- canonical URL;
- Open Graph;
- dynamic Kajian metadata.

Kajian:

    /kajian/[slug]

menghasilkan metadata berdasarkan data artikel.

Admin:

    /admin/*

harus menggunakan:

    noindex
    nofollow

agar dashboard tidak diindeks search engine.

---

# 19. Analytics & Monitoring

Basic analytics dan monitoring direncanakan.

Potential tools:

- Vercel Web Analytics;
- equivalent analytics solution;
- error monitoring solution.

Tool final masih merupakan open decision.

Monitoring digunakan untuk membantu mengetahui:

- traffic;
- public page usage;
- basic content engagement;
- application errors;
- failed API requests.

---

# 20. Backup Architecture

Database backup merupakan requirement.

Backup harus mencakup data Kajian dan content lainnya.

Aspirasi memiliki additional export requirement:

    Database
       ↓
    CSV Export

Backup ownership harus berada pada organisasi.

---

# 21. Deployment Architecture

Environment minimal:

    Development
         ↓
    Production

Production menggunakan:

- HTTPS;
- official `.org.id` domain;
- managed hosting/PaaS yang dipilih;
- managed database/storage;
- environment secrets.

Potential hosting:

    Vercel
    Netlify
    VPS

Final hosting masih merupakan open technical decision.

---

# 22. Environment Configuration

Sensitive configuration tidak boleh disimpan langsung di repository.

Contoh environment variables:

    DATABASE_URL
    AUTH_SECRET
    STORAGE_API_KEY

Environment configuration harus dipisahkan antara:

    Development
    Production

Secrets tidak boleh dimasukkan ke source code atau committed ke Git repository.

---

# 23. Error Handling

Public application harus memiliki:

    404 — Not Found
    500 — Internal Server Error

API harus mengembalikan structured JSON response.

Database stack traces dan sensitive implementation details tidak boleh dikirim kepada public user.

---

# 24. Logging

Simple server-side logging direkomendasikan untuk:

- failed login;
- API failures;
- unexpected application errors;
- relevant security events.

Logging harus menghindari penyimpanan sensitive information yang tidak diperlukan.

---

# 25. Scalability

V1 tidak membutuhkan distributed architecture.

Scalability strategy:

- relational database;
- standard ORM/query builder;
- indexed queries;
- object storage;
- CDN;
- stateless application architecture jika memungkinkan.

Database provider sebaiknya tetap dapat diganti dengan effort yang wajar.

---

# 26. Maintainability

Maintainability requirements:

- clean code;
- consistent naming;
- framework conventions;
- documented environment variables;
- documented deployment;
- documented database;
- documented API;
- documented content model;
- documented Kajian publishing flow.

Project harus dapat dilanjutkan oleh developer lain tanpa bergantung pada undocumented knowledge dari developer awal.

---

# 27. Handover Architecture

Infrastructure ownership harus diarahkan kepada organisasi.

Minimum ownership:

    GitHub Organization
            +
    Official Email
            +
    Domain
            +
    Hosting
            +
    Database
            +
    Object Storage

Technical documentation minimum:

- README;
- setup guide;
- environment guide;
- deployment guide;
- database documentation;
- API documentation;
- maintenance guide.

Non-technical administrator juga membutuhkan:

    Cara Mengubah Data Web

guide.

---

# 28. Technical Risks

Risiko utama:

| Risk | Impact | Likelihood | Priority |
|---|---|---|---|
| Rich Text XSS | High | Medium | High |
| Developer Handover Failure | High | High | High |
| Aspirasi Spam | Medium | High | High |

Mitigation telah didefinisikan pada:

- security architecture;
- validation;
- sanitization;
- rate limiting;
- documentation;
- organization ownership.

---

# 29. Open Technical Decisions

| ID | Decision | Current Options | Recommendation |
|---|---|---|---|
| TBD-01 | Full-stack Framework | Next.js / Nuxt.js / SvelteKit | Next.js / Nuxt.js |
| TBD-02 | Database & Storage | Supabase / Firebase / VPS | Supabase PostgreSQL |
| TBD-03 | Hosting | Vercel / Netlify / VPS | Vercel / Netlify |
| TBD-04 | Authentication | Email + Password / Magic Link | Email + Password |
| TBD-05 | Kajian Rich Text | Markdown / WYSIWYG HTML | Markdown |
| TBD-06 | Kajian Author | Free Text / Relation | Free Text |
| TBD-07 | Approval Workflow | In-app / Offline Coordination | Offline Coordination |

Semua recommendation di atas merupakan technical recommendation, bukan keputusan final.

---

# 30. Traceability

TSS menyediakan technical traceability untuk requirement utama.

Contoh:

    FR-009
    Kajian Homepage
        ↓
    Homepage Kajian Section
        ↓
    GET /api/public/kajian
        ↓
    kajian Table

---

    FR-010
    Kajian Detail & Slug
        ↓
    /kajian/[slug]
        ↓
    Kajian API
        ↓
    Database Slug Index
        ↓
    Dynamic SEO Metadata

---

    FR-005
    Kaizen Company Catalog
        ↓
    DarkLayout
        ↓
    Product API
        ↓
    products Table
        ↓
    WhatsApp Redirect

---

    FR-004
    Anonymous Aspirasi
        ↓
    Public Form
        ↓
    POST /api/public/aspirasi
        ↓
    Rate Limiting
        ↓
    aspirations Table

---

# 31. Technical Definition of Done

TSS dianggap ready apabila:

- [x] System architecture defined
- [x] Frontend architecture defined
- [x] Backend architecture defined
- [x] Database conceptual architecture defined
- [x] Content architecture defined
- [x] API boundary defined
- [x] Security architecture defined
- [x] Media architecture defined
- [x] Performance strategy defined
- [x] SEO strategy defined
- [x] Deployment strategy defined
- [x] Backup strategy defined
- [x] Handover strategy defined
- [x] Technical risks identified
- [x] Open technical decisions documented
- [x] PRD → TSS traceability documented
- [x] Kajian technical coverage documented
- [x] Database Design readiness validated
- [x] API Specification readiness validated

---

# 32. TSS Validation Status

| Area | Status |
|---|---|
| PRD ↔ TSS Consistency | PASS |
| Kajian Coverage | PASS |
| Architecture Consistency | PASS |
| Frontend Readiness | PASS |
| Backend Readiness | PASS |
| Database Concept Readiness | PASS |
| API Boundary Readiness | PASS |
| Security Readiness | PASS |
| Media Readiness | PASS |
| Performance Readiness | PASS |
| SEO Readiness | PASS |
| Deployment Readiness | PASS |
| Handover Readiness | PASS |

---

# 33. TSS Final Status

Technical Specification berada pada status:

    PASS
    ↓
    READY FOR DATABASE DESIGN
    +
    READY FOR API SPECIFICATION

TSS telah menyediakan technical baseline yang diperlukan untuk melanjutkan project ke technical design berikutnya.

---

# 34. Documentation Lifecycle

Dokumentasi project mengikuti lifecycle:

    PRODUCT DISCOVERY
            ↓
           PRD
            ↓
           TSS
            ↓
    DATABASE DESIGN
            ↓
    API SPECIFICATION
            ↓
    UI/UX SPECIFICATION
            ↓
       DEVELOPMENT
            ↓
         TESTING
            ↓
        PRODUCTION
            ↓
     MAINTENANCE
            ↓
         HANDOVER

Setiap stage memiliki responsibility yang berbeda.

---

# 35. Boundary Between Documents

## Product Discovery

Menjawab:

    Why?
    What problem?
    What direction?

---

## PRD

Menjawab:

    What?
    Who?
    Why?
    What should the product do?

---

## TSS

Menjawab:

    How should the system be technically structured?

---

## Database Design

Menjawab:

    How should data be structured and stored?

---

## API Specification

Menjawab:

    How do system components communicate?

---

## UI/UX Specification

Menjawab:

    How should users interact with the system?

---

## Development

Menjawab:

    How is the specification implemented?

---

# 36. Related Documentation

## Product Discovery

Folder:

    ../product-discovery/

Dokumen Product Discovery menjadi dasar product direction dan constraints.

---

## Product Requirement Document

Folder:

    ../prd/

PRD menjadi sumber utama requirement product.

---

# 37. Navigation

### Previous Stage

- [Product Discovery Documentation](../product-discovery/README.md)
- [Product Requirement Document](../prd/README.md)

### TSS Documents

- [01 — TSS Overview](./01-tss-overview.md)
- [02 — System Architecture](./02-tss-system-architecture.md)
- [03 — Frontend Architecture](./03-tss-frontend-architecture.md)
- [04 — Backend & Database Architecture](./04-tss-backend-and-database-architecture.md)
- [05 — Content & Module Architecture](./05-tss-content-and-module-architecture.md)
- [06 — API, Security & Media](./06-tss-api-security-and-media.md)
- [07 — Deployment, Performance & Handover](./07-tss-deployment-performance-and-handover.md)
- [08 — Decisions, Traceability & Readiness](./08-tss-decisions-traceability-and-readiness.md)

---

# 38. Next Technical Stage

Setelah TSS selesai, project dapat dilanjutkan ke:

    Database Design
            +
    API Specification

Database Design akan mendefinisikan struktur database secara detail.

API Specification akan mendefinisikan contract komunikasi antara frontend, backend, database/application layer, dan external service yang relevan.

---

# 39. Final Statement

Technical Specification Website Resmi PK IMM Kaizen V1.0 Revised berfungsi sebagai technical baseline antara requirement product dan implementation.

Dokumen ini menjaga agar development tidak langsung melompat dari PRD menuju coding tanpa technical design yang cukup.

Final flow:

    Product Discovery
            ↓
           PRD
            ↓
           TSS
            ↓
    Database Design
            +
    API Specification
            ↓
    UI/UX Specification
            ↓
       Development
            ↓
         Testing
            ↓
        Production
            ↓
    Maintenance & Handover

> **TSS Status: READY FOR DATABASE DESIGN & API SPECIFICATION**
