# Deklarasi penggunaan AI

Codex membantu mengaudit split data, memperbaiki notebook, memeriksa kandidat mask, membuat poligon pada objek yang terlihat, dan menjalankan eksperimen di Kaggle. Mask2Former COCO Panoptic menghasilkan kandidat mask tambahan. Pemilihan kandidat dilakukan berdasarkan inspeksi foto dan kelas acuan sebelum membuka hasil prediksi model tugas pada foto HP. Draf mask perlu diperiksa oleh pemilik foto di Roboflow sebelum digunakan sebagai bukti anotasi sendiri.

## Prompt utama yang digunakan

> Aku ingin kamu membantu mengerjakan tugas machine learning/deep learning ini secara menyeluruh berdasarkan file yang akan aku berikan, dengan mengacu pada instruksi PPT sebagai pedoman utama.

> kenapa hasilnya gada ya, aku mau hasilnya ada, tapi aku rasa akurasinya jeelek karna anotasi ku salah mungkin, tolong benerin

> ini ada update an,  update lakukan dengan benar

## Contoh perbaikan atas saran AI

Rancangan awal memvariasikan 320, 640, dan 960 pada YOLO11n saja. Rubrik yang diterima saat pelatihan sudah berlangsung meminta tabel dan grafik untuk ketiga model. Empat run baru disiapkan untuk YOLO11s dan Mask R-CNN pada 320 dan 960 dengan split, recipe model, dan seed yang sama. Tabel utama memuat hasil checkpoint pilihan validation, durasi, dan jumlah epoch. Tabel pendamping membaca AP yang tercatat pada epoch yang sama dalam setiap model.

Notebook versi pertama hanya menjalankan audit CPU. Itu menjelaskan mengapa pengguna belum melihat metrik model. Pelatihan GPU kemudian dijalankan dan hasilnya dicatat dari log pelatihan dan evaluator COCO.

[Model Mask2Former yang dipakai untuk kandidat mask](https://huggingface.co/facebook/mask2former-swin-tiny-coco-panoptic)
