# CPMK3 Segmentasi Instance Indoor

Eksperimen membandingkan YOLO11n-seg, YOLO11s-seg, dan Mask R-CNN ResNet-50 FPN. Digit NRP 0 menentukan ukuran input 320, 640, dan 960. Data latih dan validasi berasal dari ekspor COCO v2 sesuai pilihan pengguna. Kecocokan jumlah split publik dengan v5 tercatat di notebook. Asal setiap gambar dan label v5 perlu bukti tambahan.

Notebook Kaggle menyimpan dataset privat, hasil pelatihan, dan overlay revisi 40 foto HP. Revisi mask dibantu Codex dan Mask2Former. Pemeriksaan oleh pemilik foto dan screenshot proses anotasi di Roboflow menjadi bukti tersendiri.

Riwayat Git dimulai setelah rubrik tambahan diterima pada 23 November 2026. Notebook yang sudah digunakan disimpan sebagai cuplikan tahap kerja saat itu.

[Notebook hasil dan audit Kaggle](https://www.kaggle.com/code/seaalautt/cpmk3-instance-segmentation)
