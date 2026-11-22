
# SQL Documentation

Folder ini menyimpan file SQL yang berkaitan dengan pengelolaan database Kaizen Company.

## Directory Structure

```text
sql/
├── README.md
├── migrations/
│   └── README.md
├── seeds/
│   └── README.md
└── archive/
    ├── README.md
    └── legacy_supabase_queries.sql
```

## SQL Categories

### 1. Migrations

Berisi perubahan database yang telah ditinjau dan disetujui untuk menjadi bagian dari riwayat perubahan schema.

Contoh:
- Create table
- Alter table
- Add column
- Add constraint
- Create index
- Create or update RLS policies

### 2. Seeds

Berisi query untuk memasukkan data awal atau data pengembangan.

Contoh:
- Initial data
- Development data
- Reference data

### 3. Archive

Berisi query historis dari proses pengembangan database.

File dalam archive berfungsi sebagai referensi historis dan bukan migration yang siap dijalankan.

## Naming Convention

Gunakan format berikut:

```text
YYYYMMDD_description.sql
```

Contoh:

```text
20261122_create_news_table.sql
20261123_add_news_slug.sql
20261124_update_news_rls.sql
```

## Guidelines

1. Gunakan nama file yang menjelaskan perubahan.
2. Pisahkan perubahan schema dari seed data.
3. Jangan menimpa migration lama yang sudah digunakan.
4. Periksa dampak perubahan terhadap data yang sudah tersimpan.
5. Tinjau keamanan RLS sebelum migration diterapkan.
6. Simpan query historis di folder archive.
