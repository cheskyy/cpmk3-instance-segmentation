# Hipotesis sebelum run tambahan NRP 0

Catatan awal dibuat pada 23 November 2026 pukul 20:38:48 WIB, sebelum percobaan tambahan YOLO11s dan Mask R-CNN dikirim ke Kaggle. Rubrik baru diterima saat pelatihan awal sudah berjalan. Waktu itu, YOLO11n dan YOLO11s pada 640 piksel sudah punya hasil validasi awal. Mask R-CNN 640 masih dilatih. Catatan 17–19 November mencakup pengambilan foto, anotasi, pembagian data, dan persiapan kode.

- Pada 960 piksel, dugaan saya YOLO11s akan unggul pada kelas **book** dan **plug**. Input yang lebih besar membantu menjaga detail benda kecil, dan YOLO11s punya kapasitas model lebih besar dibanding YOLO11n.
- Saya menduga Mask R-CNN cukup bagus untuk kelas **chair** dan **pillow**, terutama kalau objeknya berdekatan. Model ini membuat mask per area objek, sehingga bisa membantu membedakan tiap objek yang berhimpitan. Grid mask 28×28 masih bisa kehilangan bagian tipis seperti kaki kursi.
- Dari ukuran awal 320 piksel, saya menduga kenaikan resolusi paling terasa pada objek kecil. Permukaan besar seperti **wall-other-merged** dipakai sebagai pembanding. Dugaan ini dicek lewat AP tiap kelas di set validasi dan jumlah anotasi yang tersedia.

Tiga ukuran pada tiap model memakai pembagian data, seed, dan pengaturan pelatihan yang sama. Tabel utama memakai checkpoint terbaik di validasi dengan anggaran waktu tiap model. Log yang tersedia juga dipakai untuk melihat skor pada jumlah epoch yang sama. Foto HP dipakai untuk uji akhir dan melihat selisih skor saat model bertemu foto ruangan lain.

Urutan pengerjaan bisa dicek dari waktu commit awal catatan ini dan waktu mulai pelatihan tambahan di log Kaggle.
