# simple-3dprinting-cost-calculator-v3.9.0
tested with anycubic cobra x 

📋 Ulasan Fitur & Kegunaan — Kalkulator Biaya 3D Printing v3.9.0

🎯 Tujuan Aplikasi

Aplikasi web single-file (HTML+CSS+JS) untuk menghitung Harga Pokok Produksi (HPP) dan estimasi harga jual produk 3D printing secara akurat, dengan dukungan multi-filamen. Cocok untuk hobbyist yang mulai jualan, UMKM, atau print farm kecil.

---

🔐 1. Sistem Login & Keamanan

Fitur Kegunaan
Login username + password Mencegah akses tidak sah saat file di-host publik
Password default admin/admin Bisa langsung dipakai, wajib diganti untuk produksi
Hash SHA-256 + salt Password tidak disimpan plaintext di localStorage
Migrasi password lama User lama dengan password plaintext otomatis di-hash ulang
Ganti password Via tombol 🔑 Password, verifikasi password lama
Session sessionStorage Login hilang saat tab ditutup (lebih aman)
Logout Hapus session, reload halaman

Kegunaan: Melindungi data harga & margin jual dari tangan yang tidak berhak.

---

🧵 2. Master Filamen

Fitur Kegunaan
Tambah/edit/hapus filamen Kelola daftar merek & jenis filamen (PLA, PETG, dll)
Harga per kg Basis kalkulasi biaya material per gram
Proteksi hapus Filamen yang sedang dipakai tidak bisa dihapus
Default 3 filamen PLA, PETG, PLA Generic — siap pakai
Persist di localStorage Data tidak hilang saat browser ditutup

Kegunaan: Satu kali input harga filamen → dipakai berulang untuk semua perhitungan berikutnya. Ganti harga cukup sekali, semua kalkulasi ikut update.

---

⚙️ 3. Pengaturan Dasar

Parameter Default Kegunaan
Tarif Listrik (Rp/kWh) 1500 Hitung biaya listrik printer
Daya Printer (kW) 0.35 Konsumsi rata-rata Kobra X
Depresiasi Mesin (Rp/jam) 1500 Cadangan beli printer baru
Margin Minimal (x) 2 Batas bawah harga jual
Margin Maksimal (x) 3 Batas atas harga jual
Biaya Tambahan:  
Packaging 3000 Bubblewrap, mailer, freebies
Stiker & Tinta 1000 Label produk
Switch/Gantungan 1000 Aksesoris gantungan
Reject/Gagal Cetak 10% Toleransi produk gagal

Fitur pintar:

· 🔔 Dirty tracking — Badge "● Belum disimpan" muncul saat ada perubahan belum disave
· 💾 Tombol simpan manual — Kontrol penuh kapan pengaturan di-commit
· ⚡ Shortcut Ctrl+S — Simpan cepat
· ⚠️ Warning unload — Cegah kehilangan perubahan
· 👁️ Live preview — Contoh hitungan real-time saat ubah angka

Kegunaan: Transparansi biaya operasional. Semua biaya "tak terlihat" (listrik, depresiasi, packing) dihitung, bukan cuma material.

---

➕ 4. Form Tambah Cetakan

Field Wajib Keterangan
Nama cetakan ✅ Cth: "Bracket HP 3 Warna"
Jumlah warna ❌ 1–5+ warna (info saja)
Jam & Menit cetak ✅ Waktu printing dari slicer
Waktu Purge Total (menit) ❌ Waktu purge multi-filamen
Mode biaya tambahan ✅ 🆕 3 opsi (lihat bawah)
Filamen (multi-baris) ✅ 1 baris = 1 filamen

🆕 Mode Biaya Tambahan Per Produk (v3.9.0)

Mode Yang Dihitung Contoh Kasus
✅ Dengan Biaya Tambahan Reject + Packaging + Stiker + Switch Produk siap jual, packing lengkap
⚠️ Hanya Reject Reject saja (% material) Produk butuh toleransi gagal, tanpa packing
🚫 Tanpa Biaya Tambahan Semua extra = Rp 0 Digital file, sampel, langsung serah

Kegunaan: Fleksibilitas — tidak semua produk butuh gantungan atau packing. Sekarang bisa dibedakan per produk, dan hasilnya langsung terlihat di tabel (badge warna berbeda).

Multi-Filamen Per Cetakan

· Bisa tambah banyak baris filamen
· Setiap baris: pilih filamen + berat (gram) + purge (gram)
· Harga tiap filamen dikalikan terpisah
· Cocok untuk cetakan multi-warna / multi-material

Kegunaan: Akurat untuk model kompleks. Bracket 3 warna? Input 3 baris filamen, hasilnya akurat.

---

📊 5. Tabel Rekap Kalkulasi

Kolom Isi
No Urutan
Nama Cetakan Nama produk
Warna Badge jumlah warna
Filamen Badge per filamen + berat
Total Berat Total gram semua filamen
Waktu Format "Xj Ym"
Material Biaya filamen
Listrik Daya × waktu × tarif
Mesin Depresiasi × waktu
Biaya Tambahan 🆕 Badge mode + nominal
Total Biaya HPP lengkap
Estimasi Jual Range min-max
Aksi ✎ Edit / ⧉ Duplikat / ✕ Hapus

Fitur tabel:

· 🔍 Pencarian — Cari berdasarkan nama
· ↕️ Sorting — Klik header kolom untuk sort asc/desc
· 📄 Pagination — 25 baris per halaman
· Σ Total keseluruhan — Footer dengan grand total semua produk
· 🎨 Badge mode — Visual jelas mana produk pakai extra, mana tidak

Kegunaan: Dashboard lengkap — dari HPP sampai harga jual, sekali lihat.

---

💾 6. Aksi Per Produk

Aksi Ikon Kegunaan
Edit ✎ Load data ke form, ubah, simpan ulang
Duplikat ⧉ Copy produk + " (Copy)", edit cepat
Hapus ✕ Hapus dengan konfirmasi

Teknis: Menggunakan event delegation (data-action + data-id), aman dari karakter khusus di ID.

---

📤 7. Export & Cetak

📥 Export CSV

· Header + semua kolom termasuk Mode Biaya Tambahan
· Anti CSV injection (escape =, +, -, @)
· UTF-8 BOM — aman dibuka di Excel Indonesia
· Sertakan rincian biaya, daftar filamen, pengaturan

📊 Export Excel (.xlsx)

· Format rapi dengan merge cell header
· Column width optimal
· Multi-section: data, total, rincian, daftar filamen, pengaturan

🖨️ Print (A4 Landscape)

· Layout landscape otomatis
· Tabel 13 kolom rapi dengan table-layout: fixed
· Header berulang di tiap halaman
· Footer lisensi
· Petunjuk orientasi landscape di mobile

Kegunaan: Laporan profesional untuk klien, arsip, atau analisis di Excel.

---

🎨 8. UX & UI

Fitur Kegunaan
Panel collapsible Hemat ruang, fokus ke bagian penting
State panel tersimpan Preferensi layout diingat
Toast notification Feedback instan (✅ ❌ ℹ️ ⚠️)
Modal animasi UX halus & profesional
Responsive Bekerja di HP & desktop
Keyboard shortcut Ctrl+S untuk simpan
Warning sebelum unload Cegah kehilangan data

---

🧮 9. Rumus Kalkulasi

```
Material   = Σ (berat + purge) × harga_filamen / 1000
Listrik    = daya_kW × waktu_jam × tarif_kWh
Mesin      = waktu_jam × depresiasi_per_jam
Extra:
  - full        = reject% × material + packaging + stiker + switch
  - reject-only = reject% × material
  - none        = 0
HPP        = material + listrik + mesin + extra
Jual Min   = HPP × margin_min
Jual Max   = HPP × margin_max
```

---

💡 10. Skenario Penggunaan Nyata

Skenario A — Produk siap jual

· Mode: Dengan Biaya Tambahan
· Bracket HP, packing bubblewrap + stiker + gantungan
· HPP lengkap, margin 2–3×

Skenario B — Sample untuk klien

· Mode: Tanpa Biaya Tambahan
· Sample dikirim polos tanpa packing
· HPP hanya material + listrik + mesin

Skenario C — Print farm

· Mode: Hanya Reject
· Produk massal, toleransi 10% gagal
· Packing dilakukan terpisah (tidak masuk HPP)

Skenario D — Analisis profit

1. Input semua produk
2. Lihat total di footer
3. Export Excel → analisis di spreadsheet
4. Bandingkan margin produk A vs B

---

⭐ Kelebihan

✅ Single file — Tidak butuh server, bisa dibuka offline
✅ Persisten — localStorage, data tidak hilang
✅ Aman — Password ter-hash, XSS hardening
✅ Fleksibel — Multi-filamen, mode biaya per produk
✅ Lengkap — HPP + harga jual + export + print
✅ Gratis & open source — GPL-3.0, bebas modifikasi
✅ UX modern — Toast, modal, panel collapsible, responsive

---

⚠️ Keterbatasan

· Data hanya tersimpan di browser lokal (tidak sync antar device)
· Tidak ada backup otomatis — disarankan export Excel berkala
· Tidak ada multi-user — hanya 1 akun admin
· Persentase reject bersifat global (belum per produk)
· Tidak ada history perubahan — edit langsung overwrite

---

🎯 Kesimpulan

v3.9.0 adalah versi paling matang dari kalkulator ini. Penambahan mode biaya tambahan per produk menjawab kebutuhan nyata: tidak semua produk butuh packing/gantungan lengkap. Kolom tabel yang menampilkan badge mode memudahkan membedakan produk mana yang pakai extra dan mana yang tidak — sesuatu yang tidak ada di kalkulator 3D printing biasa.

Cocok untuk:

· 🎨 Hobbyist yang mulai jualan karya 3D print
· 🏪 UMKM yang butuh hitung HPP cepat & akurat
· 🖨️ Print farm yang kelola banyak SKU
· 📊 Reseller yang butuh analisis margin per produk
