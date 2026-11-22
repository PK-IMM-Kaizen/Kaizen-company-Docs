# ⚙️ Database Functions and Triggers

Dokumen ini mencatat fungsi dan trigger yang ditemukan pada database Kaizen Company Platform.

## 1. Application Function

Hasil pemeriksaan menemukan satu fungsi aplikasi:

| Function | Purpose |
|---|---|
| `handle_new_user()` | Membuat profil aplikasi ketika user baru dibuat pada Supabase Auth |

### Function Behavior

Fungsi `handle_new_user()` menjalankan operasi berikut:

```sql
INSERT INTO public.profiles (id, email, role)
VALUES (new.id, new.email, 'admin')
ON CONFLICT (id) DO NOTHING;
```

Perilaku yang teridentifikasi:

1. Mengambil ID dan email dari record user baru.
2. Membuat record pada `public.profiles`.
3. Memberikan nilai awal role `admin`.
4. Tidak membuat duplikasi apabila ID profil sudah tersedia.

## 2. Application Trigger

Ditemukan trigger berikut:

| Trigger | Schema | Table | Timing | Event | Function |
|---|---|---|---|---|---|
| `on_auth_user_created` | `auth` | `users` | AFTER | INSERT | `handle_new_user()` |

Trigger berjalan setelah record baru dimasukkan ke `auth.users`.

## 3. Supabase Internal Triggers

Pemeriksaan juga menemukan trigger internal pada schema `storage`.

Trigger tersebut berkaitan dengan:

- Validasi nama bucket.
- Proteksi penghapusan bucket dan objek.
- Proteksi perubahan konfigurasi bucket.
- Lifecycle state.
- Versioning.
- Pembaruan timestamp objek.

Trigger internal tersebut merupakan bagian dari infrastruktur Supabase Storage.

## 4. Audit Notes

- Fungsi `handle_new_user()` merupakan bagian dari proses provisioning akun.
- Perubahan fungsi perlu memperhatikan dampaknya terhadap proses registrasi dan pembuatan akun Admin.
- Trigger `on_auth_user_created` perlu dipertahankan apabila masih digunakan oleh alur autentikasi aplikasi.
- Fungsi dan trigger internal Supabase tidak boleh diubah sembarangan.

## 5. Inventory Summary

| Category | Result |
|---|---:|
| Custom application functions identified | 1 |
| Application trigger identified | 1 |
| Storage internal triggers identified | 13 |

Jumlah trigger internal mengikuti hasil metadata yang diperiksa pada saat audit.

---

**Source:** PostgreSQL function and trigger metadata inspection.
