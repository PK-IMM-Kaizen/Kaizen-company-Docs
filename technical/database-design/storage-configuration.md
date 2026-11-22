# 📦 Supabase Storage Configuration

Dokumen ini mencatat konfigurasi bucket Supabase Storage yang ditemukan pada project Kaizen Company Platform.

## 1. Bucket Inventory

Hasil pemeriksaan menemukan enam bucket.

| No. | Bucket | Public Status |
|---:|---|---|
| 1 | `organization-assets` | Public |
| 2 | `pengurus_photos` | Public |
| 3 | `ekowir_images` | Public |
| 4 | `dad_photos` | Public |
| 5 | `dad_payments` | Public |
| 6 | `news_images` | Public |

Seluruh bucket ditemukan memiliki nilai `public = true` pada saat pemeriksaan.

## 2. Storage Usage

Pengelompokan berdasarkan nama bucket:

| Bucket | Perkiraan Penggunaan |
|---|---|
| `organization-assets` | Aset organisasi |
| `pengurus_photos` | Foto pengurus |
| `ekowir_images` | Gambar produk atau aktivitas Ekowir |
| `dad_photos` | Foto terkait pendaftaran DAD |
| `dad_payments` | Bukti pembayaran DAD |
| `news_images` | Gambar berita |

Keterangan penggunaan di atas merupakan interpretasi berdasarkan nama bucket. Struktur folder dan pemetaan file aktual perlu merujuk pada implementasi aplikasi.

## 3. Access Configuration

Supabase Storage menggunakan tabel internal pada schema `storage`, terutama:

- `storage.buckets`
- `storage.objects`

Akses terhadap file dipengaruhi oleh status public bucket dan policy pada objek Storage.

Bucket public memungkinkan file diakses menggunakan URL publik. Karena itu, file yang bersifat privat tidak seharusnya hanya mengandalkan penyembunyian URL.

## 4. Sensitive File Consideration

Bucket `dad_payments` perlu mendapatkan perhatian khusus karena digunakan untuk menyimpan bukti pembayaran pendaftaran.

Hal yang perlu dievaluasi:

- Apakah bukti pembayaran memang harus dapat diakses publik?
- Apakah URL file dapat dibagikan tanpa autentikasi?
- Apakah akses unduh perlu dibatasi kepada Admin dan Superadmin?
- Apakah file memiliki data personal yang tidak boleh tersebar?

Dokumen ini mencatat status public yang ditemukan dan tidak mengubah konfigurasi bucket production.

## 5. Storage Triggers

Pemeriksaan menemukan trigger internal pada schema `storage`, termasuk:

- `enforce_bucket_name_length_trigger`
- `protect_buckets_delete`
- `protect_bucket_control_insert`
- `protect_bucket_control_update`
- `protect_bucket_control_update_role`
- `wake_lifecycle_on_policy_write`
- `wake_lifecycle_on_versioning_enable`
- `enforce_versioning_status_transition`
- `protect_active_lifecycle_states`
- `protect_objects_delete`
- `update_objects_updated_at`

Trigger tersebut menjalankan fungsi internal Supabase Storage.

## 6. Maintenance Notes

- Jangan menghapus bucket production tanpa memeriksa referensi file pada aplikasi.
- Jangan mengubah status public/private tanpa mengevaluasi dampak URL yang sudah digunakan.
- Policy `storage.objects` harus diperiksa bersama konfigurasi bucket.
- Data pembayaran dan dokumen personal perlu diperlakukan sebagai data sensitif.

---

**Source:** Supabase Storage bucket and trigger metadata inspection.
