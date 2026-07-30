# Visualisasi WRF & WRF-Hydro — Siklon Tropis Cempaka (26–29 Nov 2017)

Rekap hasil visualisasi domain 3 (d03) WRF-ARW yang dicocokkan per-jam dengan output WRF-Hydro
(`CHRTOUT`, `RTOUT`, `GWOUT`, `LDASOUT`), sebagai bukti keterkaitan antara kondisi atmosfer (WRF)
dan respons hidrologi permukaan (WRF-Hydro) selama dampak Siklon Cempaka di pesisir selatan Jawa.

---

## 1. Ringkasan Simulasi

| Item | Keterangan |
|---|---|
| Kejadian | Siklon Tropis Cempaka, 26–29 November 2017 |
| Domain WRF | Triple-nested d01/d02/d03 (27 → 9 → 3 km), forcing ERA5 |
| Fokus visualisasi | Domain 3 (3 km), dicocokkan per-jam dengan WRF-Hydro |
| Sumber data WRF | Folder Drive `WRFOUT_Cempaka` (`wrfout_d03_YYYY-MM-DD_HH_00_00`) |
| Sumber data WRF-Hydro | Folder Drive `WRFHYDRO_OUT` (`CHRTOUT`, `RTOUT`, `GWOUT`, `LDASOUT`, `geo_em.d03`, `wrfinput_d03`, `streams.shp`) |
| Variabel WRF dipakai | Angin 10 m (U10/V10), curah hujan per jam (RAINNC+RAINC selisih antar waktu), tekanan permukaan laut (SLP, dikoreksi dari PSFC/T2/HGT) |
| Variabel WRF-Hydro dipakai | `streamflow`/`q_lateral`/`velocity`/`Head` (CHRTOUT), `zwattablrt`/`sfcheadsubrt`/`QSTRMVOLRT` (RTOUT), `SFCRNOFF`/`SOIL_M` (LDASOUT), `inflow`/`outflow`/`depth` (GWOUT) |
| Garis pantai | Dari kontur `LANDMASK` di `geo_em.d03` (tanpa cartopy untuk komputasi, cartopy hanya untuk peta zoom) |

## 2. Titik Tinjau (Review Locations)

| Lokasi | Latitude | Longitude |
|---|---|---|
| Cilacap | -7.7279 | 108.9961 |
| Kebumen | -7.6766 | 109.6537 |
| Purworejo | -7.7166 | 110.0111 |
| DIY | -7.7956 | 110.3695 |

Keempat titik ini dipakai konsisten di semua panel supaya perbandingan hujan (WRF) vs. respons debit/genangan (WRF-Hydro) bisa dibaca di lokasi yang sama.

---

## 3. Bukti Keterkaitan WRF ↔ WRF-Hydro

Urutan di bawah disusun dari **pemicu atmosferik (WRF)** → **respons hidrologi (WRF-Hydro)**, supaya alur sebab-akibatnya kelihatan jelas.

### 3.1 Panel Gabungan 2×3 — Angin, Hujan, Tekanan (WRF) vs. Debit, Kelembaban Tanah, Groundwater (WRF-Hydro)

Snapshot per-jam yang menampilkan sisi WRF dan WRF-Hydro berdampingan dalam satu figure, domain 3, saat siklon berada dekat puncak intensitasnya.

<img width="1987" height="1083" alt="snap 6x6 perbandingan WRF VS WRFHYDRO" src="https://github.com/user-attachments/assets/41101ebb-f605-4388-a6fb-346f1cc90f8a" />


**Yang dibuktikan:** pusat sirkulasi angin & sel hujan konvektif dari WRF (kiri atas & tengah atas) muncul bersamaan dengan naiknya debit sungai (`CHRTOUT`, kiri bawah) dan kelembaban tanah (`LDASOUT`, tengah bawah) di area yang sama — genangan permukaan (`RTOUT`, kanan bawah) baru muncul setelah sel hujan terbentuk, konsisten dengan urutan fisis hujan → runoff → genangan.

---

### 3.2 Peta Fokus Dampak Siklon — Hujan (WRF) vs Genangan & Status Banjir (WRF-Hydro)

Panel 2×2 yang di-zoom ke pesisir selatan Jawa, mencakup 4 titik tinjau, saat intensitas hujan sedang tinggi.

<img width="1776" height="1232" alt="fokus dampak hujan dan indikasi banjir WRFHYDRO" src="https://github.com/user-attachments/assets/237230d3-e938-486b-b5fe-555bab1005fe" />


**Yang dibuktikan:** klaster hujan intensitas tinggi (panel 1, WRF) di sekitar Kebumen–Purworejo–DIY sejalan spasial dengan genangan permukaan RTOUT (panel 3) dan indikator status genangan (panel 4, kategori ringan/waspada/banjir) yang justru paling padat di klaster wilayah yang sama — bukti langsung bahwa output WRF-Hydro merespons pola hujan WRF, bukan pola acak.

---

### 3.3 Peta Fokus Hidrologi — Jaringan Sungai, Genangan, dan Status Banjir (murni sisi WRF-Hydro, dicocokkan waktu WRF)

Panel 1×3 pada jam sesudah puncak hujan, menunjukkan bagaimana respons hidrologi berkembang/menurun.

<img width="2189" height="608" alt="fokus hidrologi banjir" src="https://github.com/user-attachments/assets/0bfb9018-06b5-48de-8114-a3fd6c34968e" />


**Yang dibuktikan:** dengan timestamp yang sudah dicocokkan ke jam WRF (per-jam, lihat bagian 8 notebook), pola genangan & status banjir di jam ini bisa dibandingkan langsung terhadap timestamp hujan WRF terkait (mis. dari 3.2) untuk melihat jeda waktu (lag) antara puncak hujan dan puncak genangan.

---

### 3.4 Peta Intensitas Aliran Sungai (Streamflow, CHRTOUT) — Domain 3

Snapshot jaringan sungai dengan intensitas debit air pada jaringan streams.shp, di jam sesudah kejadian hujan utama.

<img width="1281" height="807" alt="streamflow" src="https://github.com/user-attachments/assets/e80b8136-0beb-425a-b706-d2f0eefc009f" />


**Yang dibuktikan:** segmen sungai dengan debit tertinggi (kuning-hijau, mendekati skala atas colorbar) terkonsentrasi di sekitar Cilacap dan anak sungai yang menampung aliran dari area hujan lebat pada 3.1–3.2 — memperlihatkan propagasi debit dari hulu (area hujan) ke hilir (pesisir) sesuai arah aliran sungai riil.

---

## 4. Ringkasan Keterkaitan (untuk kesimpulan laporan)

| Tahap | Variabel WRF | Variabel WRF-Hydro | Pola yang teramati |
|---|---|---|---|
| Pemicu | Angin 10 m, tekanan minimum (jejak siklon) | — | Pusat tekanan rendah bergerak melintasi pesisir selatan Jawa |
| Curah hujan | Curah hujan per jam (RAINNC+RAINC) | Kelembaban tanah (SOIL_M) naik selaras | Sel hujan konvektif → tanah cepat jenuh di lokasi yang sama |
| Runoff | — | Surface runoff (SFCRNOFF), debit sungai (streamflow) naik | Debit sungai naik menyusul jam-jam hujan tinggi |
| Genangan/banjir | — | Genangan permukaan (RTOUT), status genangan (ringan/waspada/banjir) | Titik genangan/banjir berhimpit dengan klaster hujan terberat |

**Catatan penyusunan laporan:** dengan urutan 3.1 → 3.4 di atas, pembuktian keterkaitan WRF–WRF-Hydro dibangun secara kronologis-fisis (hujan → tanah jenuh → runoff → genangan/banjir → debit sungai ke hilir), bukan sekadar menampilkan gambar berdampingan.

---
