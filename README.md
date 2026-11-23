# CPMK3 Segmentasi Instance Indoor

Eksperimen membandingkan YOLO11n-seg, YOLO11s-seg, dan Mask R-CNN ResNet-50 FPN. Digit NRP 0 menentukan ukuran input 320, 640, dan 960. Data latih dan validasi berasal dari ekspor COCO v2 sesuai pilihan pengguna. Kecocokan jumlah split publik dengan v5 tercatat di notebook. Asal setiap gambar dan label v5 perlu bukti tambahan.

Notebook Kaggle menyimpan dataset privat, hasil pelatihan, dan overlay revisi 40 foto HP. Revisi mask dibantu Codex dan Mask2Former. Pemeriksaan oleh pemilik foto dan screenshot proses anotasi di Roboflow menjadi bukti tersendiri.

Riwayat Git dimulai setelah rubrik tambahan diterima pada 23 November 2026. Notebook yang sudah digunakan disimpan sebagai cuplikan tahap kerja saat itu.

[Notebook hasil dan audit Kaggle](https://www.kaggle.com/code/seaalautt/cpmk3-instance-segmentation)

## Notebook dan bukti proses

1. Pelatihan awal melatih ketiga model pada 640, serta YOLO11n pada 320 dan 960.
2. Audit revisi memasang draf 352 mask untuk 40 foto HP dan menghasilkan overlay serta riwayat perubahan.
3. Dua notebook NRP tambahan melatih YOLO11s dan Mask R-CNN pada 320 dan 960.
4. Evaluasi memuat sembilan checkpoint, menilai validation per ukuran, dan membandingkan tiga baseline 640 pada kedua test set. Skor sebelum dan setelah revisi HP memakai prediksi yang sama.
5. Demo memuat model terlatih untuk inferensi foto baru. Kontrol ambang dan pilihan kelas dapat digunakan saat tanya jawab.

Hipotesis ada di logbook dengan waktu pencatatan sebelum run tambahan. Rubrik juga meminta entri sebelum training pertama. Sumber yang ditinjau belum memuat entri tersebut. Lampirkan entri asli jika pernah dibuat.

Log training asli, catatan durasi GPU, EXIF, overlay dan tabel hasil ada pada output Kaggle. Pengguna memeriksa dan mengesahkan anotasi di Roboflow serta menunjukkan inferensi foto baru saat sesi demo.

[Logbook mingguan](logbook/2026-11-23.md)  
[Hipotesis run tambahan](logbook/2026-11-23-hipotesis-run-tambahan.md)  
[Deklarasi AI](Deklarasi_AI.md)
