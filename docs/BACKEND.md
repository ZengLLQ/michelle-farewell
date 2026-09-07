# Backend Opsional

`backend/server.py` menyediakan API contoh status menggunakan FastAPI dan MongoDB. Halaman surat tidak memanggil API ini.

## Setup PowerShell

Siapkan Python yang kompatibel dengan `requirements.txt` dan MongoDB lokal yang berjalan atau URI MongoDB yang dapat diakses. Repository belum mengunci versi Python.

Dari root proyek:

```powershell
cd backend
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

Buat `backend/.env` secara lokal:

```dotenv
MONGO_URL=mongodb://127.0.0.1:27017
DB_NAME=farewell_michelle
CORS_ORIGINS=http://localhost:3000
```

Ganti nilai sesuai lingkungan sendiri. `.env` diabaikan Git; jangan commit kredensial. Server membaca `.env` dari direktori backend.

Jalankan dari `backend`:

```powershell
.\.venv\Scripts\python.exe -m uvicorn server:app --reload --host 127.0.0.1 --port 8000
```

Dokumentasi API tersedia di [localhost:8000/docs](http://localhost:8000/docs). `--reload` dipakai untuk pengembangan.

## Environment

| Variabel | Wajib | Fungsi |
| --- | --- | --- |
| `MONGO_URL` | Ya | URI koneksi MongoDB |
| `DB_NAME` | Ya | Nama database |
| `CORS_ORIGINS` | Tidak | Origin dipisahkan koma; default `*` |

Dua variabel wajib dibaca saat import modul. Gunakan origin eksplisit sesuai frontend; parser tidak menghapus spasi setelah koma. Middleware mengaktifkan credentials serta mengizinkan semua metode dan header.

## Kontrak API

| Metode | Path | Input | Hasil |
| --- | --- | --- | --- |
| GET | `/api/` | Tidak ada | `{"message":"Hello World"}` |
| POST | `/api/status` | JSON `{"client_name":"local-check"}` | Objek status baru |
| GET | `/api/status` | Tidak ada | Array maksimal 1.000 status |

Objek status berisi `id` UUID string, `client_name` string, dan `timestamp` datetime UTC. Timestamp disimpan sebagai string ISO dalam koleksi `status_checks`. `_id` MongoDB tidak dikembalikan oleh endpoint daftar. Tidak ada pagination atau urutan eksplisit.

Contoh dari terminal lain:

```powershell
Invoke-RestMethod -Uri 'http://localhost:8000/api/'
Invoke-RestMethod -Uri 'http://localhost:8000/api/status' -Method Post -ContentType 'application/json' -Body '{"client_name":"local-check"}'
Invoke-RestMethod -Uri 'http://localhost:8000/api/status'
```

POST menambahkan satu dokumen ke database. `GET /api/` hanya membuktikan aplikasi menjawab, bukan koneksi database sehat. Operasi status membutuhkan MongoDB yang dapat diakses.

## Status dan pengujian

Endpoint belum mempunyai autentikasi atau otorisasi. Backend adalah scaffold status, bukan layanan surat lengkap. `requirements.txt` mencantumkan dependency lebih luas daripada import dalam server.

Konfigurasi pytest memerlukan `pytest-xdist` dengan `-n 2 --dist loadscope`. Setelah ada test case, jalankan dari `backend`:

```powershell
.\.venv\Scripts\python.exe -m pytest
```

Saat ini belum ada test case backend yang disertakan. Jika pip gagal mendapatkan paket, periksa pesan error dan sumber paket terkait; panduan ini tidak mengasumsikan semua dependency telah diuji pada setiap versi Python atau Windows.

Kembali ke [README](../README.md).
