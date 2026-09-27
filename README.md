# BOWOX STORE — Website Pembeli & Admin

Paket ini berisi **2 website** yang saling terhubung:

| File | Fungsi |
|---|---|
| `index.html` | Website untuk **PEMBELI** (buat akun/masuk, pilih paket, order, isi saldo, kirim bukti transfer) |
| `admin.html` | Website untuk **ADMIN** (buat akun/masuk, ACC order, cek bukti transfer, kirim link join / tandai selesai, ACC isi saldo) |
| `assets/qris.jpeg` | Gambar QRIS pembayaran toko Anda — **belum termasuk**, lihat bagian "QR Belum Muncul" di bawah |

---

## ⚠️ QR Belum Muncul / Rusak

Gambar QRIS asli toko Anda belum pernah saya terima, jadi QR-nya tampil patah (ikon gambar rusak). Ini **bukan bug kode**, filenya memang belum ada.

**Cara paling gampang (disarankan):** kirim/upload foto QRIS toko Anda (jpg/png) di chat ini, nanti saya tempelkan langsung ke dalam file HTML-nya — tidak perlu folder `assets` sama sekali, tinggal 2 file yang perlu diupload ke GitHub.

**Cara lain — pakai link hosting gambar (misal catbox.moe):**
1. Buka [catbox.moe](https://catbox.moe), upload foto QRIS Anda, salin link langsung yang dihasilkan (contoh: `https://files.catbox.moe/xxxxx.jpg`).
2. Buka `index.html` dengan Notepad, cari baris `const QRIS_IMAGE_URL = "assets/qris.jpeg";` (ada di bagian atas kode `<script>`).
3. Ganti isinya dengan link catbox tadi, contoh: `const QRIS_IMAGE_URL = "https://files.catbox.moe/xxxxx.jpg";`
4. Simpan, upload ulang `index.html` ke GitHub. QR akan langsung muncul, tanpa folder `assets` sama sekali.

**Kalau mau pakai folder assets sendiri:** buat folder `assets` persis di sebelah `index.html`, taruh gambar dengan nama persis `qris.jpeg` (biarkan `QRIS_IMAGE_URL` tetap `assets/qris.jpeg`).

---

## Alur Sistem

1. Pembeli buka `index.html` → **Buat Akun** (username, email, password, ulangi password) kalau baru pertama kali, atau **Masuk** kalau sudah punya akun.
2. **Isi Saldo dulu**: isi nominal → tekan **ISI SALDO SEKARANG** → QR & nominal transfer muncul → transfer → tekan **SAYA SUDAH TRANSFER** → upload bukti → admin tekan **ACC** di `admin.html` → saldo bertambah otomatis. Semua mutasi (isi saldo, dipakai order, refund) tercatat di **Riwayat Saldo**.
3. Pembeli pilih paket → tekan **PESAN SEKARANG**:
   - Untuk layanan *suntik* (Followers/Views/Likes TikTok & Instagram): **wajib** isi link/username akun yang mau di-suntik.
   - Untuk layanan lain (MurSC, Akun Telegram, Jasa Website): tidak perlu isi apa-apa lagi, tinggal pesan.
   - Kalau saldo tidak cukup, muncul pop-up **"Saldo Belum Cukup"** dengan tombol langsung ke Isi Saldo — order tidak bisa lanjut sebelum saldo cukup.
   - Kalau saldo cukup: **saldo langsung terpotong otomatis**, tidak perlu transfer / kirim bukti lagi per order.
4. Admin buka `admin.html` → **Masuk** → tekan **ACC** atau **TOLAK**. Kalau **TOLAK**, saldo yang sudah terpotong otomatis dikembalikan ke pembeli (tercatat di Riwayat Saldo).
5. Setelah **ACC**:
   - Layanan *suntik* → admin proses ke akun target, lalu tekan **TANDAI SELESAI**.
   - Layanan lain (MurSC/Telegram/Website) → admin tekan **KIRIM LINK JOIN**, isi link → langsung muncul di *Pesanan Saya* milik pembeli. Order otomatis dianggap selesai begitu link diterima.

---

## Login Pembeli & Admin

Baik pembeli maupun admin sekarang pakai **akun sendiri** (username + password), bukan sekadar ketik nama:

- **Buat Akun**: username, email, password, ulangi password. Username tidak boleh dobel, jadi saldo & histori pesanan pasti aman tersimpan di akun masing-masing.
- **Masuk**: username + password.
- **Lupa Password**: masukkan username + email yang didaftarkan → langsung bisa set password baru. Karena situs ini statis (tanpa server), resetnya lewat pencocokan username+email, bukan email sungguhan yang terkirim.
- **Akun admin default**: username `bowox`, password `bowox2024` — langsung bisa dipakai. Akun ini belum punya email; login dulu → tab **AKUN SAYA** → isi email supaya "Lupa Password" bisa dipakai untuk akun ini juga.
- Tombol dengan nama akun di pojok kanan atas (pembeli) berfungsi untuk **keluar/logout** dari akun.

---

## Cara Menjalankan di GitHub Pages (Gratis)

1. Buat akun di [github.com](https://github.com) jika belum punya.
2. Klik tombol **New** (atau **New repository**) → beri nama misalnya `bowox-store` → pilih **Public** → klik **Create repository**.
3. Di halaman repo, klik **uploading an existing file**.
4. Seret/upload `index.html`, `admin.html`, dan `README.md`. Kalau sudah punya gambar QRIS, buat juga folder `assets` berisi `qris.jpeg` lalu upload sekalian.
5. Klik **Commit changes** di bagian bawah.
6. Masuk ke tab **Settings** (di repo yang sama) → menu **Pages** di sidebar kiri.
7. Di bagian **Branch**, pilih **main** dan folder **/ (root)** → klik **Save**.
8. Tunggu 1–2 menit, lalu website Anda aktif di:
   - Pembeli: `https://USERNAME.github.io/bowox-store/`
   - Admin: `https://USERNAME.github.io/bowox-store/admin.html`

   (Ganti `USERNAME` dengan username GitHub Anda, dan `bowox-store` kalau nama repo-nya beda.)

### Kalau mau coba dulu tanpa GitHub
Cukup taruh `index.html`, `admin.html`, dan folder `assets` dalam satu folder yang sama di komputer/HP, lalu buka `index.html` langsung dua kali klik. Semua fitur jalan normal, hanya saja data hanya tersimpan di browser itu saja (lihat catatan di bawah).

---

## Catatan Penting

- Data order, saldo, dan akun tersimpan di **browser (localStorage)**. Website pembeli dan admin **harus diakses dari domain & browser yang sama** agar datanya nyambung (contoh: admin dan pembeli sama-sama lewat link GitHub Pages Anda, dan admin tidak memakai mode incognito).
- File bukti transfer maksimal ±800KB (screenshot biasa sudah cukup).
- Untuk reset semua data (akun, order, saldo): buka browser → tekan F12 → tab Console → ketik `localStorage.clear()` → Enter.
- Ini semua berjalan di sisi browser (client-side), jadi cocok untuk skala kecil-menengah. Kalau nanti ingin data tersimpan online dan sinkron lintas perangkat (HP pembeli ↔ laptop admin secara real-time), perlu backend seperti Firebase — bisa minta dibuatkan versi itu terpisah.

© 2026 BOWOX STORE
