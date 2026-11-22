
# SQL Archive

Folder ini menyimpan kumpulan query SQL historis yang digunakan selama proses pengembangan database Kaizen Company.

## Archived Files

| File | Description |
|---|---|
| `legacy_supabase_queries.sql` | Kumpulan query Supabase historis, termasuk perubahan tabel, RLS, trigger, storage, dan data awal |

## Important Notes

File arsip merupakan dokumentasi historis, bukan migration final.

Kumpulan query dapat mengandung:
- Definisi tabel yang berulang.
- Perubahan kolom yang dilakukan pada waktu berbeda.
- Policy RLS yang sudah tidak digunakan.
- Konfigurasi Storage yang pernah berubah.
- Data pengembangan atau dummy.
- Query yang tidak aman untuk langsung diterapkan pada production.

## Usage Guidelines

1. Gunakan file ini sebagai referensi historis.
2. Jangan menjalankan seluruh isi file sekaligus pada database production.
3. Periksa kondisi schema aktif sebelum menggunakan query tertentu.
4. Tinjau ulang RLS dan Storage policies.
5. Pindahkan perubahan yang sudah diverifikasi ke folder migrations.
6. Pisahkan data awal yang valid ke folder seeds.

## Latest Archive

Arsip harus menggunakan kumpulan query terbaru yang telah diberikan, bukan versi sebelumnya.
