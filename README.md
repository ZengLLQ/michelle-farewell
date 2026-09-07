# Farewell Michelle

Halaman surat perpisahan personal untuk Michelle dengan nuansa ungu, kartu kaca, latar 3D, dan animasi saat membaca. Dibangun menggunakan React untuk pengalaman membaca satu halaman di desktop maupun ponsel.

## Fitur

- Pembuka dengan animasi teks dan petunjuk scroll.
- Tujuh paragraf surat yang muncul bertahap saat masuk viewport.
- Latar 3D dengan bentuk organik, partikel, serta warna dan kamera yang mengikuti scroll.
- Kartu kaca dengan tilt mouse, percikan klik/tap, dan scroll halus.
- Indikator progres membaca dan tanda tangan bergaya tulisan tangan.

## Mulai cepat

Siapkan Node.js dan Yarn Classic **1.22.22**, sesuai `packageManager` frontend. Repository tidak mengunci versi Node. Dari root proyek, jalankan di PowerShell:

```powershell
cd frontend
yarn install --frozen-lockfile
yarn start
```

Buka [localhost:3000](http://localhost:3000). Root tidak memiliki `package.json`; jalankan Yarn dari `frontend` menggunakan `frontend/yarn.lock`.

Halaman saat ini tidak memerlukan backend, MongoDB, atau environment variable frontend. Isi surat tersimpan dalam komponen React.

## Dokumentasi

| Panduan | Isi |
| --- | --- |
| [Pengembangan](docs/DEVELOPMENT.md) | Setup, arsitektur, konfigurasi, build, verifikasi, dan troubleshooting |
| [Kustomisasi](docs/CUSTOMIZATION.md) | Mengubah surat, nama, warna, dan animasi |
| [Backend opsional](docs/BACKEND.md) | Setup Python/MongoDB, environment, dan API |
| [Frontend](frontend/README.md) | Ringkasan perintah frontend |

## Struktur proyek

```text
farewell-michelle/
├── frontend/
│   ├── public/index.html     # HTML, metadata, skrip eksternal
│   ├── src/App.js            # Komposisi halaman dan scroll
│   ├── src/components/      # Konten dan efek visual
│   ├── src/components/ui/   # Komponen UI pendukung
│   ├── craco.config.js      # Alias dan dev server
│   ├── package.json
│   └── yarn.lock
├── backend/
│   ├── server.py            # FastAPI dan penyimpanan status
│   ├── requirements.txt
│   └── pytest.ini
├── docs/                    # Panduan proyek
├── memory/PRD.md             # Catatan kebutuhan awal
├── design_guidelines.json    # Referensi desain
└── test_result.md            # Catatan pengujian historis
```

## Teknologi

| Bagian | Teknologi |
| --- | --- |
| UI | React 19, Tailwind CSS 3 |
| Animasi | Framer Motion 11, Lenis |
| 3D | Three.js, React Three Fiber, Drei |
| Tooling | react-scripts 5, CRACO 7, Yarn Classic |
| Backend opsional | FastAPI, Pydantic, Motor, MongoDB |

## Build produksi

Dari folder `frontend`:

```powershell
yarn build
```

Hasil ada di `frontend/build/` untuk hosting statis. Lihat [panduan hosting](docs/DEVELOPMENT.md#build-dan-hosting). Repository tidak menetapkan URL deployment produksi.

## WebStorm

Pilih **File > Open**, lalu buka folder root `farewell-michelle`. Buka `README.md` untuk navigasi dokumentasi. Jalankan perintah frontend melalui terminal terintegrasi, atau buat run configuration untuk script `start` dalam `frontend/package.json`.

## Status implementasi

Frontend belum terhubung ke backend. Tidak ada login, formulir pengiriman surat, atau editor konten. HTML memuat skrip Emergent dan inisialisasi PostHog; font dimuat dari Google Fonts. Frontend tidak sepenuhnya offline meskipun tidak memakai API lokal.

Dokumentasi menjelaskan kode saat ini. Catatan PRD dan hasil tes historis bukan bukti bahwa semua rencana atau tes telah diterapkan pada versi sekarang.
