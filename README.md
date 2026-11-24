# CPMK3 Segmentasi Instance Indoor

Eksperimen membandingkan YOLO11n-seg, YOLO11s-seg, dan Mask R-CNN ResNet-50 FPN. Digit NRP 0 menentukan ukuran input 320, 640, dan 960. Data latih dan validasi berasal dari ekspor COCO v2 sesuai pilihan pengguna. Kecocokan jumlah split publik dengan v5 tercatat di notebook. Asal setiap gambar dan label v5 perlu bukti tambahan.

Notebook Kaggle menyimpan dataset privat, hasil pelatihan, dan overlay revisi 40 foto HP. Revisi mask dibantu Codex dan Mask2Former. Draf 352 mask masih menunggu pemeriksaan manual di Roboflow. Tangkapan layar satu pengeditan polygon yang cocok dengan set uji tercantum di halaman 2 laporan.

Riwayat Git dimulai setelah rubrik tambahan diterima pada 23 November 2026. Notebook yang sudah digunakan disimpan sebagai cuplikan tahap kerja saat itu.

Evaluasi versi 4 selesai pada 24 November 2026. Output memuat sembilan hasil validasi, perbandingan tiga model pada kedua set uji, grafik, lima studi kasus, dan sel demo. [Output Kaggle](https://www.kaggle.com/code/seaalautt/cpmk3-instance-segmentation/output)

## Hasil dan bukti proses

- [Tabel hasil evaluasi](hasil/)
- [CSV pelatihan asli dan waktu GPU](bukti/log-training/)
- [Logbook 23 November](logbook/2026-11-23.md) dan [pembaruan 24 November](logbook/2026-11-24.md)
- [Hipotesis run tambahan](logbook/2026-11-23-hipotesis-run-tambahan.md)
- [Deklarasi AI](Deklarasi_AI.md)

## Notebook

1. Pelatihan awal melatih ketiga model pada 640, serta YOLO11n pada 320 dan 960. [Notebook pelatihan awal](notebooks/01-pelatihan-awal.ipynb)
2. Audit revisi memasang draf 352 mask untuk 40 foto HP dan menghasilkan overlay serta riwayat perubahan. [Notebook audit revisi](notebooks/02-audit-revisi-mask-hp.ipynb)
3. Dua notebook NRP tambahan melatih YOLO11s dan Mask R-CNN pada 320 dan 960. [Notebook YOLO11s](notebooks/03-nrp-yolo11s-tambahan.ipynb) dan [notebook Mask R-CNN](notebooks/03-nrp-mask-r-cnn-tambahan.ipynb)
4. Evaluasi memuat sembilan checkpoint, menilai validasi per ukuran, dan membandingkan tiga baseline 640 pada kedua set uji. Skor sebelum dan setelah revisi HP memakai prediksi yang sama. [Notebook evaluasi](notebooks/04-perbandingan-sembilan-run.ipynb)
5. Demo memuat model terlatih untuk inferensi foto baru. Kontrol ambang dan pilihan kelas dapat digunakan saat tanya jawab. [Notebook demo](notebooks/05-demo-foto-baru.ipynb)

## Menjalankan ulang evaluasi di Kaggle

1. Impor notebook evaluasi dan pilih GPU. Aktifkan internet untuk pemasangan dependensi pada sel pertama.
2. Lampirkan kedua dataset privat sebagai Kaggle Input. [Ekspor indoor dan foto uji](https://www.kaggle.com/datasets/seaalautt/cpmk3-indoor-test40) dan [patch anotasi HP](https://www.kaggle.com/datasets/seaalautt/cpmk3-review-mask-hp)
3. Lampirkan output versi 1 dari masing-masing notebook pelatihan. [Pelatihan awal](https://www.kaggle.com/code/seaalautt/cpmk3-training-gpu/output), [Mask R-CNN tambahan](https://www.kaggle.com/code/seaalautt/cpmk3-nrp-mask-r-cnn/output), dan [YOLO11s tambahan](https://www.kaggle.com/code/seaalautt/cpmk3-nrp-yolo11s/output)
4. Gunakan `RUN_TRAINING = False` untuk evaluasi checkpoint yang tersedia. Notebook mencari input di `/kaggle/input` dan menulis hasil ke `/kaggle/working/cpmk3_final`.

Hipotesis bertanggal dicatat sebelum run tambahan. Catatan sebelum training pertama belum tersedia. Metadata EXIF, overlay, dan contoh kegagalan bergambar tersedia di Output Kaggle.
