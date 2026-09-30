# Birthday Surprise

Halaman ulang tahun statis: satu `index.html`, tanpa build, tanpa server. Semua teks diatur dari satu objek `CFG`, jadi bisa dipakai ulang tiap tahun.

## Isi folder

| File | Fungsi |
|---|---|
| `index.html` | Seluruh halaman (HTML, CSS, JS) |
| `vercel.json` | Pengaturan Vercel (URL bersih, cache foto) |
| `img/` | Foto: `1.jpg`-`4.jpg` untuk cerita, `g1.jpg` dst. untuk galeri |

## Kustomisasi (blok `CFG` di awal `<script>`)

| Kunci | Isi | Contoh |
|---|---|---|
| `name` | Nama yang berulang tahun | `'Sinta'` |
| `from` | Nama pengirim | `'Ayasa'` |
| `birthday` | Bulan-tanggal, format `MM-DD` | `'06-15'` |
| `since` | Tanggal server pertama, format `YYYY-MM-DD` | `'2024-01-01'` |
| `unlock` | Kunci kejutan sampai waktu ini. Kosong = tidak dikunci | `'2026-06-15T00:00:00+07:00'` |
| `gallery` | Daftar `{src, cap}` untuk galeri geser. `[]` = sembunyikan | lihat file |
| `chapters` | Daftar bab: `skip`, `sub`, `date`, `title`, `text`, `photo`, `back` | lihat file |

Tips foto: kompres ke lebar sekitar 1200 px (di bawah 300 KB per foto) supaya cepat dibuka di HP.

## Fitur

- **Cerita timeskip:** kartu foto yang bisa dibalik untuk membuka pesan rahasia.
- **Galeri:** geser dengan jari, tombol panah, atau keyboard.
- **Penghitung otomatis:** hari sejak server pertama dan hitung mundur ke ulang tahun berikutnya.
- **Kue dan permintaan:** permintaan ditulis sebelum lilin ditiup, disimpan per tahun, dan ditampilkan lagi tahun depan.
- **Musik:** kotak musik WebAudio berisi 4 bagian bergantian (lagu, arpeggio, lagu naik nada, arpeggio), dengan volume dan timer tidur 5/15/30 menit. Saat timer habis, musik memudar lalu berhenti.
- **Interaksi:** ketuk hewan untuk pencapaian; ketuk latar kosong dan ikan berenang ke titik itu.

## Deploy ke Vercel

**Lewat GitHub**
1. Buat repository baru, upload isi folder ini.
2. Di Vercel: Add New > Project > pilih repository.
3. Framework Preset: **Other**. Kosongkan Build Command dan Output Directory. Deploy.

**Lewat CLI**
```bash
npm i -g vercel
cd birthday-vercel
vercel --prod
```

Update berikutnya: ubah `CFG` atau ganti foto, lalu push (GitHub) atau jalankan `vercel --prod` lagi.

## Pakai ulang tahun depan

1. Tambah bab atau foto baru di `chapters` dan `gallery`.
2. Perbarui `unlock` jika ingin dikunci lagi.
3. Push. `since` dan `birthday` tetap, jadi penghitung menyesuaikan sendiri.

## Cek sebelum dikirim

- [ ] Nama, tanggal, dan teks contoh sudah diganti
- [ ] Semua foto ada di `img/` dan namanya sama dengan di `CFG`
- [ ] Coba di HP: ketuk Putar musik, atur timer, tiup lilin
- [ ] Jika memakai `unlock`, tes dengan `?preview` di akhir URL

## Batasan

- **Kunci kejutan hanya menutup tampilan.** Isi halaman tetap ada di source dan bisa dilihat lewat "View Source". Untuk rahasia sungguhan, jangan taruh di halaman ini. Tambahkan `?preview` di URL untuk melewati kunci saat menguji.
- **Data tersimpan di browser** (`localStorage`): permintaan, jumlah ketukan, volume. Data hilang kalau dia ganti perangkat atau menghapus data browser.
- **Musik hanya mulai setelah ketukan.** Aturan autoplay browser, terutama di iPhone.

## Pemecahan masalah

| Masalah | Penyebab dan solusi |
|---|---|
| Foto tidak muncul | Nama atau lokasi file tidak cocok dengan `CFG`. Perhatikan huruf besar-kecil di Linux/Vercel |
| Halaman terkunci terus | `unlock` masih di masa depan atau zona waktu keliru. Pakai akhiran `+07:00` untuk WIB |
| Tidak ada suara | Ketuk **Putar musik** dulu, cek volume dan mode senyap di HP |
| Perubahan tidak terlihat | Refresh keras (Ctrl+Shift+R), atau cek apakah deploy terbaru sudah selesai |
