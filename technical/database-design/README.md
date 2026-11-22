
# Database Design

Dokumentasi ini berisi rancangan, struktur, keamanan, dan pengelolaan database untuk Kaizen Company.

Database menggunakan Supabase sebagai layanan backend database dan memanfaatkan PostgreSQL sebagai sistem manajemen basis data.

## Documentation Index

| Document | Description |
|---|---|
| [Database Schema](./database-schema.md) | Dokumentasi tabel, kolom, tipe data, dan relasi database |
| [RLS Policies](./rls-policies.md) | Dokumentasi Row Level Security dan aturan akses data |
| [SQL Documentation](./sql/README.md) | Panduan pengelolaan file SQL |
| [SQL Migrations](./sql/migrations/README.md) | Perubahan struktur database yang telah ditinjau |
| [SQL Seeds](./sql/seeds/README.md) | Data awal dan data pengembangan |
| [SQL Archive](./sql/archive/README.md) | Arsip query historis |

## Database Technology

| Component | Technology |
|---|---|
| Database Management System | PostgreSQL |
| Backend Platform | Supabase |
| Database Access | Supabase Client |
| Authentication | Supabase Auth |
| File Storage | Supabase Storage |
| Access Control | PostgreSQL Row Level Security (RLS) |

## Documentation Principles

1. Setiap perubahan struktur database harus terdokumentasi.
2. Perubahan database yang digunakan sebagai acuan implementasi harus disimpan sebagai migration.
3. Query untuk data awal dipisahkan dari migration.
4. Query historis tidak langsung dianggap sebagai migration aktif.
5. Setiap perubahan RLS harus melalui peninjauan keamanan.
6. Dokumentasi harus diperbarui ketika struktur database berubah.

## Important Notes

File SQL pada folder `archive/` merupakan kumpulan query historis dari proses pengembangan. File tersebut tidak boleh langsung dijalankan sebagai satu rangkaian migration tanpa pemeriksaan dan penyesuaian terlebih dahulu.

Dokumentasi ini akan diperbarui seiring perkembangan database Kaizen Company.
