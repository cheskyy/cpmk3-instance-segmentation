# Deklarasi penggunaan AI

Saya menggunakan AI untuk mendapatkan saran dan membantu memperbaiki kode notebook. AI juga membantu mengecek pembagian data, menyiapkan draf anotasi foto uji, dan menjalankan eksperimen di Kaggle.

Mask2Former digunakan untuk menghasilkan kandidat mask tambahan. Kandidat ditinjau berdasarkan bentuk objek dan kelas acuan sebelum evaluasi. Draf anotasi masih perlu diperiksa di Roboflow.

## Cuplikan prompt utama

Permintaan awal mencakup penyusunan dan pengecekan notebook sesuai instruksi PPT.

> Periksa kembali kode sebelum diberikan. Pastikan seluruh cell saling terhubung, pembagian dataset benar, label terbaca, metode sesuai instruksi, dan notebook dapat dijalankan tanpa kesalahan yang seharusnya bisa diantisipasi.

## Contoh perbaikan atas saran AI

Saran awal menguji ukuran 320, 640, dan 960 piksel pada YOLO11n saja. Rubrik terbaru meminta perbandingan ketiga model, sehingga percobaan 320 dan 960 piksel ditambahkan untuk YOLO11s dan Mask R-CNN. Kesembilan konfigurasi dibandingkan pada set validasi yang sama. [Hasil eksperimen NRP 0](hasil/eksperimen_nrp_0.csv)

[Model Mask2Former yang dipakai untuk kandidat mask](https://huggingface.co/facebook/mask2former-swin-tiny-coco-panoptic)
