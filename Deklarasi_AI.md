# Deklarasi penggunaan AI

Saya menggunakan AI untuk mendapatkan saran dan membantu memperbaiki kode notebook. Saya juga memakai bantuan AI saat mengecek pembagian data, membuat draf anotasi foto uji, dan menjalankan percobaan di Kaggle.

Saat menyunting dokumen yang sudah ada, saya menggunakan AI untuk merapikan kalimat tanpa menambahkan isi baru.

Mask2Former membantu membuat kandidat mask tambahan. Kandidatnya dicek dari bentuk objek dan kecocokan kelas sebelum evaluasi. Draf anotasi masih perlu dicek di Roboflow.

## Cuplikan prompt utama

Saya meminta bantuan menyusun dan mengecek notebook sesuai instruksi PPT.

> Periksa kembali kode sebelum diberikan. Pastikan seluruh cell saling terhubung, pembagian dataset benar, label terbaca, metode sesuai instruksi, dan notebook dapat dijalankan tanpa kesalahan yang seharusnya bisa diantisipasi.

## Contoh perbaikan atas saran AI

Saran awal memakai ukuran 320, 640, dan 960 piksel untuk YOLO11n saja. Rubrik terbaru meminta hasil dari tiga model. Ukuran 320 dan 960 piksel pun ditambahkan untuk YOLO11s dan Mask R-CNN. Semua percobaan dibandingkan pada set validasi yang sama. [Hasil eksperimen NRP 0](hasil/eksperimen_nrp_0.csv)

[Model Mask2Former yang dipakai untuk kandidat mask](https://huggingface.co/facebook/mask2former-swin-tiny-coco-panoptic)
