# Technical Specification — Decisions, Traceability & Readiness

> **Project:** Website Resmi PK IMM Kaizen V1.0  
> **Document:** Technical Specification (TSS)  
> **Version:** 1.1 Revised  
> **Status:** Draft — Technical Planning  
> **Stage:** Technical Specification  
> **Audience:** Technical Team / Developer / System Maintainer

---

## 1. Document Information

| Field | Value |
|---|---|
| Product | Website Resmi PK IMM Kaizen |
| Product Version | V1.0 |
| Document | Technical Specification |
| Document Version | 1.1 Revised |
| Section | Decisions, Traceability & Readiness |
| Status | Draft — Technical Planning |
| Source | PRD — Website Resmi PK IMM Kaizen V1.0 Revised |
| Related Document | Product Discovery V1.0 |
| Previous Document | TSS — Deployment, Performance & Handover |
| Next Stage | Database Design & API Specification |

---

## 2. Purpose

Dokumen ini merupakan bagian penutup dari Technical Specification (TSS).

Tujuannya adalah:

1. mendokumentasikan technical risks;
2. mencatat technical decisions yang masih terbuka;
3. memberikan recommendation terhadap technology stack;
4. memastikan requirement PRD memiliki technical coverage;
5. memastikan seluruh bagian penting dari TSS telah didefinisikan;
6. memastikan sistem siap dilanjutkan ke Database Design;
7. memastikan sistem siap dilanjutkan ke API Specification;
8. memastikan tidak terdapat konflik teknis besar dengan PRD.

Dokumen ini bukan tempat untuk membuat keputusan produk baru yang belum disepakati.

Keputusan produk tetap mengikuti:

    Product Discovery
            ↓
          PRD
            ↓
          TSS

---

# 3. Technical Risks

## 3.1 Risk Overview

Technical risks utama yang telah diidentifikasi:

| Risk | Impact | Likelihood | Priority |
|---|---|---|---|
| Rich Text XSS | High | Medium | High |
| Developer Handover Failure | High | High | High |
| Aspirasi Spam | Medium | High | High |

---

# 4. Risk — Rich Text XSS

## 4.1 Description

Kajian menggunakan native content yang memungkinkan penyimpanan konten artikel.

Jika implementation menggunakan rich text atau HTML tanpa sanitization yang tepat, terdapat risiko:

    User / Admin Input
           ↓
    Unsanitized Content
           ↓
        Database
           ↓
       Public Page
           ↓
            XSS

---

## 4.2 Impact

Potential impact:

- malicious script execution;
- session compromise;
- content manipulation;
- user redirection;
- browser-based attacks.

---

## 4.3 Mitigation

Required technical mitigation:

- sanitize rich text;
- validate content server-side;
- jangan merender raw HTML tanpa sanitizer;
- gunakan safe Markdown renderer jika Markdown dipilih;
- gunakan sanitizer seperti DOMPurify jika HTML diperlukan;
- validasi output sebelum ditampilkan.

---

## 4.4 Risk Status

    Risk: HIGH
    Mitigation: REQUIRED
    Status: MUST BE ADDRESSED

---

# 5. Risk — Developer Handover Failure

## 5.1 Description

Project dikembangkan oleh solo developer.

Risiko utama adalah project terlalu bergantung pada pengetahuan developer awal.

Potential failure:

    Developer Initial
           ↓
    Knowledge Concentration
           ↓
    Developer Unavailable
           ↓
    Maintenance Difficulty

---

## 5.2 Impact

Potential impact:

- deployment tidak dapat dilakukan;
- infrastructure sulit diakses;
- developer baru membutuhkan waktu lama untuk memahami project;
- maintenance terhambat;
- perubahan organisasi dapat menyebabkan kehilangan technical ownership.

---

## 5.3 Mitigation

Required mitigation:

- GitHub Organization ownership;
- centralized infrastructure accounts;
- official organization email;
- README;
- deployment documentation;
- environment documentation;
- database documentation;
- API documentation;
- architecture documentation;
- backup documentation.

---

## 5.4 Risk Status

    Risk: HIGH
    Mitigation: REQUIRED
    Status: MUST BE ADDRESSED

---

# 6. Risk — Aspirasi Spam

## 6.1 Description

Aspirasi dapat dikirim secara publik tanpa login.

Karena anonymous submission merupakan requirement, endpoint Aspirasi berpotensi disalahgunakan oleh automated request atau spam.

Flow risk:

    Public User
         ↓
     Public API
         ↓
    Repeated Requests
         ↓
          Spam

---

## 6.2 Impact

Potential impact:

- database pollution;
- administrative overload;
- abusive content;
- unnecessary API usage;
- increased operational cost.

---

## 6.3 Mitigation

Recommended mitigation:

- rate limiting;
- honeypot;
- request validation;
- optional CAPTCHA/Turnstile jika dibutuhkan;
- server-side validation.

Untuk V1, kombinasi:

    Honeypot
        +
    Rate Limiter

direkomendasikan sebagai baseline sederhana.

---

## 6.4 Risk Status

    Risk: MEDIUM
    Likelihood: HIGH
    Mitigation: REQUIRED
    Status: MUST BE ADDRESSED

---

# 7. Open Technical Decisions

Beberapa keputusan teknis belum ditetapkan secara final.

Decision identifiers:

    TBD-01
    TBD-02
    TBD-03
    TBD-04
    TBD-05
    TBD-06
    TBD-07

---

# 8. TBD-01 — Full-stack Framework

## Question

Framework full-stack apa yang akan digunakan?

### Candidates

- Next.js
- Nuxt.js
- SvelteKit

### Requirement

Framework harus mendukung:

- frontend;
- backend/API;
- dynamic routing;
- SSR/SSG/ISR atau equivalent;
- SEO;
- authentication;
- deployment sederhana;
- maintainability.

### Recommendation

    Next.js
    atau
    Nuxt.js

Keduanya sesuai dengan architecture yang dirancang.

### Status

    OPEN DECISION

Keputusan final ditetapkan sebelum implementation.

---

# 9. TBD-02 — Database & Storage Provider

## Question

Provider database dan object storage apa yang digunakan?

### Candidates

- Supabase
- Firebase
- VPS-managed infrastructure

### Requirement

Provider harus mendukung:

- relational database;
- secure connection;
- backup;
- object storage;
- image handling;
- maintainability;
- organization ownership.

### Recommendation

    Supabase PostgreSQL

Alasan teknis:

- relational database;
- PostgreSQL;
- managed service;
- object storage tersedia;
- cocok untuk solo developer;
- operational overhead relatif rendah.

### Status

    OPEN DECISION

---

# 10. TBD-03 — Hosting Platform

## Question

Application akan di-deploy menggunakan platform apa?

### Candidates

- Vercel
- Netlify
- VPS

### Requirement

Hosting harus mendukung:

- full-stack framework;
- environment variables;
- HTTPS;
- deployment automation;
- preview/development environment;
- production deployment;
- organization ownership.

### Recommendation

    Vercel
    atau
    Netlify

Untuk arsitektur full-stack modern, serverless/PaaS seperti Vercel atau Netlify sangat dipertimbangkan karena dapat mengurangi operational complexity.

### Status

    OPEN DECISION

---

# 11. TBD-04 — Authentication Method

## Question

Metode authentication Super Admin apa yang digunakan?

### Candidates

- Email + Password
- Magic Link

### Requirement

Authentication harus:

- hanya untuk Super Admin;
- tidak menyediakan public registration;
- secure;
- mudah di-maintain;
- sesuai dengan infrastructure yang dipilih.

### Recommendation

    Email + Password

Alasan:

- familiar untuk administrator;
- tidak bergantung pada email link setiap login;
- implementation relatif straightforward;
- sesuai dengan single Super Admin model.

### Status

    OPEN DECISION

---

# 12. TBD-05 — Kajian Rich Text Format

## Question

Format content Kajian yang digunakan apa?

### Candidates

- Markdown
- WYSIWYG HTML

### Markdown

Advantages:

- sederhana;
- portable;
- mudah di-version;
- lebih mudah dikontrol;
- security surface lebih kecil jika renderer aman.

### WYSIWYG HTML

Advantages:

- lebih mudah bagi non-technical content editor;
- formatting dapat dilakukan melalui visual editor.

Risiko:

- HTML sanitization lebih kompleks;
- XSS attack surface lebih besar;
- implementation lebih kompleks.

### Recommendation

    Markdown

untuk V1.

Namun keputusan final masih terbuka.

### Status

    OPEN DECISION

---

# 13. TBD-06 — Kajian Author Model

## Question

Bagaimana author Kajian direpresentasikan?

### Option A — Free Text

Contoh:

    author: "Bidang Hikmah dan Politik"

Advantages:

- sederhana;
- tidak membutuhkan relation tambahan;
- fleksibel.

### Option B — Management Member Relation

Author memiliki relation ke data pengurus/member.

Contoh:

    kajian.author_id
            ↓
    management_members.id

Advantages:

- data lebih terstruktur;
- author dapat dikaitkan dengan entity existing.

Potential issue:

- perubahan kepengurusan;
- historical author attribution;
- dependency antar entity.

### Recommendation

    Free Text

untuk V1.

### Status

    OPEN DECISION

---

# 14. TBD-07 — Kajian Approval Workflow

## Question

Apakah Kajian membutuhkan approval workflow khusus?

### Existing Product Constraint

V1 hanya memiliki:

    Super Admin

sebagai administrative role.

Tidak terdapat role khusus untuk Bidang Hikmah/Politik.

### Recommendation

Tidak membuat complex in-app approval workflow pada V1.

Workflow dapat dilakukan melalui koordinasi internal:

    Content Author / Bidang
            ↓
    Internal Coordination
            ↓
        Super Admin
            ↓
        Dashboard
            ↓
    Draft / Publish

### Status

    OPEN DECISION

---

# 15. Technical Decision Summary

| ID | Decision | Options | Recommendation | Status |
|---|---|---|---|---|
| TBD-01 | Framework | Next.js / Nuxt.js / SvelteKit | Next.js / Nuxt.js | Open |
| TBD-02 | DB & Storage | Supabase / Firebase / VPS | Supabase PostgreSQL | Open |
| TBD-03 | Hosting | Vercel / Netlify / VPS | Vercel / Netlify | Open |
| TBD-04 | Authentication | Email + Password / Magic Link | Email + Password | Open |
| TBD-05 | Rich Text | Markdown / WYSIWYG HTML | Markdown | Open |
| TBD-06 | Kajian Author | Free Text / Relation | Free Text | Open |
| TBD-07 | Approval | In-app / Offline Coordination | Offline Coordination | Open |

---

# 16. Technology Recommendation

Berdasarkan technical requirements yang telah didefinisikan, recommended stack adalah:

    Frontend + Backend
            ↓
    Next.js / Nuxt.js

    Database
            ↓
    PostgreSQL

    Managed Database + Storage
            ↓
    Supabase

    ORM
            ↓
    Prisma / Drizzle

    Hosting
            ↓
    Vercel / Netlify

    Analytics
            ↓
    Vercel Web Analytics / Equivalent

    Error Monitoring
            ↓
    Selected Monitoring Tool

Stack final tetap bergantung pada keputusan TBD.

---

# 17. Technology Selection Principles

Pemilihan teknologi harus mempertimbangkan:

## 17.1 Simplicity

Teknologi harus cukup sederhana untuk dikelola oleh solo developer.

## 17.2 Maintainability

Developer berikutnya harus dapat memahami stack tanpa learning curve yang tidak perlu.

## 17.3 Portability

Database dan application layer tidak boleh terlalu terikat pada satu provider tanpa alasan teknis.

## 17.4 Security

Technology harus mendukung:

- authentication;
- authorization;
- secure storage;
- environment secrets;
- input validation;
- XSS mitigation.

## 17.5 Cost Awareness

V1 harus menghindari infrastructure yang membutuhkan operational cost tinggi tanpa kebutuhan yang jelas.

## 17.6 Handover

Infrastructure account harus dapat dipindahkan dan dimiliki organisasi.

---

# 18. PRD → TSS Traceability

## 18.1 Purpose

Traceability memastikan requirement utama dari PRD memiliki technical implementation boundary yang jelas.

---

# 19. Kajian Homepage

### PRD Requirement

Kajian ditampilkan pada homepage sebagai section.

### Technical Coverage

    Homepage
        ↓
    Kajian Section
        ↓
    GET /api/public/kajian
        ↓
    Published Kajian

### Technical Components

- Homepage UI;
- Kajian API;
- database `kajian`;
- published status filtering.

### Traceability

    PRD Requirement
            ↓
    FR-009 — Kajian Homepage
            ↓
    TSS Frontend Architecture
            ↓
    TSS API Architecture
            ↓
    Database Design

---

# 20. Kajian Detail & Slug

### PRD Requirement

User dapat membuka artikel Kajian melalui detail page dengan unique URL.

### Technical Coverage

    /kajian/[slug]

### Components

- dynamic route;
- slug lookup;
- database index;
- metadata generation;
- 404 handling;
- published status validation.

### Traceability

    PRD Requirement
            ↓
    FR-010 — Kajian Detail & Slug
            ↓
    Dynamic Route
            ↓
    Kajian API
            ↓
    Database Slug Index
            ↓
    SEO Metadata

---

# 21. Kajian CMS

### PRD Requirement

Super Admin dapat melakukan CRUD Kajian.

### Technical Coverage

    Super Admin
          ↓
    Admin Dashboard
          ↓
       Admin API
          ↓
      kajian table

Operations:

    Create
    Read
    Update
    Delete
    Publish
    Unpublish

### Security

- admin authentication;
- admin authorization;
- input validation;
- rich text sanitization.

### Traceability

    CMS-Kajian CRUD & Lifecycle
            ↓
        Admin API
            ↓
    Authentication Middleware
            ↓
         Validation
            ↓
      XSS Sanitization
            ↓
        kajian Table

---

# 22. Kaizen Company Catalog

### PRD Requirement

Kaizen Company menyediakan katalog produk/service dengan WhatsApp CTA.

### Technical Coverage

    DarkLayout
        ↓
    Product List
        ↓
    Product Detail
        ↓
    WhatsApp CTA

API:

    GET /api/public/products

### Traceability

    FR-005 — Kaizen Company Catalog
            ↓
    Frontend DarkLayout
            ↓
    Public Product API
            ↓
    products Table
            ↓
    WhatsApp Redirect

---

# 23. Aspirasi Anonymous

### PRD Requirement

User dapat mengirim aspirasi tanpa login dan tanpa identitas.

### Technical Coverage

    Public Form
          ↓
    POST /api/public/aspirasi
          ↓
      Validation
          ↓
    Rate Limiting
          ↓
       Honeypot
          ↓
    aspirations Table

Database boundary:

    aspirations
    ├── id
    ├── content
    └── created_at

Tidak menyimpan:

    user_id
    name
    email
    phone
    ip_address

### Traceability

    FR-004 — Aspirasi Anonim
            ↓
        Public Form
            ↓
        Public API
            ↓
    Security Middleware
            ↓
    Aspirations Storage

---

# 24. Berita PWMU

### PRD Requirement

Website menampilkan directory/highlight berita dan mengarahkan user ke artikel original PWMU.

### Technical Coverage

    Berita Card
        ↓
    Thumbnail
    Title
    Excerpt
    PWMU URL
        ↓
    External Redirect
        ↓
        PWMU

Link harus membuka external source sesuai requirement.

### Traceability

    Berita Requirement
            ↓
       News Module
            ↓
        news Table
            ↓
         PWMU URL
            ↓
     External Redirect

---

# 25. Public Content Visibility

Status content harus menentukan visibility.

### Public

    Published / Active
            ↓
      Public Website

### Non-Public

    Draft / Unpublished / Inactive
            ↓
        Admin Only

Exception dapat berlaku sesuai module-specific rules.

---

# 26. Technical Architecture Traceability

High-level architecture:

    Public User
         │
         ▼
       HTTPS
         │
         ▼
    Full-stack Application
         │
         ├── Public UI
         │
         ├── Admin UI
         │
         ├── API Layer
         │
         ├── Authentication
         │
         ├── Validation
         │
         └── Business Logic
         │
         ├───────────────┐
         ▼               ▼
    Relational DB    Object Storage
         │
         └───────────────┐
                         ▼
                 Backup / Monitoring

---

# 27. Technical Definition of Done

TSS dianggap secara teknis complete apabila requirement berikut terpenuhi.

## 27.1 Architecture

- [ ] Full-stack architecture defined
- [ ] Frontend architecture defined
- [ ] Backend architecture defined
- [ ] Database architecture defined
- [ ] Media architecture defined
- [ ] Security boundary defined
- [ ] Deployment architecture defined

---

## 27.2 Kajian

- [ ] Kajian homepage section covered
- [ ] Kajian standalone detail covered
- [ ] Dynamic slug route defined
- [ ] Kajian database entity defined
- [ ] Kajian API boundary defined
- [ ] Draft/Published/Unpublished states defined
- [ ] Rich text security defined
- [ ] SEO metadata defined
- [ ] Kajian backup included

---

## 27.3 Admin

- [ ] Single Super Admin model defined
- [ ] Authentication boundary defined
- [ ] Authorization boundary defined
- [ ] Admin API protected
- [ ] Admin noindex defined
- [ ] CRUD boundary defined

---

## 27.4 Aspirasi

- [ ] Anonymous submission defined
- [ ] Public API defined
- [ ] Rate limiting defined
- [ ] Honeypot considered
- [ ] Identity fields excluded
- [ ] IP permanent storage excluded
- [ ] CSV export defined

---

## 27.5 Media

- [ ] Image validation defined
- [ ] WebP requirement defined
- [ ] File size limit defined
- [ ] Object storage defined
- [ ] Unauthorized upload protection defined

---

## 27.6 Security

- [ ] XSS protection defined
- [ ] CSRF protection considered
- [ ] SQL/NoSQL injection protection defined
- [ ] Rate limiting defined
- [ ] Rich text sanitization defined
- [ ] Environment secrets defined
- [ ] Sensitive error protection defined

---

## 27.7 Performance

- [ ] SSG/SSR/ISR strategy defined
- [ ] Lazy loading defined
- [ ] Image optimization defined
- [ ] CDN recommended
- [ ] Database indexing considered

---

## 27.8 SEO

- [ ] Metadata defined
- [ ] Canonical URL defined
- [ ] Open Graph defined
- [ ] Kajian dynamic metadata defined
- [ ] Admin noindex defined
- [ ] Published content indexing boundary defined

---

## 27.9 Deployment

- [ ] Development environment defined
- [ ] Production environment defined
- [ ] Domain requirement defined
- [ ] Hosting options defined
- [ ] Environment variables defined
- [ ] Error handling defined
- [ ] Logging defined
- [ ] Backup defined

---

## 27.10 Handover

- [ ] GitHub ownership defined
- [ ] Domain ownership defined
- [ ] Hosting ownership defined
- [ ] Database ownership defined
- [ ] Storage ownership defined
- [ ] Official email ownership defined
- [ ] Deployment documentation required
- [ ] Maintenance documentation required

---

# 28. Technical Validation

## 28.1 PRD ↔ TSS Consistency

**Status: PASS**

Technical Specification translates the PRD requirements into:

- architecture;
- frontend;
- backend;
- database;
- API;
- security;
- deployment;
- performance;
- handover.

No major technical architecture conflict has been identified with the revised PRD scope.

---

# 29. Kajian Technical Coverage

**Status: PASS**

Kajian is technically covered through:

- homepage section;
- standalone dynamic route;
- slug;
- database entity;
- public API;
- admin CRUD;
- publishing lifecycle;
- rich text security;
- SEO;
- backup.

Kajian is therefore technically supported by the Revised TSS.

---

# 30. Architecture Consistency

**Status: PASS**

The proposed architecture remains consistent with V1 goals:

    Simple
    Secure
    Maintainable
    Scalable Enough
    Handover-Friendly

No microservices or distributed architecture is required for V1.

---

# 31. Database Readiness

**Status: READY FOR DATABASE DESIGN**

TSS telah mendefinisikan conceptual entities:

- users;
- organization_profile;
- management_members;
- divisions;
- news;
- kajian;
- alumni;
- products;
- aspirations.

Database Design stage selanjutnya harus mendefinisikan:

- table schema;
- columns;
- data types;
- primary keys;
- foreign keys;
- constraints;
- indexes;
- relationships;
- migration strategy.

---

# 32. API Readiness

**Status: READY FOR API SPECIFICATION**

TSS telah mendefinisikan API boundary untuk:

### Public

    GET /api/public/pengurus
    GET /api/public/products
    GET /api/public/kajian
    GET /api/public/kajian/:slug
    POST /api/public/aspirasi

### Admin

    /api/admin/pengurus
    /api/admin/products
    /api/admin/kajian

API Specification selanjutnya harus mendefinisikan:

- HTTP methods;
- request parameters;
- request body;
- response body;
- status codes;
- authentication;
- authorization;
- validation;
- error responses;
- pagination jika diperlukan.

---

# 33. Security Readiness

**Status: READY**

Security boundary telah didefinisikan untuk:

- authentication;
- authorization;
- XSS;
- CSRF;
- SQL/NoSQL injection;
- rate limiting;
- rich text sanitization;
- environment secrets;
- admin indexing;
- sensitive error handling.

Implementation detail akan dilanjutkan pada Development dan Security Testing.

---

# 34. SEO Readiness

**Status: READY**

SEO technical requirements telah mencakup:

- dynamic page title;
- meta description;
- canonical URL;
- Open Graph;
- Kajian dynamic metadata;
- published content indexing;
- admin noindex.

---

# 35. Deployment & Handover Readiness

**Status: READY**

Deployment architecture telah mencakup:

- development environment;
- production environment;
- domain;
- hosting;
- database;
- object storage;
- environment variables;
- backup;
- monitoring;
- error handling;
- logging.

Handover architecture telah mencakup:

- organization ownership;
- GitHub;
- domain;
- hosting;
- database;
- storage;
- official email;
- technical documentation.

---

# 36. Final Technical Validation Matrix

| Validation Area | Status |
|---|---|
| PRD ↔ TSS Consistency | PASS |
| Kajian Coverage | PASS |
| Architecture Consistency | PASS |
| Frontend Architecture | PASS |
| Backend Architecture | PASS |
| Database Concept | PASS |
| API Boundary | PASS |
| Security Boundary | PASS |
| Media Architecture | PASS |
| Performance Strategy | PASS |
| SEO Strategy | PASS |
| Deployment Strategy | PASS |
| Backup Strategy | PASS |
| Handover Strategy | PASS |
| Database Design Readiness | PASS |
| API Specification Readiness | PASS |

---

# 37. Remaining Open Decisions

Technical planning masih memiliki beberapa keputusan yang harus ditetapkan sebelum implementation final:

    TBD-01 — Framework
    TBD-02 — Database & Storage Provider
    TBD-03 — Hosting Platform
    TBD-04 — Authentication Method
    TBD-05 — Kajian Rich Text Format
    TBD-06 — Kajian Author Model
    TBD-07 — Kajian Approval Workflow

Open decisions tidak menghalangi penyusunan Database Design dan API Specification pada level konseptual.

Namun keputusan implementation final harus ditetapkan sebelum development production dimulai.

---

# 38. Recommended Decision Order

Untuk mengurangi dependency antar keputusan, urutan penetapan yang direkomendasikan:

    TBD-01
    Framework
        ↓
    TBD-02
    Database & Storage
        ↓
    TBD-03
    Hosting
        ↓
    TBD-04
    Authentication
        ↓
    TBD-05
    Kajian Content Format
        ↓
    TBD-06
    Kajian Author Model
        ↓
    TBD-07
    Approval Workflow

Urutan tersebut bukan mandatory implementation sequence, tetapi membantu mengurangi ambiguity.

---

# 39. TSS Final Status

    TECHNICAL SPECIFICATION
            ↓
    Architecture Defined
            ↓
    Security Defined
            ↓
    Performance Defined
            ↓
    Deployment Defined
            ↓
    Handover Defined
            ↓
    Traceability Completed
            ↓
    Validation Completed
            ↓
            PASS
            ↓
    READY FOR DATABASE DESIGN
            +
    READY FOR API SPECIFICATION

---

# 40. Final Statement

Technical Specification Website Resmi PK IMM Kaizen V1.0 Revised telah mendefinisikan technical direction yang diperlukan untuk melanjutkan project dari requirement menuju implementation planning.

TSS menetapkan prinsip bahwa sistem harus:

1. sederhana untuk V1;
2. aman untuk public dan admin;
3. mendukung native Kajian content;
4. mendukung anonymous Aspirasi;
5. mendukung Kaizen Company catalog;
6. memiliki public/admin boundary yang jelas;
7. memiliki backup;
8. memiliki performance strategy;
9. memiliki SEO strategy;
10. dapat dideploy secara manageable;
11. dapat dipelihara oleh developer berikutnya;
12. dapat diserahterimakan kepada organisasi.

Technical Specification tidak menetapkan implementation detail yang seharusnya menjadi tanggung jawab Database Design, API Specification, UI/UX Specification, dan Development.

Boundary berikutnya adalah:

    Product Discovery
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

---

# 41. Next Stage

Tahap berikutnya adalah:

## Database Design

Fokus:

- database schema;
- tables;
- columns;
- data types;
- primary keys;
- foreign keys;
- constraints;
- indexes;
- relationships;
- migration;
- data integrity.

Kemudian dilanjutkan dengan:

## API Specification

Fokus:

- endpoint;
- HTTP method;
- request;
- response;
- authentication;
- authorization;
- validation;
- error handling;
- status codes;
- public/admin API boundary.

---

## Navigation

- [← TSS Deployment, Performance & Handover](./07-tss-deployment-performance-and-handover.md)
- [TSS README](./README.md)
- [↑ Technical Documentation](../README.md)
