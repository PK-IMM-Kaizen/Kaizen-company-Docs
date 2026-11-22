# 🗄️ Database Design

Dokumentasi struktur dan konfigurasi database untuk **Kaizen Company Platform**.

Database menggunakan **Supabase**, dengan PostgreSQL sebagai relational database dan Supabase Auth serta Supabase Storage sebagai layanan pendukung.

## 📌 Overview

Dokumentasi ini menjelaskan kondisi database berdasarkan hasil pemeriksaan pada project Supabase yang sedang digunakan.

| Komponen | Hasil Pemeriksaan |
|---|---|
| Database | PostgreSQL (Supabase) |
| Schema aplikasi | `public` |
| Authentication | Supabase Auth |
| File storage | Supabase Storage |
| Tabel aplikasi | 12 |
| Kolom aplikasi | 103 |
| Constraints | 60 |
| Indexes | 13 |
| Foreign keys | 27 terdeteksi pada schema `public` dan `auth` |
| RLS | Aktif pada seluruh 12 tabel aplikasi |
| RLS policies | 47 terdeteksi pada tabel aplikasi dan Storage |
| Custom function | 1 fungsi aplikasi teridentifikasi |
| Application views | Tidak ditemukan |
| Application materialized views | Tidak ditemukan |

> **Catatan:** Angka di atas merupakan hasil inventarisasi pada saat audit, bukan jaminan bahwa kondisi database tidak berubah setelah pemeriksaan dilakukan.

## 📂 Documentation Index

| Dokumen | Deskripsi |
|---|---|
| [Database Schema](./database-schema.md) | Daftar tabel dan gambaran struktur database |
| [Relationships](./relationships.md) | Relasi antar tabel dan foreign key |
| [RLS Policies](./rls-policies.md) | Row Level Security dan kebijakan akses |
| [Storage Configuration](./storage-configuration.md) | Konfigurasi bucket dan akses file |
| [Functions and Triggers](./functions-and-triggers.md) | Fungsi database dan trigger |
| [Database Privileges](./database-privileges.md) | Hak akses PostgreSQL |
| [SQL Audit Report](./review/sql-audit-report.md) | Temuan dan catatan audit SQL |

## 🧩 Application Tables

Database aplikasi memiliki 12 tabel pada schema `public`:

1. `profiles`
2. `organization_profile`
3. `news`
4. `aspirations`
5. `pengurus`
6. `alumni`
7. `products`
8. `dad_registrations`
9. `site_settings`
10. `system_logs`
11. `divisions`
12. `agendas`

## 🔐 Access Control

Aplikasi menggunakan dua jenis role utama:

- **Superadmin** — memiliki seluruh hak operasional Admin serta kewenangan tambahan untuk membuat, mengedit, dan menghapus akun Admin.
- **Admin** — memiliki hak operasional yang sama dengan Superadmin untuk mengelola modul aplikasi, tetapi tidak memiliki kewenangan pengelolaan akun Admin.

Perbedaan role aplikasi tersebut tidak sama dengan role PostgreSQL seperti `anon`, `authenticated`, dan `service_role`.

Akses data pada database juga dipengaruhi oleh konfigurasi GRANT dan Row Level Security (RLS).

## 🗂️ SQL Repository

SQL dipisahkan berdasarkan tujuan dan statusnya:

| Direktori | Penggunaan |
|---|---|
| `sql/migrations/` | Perubahan struktur database yang terkontrol |
| `sql/seeds/` | Data awal atau data referensi |
| `sql/archive/` | SQL historis dan query lama |

SQL historis tidak dianggap sebagai migration final. Setiap perubahan database production harus didokumentasikan dan ditinjau sebelum diterapkan.

## ⚠️ Documentation Notes

- Dokumentasi menggambarkan kondisi database berdasarkan hasil inspeksi.
- Detail kebijakan RLS perlu merujuk pada definisi policy aktual, bukan hanya jumlah policy.
- Objek internal Supabase pada schema `auth` dan `storage` dibedakan dari objek milik aplikasi.
- Tidak ada migration yang dijalankan hanya dengan menyalin SQL dari arsip historis.
- Perubahan pada database production harus dilakukan secara terkontrol.

---

**Project:** Kaizen Company Platform  
**Database Provider:** Supabase  
**Documentation Scope:** Database Structure, Relationships, Security, Storage, and SQL Audit
