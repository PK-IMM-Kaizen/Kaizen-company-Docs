# 🔐 Row Level Security (RLS)

Dokumen ini menjelaskan konfigurasi Row Level Security pada database Kaizen Company Platform.

## 1. RLS Status

Hasil pemeriksaan menunjukkan RLS aktif pada seluruh 12 tabel aplikasi di schema `public`.

| Metric | Result |
|---|---:|
| Application tables | 12 |
| Tables with RLS enabled | 12 |
| Tables without RLS | 0 |
| Detected policies | 47 |

Angka 47 merupakan jumlah policy yang terdeteksi pada cakupan tabel aplikasi dan Storage, bukan jumlah policy khusus untuk schema `public` saja.

## 2. Application Roles

Aplikasi menggunakan dua role utama:

### Superadmin

Superadmin memiliki seluruh hak operasional Admin, dengan tambahan kewenangan:

- Membuat akun Admin.
- Mengedit akun Admin.
- Menghapus akun Admin.

### Admin

Admin memiliki hak operasional yang sama dengan Superadmin untuk mengelola modul aplikasi.

Admin tidak memiliki kewenangan untuk membuat, mengedit, atau menghapus akun Admin lainnya.

## 3. Supabase Database Roles

Role aplikasi berbeda dari role PostgreSQL/Supabase.

| Database Role | Fungsi |
|---|---|
| `anon` | Permintaan tanpa autentikasi |
| `authenticated` | Permintaan dengan pengguna terautentikasi |
| `service_role` | Role layanan dengan hak istimewa tinggi |

RLS menentukan baris data yang dapat diakses oleh suatu request berdasarkan policy yang berlaku.

Dengan demikian, GRANT database dan hak akses aplikasi harus dibaca sebagai dua lapisan yang berbeda.

## 4. Policy Inventory

Pemeriksaan menemukan policy dengan kondisi seperti:

- `USING (true)`
- `WITH CHECK (true)`
- Policy dengan target role `public`

Kondisi tersebut tidak otomatis berarti seluruh pengguna aplikasi memiliki akses penuh. Efek akhirnya bergantung pada operasi policy, target role, kombinasi policy permissive/restrictive, serta GRANT yang berlaku.

Namun, policy dengan kondisi terbuka perlu ditinjau secara khusus, terutama pada tabel yang menyimpan data personal atau data administratif.

## 5. Authentication Trigger

Terdapat fungsi `handle_new_user()` yang dipanggil ketika user baru dibuat pada `auth.users`.

Fungsi tersebut membuat record profil dengan role awal `admin`.

```sql
INSERT INTO public.profiles (id, email, role)
VALUES (new.id, new.email, 'admin')
ON CONFLICT (id) DO NOTHING;
```

Perilaku ini merupakan bagian penting dari alur pembuatan akun. Dokumentasi ini mencatat perilaku yang ditemukan, bukan mengubah aturan provisioning akun production.

## 6. Security Review Notes

Hal-hal berikut perlu diperhatikan saat melakukan review policy:

1. Pastikan policy untuk tabel sensitif membatasi operasi sesuai kebutuhan aplikasi.
2. Pastikan role aplikasi diperiksa melalui sumber data yang tepercaya.
3. Hindari memberi pengguna kemampuan mengubah role dirinya sendiri tanpa kontrol otorisasi.
4. Periksa policy `INSERT`, `UPDATE`, `DELETE`, dan `SELECT` secara terpisah.
5. Periksa target role policy, termasuk penggunaan `public`.
6. Pastikan akses file Storage konsisten dengan policy tabel yang menyimpan path file.

## 7. Audit Scope Limitation

Inventarisasi saat ini telah mengonfirmasi status RLS dan jumlah policy. Akan tetapi, matriks izin final per tabel dan per operasi harus disusun dari definisi lengkap setiap policy.

Dokumen ini tidak menyimpulkan bahwa semua policy yang ada sudah benar atau salah hanya berdasarkan jumlah policy dan keberadaan `USING (true)`.

---

**Source:** Supabase RLS status and policy metadata inspection.
