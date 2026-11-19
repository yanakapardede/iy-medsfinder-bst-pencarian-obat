# PROYEK STRUKTUR DATA DAN ALGORITMA

# IY MEDSFINDER: Pencarian Data Pemesan Obat Apotek Berbasis Binary Search Tree

## Anggota Kelompok

| No. | Nama | NIM |
|:---:|---|---|
| 1 | Yanaka Sofia Pardede | 24031554065 | 
| 2 | Annisa Ramadhani | 24031554206 |

**Program Studi:** S1 Sains Data, Fakultas Matematika dan Ilmu Pengetahuan Alam

## Deskripsi Proyek

Proyek ini merupakan proyek mata kuliah **Struktur Data dan Algoritma** yang bertujuan untuk menerapkan **Binary Search Tree (BST)** pada kasus nyata, yaitu pencarian data pemesan obat di apotek.

Data pemesanan obat disusun ke dalam BST dengan **nama obat sebagai kunci (key)**. Setiap node merepresentasikan satu jenis obat dan menyimpan seluruh data pemesanan untuk obat tersebut. Pengguna dapat mencari obat melalui antarmuka web interaktif (Gradio), dan struktur pohon dapat divisualisasikan dalam bentuk teks di terminal, gambar Matplotlib, maupun file Graphviz (`.dot`).

## Tujuan

1. Mengimplementasikan operasi `insert` dan `search` pada Binary Search Tree.
2. Mengorganisasi data pemesanan obat berdasarkan urutan alfabet nama obat.
3. Menyediakan aplikasi pencarian data pemesan obat yang mudah digunakan.
4. Memvisualisasikan struktur BST agar proses penyusunan data lebih mudah dipahami.

## Sumber Data

| Berkas | Isi | Format |
|---|---|---|
| `Data SDA.csv` | Data pemesanan obat apotek | CSV |

Kolom pada dataset:

| Kolom | Deskripsi |
|---|---|
| `Nama Obat` | Nama obat yang dipesan (digunakan sebagai kunci BST) |
| `Nama Pemesan` | Nama pelanggan yang memesan |
| `Kategori Penyakit` | Kategori penyakit terkait pesanan |
| `Tanggal Pesan` | Tanggal pemesanan |

## Cakupan Data

- **Jumlah data pemesanan:** 200 baris.
- **Jumlah obat unik (node BST):** 28 obat.
- **Obat dengan data terbanyak:** Paracetamol (16 data), diikuti Sumatriptan (13 data).
- **Obat dengan data tersedikit:** Atorvastatin (2 data).

## Struktur Data yang Digunakan

Struktur utama adalah **Binary Search Tree**. Setiap node menyimpan:

| Atribut | Keterangan |
|---|---|
| `nama_obat` | Kunci node (huruf kecil, tanpa spasi berlebih) |
| `data` | List berisi seluruh data pemesanan untuk obat tersebut |
| `left` | Anak kiri (nama obat yang secara alfabet lebih kecil) |
| `right` | Anak kanan (nama obat yang secara alfabet lebih besar) |

Aturan penyusunan:

- Nama obat dinormalisasi dengan `strip().lower()` sebelum dibandingkan, sehingga pencarian **tidak membedakan huruf besar/kecil**.
- Jika nama obat lebih kecil dari node saat ini, data masuk ke subpohon kiri. Jika lebih besar, masuk ke subpohon kanan.
- Jika nama obat **sudah ada**, data tidak membuat node baru, tetapi ditambahkan ke list `data` pada node yang sama.

## Cara Kerja Program

1. Membaca `Data SDA.csv` menggunakan Pandas.
2. Membuat BST kosong, lalu memasukkan setiap baris data dengan fungsi `insert` (rekursif).
3. Menyusun daftar nama obat unik (terurut alfabet) untuk pilihan dropdown.
4. Pengguna mengetik atau memilih nama obat pada antarmuka Gradio.
5. Fungsi `search` menelusuri BST secara iteratif dari root hingga node ditemukan atau mencapai `None`.
6. Jika ditemukan, ditampilkan tabel berisi `Nama Pemesan`, `Kategori Penyakit`, dan `Tanggal Pesan`. Jika tidak, ditampilkan pesan bahwa obat tidak ditemukan.

## Fitur

### 1. Pencarian Obat
Pengguna dapat mengetik nama obat pada kotak teks atau memilihnya dari dropdown (pilihan dropdown otomatis mengisi kotak teks), lalu menekan tombol **Cari Data**.

### 2. Visualisasi BST di Terminal
Fungsi `print_tree_terminal` mencetak pohon dengan traversal *Right-Node-Left*, sehingga nama obat tampil **terurut menurun** dari atas ke bawah. Setiap node menampilkan nama obat dan jumlah datanya.

### 3. Visualisasi BST dengan Matplotlib
Fungsi `visualize_bst_matplotlib` menyimpan gambar pohon (seluruh pohon maupun subpohon dari obat yang dicari) ke file `.png`. Posisi sumbu x ditentukan secara *in-order*, sedangkan sumbu y berdasarkan kedalaman node.

### 4. Representasi Graphviz
File `bst_obat.dot` berisi struktur BST dalam format Graphviz DOT (label node berupa nama obat dan jumlah data). File ini dapat di-render menjadi gambar:

```bash
dot -Tpng bst_obat.dot -o bst_obat.png
```

## Hasil: Struktur BST

Berdasarkan `bst_obat.dot`:

| Aspek | Hasil |
|---|---|
| Root | Mebendazole |
| Jumlah node | 28 |
| Kedalaman maksimum | 7 (8 level) |
| Anak kiri root | Flixotide |
| Anak kanan root | Sumatriptan |

Cabang kiri terdalam: Mebendazole → Flixotide → Captopril → Actifed → Amlodipine → Antasida → Bodrex Flu → Atorvastatin.

Bentuk pohon bergantung pada **urutan data masuk**, karena root adalah obat pada baris pertama dataset dan tidak ada proses penyeimbangan.

## Kompleksitas

| Operasi | Rata-rata | Terburuk |
|---|:---:|:---:|
| `insert` | O(log n) | O(n) |
| `search` | O(log n) | O(n) |

Kasus terburuk terjadi bila data masuk dalam urutan alfabet sehingga pohon berbentuk seperti linked list. Pada data ini, pohon cukup bercabang dengan kedalaman 7 untuk 28 node.

## Cara Menjalankan Proyek

### 1. Clone Repository

```bash
git clone https://github.com/yanakapardede/iy-medsfinder-bst-pencarian-obat.git
cd iy-medsfinder-bst-pencarian-obat
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

atau

```bash
pip install pandas numpy matplotlib gradio
```

(Opsional) Instal [Graphviz](https://graphviz.org/download/) untuk me-render `bst_obat.dot`.

### 3. Jalankan Aplikasi

```bash
python main.py
```

Saat dijalankan, program akan:
1. Mencetak struktur BST di terminal (terurut menurun).
2. Menyimpan gambar `bst_keseluruhan_matplotlib.png`.
3. Mencari obat contoh (`Paracetamol`), mencetak subpohonnya, dan menyimpan `subtree_paracetamol_matplotlib.png`.
4. Menjalankan antarmuka web Gradio (buka alamat lokal yang tampil di terminal, umumnya `http://127.0.0.1:7860`).

## Rencana Pengembangan
- Menambahkan fitur tambah, ubah, dan hapus data pemesanan.
- Menambahkan pencarian sebagian (prefix) dan pencarian berdasarkan nama pemesan atau kategori penyakit.
- Menggunakan pohon seimbang (AVL) untuk menjamin kinerja O(log n).
- Menampilkan visualisasi pohon langsung pada antarmuka Gradio.
