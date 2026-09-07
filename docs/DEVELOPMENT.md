# Panduan Pengembangan

## Setup

Gunakan Node.js yang kompatibel dengan dependency di `frontend/package.json` dan Yarn Classic 1.22.22. Repository tidak mempunyai `.nvmrc` atau deklarasi `engines` untuk mengunci Node. Browser memerlukan JavaScript dan WebGL untuk latar 3D. Python/MongoDB hanya diperlukan untuk [backend opsional](BACKEND.md).

Dari root proyek:

```powershell
cd frontend
yarn install --frozen-lockfile
yarn start
```

Server default berada di [localhost:3000](http://localhost:3000). Hentikan dengan `Ctrl+C`. Gunakan lockfile Yarn yang tersedia; hindari mencampur lockfile npm. Instalasi mengambil paket visual editing dari URL tarball dalam manifest.

## Arsitektur

`src/index.js` memasang `App` ke elemen `root`. `App` menjalankan Lenis melalui `requestAnimationFrame`, memasang latar dan efek tap, lalu merender `Hero`, `Letter`, dan `Signature`. Loop dan instance Lenis dibersihkan saat komponen dilepas.

| Komponen | Tanggung jawab |
| --- | --- |
| `Hero.js` | Pembuka, nama penerima, parallax, petunjuk scroll |
| `Letter.js` | Array konten dan kemunculan paragraf |
| `Signature.js` | Pesan penutup dan tanda tangan |
| `GlassCard.js` | Kartu kaca dan tilt mouse berbasis spring |
| `AuroraBackground.js` | Scene, kamera, material, dan partikel 3D |
| `TapSparkles.js` | Percikan pada event pointerdown |

Semua file komponen tersebut ada di `frontend/src/components/`. Latar membaca posisi scroll melalui ref dan memperbarui warna, rotasi, serta kamera setiap frame. Halaman tidak memasang router atau mengambil konten dari API. Dependency tambahan dan komponen `ui/` tidak semuanya digunakan oleh halaman aktif.

## Konfigurasi

| Lokasi / variabel | Fungsi |
| --- | --- |
| `craco.config.js` | Alias `@` ke `src`, lint hooks, kompatibilitas webpack-dev-server 5 |
| `tailwind.config.js` | Konfigurasi Tailwind |
| `jsconfig.json` | Resolusi import editor |
| `ENABLE_HEALTH_CHECK=true` | Plugin health check webpack dan endpoint pada dev server |
| `PORT` | Port development server |
| `PUBLIC_URL` | Base URL aset saat build untuk subpath |

Contoh mengganti port di PowerShell, dari `frontend`:

```powershell
$env:PORT = '3001'
yarn start
```

Sesudah server berhenti, hapus override dengan `Remove-Item Env:PORT`. Frontend tidak membutuhkan `.env` atau `REACT_APP_*` untuk halaman saat ini. File `.env` diabaikan Git.

Wrapper visual editing hanya dimuat pada mode development. Skrip eksternal dalam `public/index.html` tetap menjadi bagian HTML produksi.

## Build dan hosting

Dari `frontend`, jalankan `yarn build`. Gunakan direktori proyek hosting `frontend`, perintah instalasi `yarn install --frozen-lockfile`, perintah build `yarn build`, dan direktori publikasi `build`. Jika layanan bekerja dari root repository, sesuaikan langkah masuk folder dan gunakan `frontend/build` sebagai hasil publikasi.

Untuk subpath, set `PUBLIC_URL` sebelum build dan verifikasi URL aset pada lokasi sebenarnya. Sajikan hasil melalui HTTP; membuka `public/index.html` lewat `file://` tidak menjalankan aplikasi. Backend tidak perlu diterbitkan untuk halaman surat saat ini.

## Verifikasi perubahan

Untuk perubahan aplikasi, jalankan build dan periksa browser:

1. Pembuka, tujuh paragraf, dan tanda tangan lengkap, termasuk emoji dan karakter non-Latin.
2. Teks terbaca di ponsel maupun desktop tanpa scroll horizontal.
3. Progres scroll, kemunculan paragraf, latar, tilt mouse, dan percikan tap bekerja.
4. Console tidak menunjukkan error aplikasi dan aset build termuat melalui hosting.

`yarn test` tersedia, tetapi belum ada test case frontend dalam repository. Folder root `tests/` hanya berisi `__init__.py`; backend memiliki konfigurasi pytest, bukan kumpulan tes implementasi. `test_result.md` merupakan catatan historis.

Untuk dokumentasi, periksa kecocokan perintah dan path dengan kode, tautan lokal, serta `git diff --check`. Build saja tidak membuktikan animasi atau aksesibilitas benar. Kode belum menyediakan fallback WebGL khusus atau penanganan preferensi reduced motion.

## Troubleshooting

| Gejala | Pemeriksaan |
| --- | --- |
| `package.json` tidak ditemukan | Masuk ke folder `frontend` |
| `craco` tidak ditemukan | Instal dependency dari `frontend` |
| Port 3000 terpakai | Gunakan `PORT` lain |
| Paket visual editing gagal diunduh | Periksa akses host tarball yang tertera di manifest |
| Latar gagal atau lambat | Periksa WebGL, hardware acceleration, console, DPR, dan jumlah partikel |
| Font tanda tangan berbeda | Periksa akses Google Fonts; tersedia fallback cursive |
| Backend gagal karena environment | Isi `MONGO_URL` dan `DB_NAME` sebelum menjalankan server |

Kembali ke [README](../README.md).
