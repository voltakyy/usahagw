# usahagw

[![Live demo](https://img.shields.io/badge/live-GitHub%20Pages-2f7d5a?style=flat-square&logo=github)](https://voltakyy.github.io/usahagw/)
[![Static site](https://img.shields.io/badge/stack-HTML%20%2B%20CSS%20%2B%20JS-D9A441?style=flat-square)](#stack)
[![SAK EMKM](https://img.shields.io/badge/laporan-sederhana%20SAK%20EMKM-197C7A?style=flat-square)](#laporan-yang-dihasilkan)

Pembukuan usaha mikro, kecil, dan menengah dalam satu halaman web. Catat omzet
dan beban harian, lalu baca hasilnya sebagai laporan yang mengikuti kerangka
penyajian **SAK EMKM**: laba rugi, neraca, dan catatan atas laporan keuangan.

**Live:** <https://voltakyy.github.io/usahagw/>

## Untuk siapa

Warung, toko, penyedia jasa, dan usaha rumahan yang butuh pembukuan rapi tanpa
langganan software akuntansi. Cocok untuk pemilik usaha yang ingin tahu:

- berapa omzet dan beban bulan ini;
- berapa laba bersih dan marginnya;
- berapa kas, piutang, utang, dan modal bersih saat ini;
- ke mana saja uang usaha mengalir.

## Fitur

- **Pendapatan dan beban usaha** dengan kategori yang sudah dipetakan untuk kebutuhan pembukuan.
- **Kalender transaksi** untuk menelusuri arus kas per tanggal.
- **Utang dan piutang** yang tidak mengacaukan perhitungan laba.
- **Tabungan dan dana darurat** diperlakukan sebagai pemindahan kas, bukan beban.
- **Grafik** arus kas, tren harian, dan komposisi simpanan (Chart.js).
- **Indikator kesehatan keuangan**: rasio tabungan, rasio gaya hidup, likuiditas,
  dana darurat, dan skor literasi finansial.
- **Ekspor Excel lima sheet** dan cetak/simpan laporan sebagai PDF.
- **Cadangan JSON** untuk memindahkan data antar-perangkat.
- **Login Google** dan penyimpanan data per akun melalui Supabase.

## Laporan yang dihasilkan

| Laporan | Isi | Kegunaan |
| --- | --- | --- |
| Arus kas pemilik usaha | Saldo awal, masuk, keluar, saldo berjalan | Melihat uang tunai harian |
| Laba rugi bulanan | Pendapatan, beban, laba bersih, margin | Menilai untung/rugi periode |
| Neraca kumulatif | Aset = kewajiban + ekuitas | Melihat posisi keuangan |
| Jurnal umum | Debit dan kredit seimbang per transaksi | Jejak audit sederhana |
| CALK | Penjelasan angka dan kebijakan pencatatan | Melengkapi penyajian SAK EMKM |

Ekspor Excel berisi sheet `Laporan`, `Laba Rugi`, `Neraca`, `Jurnal Umum`, dan
`Ringkasan`. Laba rugi memakai angka bulan berjalan, sedangkan neraca memakai
posisi kumulatif.

## Alur pemakaian

1. Pasang target anggaran dan target tabungan di beranda.
2. Catat omzet setiap kali uang masuk, lalu catat beban saat uang keluar.
3. Buka tab **Laporan** untuk memeriksa arus kas, laba rugi, neraca, dan jurnal.
4. Unduh Excel atau cetak PDF pada akhir bulan.
5. Simpan cadangan JSON secara berkala dari tombol **Ekspor**.

## Stack

| Bagian | Teknologi |
| --- | --- |
| Antarmuka | HTML, CSS, JavaScript (tanpa framework, tanpa build step) |
| Grafik | Chart.js 4 |
| Excel | SheetJS (xlsx) |
| Autentikasi & database | Supabase Auth (Google) + Postgres |
| Hosting | GitHub Pages (statis) |

## Menjalankan lokal

```powershell
npx serve .
# atau
python -m http.server 8000
```

Buka alamat yang muncul, lalu masuk dengan akun Google. Jangan membuka
`index.html` lewat `file://` karena login Supabase membutuhkan origin HTTP.

Untuk instance sendiri, siapkan project Supabase dengan tabel `transactions`
dan `settings` ber-RLS, aktifkan provider Google, lalu sesuaikan
`supabase-client.js` dan daftar redirect URL.

## Struktur

```text
index.html           shell aplikasi dan seluruh markup laporan
login.html           halaman masuk Google
app.js               state, sinkronisasi, laporan, ekspor
style.css            sistem visual dan layout responsif
supabase-client.js   inisialisasi Supabase (sessionStorage)
DESIGN.md            batasan desain aplikasi
```

## Hubungan dengan gwcatat

`usahagw` adalah fork dari
[`gwcatat`](https://github.com/voltakyy/gwcatat-aplikasi-kelola-uang) yang
diarahkan ke pembukuan usaha. Mesin pencatatan, sinkronisasi, laporan, dan ekspor
masih satu keturunan; perbedaan utamanya ada pada branding dan penekanan sebagai
aplikasi pembukuan UMKM. Perbaikan inti di salah satu repo dapat dipindahkan ke
repo lainnya.

## Batasan

- Laporan mengikuti **penyederhanaan** SAK EMKM, bukan implementasi penuh seluruh
  standar akuntansi.
- Satu akun diperlakukan sebagai satu pembukuan usaha; belum ada pemisahan
  multi-cabang atau multi-unit.
- Aplikasi ini alat bantu pembukuan, bukan pengganti akuntan atau konsultan pajak.
- Keamanan data bergantung pada kebijakan RLS di project Supabase yang dipakai.
