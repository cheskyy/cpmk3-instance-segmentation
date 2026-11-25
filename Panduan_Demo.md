# Panduan demo dan tanya jawab

Pakai notebook demo untuk mencoba foto yang diambil saat sesi. Notebook memuat bobot yang sudah dilatih, lalu menggambar mask pada foto baru. [Buka notebook demo](notebooks/05-demo-foto-baru.ipynb)

## Sebelum sesi

1. Masuk ke Kaggle sebagai `seaalautt` dan impor notebook demo. Pilih GPU kalau tersedia. Aktifkan internet jika sel pertama perlu memasang pustaka.
2. Tambahkan dua sumber di **Input**, masing-masing satu kali. Output pelatihan awal versi 1 berisi tiga bobot pada 640 piksel. Output evaluasi versi 4 berisi tabel AP, termasuk AP per kelas. [Pelatihan awal di Kaggle](https://www.kaggle.com/code/seaalautt/cpmk3-training-gpu) · [Evaluasi di Kaggle](https://www.kaggle.com/code/seaalautt/cpmk3-instance-segmentation)
3. Jalankan sel dari atas sampai kontrol **Pilih foto** dan **Tampilkan AP** muncul. Sel terakhir mencoba gambar sintetis untuk mengecek apakah bobot bisa dibaca. Coba juga satu foto latihan supaya urutan kliknya sudah hafal.
4. Buka tabel hasil di tab lain. Bagian yang paling sering dipakai saat menjawab adalah perbandingan dua set uji dan hasil kasus 3. [Halaman hasil](hasil/README.md) · [Lima kasus](hasil/uji_lima_kasus.csv)

## Alur 10 menit

| Waktu | Yang dilakukan |
|---|---|
| 0–2 menit | Ambil foto ruangan baru dengan HP saat sesi. Pilih sudut yang menampilkan objek seperti kursi, lantai, atau pintu. Unggah JPG atau PNG lewat **Pilih foto**. |
| 2–4 menit | Pilih `YOLO11s`, biarkan **Ambang** di `0.35`, lalu klik **Jalankan inferensi**. Tunjukkan foto asli dan foto dengan mask. Tunjuk satu objek yang tertangkap dan satu kesalahan kalau ada. |
| 4–6 menit | Kalau diminta mengganti threshold, naikkan **Ambang** ke `0.60` pada foto yang sama. Bandingkan jumlah mask di judul gambar sebelum dan sesudahnya. |
| 6–8 menit | Kalau diminta AP satu kelas, pilih `chair` dan **Test asli**, lalu klik **Tampilkan AP**. Dengan `YOLO11s`, hasil evaluasi tersimpannya **19,22% mask AP50–95**. |
| 8–10 menit | Jelaskan satu angka dari tabel hasil. Siapkan juga satu contoh kegagalan agar bisa menunjukkan bedanya skor keyakinan dan bentuk mask. |

Kalau tombol unggah tidak muncul, tambahkan foto sebagai input privat di Kaggle dan salin path JPG atau PNG. Pada sel yang memuat `DEMO_PATH`, isi tiga baris ini lalu jalankan selnya.

```python
DEMO_PATH = "/kaggle/input/nama-dataset/foto-baru.jpg"
DEMO_MODEL = "YOLO11s"
DEMO_THRESHOLD = 0.35
```

Ganti contoh path dengan path foto yang baru diunggah. Kalau diminta mengganti ambang, ubah `DEMO_THRESHOLD` lalu jalankan lagi sel itu. Untuk menampilkan AP lewat sel kode, jalankan `ap_satu_kelas("YOLO11s", "chair", "original")`.

## Pertanyaan yang bisa dilatih

**Kenapa ada tiga model?**

Tugasnya membandingkan tiga model dari minimal dua keluarga arsitektur. YOLO11n dan YOLO11s memprediksi objek dan mask dalam satu tahap. Mask R-CNN menyiapkan calon area objek dulu, lalu memprediksi kelas dan mask untuk area tersebut. Perbandingan pada ukuran 640 piksel memakai dua set uji yang sama untuk ketiganya. [Tabel perbandingan model](hasil/perbandingan_640.csv)

**Apa yang berubah saat ambangnya dinaikkan?**

Baris `kept = [p for p in predictions if p['score']>=threshold]` memilih mask yang ditampilkan. Menggeser ambang dari 0,35 ke 0,60 menyembunyikan mask dengan skor di bawah 0,60. Tombol **Tampilkan AP** membaca tabel dari evaluasi yang sudah selesai.

**Angka 10,50% itu artinya apa?**

Itu mask AP50–95 YOLO11s pada 40 foto uji HP dengan input 640 piksel. AP merangkum precision dan recall dari prediksi yang diurutkan berdasarkan skor. Evaluator mencocokkan kelas dan bentuk mask, lalu merata-ratakan hasil pada ambang IoU 0,50 sampai 0,95 dan kelas yang punya anotasi. Mask yang terlalu lebar, terpotong, atau salah kelas menurunkan skor. Contohnya, AP kelas `chair` pada uji HP hanya 6,35%. Angka itu ikut masuk ke rata-rata bersama kelas lainnya. [Tabel hasil dua set uji](hasil/perbandingan_640.csv)

**Kenapa kasus 3 pada 320 piksel dapat nol kecocokan?**

Setiap prediksi perlu lolos skor 0,50, punya kelas yang sama, dan tumpang tindih dengan mask anotasi minimal 0,50 IoU. Lima prediksi plafon dan satu dinding lolos skor dengan IoU terbaik sekitar 0,38. Mask lantai punya IoU sekitar 0,60 dan skor sekitar 0,40, sehingga tersaring. Di 640 dan 960 piksel, mask lantai lolos dengan foto dan bobot yang sama. Kursi di foto saling menutupi dan cahaya dari belakang cukup terang. Pengaruh masing-masing kondisi foto belum diuji terpisah. [Uji lima kasus](hasil/uji_lima_kasus.csv)

**Apa yang diuji untuk NRP 0 dan bagaimana membandingkan foto HP?**

Untuk NRP 0, tiga model dicoba pada 320, 640, dan 960 piksel. Sembilan hasilnya dibandingkan pada 164 foto validasi. Data uji asli dan 40 foto HP digunakan untuk penilaian akhir. Untuk membahas perbedaan kedua set uji, lihat 35 kelas yang sama. Pada YOLO11s, AP uji HP lebih tinggi sekitar 0,53 poin persentase pada perbandingan itu. Isi ruangan, jumlah objek, dan anotasi juga memengaruhi perbandingan. [Eksperimen ukuran input](hasil/eksperimen_nrp_0.csv) · [Selisih kedua set uji](hasil/domain_shift.csv)

**Apa yang masih perlu dicek dari laporan?**

Pelatihan memakai ekspor COCO v2. Isi gambar dan label v5 masih perlu diverifikasi. Draf anotasi 40 foto HP masih perlu ditinjau di Roboflow. Hipotesis yang tercatat pada 23 November ditulis sebelum run tambahan, saat pelatihan awal sudah berjalan. [Logbook](logbook/2026-11-24.md) · [Catatan hipotesis](logbook/2026-11-23-hipotesis-run-tambahan.md)
