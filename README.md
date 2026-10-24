# Prediksi SPMB SMP Negeri Kota Bandung

Dashboard dan model sederhana untuk memperkirakan peluang seorang siswa SD diterima di SMP negeri Kota Bandung, memakai data resmi SPMB 2023–2026.

**Coba langsung:** https://rendynoa.github.io/prediksi-spmb-smp-bandung/

## Latar belakang

Sejak 2025, penerimaan SMP negeri di Kota Bandung memakai SPMB (pengganti PPDB). Jalur zonasi diganti jalur domisili, dan mulai 2026 jalur prestasi rapor ikut menghitung nilai TKA. Informasi yang beredar di media sering tidak lengkap, sementara datanya sebenarnya terbuka di situs resmi.

Proyek ini lahir dari kebutuhan nyata: membantu keluarga memilih strategi pendaftaran SMP (jalur rapor, kejuaraan, atau domisili) berdasarkan data, bukan kabar dari grup WhatsApp.

## Fitur

- **Kalkulator nilai rapor**: input nilai per mapel per semester, peringkat kelas, dan nilai TKA (B. Indonesia & Matematika), lalu dihitung dengan rumus resmi 2026.
- **Peluang jalur prestasi**: rapor atau kejuaraan, untuk 75 SMPN se-kota. Pilihan sekolah bisa memakai rekomendasi otomatis atau dipilih sendiri.
- **Skor piagam kejuaraan** sesuai tabel resmi Panduan SPMB 2026.
- **Simulasi jalur domisili** untuk 19 SMPN Wilayah B (Bandung timur), berdasarkan tren batas jarak 2023–2026.
- **Data SMA 2026** (SPMB Jawa Barat) untuk melihat peluang domisili ke SMAN dari titik rumah.
- **Workbook Excel** dengan rumus yang sama, bisa diubah asumsinya.

## Isi repositori

| File | Isi |
|---|---|
| `index.html` | Dashboard interaktif (satu file, tanpa server) |
| `Prediksi_SPMB_SMP_Bandung.xlsx` | Workbook: sumber & metode, kalkulator, data per sekolah |
| `data/smp_kota_2026.csv` | 75 SMPN: lokasi, kuota & pendaftar, batas skor rapor dan kejuaraan 2026 |
| `data/smp_wilayah_b_domisili.csv` | 19 SMPN Wilayah B: batas jarak domisili 2023–2026, skor rapor terendah 2023–2025 |
| `data/sma_kota_2026.csv` | 27 SMAN: kuota, batas skor rapor, batas jarak domisili 2026 |
| `data/skor_kejuaraan_2026.csv` | Tabel skor piagam kejuaraan |

## Sumber data

- [spmb.bandung.go.id](https://spmb.bandung.go.id): Rekapitulasi 2023–2025, Info Sekolah, Hasil Seleksi Tahap 1 & 2 tahun 2026, Panduan SPMB 2026.
- [spmb.jabarprov.go.id](https://spmb.jabarprov.go.id): klasemen final SMAN Kota Bandung 2026.

Data diambil Oktober 2026 dari halaman publik. Repositori ini **hanya menyimpan statistik per sekolah** (kuota, jumlah pendaftar, skor/jarak terendah, median, tertinggi). Nama dan data pribadi siswa tidak disimpan.

## Metode singkat

- **Skor rapor (Panduan 2026):** `NA = 70% × (40% × rata-rata rapor 8 mapel + bobot peringkat) + 30% × TKA`. Bobot peringkat = `60 − (60/28) × (n − 1)` untuk peringkat 1–3, selain itu 0. Rumus ini dicek terhadap skor siswa yang benar-benar diterima pada 2026.
- **Peluang rapor:** skor siswa dibandingkan dengan skor terendah yang diterima tahun 2026, dengan ketidakpastian normal (TKA ±7 poin, pergeseran batas ±1,8 poin untuk sekolah selektif).
- **Peluang kejuaraan:** skor piagam tertinggi dibandingkan dengan skor terendah yang diterima 2026.
- **Peluang domisili:** batas jarak 2027 dimodelkan log-normal dari batas 2023–2026 (bobot 5/15/25/55%).
- **Peluang gabungan:** `1 − (1 − P1)(1 − P2)`, pilihan dianggap independen.

## Keterbatasan

- Rumus rapor dengan TKA baru dipakai satu tahun (2026), jadi model belum bisa diuji mundur.
- Batas jarak domisili sekolah baru/kecil bisa melonjak tajam antar-tahun.
- Perilaku pendaftar tahun berikutnya tidak bisa diprediksi.
- "Sekolah diminati" di sini berarti selektif (skor masuk & rasio peminat), bukan ukuran mutu pengajaran.
- Aturan tahun berikutnya bisa berubah. Baca persentase sebagai kategori (tinggi / sedang / rendah), bukan angka pasti.

## Penafian

Proyek independen, bukan situs resmi Dinas Pendidikan Kota Bandung atau Provinsi Jawa Barat. Selalu cek aturan terbaru di situs resmi SPMB.

## Teknologi

HTML, CSS, JavaScript murni (tanpa framework), Excel (rumus `NORMSDIST`, `INDEX/MATCH`), Python (pengolahan data & pembuatan workbook).

## Lisensi

Kode dirilis dengan lisensi MIT (lihat `LICENSE`). Data bersumber dari situs resmi pemerintah dan tetap mengikuti ketentuan sumbernya.
