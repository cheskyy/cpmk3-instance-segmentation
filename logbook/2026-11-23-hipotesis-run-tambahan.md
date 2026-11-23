# Hipotesis sebelum run tambahan NRP 0

Dicatat 23 November 2026 20:38:48 WIB, sebelum pengiriman run tambahan YOLO11s dan Mask R-CNN ke Kaggle. Rubrik baru diterima setelah pelatihan awal berjalan. Pada saat catatan dibuat, YOLO11n 640 dan YOLO11s 640 sudah menghasilkan validasi awal. Mask R-CNN 640 sedang berlatih. Logbook yang diberikan untuk 17–19 November berisi kegiatan foto, anotasi, pemisahan, dan persiapan kode.

- Aku memperkirakan YOLO11s unggul pada kelas **book** dan **plug** di resolusi 960. Ukuran yang lebih besar mempertahankan detail objek kecil sebelum prediksi dense, dan kapasitas YOLO11s lebih besar daripada YOLO11n.
- Aku memperkirakan Mask R-CNN kompetitif pada kelas **chair** dan **pillow**, khususnya saat objek berdekatan. Proposal region dan mask per ROI dapat memisahkan instance yang berhimpitan. Grid mask 28×28 dapat tetap membatasi detail kaki kursi yang tipis.
- Aku memperkirakan peningkatan resolusi dari 320 lebih membantu objek kecil daripada permukaan besar seperti **wall-other-merged**. Uji dengan AP kelas pada validation, lalu laporkan angka aktual beserta ground truth yang tersedia.

Bandingkan tiga ukuran per model dengan split, seed, dan recipe sama. Sajikan hasil checkpoint terbaik validation dengan anggaran waktu per model, serta hasil pada jumlah epoch yang sama dalam tiap model jika log tersedia. Test HP disimpan untuk evaluasi akhir dan pengukuran domain shift.

Ini merupakan catatan prospektif untuk run tambahan. Bukti yang akan dikumpulkan adalah waktu commit ini dan waktu mulai run tambahan di log Kaggle.
