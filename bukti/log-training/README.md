# Log pelatihan asli

Setiap subfolder run memuat CSV asli dari output Kaggle. Untuk YOLO, `results.csv` mencatat loss dan metrik per epoch dari Ultralytics. Untuk Mask R-CNN, `maskrcnn_train.csv` mencatat loss dan mask AP50–95 validasi dari COCOeval.

| Sumber | Run | CSV durasi asli |
|---|---|---|
| Pelatihan awal | YOLO11n 320/640/960, YOLO11s 640, Mask R-CNN 640 | [Pelatihan awal](durasi/pelatihan-awal.csv) |
| Mask R-CNN tambahan | Mask R-CNN 320/960 | [Mask R-CNN tambahan](durasi/mask-r-cnn-tambahan.csv) |
| YOLO11s tambahan | YOLO11s 320/960 | [YOLO11s tambahan](durasi/yolo11s-tambahan.csv) |

Kolom `utc` memakai UTC. Catatan `seconds` mengukur waktu berjalan selama pelatihan pada Tesla T4, termasuk validasi dan penyimpanan checkpoint. Durasi kumulatif tercatat sebesar 61,31 menit untuk YOLO11n-seg, 91,27 menit untuk YOLO11s-seg, dan 121,94 menit untuk Mask R-CNN. Alokasi Mask R-CNN adalah 120 menit.

- [Output pelatihan awal di Kaggle](https://www.kaggle.com/code/seaalautt/cpmk3-training-gpu/output)
- [Output Mask R-CNN tambahan di Kaggle](https://www.kaggle.com/code/seaalautt/cpmk3-nrp-mask-r-cnn/output)
- [Output YOLO11s tambahan di Kaggle](https://www.kaggle.com/code/seaalautt/cpmk3-nrp-yolo11s/output)
