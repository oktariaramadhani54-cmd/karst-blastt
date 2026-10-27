# Integrasi Google Sheets — KarstBlast V11

Kode Apps Script di folder `google-apps-script/Code.gs` sudah dikonfigurasi untuk spreadsheet tujuan ini:

https://docs.google.com/spreadsheets/d/1t4E3sSmITD9qHuASmgGecfOXJL2u1mvFnix0inKxsF8/edit

## Langkah setup

1. Buka spreadsheet tersebut menggunakan akun Google yang punya akses **Editor**.
2. Pilih **Extensions / Ekstensi → Apps Script**.
3. Ganti kode contoh dengan seluruh isi `google-apps-script/Code.gs`, lalu simpan.
4. Buka **Project Settings → Script Properties → Add script property**. Tambahkan `KARSTBLAST_SYNC_KEY` dengan token acak minimal 16 karakter. Contoh hanya format; buat token sendiri dan jangan publikasikan.
5. Pilih **Deploy → New deployment → Web app**. Execute as: **Me**. Who has access: **Anyone** (dibutuhkan agar website statis dapat memanggil endpoint). Setujui izin Google.
6. Salin URL Web App yang berakhir `/exec`.
7. Buka website KarstBlast melalui HTTPS, panel **Google Spreadsheet**. Masukkan URL `/exec` dan token yang sama dengan Script Properties, pilih **SIMPAN KONFIGURASI**, lalu **TES KONEKSI**.
8. Setelah status terhubung, simpan data uji dengan **SIMPAN KE SHEETS**. Periksa tab `Log_Penyimpanan`, `Ringkasan_Blast`, dan `Arsip_Workspace` yang dibuat otomatis. Refresh dan uji **MUAT BACKUP TERAKHIR** hanya setelah memastikan snapshot uji benar.

Jika kode Apps Script diubah setelah deployment, buka **Deploy → Manage deployments** dan edit/update versi Web App agar perubahan terpakai.

## Penting

- Koneksi Google asli **belum terverifikasi** oleh build ini; tes V11 sebelumnya menggunakan mock endpoint.
- URL spreadsheet bukan URL Web App. Website memerlukan URL `/exec` dari deployment Apps Script, bukan link `/edit` di atas.
- Karena panel memakai JSONP, sync key terkirim sebagai parameter URL dan disimpan di localStorage. Jangan gunakan sistem ini untuk data rahasia/sensitif perusahaan. Batasi akses penyebaran endpoint/token dan rotasi token bila bocor. Untuk penggunaan produksi yang aman, gunakan OAuth/autentikasi dan backend serverless dengan secret tersimpan sebagai environment variable.
- Backup hanya mencakup working copy yang diserialisasi aplikasi; foto PSD, kalibrasi foto, canvas, dan dataset fragmen sesi tidak ikut.
