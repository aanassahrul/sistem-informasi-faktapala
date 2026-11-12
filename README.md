# Sistem Informasi UKM FAKTAPALA

Starter template backend untuk Sistem Informasi UKM FAKTAPALA menggunakan Laravel 12, MySQL, Bootstrap (Blade), dan Docker.

## Fitur/rencana modul
- Website publik: profil, berita, pengumuman, galeri, pendaftaran anggota.
- Admin: verifikasi pendaftaran, manajemen anggota, divisi, kepengurusan, kegiatan, inventaris, peminjaman, berita, pengumuman, galeri.
- Anggota: profil, kegiatan, pengajuan peminjaman dan riwayat.

## Struktur
```text
app/Models/                 Model Eloquent
app/Http/Controllers/       Controller (Admin, Anggota, Public)
app/Http/Middleware/        Middleware role
database/migrations/        Struktur 17 tabel
database/seeders/           Seeder role awal
resources/views/            Blade views
routes/web.php              Rute web
docker/                     Konfigurasi PHP
```

## Persyaratan
- Docker Desktop aktif
- Git
- Tidak perlu XAMPP untuk project ini

## Menjalankan project (Windows PowerShell)

1. Ekstrak ZIP, buka terminal pada folder project.
2. Buat file `.env` dari `.env.example`:
   ```powershell
   Copy-Item .env.example .env
   ```
3. Jalankan container:
   ```bash
   docker compose up -d --build
   ```
4. Install dependency Laravel:
   ```bash
   docker compose exec app composer install
   ```
5. Buat application key:
   ```bash
   docker compose exec app php artisan key:generate
   ```
6. Jalankan migration dan seeder:
   ```bash
   docker compose exec app php artisan migrate --seed
   ```
7. Buka:
   - Aplikasi: http://localhost:8000
   - phpMyAdmin: http://localhost:8080

> Catatan: Folder ini adalah starter scaffold. Untuk menjalankan Laravel secara penuh, buat kerangka Laravel 12 terlebih dahulu dengan `composer create-project laravel/laravel . "^12.0"` pada folder kosong, lalu salin/merge file template ini (khususnya `docker-compose.yml`, `Dockerfile`, `.env.example`, `routes`, `database`, dan `app`). Jangan menimpa file inti Laravel yang sudah ada tanpa membandingkannya.

## Database
Migration menyiapkan tabel inti: roles, users, pendaftaran_anggota, divisi, anggota, jabatan, periode_kepengurusan, pengurus, kegiatan, peserta_kegiatan, dokumentasi, inventaris, peminjaman, detail_peminjaman, berita, pengumuman, galeri.

Role awal: `admin` dan `anggota`. Pengunjung umum tidak perlu akun.

## Catatan keamanan dan pengembangan
- Aktifkan verifikasi email / validasi pendaftaran sebelum akun anggota dibuat.
- Gunakan hashing password bawaan Laravel.
- Terapkan middleware otorisasi; jangan hanya menyembunyikan menu di frontend.
- Gunakan transaksi database saat menerima pendaftaran dan saat menyetujui peminjaman.
- Atur upload file dengan validasi tipe dan ukuran.
- Tambahkan pagination, audit log, backup, dan pengujian sebelum deployment.
- Jangan commit `.env`, password, token, atau data anggota asli.

## GitHub
```bash
git init
git add .
git commit -m "Initial scaffold Sistem Informasi FAKTAPALA"
git branch -M main
git remote add origin https://github.com/USERNAME/sistem-informasi-faktapala.git
git push -u origin main
```
Buat repository kosong di GitHub terlebih dahulu, tanpa README/license otomatis.
