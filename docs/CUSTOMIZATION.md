# Kustomisasi Konten dan Tampilan

## Konten

| Yang diubah | Lokasi | Cara |
| --- | --- | --- |
| Baris judul | `frontend/src/components/Hero.js` | Edit array `lines` dan `MaskedLine` tambahan |
| Penerima | `frontend/src/components/Hero.js` | Edit elemen `data-testid="hero-name"` |
| Surat | `frontend/src/components/Letter.js` | Edit array `paragraphs`; satu string menghasilkan satu paragraf |
| Penutup dan pengirim | `frontend/src/components/Signature.js` | Edit kalimat penutup dan teks tanda tangan |
| Judul tab dan deskripsi | `frontend/public/index.html` | Edit `<title>` dan meta description |

Pertahankan sintaks string JavaScript yang valid dan simpan UTF-8 agar emoji serta karakter Mandarin utuh. Saat hanya mengubah desain, pertahankan isi string dan batas paragraf.

## Tampilan dan animasi

- **Palet latar:** `color`/`colorB` mesh, lampu, dan latar Canvas di `AuroraBackground.js`; warna body juga berada di `App.css`.
- **Kartu kaca:** radius, transparansi, blur, border, serta bayangan di `GlassCard.js`. Padding setiap bagian diatur saat kartu dipakai di `Hero.js` atau `Letter.js`.
- **Tipografi:** `.font-heading`, `.font-apple`, dan `.font-signature` di `App.css`. Caveat dimuat dari Google Fonts.
- **Lebar dan jarak:** kelas Tailwind `max-w-lg`, padding, `space-y-7`, dan breakpoint `sm:` di komponen konten.
- **Animasi teks:** properti `initial`, `animate`, `whileInView`, dan `transition` pada komponen masing-masing.
- **Scroll halus:** konfigurasi Lenis di `App.js`.
- **Percikan:** jumlah, ukuran, jarak, dan waktu pembersihan di `TapSparkles.js`; keyframe `burst` di `App.css`.
- **Beban rendering:** jumlah Sparkles, segmen sphere, dan DPR Canvas di `AuroraBackground.js`.

Nama komponen di atas relatif terhadap `frontend/src/components/`; `App.js` dan `App.css` berada di `frontend/src/`.

## Alur pembaruan

Konten dikompilasi bersama frontend. Mengganti surat memerlukan build dan publikasi ulang; tidak ada dashboard editor atau sumber konten remote. Jangan menaruh secret dalam komponen atau environment frontend karena hasilnya dapat dibaca browser.

Integrasi Emergent dan PostHog ada di `public/index.html`; font eksternal ada di HTML dan `App.css`. Perubahan integrasi perlu diperiksa pada build produksi.

Setelah mengedit, ikuti [verifikasi perubahan](DEVELOPMENT.md#verifikasi-perubahan).
