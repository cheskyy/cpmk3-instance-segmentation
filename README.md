# CPMK3 Segmentasi Instance Indoor

Tugas ini membandingkan YOLO11n-seg, YOLO11s-seg, dan Mask R-CNN ResNet-50 FPN. Sesuai digit NRP 0, tiap model dicoba dengan ukuran input 320, 640, dan 960 piksel. Data latih dan validasi memakai ekspor COCO v2. Jumlah gambar per bagian pada data publik cocok dengan v5. Kecocokan tiap gambar dan label masih perlu dicek.

Dataset privat, hasil pelatihan, dan overlay untuk 40 foto HP ada di Kaggle. Codex dan Mask2Former membantu menyiapkan draf 352 mask. Drafnya masih perlu dicek di Roboflow. Halaman 2 laporan menunjukkan satu contoh pengeditan polygon pada foto yang cocok dengan set uji.

Riwayat Git mulai dicatat setelah rubrik tambahan diterima pada 23 November 2026. Notebook di repo ini mencatat cara kerja pada tiap tahap.

Evaluasi versi 4 selesai di Kaggle pada 24 November 2026. Tabel dan grafiknya bisa dibuka langsung dari repo ini.

## Berkas submission

1. **Laporan PDF** mengikuti urutan rubrik dan memuat lima studi kasus bergambar. [Buka atau unduh laporan](laporan/Visi_Komputer_Laporan_Chelsea_5054241010_Revisi.pdf)
2. **Tautan repositori ini** memberi akses ke riwayat commit, notebook, logbook, dan hasil evaluasi. Pastikan akun penilai mendapat akses jika GitHub menolak membuka repositori tanpa login.
3. **ZIP bukti pendamping** diserahkan sebagai lampiran. Isinya logbook, deklarasi AI, notebook, CSV pelatihan per epoch dan waktu GPU, tabel dan grafik hasil, panel prediksi, serta metadata EXIF untuk 40 foto HP. ZIP dapat dibuka tanpa akun Kaggle.

| Rubrik | Bukti yang tersedia | Catatan |
|---|---|---|
| Test set buatan sendiri | 40 foto HP, 11 kondisi sulit pada seleksi awal, tangkapan layar anotasi, EXIF di ZIP, skor dan domain shift. [Laporan PDF](laporan/Visi_Komputer_Laporan_Chelsea_5054241010_Revisi.pdf) · [Tabel domain shift](hasil/domain_shift.csv) | 352 mask merupakan draf yang masih perlu ditinjau. Ekspor yang dipakai COCO v2. [Versi v5 rujukan](https://universe.roboflow.com/panopticindoor/panoptic-indoor-segmentation/dataset/5) |
| Parameter NRP 0 | Tiga model × tiga input, yaitu 320, 640, dan 960 piksel. [Tabel](hasil/eksperimen_nrp_0.csv) · [Grafik](hasil/grafik/nrp_input_size.png) | Skor tertinggi 20,95% di validasi untuk YOLO11s-seg 960 px. |
| Hipotesis | [Logbook hipotesis run tambahan](logbook/2026-11-23-hipotesis-run-tambahan.md) | Catatan sebelum training pertama belum tersedia. |
| Analisis kegagalan | Lima studi kasus bergambar di halaman 5–6 PDF. [Tabel uji ulang](hasil/uji_lima_kasus.csv) | Model yang dianalisis adalah YOLO11n-seg. |
| Bukti proses | [Log pelatihan dan GPU](bukti/log-training/) · [Logbook 23 November](logbook/2026-11-23.md) · [Logbook 24 November](logbook/2026-11-24.md) | Riwayat Git bertahap tercatat sejak 23 November. |
| Penggunaan AI | [Deklarasi AI, prompt, dan koreksi](Deklarasi_AI.md) | Draf mask mencakup bantuan Codex dan Mask2Former. |
| Demo dan tanya jawab | [Notebook demo](notebooks/05-demo-foto-baru.ipynb) · [Langkah demo](#menjalankan-demo-foto-baru) | Inferensi pada foto baru dilakukan saat sesi. |

## Hasil dan catatan pengerjaan

- [Laporan lengkap dari persiapan data sampai hasil uji](laporan/README.md) · [Contoh gambar ground truth](laporan/README.md#2-anotasi-dan-contoh-ground-truth) · [Daftar pengujian yang sudah dilakukan](laporan/README.md#4-pengujian-yang-sudah-dilakukan)

- Hasil evaluasi asli disimpan di Version 4 dari notebook Kaggle privat `seaalautt/cpmk3-instance-segmentation`. Kode dan tabel yang bisa diperiksa dari repo atau ZIP tersedia di sini. [Notebook evaluasi](notebooks/04-perbandingan-sembilan-run.ipynb)
- [Tabel dan grafik hasil evaluasi](hasil/README.md)
- [CSV pelatihan asli dan waktu GPU](bukti/log-training/)
- [Logbook 23 November](logbook/2026-11-23.md) dan [pembaruan 24 November](logbook/2026-11-24.md)
- [Hipotesis run tambahan](logbook/2026-11-23-hipotesis-run-tambahan.md)
- [Deklarasi AI](Deklarasi_AI.md)

## Notebook

1. Ketiga model dilatih pada 640 piksel. YOLO11n juga dicoba pada 320 dan 960 piksel. [Notebook pelatihan awal](notebooks/01-pelatihan-awal.ipynb)
2. Lihat draf 352 mask pada 40 foto HP serta catatan perubahan dan overlay-nya. [Notebook audit revisi](notebooks/02-audit-revisi-mask-hp.ipynb)
3. YOLO11s dan Mask R-CNN juga dilatih pada 320 dan 960 piksel untuk percobaan NRP. [Notebook YOLO11s](notebooks/03-nrp-yolo11s-tambahan.ipynb) dan [notebook Mask R-CNN](notebooks/03-nrp-mask-r-cnn-tambahan.ipynb)
4. Sembilan checkpoint dinilai pada set validasi. Untuk dua set uji, ketiga model dibandingkan pada ukuran 640 piksel. Skor sebelum dan sesudah revisi label HP dihitung dengan prediksi yang sama. [Notebook evaluasi](notebooks/04-perbandingan-sembilan-run.ipynb)
5. Coba model yang sudah dilatih dengan foto baru. Saat tanya jawab, ambang skor dan kelas bisa dipilih langsung. [Notebook demo](notebooks/05-demo-foto-baru.ipynb)

## Menjalankan ulang evaluasi di Kaggle

Masuk ke Kaggle sebagai `seaalautt` atau pakai akun yang sudah diberi akses ke sumber privat. Cari nama atau ID di bawah ini lewat **Add Input**. Catatan dan log bisa dibuka langsung di GitHub.

| Nama di Kaggle | ID di Kaggle | Bukti di GitHub |
|---|---|---|
| CPMK3 Indoor Test40 | `seaalautt/cpmk3-indoor-test40` | [Catatan pembagian data](logbook/2026-11-23.md) |
| CPMK3 Review Mask HP | `seaalautt/cpmk3-review-mask-hp` | [Notebook audit anotasi](notebooks/02-audit-revisi-mask-hp.ipynb) |
| CPMK3 Training GPU | `seaalautt/cpmk3-training-gpu` | [Log waktu pelatihan awal](bukti/log-training/durasi/pelatihan-awal.csv) |
| CPMK3 NRP YOLO11s | `seaalautt/cpmk3-nrp-yolo11s` | [Log waktu YOLO11s tambahan](bukti/log-training/durasi/yolo11s-tambahan.csv) |
| CPMK3 NRP Mask R-CNN | `seaalautt/cpmk3-nrp-mask-r-cnn` | [Log waktu Mask R-CNN tambahan](bukti/log-training/durasi/mask-r-cnn-tambahan.csv) |

1. Impor notebook evaluasi ke Kaggle, pilih GPU, lalu aktifkan internet supaya sel pertama bisa memasang pustaka yang dibutuhkan.
2. Tambahkan kedua dataset dan output **Version 1** dari ketiga notebook pelatihan.
3. Pakai `RUN_TRAINING = False` untuk menilai checkpoint yang sudah ada. Notebook membaca input dari `/kaggle/input` dan menyimpan hasil ke `/kaggle/working/cpmk3_final`.

Hipotesis dibuat sebelum pelatihan tambahan. Catatan hipotesis sebelum pelatihan pertama masih belum tersedia. Metadata EXIF, overlay, dan gambar contoh kegagalan bisa dilihat di Output Kaggle.


## Menjalankan demo foto baru

1. Impor [notebook demo](notebooks/05-demo-foto-baru.ipynb) ke Kaggle. Dengan akun yang punya akses, tambahkan output privat `seaalautt/cpmk3-training-gpu` Version 1 dan `seaalautt/cpmk3-instance-segmentation` Version 4. Tambahkan setiap output satu kali.
2. Jalankan sel dari atas hingga muncul **Pilih foto**. Unggah JPG atau PNG baru, pilih model, lalu klik **Jalankan inferensi**. Foto dan mask prediksi muncul berdampingan.
3. Untuk menunjukkan perubahan ambang, geser **Ambang** dari 0,35 ke 0,60 pada foto yang sama. **Tampilkan AP** membaca skor per kelas dari evaluasi terdahulu.
