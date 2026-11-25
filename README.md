# CPMK3 Segmentasi Instance Indoor

Tugas ini membandingkan YOLO11n-seg, YOLO11s-seg, dan Mask R-CNN ResNet-50 FPN. Sesuai digit NRP 0, tiap model dicoba dengan ukuran input 320, 640, dan 960 piksel. Data latih dan validasi memakai ekspor COCO v2. Jumlah gambar per bagian pada data publik cocok dengan v5. Kecocokan tiap gambar dan label masih perlu dicek.

Dataset privat, hasil pelatihan, dan overlay untuk 40 foto HP ada di Kaggle. Codex dan Mask2Former membantu menyiapkan draf 352 mask. Drafnya masih perlu dicek di Roboflow. Halaman 2 laporan menunjukkan satu contoh pengeditan polygon pada foto yang cocok dengan set uji.

Riwayat Git mulai dicatat setelah rubrik tambahan diterima pada 23 November 2026. Notebook di repo ini mencatat cara kerja pada tiap tahap.

Evaluasi versi 4 selesai di Kaggle pada 24 November 2026. Tabel dan grafiknya bisa dibuka langsung dari repo ini.

## Hasil dan catatan pengerjaan

- [Laporan revisi (PDF)](laporan/Visi_Komputer_Laporan_Chelsea_5054241010_Revisi.pdf)
- [Buka Output Kaggle versi 4](hasil/README.md)
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

Pakai akun Kaggle `seaalautt` untuk membuka dataset dan output pelatihan yang privat.

1. Impor notebook evaluasi ke Kaggle, pilih GPU, lalu aktifkan internet supaya sel pertama bisa memasang pustaka yang dibutuhkan.
2. Tambahkan dua dataset privat ke bagian Input. [Ekspor indoor dan foto uji](https://www.kaggle.com/datasets/seaalautt/cpmk3-indoor-test40) dan [patch anotasi HP](https://www.kaggle.com/datasets/seaalautt/cpmk3-review-mask-hp)
3. Tambahkan output versi 1 dari ketiga notebook pelatihan. [Pelatihan awal](https://www.kaggle.com/code/seaalautt/cpmk3-training-gpu/output), [Mask R-CNN tambahan](https://www.kaggle.com/code/seaalautt/cpmk3-nrp-mask-r-cnn/output), dan [YOLO11s tambahan](https://www.kaggle.com/code/seaalautt/cpmk3-nrp-yolo11s/output)
4. Pakai `RUN_TRAINING = False` untuk menilai checkpoint yang sudah ada. Notebook membaca input dari `/kaggle/input` dan menyimpan hasil ke `/kaggle/working/cpmk3_final`.

Hipotesis dibuat sebelum pelatihan tambahan. Catatan hipotesis sebelum pelatihan pertama masih belum tersedia. Metadata EXIF, overlay, dan gambar contoh kegagalan bisa dilihat di Output Kaggle.
