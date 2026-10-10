#Tugas 05 — Advanced CNNs and Transfer Learning

Eksperimen klasifikasi citra menggunakan subset 10 kelas dari dataset Oxford-IIIT Pet. Proyek ini membandingkan training from scratch, feature extraction, fine-tuning, data augmentation, dan arsitektur MobileNetV3-Small.

## Eksperimen

| ID | Model / strategi | Tujuan |
|---|---|---|
| B1 | ResNet-18 from scratch | Baseline tanpa pretrained weights |
| B2 | ResNet-18 feature extraction | Backbone pretrained dibekukan; classifier dilatih |
| B3 | ResNet-18 fine-tuning | Layer4 dan classifier dilatih |
| B4-NoAug | ResNet-18 fine-tuning tanpa augmentation | Pembanding untuk eksperimen augmentation |
| B4-Aug | ResNet-18 fine-tuning dengan augmentation | Mengevaluasi pengaruh augmentation |
| B5 | MobileNetV3-Small pretrained | Membandingkan performa dan efisiensi arsitektur |

## Struktur proyek

```text
Tugas05_VSCode_Notebook/
├── main.ipynb
├── data/
│   └── oxford_pet/             # Dataset yang digunakan notebook
├── checkpoints/                # Checkpoint model hasil training
├── results/                    # CSV/JSON metrik dan visualisasi
├── README.md
└── requirements.txt
```

Struktur folder aktual dapat berbeda sesuai lokasi penyimpanan notebook. Hindari mengunggah dataset besar atau checkpoint ke GitHub jika membuat repositori terlalu besar.

## Persyaratan

- Python yang kompatibel dengan versi PyTorch dan torchvision yang digunakan.
- Jupyter Notebook atau VS Code dengan ekstensi Python dan Jupyter.
- Dependensi Python dalam `requirements.txt`.
- Pada perangkat Apple Silicon, notebook dapat menggunakan backend **MPS** jika didukung instalasi PyTorch.

## Instalasi

1. Clone repositori:

   ```bash
   git clone <URL_REPOSITORI>
   cd <FOLDER_REPOSITORI>
   ```

2. Buat dan aktifkan virtual environment:

   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   ```

   Untuk Windows PowerShell:

   ```powershell
   .venv\Scripts\Activate.ps1
   ```

3. Instal dependensi:

   ```bash
   python -m pip install --upgrade pip
   pip install -r requirements.txt
   ```

4. Buka `main.ipynb` melalui VS Code atau Jupyter, pilih kernel dari virtual environment, lalu jalankan sel notebook sesuai urutan.

## Dataset dan reproduksibilitas

Notebook menggunakan subset 10 kelas Oxford-IIIT Pet dengan pembagian data berikut:

- Training: 1.386 citra
- Validation: 297 citra
- Test: 298 citra
- Random seed pembagian data: `42`

Notebook menyimpan informasi split ke `data/splits_seed42.json` dan hasil eksperimen ke folder `results/` sesuai konfigurasi notebook. Checkpoint model disimpan ke folder `checkpoints/`.

Dataset dapat diunduh oleh notebook jika kode pengunduhan dijalankan dan koneksi internet tersedia. Hasil dan waktu training dapat berbeda bergantung pada perangkat keras, versi library, dan konfigurasi runtime.

## Artefak hasil

Hasil eksperimen dapat mencakup:

- `summary_metrics.csv` dan `summary_metrics.json`
- Riwayat training setiap model
- Confusion matrix dan classification report
- Grafik training loss dan validation loss
- Daftar citra test yang salah diklasifikasikan
- Visualisasi failure analysis B3

Nama dan ketersediaan file mengikuti hasil eksekusi notebook.

## Ringkasan hasil eksperimen

Berdasarkan satu kali run yang dicatat dalam laporan:

| Model | Test accuracy | Macro F1 | Durasi training |
|---|---:|---:|---:|
| B1 — ResNet-18 from scratch | 41,28% | 0,3439 | 273,2 detik |
| B2 — Feature extraction | 95,30% | 0,9527 | 168,2 detik |
| B3 — Fine-tuning | 97,32% | 0,9733 | 156,9 detik |
| B4-NoAug | 97,32% | 0,9732 | 175,3 detik |
| B4-Aug | 96,64% | 0,9666 | 89,2 detik |
| B5 — MobileNetV3-Small | 93,62% | 0,9363 | 52,9 detik |

B3 memperoleh Macro F1 tertinggi pada run tersebut, sedangkan B5 memiliki durasi training paling singkat. Hasil ini berasal dari satu run dan bukan jaminan performa pada dataset atau perangkat lain.

## Catatan

- Jangan memasukkan kredensial, token, atau informasi pribadi ke repositori.
- Pastikan output notebook, tabel, dan visualisasi yang diperlukan untuk penilaian tersimpan sebelum pengumpulan.
- Periksa kompatibilitas versi dependensi dengan lingkungan yang digunakan.
