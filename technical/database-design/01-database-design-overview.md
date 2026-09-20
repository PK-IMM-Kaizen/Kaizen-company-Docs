# Database Design — Overview

> **Project:** Website Resmi PK IMM Kaizen V1.0  
> **Document:** Database Design  
> **Version:** 1.2 Revised  
> **Status:** Final Draft  
> **Stage:** Database Design  
> **Audience:** Technical Team / Developer / Database Maintainer

---

## 1. Document Information

| Field | Value |
|---|---|
| Document Title | Database Design — Website Resmi PK IMM Kaizen |
| Product | Website Resmi PK IMM Kaizen V1.0 |
| Version | 1.2 Revised |
| Status | Final Draft |
| Date | September 2026 |
| Author | Senior Database Architect |
| Source Document | PRD V1.1 Revised, TSS V1.1 Revised |
| Database | PostgreSQL |
| Database Provider | Supabase |

---

# 2. Purpose

Dokumen Database Design mendefinisikan struktur penyimpanan data untuk Website Resmi PK IMM Kaizen V1.0.

Dokumen ini menerjemahkan kebutuhan dari:

    Product Requirement Document
                +
    Technical Specification
                ↓
        Database Design
                ↓
       API Specification
                ↓
          Development

Database Design menjadi technical baseline untuk:

- struktur database;
- entity;
- table;
- column;
- data type;
- primary key;
- foreign key;
- constraint;
- relationship;
- indexing;
- authentication identity;
- authorization melalui RLS;
- media storage;
- backup;
- migration;
- seed data;
- handover.

---

# 3. Executive Summary

Database Design ini merumuskan struktur penyimpanan data untuk Website Resmi PK IMM Kaizen.

Database menggunakan:

    PostgreSQL
          ↓
       Supabase

Supabase digunakan sebagai Database-as-a-Service (DaaS).

Revisi V1.2 berfokus pada penguatan technical design, terutama:

- keamanan Row Level Security (RLS);
- integrasi Supabase Auth;
- penghapusan penyimpanan password manual;
- relasi antar entity;
- indexing;
- konsistensi timestamp;
- product stock sebagai numeric;
- security constraints;
- maintainability;
- handover readiness.

---

# 4. Database Architecture

## 4.1 Database Engine

Database menggunakan:

    PostgreSQL

dengan:

    Supabase

sebagai provider.

---

## 4.2 Architecture Overview

High-level architecture:

    Web Application
          │
          ▼
       Supabase
          │
          ├── PostgreSQL Database
          │
          ├── Supabase Auth
          │
          └── Supabase Storage

Application layer tetap bertanggung jawab terhadap:

- business logic;
- request validation;
- rate limiting;
- API processing.

Database bertanggung jawab terhadap:

- data persistence;
- relational integrity;
- constraints;
- access control melalui RLS;
- data consistency.

---

# 5. Database Provider Rationale

Supabase dipilih sebagai database provider karena menyediakan:

- PostgreSQL;
- relational database;
- Row Level Security;
- integrated authentication;
- object storage;
- managed database infrastructure.

PostgreSQL juga menyediakan fitur relational standard yang diperlukan oleh project.

---

# 6. Portability

Schema dirancang menggunakan fitur standar PostgreSQL sebanyak mungkin.

Contoh:

- primary key;
- foreign key;
- CHECK constraint;
- UNIQUE constraint;
- standard data types;
- relational integrity.

Tujuannya adalah menjaga kemungkinan migrasi di masa depan.

Architecture:

    Supabase PostgreSQL
            ↓
      Standard PostgreSQL
            ↓
    Possible Self-managed VPS

Database tidak dirancang dengan ketergantungan yang tidak diperlukan terhadap fitur proprietary.

---

# 7. Design Principles

Database Design mengikuti beberapa prinsip utama.

---

## 7.1 Normalization yang Wajar

Database tidak dinormalisasi secara berlebihan.

Normalisasi hanya dilakukan sejauh memberikan manfaat terhadap:

- data integrity;
- maintainability;
- query consistency;
- relationship management.

Contoh:

Author Kajian tidak dibuat sebagai entity terpisah.

Sebaliknya:

    kajian.author
          ↓
      VARCHAR

Hal ini dilakukan karena struktur organisasi dapat berubah dan author tidak selalu harus menjadi bagian dari kepengurusan aktif.

---

# 8. Referential Integrity

Relasi penting menggunakan foreign key untuk menjaga integritas data.

Contoh:

    divisions
        │
        │ 1:N
        ▼
    management_members

Management member memiliki:

    division_id

yang mereferensikan:

    divisions.id

Untuk relasi penting, digunakan:

    ON DELETE RESTRICT

Tujuannya untuk mencegah penghapusan data parent yang masih memiliki data child.

---

# 9. Minimal Complexity

Database tidak membuat entity yang tidak dibutuhkan oleh PRD.

V1 tidak memiliki table untuk:

- orders;
- cart;
- comments;
- public_users;
- payment;
- transactions.

Database hanya mencakup entity yang diperlukan oleh product scope.

---

# 10. Handover-Friendly Design

Database harus dapat dipahami oleh developer berikutnya.

Prinsip yang digunakan:

- naming convention yang konsisten;
- snake_case;
- struktur table yang jelas;
- relationship eksplisit;
- standard PostgreSQL;
- migration-based schema;
- documented constraints;
- documented indexing;
- documented RLS.

---

# 11. Entity Overview

Database memiliki entity utama berikut:

| Entity | Purpose |
|---|---|
| `super_admins` | Identity dan allowlist Super Admin |
| `organization_profile` | Identitas dan informasi organisasi |
| `divisions` | Data bidang organisasi |
| `management_members` | Data personalia pengurus |
| `kajian` | Native Kajian & Pemikiran content |
| `news` | Directory berita yang mengarah ke PWMU |
| `alumni` | Showcase alumni |
| `products` | Katalog Kaizen Company |
| `aspirations` | Aspirasi publik secara anonim |

Selain entity aplikasi tersebut, authentication menggunakan entity bawaan Supabase:

    auth.users

---

# 12. Authentication Architecture

Authentication menggunakan:

    Supabase Auth

Supabase Auth menjadi sumber authentication identity.

Database aplikasi tidak menyimpan:

    password_hash

secara manual.

Architecture:

    Supabase Auth
          │
          ▼
      auth.users
          │
          │ UUID
          ▼
     super_admins
          │
          ▼
      Admin Access

---

# 13. Super Admin Identity

Table:

    super_admins

digunakan sebagai extension dan allowlist dari:

    auth.users

Konsepnya:

    auth.users
         │
         │ authenticated identity
         ▼
    super_admins
         │
         │ allowlisted
         ▼
    Super Admin CMS Access

Jika UUID user yang login terdapat pada:

    super_admins.id

maka user tersebut dianggap sebagai:

    SUPER_ADMIN

---

# 14. Role Model

V1 hanya memiliki satu logical role:

    SUPER_ADMIN

Tidak terdapat role:

- staff;
- editor;
- author;
- division admin;
- public user account.

Model ini mengikuti scope V1 dan menjaga architecture tetap sederhana.

---

# 15. Organization Profile

Entity:

    organization_profile

digunakan untuk menyimpan informasi utama organisasi.

Data mencakup:

- name;
- history;
- vision;
- mission;
- address;
- email;
- social links.

Table ini menggunakan konsep:

    Single Row

Primary key:

    id = 1

---

# 16. Divisions

Entity:

    divisions

digunakan untuk menyimpan data bidang organisasi.

Data utama:

- name;
- description;
- display_order.

Division digunakan sebagai parent entity untuk:

    management_members

Relationship:

    divisions
        │
        │ 1:N
        ▼
    management_members

---

# 17. Management Members

Entity:

    management_members

menyimpan data personalia kepengurusan.

Data utama:

- name;
- photo_url;
- position;
- division_id;
- status;
- display_order.

Status:

    active
    inactive

Data inactive dapat tetap disimpan untuk menjaga historical data.

---

# 18. Kajian

Entity:

    kajian

digunakan untuk menyimpan native Kajian & Pemikiran content.

Data utama:

- title;
- slug;
- thumbnail_url;
- excerpt;
- content;
- author;
- status;
- published_at.

Kajian memiliki:

    unique slug

untuk kebutuhan dynamic route dan SEO.

Route application:

    /kajian/[slug]

---

# 19. Kajian Content Model

Content Kajian disimpan sebagai full text.

Recommended format:

    Markdown

Field:

    content TEXT

Author menggunakan:

    VARCHAR

bukan foreign key ke management member.

Alasannya adalah author tidak harus selalu merupakan pengurus aktif.

---

# 20. Kajian Status

Kajian memiliki tiga status:

    draft
    published
    unpublished

Visibility:

    draft
        ↓
    Admin Only

    published
        ↓
    Public

    unpublished
        ↓
    Admin Only

Status harus divalidasi menggunakan CHECK constraint.

---

# 21. News

Entity:

    news

digunakan untuk menyimpan directory berita yang berasal dari PWMU.

Database tidak menyimpan full article body PWMU.

Data utama:

- title;
- excerpt;
- thumbnail_url;
- pwmu_url;
- status;
- published_at.

Flow:

    Website
       ↓
    News Directory
       ↓
    pwmu_url
       ↓
    Original PWMU Article

---

# 22. News Content Model

News berbeda dengan Kajian.

### Kajian

    Native Content
        ↓
    Full article stored locally

### News

    External Content
        ↓
    PWMU URL
        ↓
    Redirect to original article

Perbedaan ini harus dipertahankan pada database design.

---

# 23. Alumni

Entity:

    alumni

digunakan untuk showcase alumni.

Data utama:

- name;
- photo_url;
- achievement;
- status.

Status:

    published
    unpublished

Alumni yang berstatus unpublished tidak ditampilkan pada public website.

---

# 24. Products

Entity:

    products

digunakan untuk katalog Kaizen Company.

Data utama:

- name;
- description;
- stock;
- price;
- category;
- image_url;
- whatsapp_number;
- status.

Product tidak menggunakan order atau payment table.

---

# 25. Product Stock

Stock menggunakan tipe numeric:

    INT

Default:

    0

Constraint:

    stock >= 0

Interpretasi:

    stock > 0
        ↓
      Available

    stock = 0
        ↓
      Habis

Stock diperbarui secara manual oleh Super Admin.

---

# 26. Product Contact

Setiap product menyimpan:

    whatsapp_number

sehingga nomor WhatsApp dapat berbeda untuk setiap product/service.

Flow:

    Product
       ↓
    whatsapp_number
       ↓
    WhatsApp CTA

Tidak dibutuhkan table contact terpisah untuk V1.

---

# 27. Product Status

Product memiliki status:

    active
    inactive

Product inactive tidak ditampilkan pada public catalog.

Data tetap dapat dipertahankan untuk kebutuhan administrasi.

---

# 28. Aspirations

Entity:

    aspirations

digunakan untuk menyimpan kritik dan saran dari publik.

Karakteristik utama:

    Anonymous
    Public Submission
    Internal Administration

Data utama:

- content;
- created_at.

---

# 29. Anonymous Data Boundary

Aspirations tidak menyimpan:

- user_id;
- name;
- email;
- phone;
- IP address.

Database representation:

    aspirations
    ├── id
    ├── content
    └── created_at

Rate limiting dilakukan pada application layer.

IP dapat digunakan sementara untuk rate limiting, tetapi tidak disimpan sebagai permanent application data.

---

# 30. Database Scope

Database V1 secara keseluruhan:

    auth.users
          │
          ▼
    super_admins

    organization_profile

    divisions
          │
          ▼
    management_members

    kajian

    news

    alumni

    products

    aspirations

Tidak terdapat entity tambahan di luar kebutuhan product scope tanpa technical justification.

---

# 31. Database Responsibility Boundary

Database bertanggung jawab terhadap:

- persistence;
- relational integrity;
- constraints;
- uniqueness;
- status validity;
- access policies;
- timestamps;
- indexing.

Application layer bertanggung jawab terhadap:

- business logic;
- request validation;
- rate limiting;
- content processing;
- API response;
- user interaction.

---

# 32. Security Architecture Overview

Database security menggunakan:

    Supabase Auth
          +
    super_admins Allowlist
          +
    Row Level Security

High-level authorization:

    auth.uid()
        ↓
    Check super_admins
        ↓
    SUPER_ADMIN
        ↓
    Full CMS Access

Public access dibatasi berdasarkan status content.

---

# 33. RLS Overview

Row Level Security digunakan untuk membatasi akses langsung terhadap database.

Public access hanya diperbolehkan terhadap content yang memenuhi visibility condition.

Contoh:

    status = 'published'

atau:

    status = 'active'

Public INSERT hanya diperbolehkan pada:

    aspirations

Akses lainnya ditolak secara default.

---

# 34. Super Admin Database Access

Super Admin dapat memiliki:

    SELECT
    INSERT
    UPDATE
    DELETE

terhadap operational tables.

Exception:

    aspirations

Super Admin hanya membutuhkan:

    SELECT
    DELETE

terhadap Aspirasi.

Aspirasi tidak dapat diedit setelah dikirim karena merupakan submission asli dari publik.

---

# 35. Database Security Principle

Database harus menerapkan prinsip:

    Default Deny
          ↓
    Explicit Allow
          ↓
    RLS Policy

Tidak ada public write access terhadap content management tables.

---

# 36. Summary

Database Design V1.2 Revised menggunakan PostgreSQL melalui Supabase dengan fokus pada:

- relational integrity;
- simple normalized structure;
- Supabase Auth;
- Super Admin allowlist;
- strict RLS;
- explicit constraints;
- indexed public queries;
- anonymous aspirations;
- native Kajian;
- external PWMU news;
- numeric product stock;
- product-specific WhatsApp contact;
- standard timestamps;
- migration-based schema;
- maintainability;
- portability;
- handover readiness.

Database architecture tetap mengikuti prinsip:

    Simple
    Secure
    Maintainable
    Portable
    Handover-Friendly

---

## Navigation

- [← TSS README](../tss/README.md)
- [Database Design — Next →](./02-database-design-schema.md)
