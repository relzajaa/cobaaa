<div align="center">

# 🔬 Sistem Peminjaman Peralatan Laboratorium

**Aplikasi terminal berbasis Python OOP untuk mencatat peminjaman alat laboratorium oleh mahasiswa.**

![Python](https://img.shields.io/badge/Python-3.8%2B-3776AB?logo=python&logoColor=white)
![OOP](https://img.shields.io/badge/Paradigma-OOP-green)
![Penyimpanan](https://img.shields.io/badge/Penyimpanan-CSV-informational)
![Kelompok](https://img.shields.io/badge/Kelompok-3-orange)

</div>

## 📑 Daftar Isi

1. [Nama Aplikasi](#-nama-aplikasi)
2. [Anggota Kelompok](#-anggota-kelompok)
3. [Deskripsi Sistem](#-deskripsi-sistem)
4. [Struktur Program](#-struktur-program)
5. [Cara Menjalankan](#-cara-menjalankan)
6. [Pembagian Kontribusi](#-pembagian-kontribusi)


## 📌 Nama Aplikasi

**Sistem Peminjaman Peralatan Laboratorium**

Aplikasi ini dibuat dengan Python dan dijalankan lewat terminal. Data disimpan di file **CSV** (folder `Data_Sistem/`) dan **tersimpan otomatis** setiap selesai satu aksi, tanpa database.


## 👥 Anggota Kelompok

**Kelompok 3**

| No | Nama | NIM | Akun GitHub |
|:--:|------|-----|-------------|
| 1 | Farrel Muflif Muzzaki | K3525024 | [@relzajaa](https://github.com/relzajaa) |
| 2 | Gisma Dian Utami | K3525026 | [@gismadian](https://github.com/gismadian) |
| 3 | Nourin Akbar Pratama | K3525067 | [@Akbarr-11](https://github.com/Akbarr-11) |
| 4 | Azzahra Hendar Asafira | K3525081 | [@azzahrahendar](https://github.com/azzahrahendar) |


## 📝 Deskripsi Sistem

Sistem ini membantu petugas lab mencatat **siapa** meminjam **alat apa**, **kapan** harus kembali, dan **bagaimana kondisi** alat saat dikembalikan.

### ✨ Fitur

| Menu | Fitur | Keterangan |
|:--:|-------|------------|
| 1 | Kelola Data Mahasiswa | Tambah, edit, hapus, cari, dan lihat daftar mahasiswa |
| 2 | Kelola Data Alat | Tambah (bisa banyak unit sekaligus), edit, hapus, cari, lihat daftar, dan tambah kategori |
| 3 | Buat Transaksi Peminjaman | Satu transaksi boleh berisi beberapa alat, lama pinjam 1–7 hari |
| 4 | Tampilkan Transaksi | Semua transaksi beserta detailnya, ada tanda **TERLAMBAT** |
| 5 | Proses Pengembalian Alat | Alat dikembalikan satu per satu, lengkap dengan kondisi dan tanggal |
| 6 | Cari Transaksi Berdasarkan Mahasiswa | Cari memakai NIM |
| 7 | Tampilkan Alat yang Tersedia | Daftar alat dan jumlah stok |
| 8 | Tampilkan Alat yang Sedang Dipinjam | Alat yang belum kembali |
| 9 | Tampilkan Alat yang Rusak | Alat berkondisi rusak ringan atau rusak berat |
| 10 | Tampilkan Riwayat Peminjaman Mahasiswa | Transaksi yang sudah selesai, terbaru di atas |
| 11 | Keluar dari Program | Menutup aplikasi |
| 12 | Pencarian Alat | Cari berdasarkan kode, nama, atau kategori |
| 13 | Statistik Peminjaman | Alat terpopuler, mahasiswa teraktif, jumlah transaksi aktif dan selesai |
| 14 | Lihat Alat dalam Pemeliharaan | Alat rusak yang sedang menunggu perbaikan |
| 15 | Selesaikan Pemeliharaan Alat | Alat diperbaiki lalu kembali tersedia dalam kondisi baik |

### 📋 Aturan Peminjaman

1. Satu mahasiswa maksimal punya **2 transaksi aktif**.
2. Alat hanya bisa dipinjam jika statusnya **Tersedia**.
3. Satu transaksi bisa berisi **banyak alat**. Kode alat yang diketik dua kali dihitung sekali.
4. Pengembalian dicatat **per alat** (tanggal, kondisi, dan hari terlambat). Status transaksi berubah otomatis: *Dipinjam → Sebagian dikembalikan → Selesai*.
5. Alat yang kembali **Baik** langsung tersedia. Alat **rusak** masuk *Pemeliharaan* sampai diselesaikan lewat menu 15.
6. Mahasiswa atau alat yang **sudah punya riwayat transaksi tidak bisa dihapus**, supaya riwayat tetap utuh.

Siklus status sebuah alat:

```mermaid
stateDiagram-v2
    direction LR
    [*] --> Tersedia
    Tersedia --> Dipinjam : dipinjam
    Dipinjam --> Tersedia : kembali, kondisi Baik
    Dipinjam --> Pemeliharaan : kembali, kondisi Rusak
    Pemeliharaan --> Tersedia : pemeliharaan selesai
```

### ✅ Pemeriksaan Input

- NIM dan kode alat tidak boleh sama dengan yang sudah ada.
- No. HP hanya angka, panjang 10–13 digit.
- Tanggal kembali berformat `DD-MM-YYYY` dan tidak boleh sebelum tanggal pinjam.
- Jika ada kesalahan, muncul pesan `[!]` berwarna merah dan program tidak berhenti.
- Jika file CSV tidak bisa dibaca, program berhenti dengan pesan error agar data yang ada tidak tertimpa data kosong.

### 🖥️ Tampilan Program

Ini tampilan menu utama saat program dijalankan (garis dan kotak berwarna kuning, tulisan berwarna putih):

<pre style="background:#0c0c0c; color:#ffffff; padding:12px; overflow-x:auto; line-height:1.3">
      <span style="color:#F5F543">╔══════════════════════════════════════════════════════════════════╗</span>
      <span style="color:#F5F543">║</span>          <span style="color:#F5F543"><b>♦</b></span>  <b>SISTEM PEMINJAMAN PERALATAN LABORATORIUM</b>  <span style="color:#F5F543"><b>♦</b></span>          <span style="color:#F5F543">║</span>
      <span style="color:#F5F543">╚══════════════════════════════════════════════════════════════════╝</span>

                 Hari ini: 08-11-2026   |   Transaksi aktif: 0

      <span style="color:#F5F543">┌──────────────────────────────────────────────────────────────────┐</span>
      <span style="color:#F5F543">│</span>                            <b>MENU UTAMA</b>                            <span style="color:#F5F543">│</span>
      <span style="color:#F5F543">╞══════════════════════════════════════════════════════════════════╡</span>
      <span style="color:#F5F543">│</span>  1. Kelola Data Mahasiswa                                        <span style="color:#F5F543">│</span>
      <span style="color:#F5F543">│</span>  2. Kelola Data Alat                                             <span style="color:#F5F543">│</span>
      <span style="color:#F5F543">│</span>  3. Buat Transaksi Peminjaman                                    <span style="color:#F5F543">│</span>
      <span style="color:#F5F543">│</span>  4. Tampilkan Transaksi                                          <span style="color:#F5F543">│</span>
      <span style="color:#F5F543">│</span>  5. Proses Pengembalian Alat                                     <span style="color:#F5F543">│</span>
      <span style="color:#F5F543">│</span>  6. Cari Transaksi Berdasarkan Mahasiswa                         <span style="color:#F5F543">│</span>
      <span style="color:#F5F543">│</span>  7. Tampilkan Alat yang Tersedia                                 <span style="color:#F5F543">│</span>
      <span style="color:#F5F543">│</span>  8. Tampilkan Alat yang Sedang Dipinjam                          <span style="color:#F5F543">│</span>
      <span style="color:#F5F543">│</span>  9. Tampilkan Alat yang Rusak                                    <span style="color:#F5F543">│</span>
      <span style="color:#F5F543">│</span> 10. Tampilkan Riwayat Peminjaman Mahasiswa                       <span style="color:#F5F543">│</span>
      <span style="color:#F5F543">│</span> 11. Keluar dari Program                                          <span style="color:#F5F543">│</span>
      <span style="color:#F5F543">└──────────────────────────────────────────────────────────────────┘</span>

      <span style="color:#F5F543">┌──────────────────────────────────────────────────────────────────┐</span>
      <span style="color:#F5F543">│</span>                          <b>MENU TANTANGAN</b>                          <span style="color:#F5F543">│</span>
      <span style="color:#F5F543">╞══════════════════════════════════════════════════════════════════╡</span>
      <span style="color:#F5F543">│</span> 12. Pencarian Alat                                               <span style="color:#F5F543">│</span>
      <span style="color:#F5F543">│</span> 13. Statistik Peminjaman                                         <span style="color:#F5F543">│</span>
      <span style="color:#F5F543">│</span> 14. Lihat Alat dalam Pemeliharaan                                <span style="color:#F5F543">│</span>
      <span style="color:#F5F543">│</span> 15. Selesaikan Pemeliharaan Alat                                 <span style="color:#F5F543">│</span>
      <span style="color:#F5F543">└──────────────────────────────────────────────────────────────────┘</span>
      Pilih menu (1-15): 
</pre>


## 🗂️ Struktur Program

### 📁 Susunan Folder

```text
Project2_FIX/
├── main.py                    # pintu masuk program
├── README.md
├── Data_Sistem/               # penyimpanan data (file CSV)
│   ├── mahasiswa.csv
│   ├── alat.csv
│   ├── kategori.csv
│   ├── transaksi.csv
│   └── detail.csv
└── Sistem_Peminjaman_Lab/
    ├── __init__.py
    ├── mahasiswa.py           # Mahasiswa, penyimpanan CSV, MahasiswaManager
    ├── alat.py                # Enum, Alat, penyimpanan CSV, AlatManager
    ├── transaksi.py           # Enum, Transaksi, penyimpanan CSV, TransaksiManager
    ├── menu_app.py            # menu dan alur input (UI)
    └── tampilan.py            # fungsi bantu cetak di terminal
```

### 🧱 Empat Lapisan Program

```mermaid
flowchart TD
    A["main.py"] --> B["MenuApp (menu_app.py)"]
    B -. memakai .-> T["tampilan.py"]
    B --> M1["MahasiswaManager"]
    B --> M2["AlatManager"]
    B --> M3["TransaksiManager"]
    M3 -. memakai .-> M1
    M3 -. memakai .-> M2
    M1 --> D1["Mahasiswa"]
    M2 --> D2["Alat"]
    M3 --> D3["Transaksi"]
    D3 --> D4["DetailPeminjaman"]
    D4 --> D2
    M1 -.-> CSV[("File CSV")]
    M2 -.-> CSV
    M3 -.-> CSV
```

| Lapisan | Class / File | Tugas |
|---------|--------------|-------|
| **UI** | `MenuApp`, `tampilan.py` | Menampilkan menu dan tabel, membaca input, menangkap pesan error |
| **Manager** | `MahasiswaManager`, `AlatManager`, `TransaksiManager` | Menyimpan data di `dict` dan memeriksa aturan |
| **Penyimpanan** | `PenyimpananMahasiswa`, `PenyimpananAlat`, `PenyimpananTransaksi` | Membaca dan menulis file CSV |
| **Domain** | `Mahasiswa`, `Alat`, `Transaksi`, `DetailPeminjaman`, Enum | Objek data dan pilihan tetap |

### 🧩 Class dan Enum (11 class + 3 enum)

| Jenis | Nama | File | Tugas |
|-------|------|------|-------|
| Class | `MenuApp` | `menu_app.py` | Menjalankan menu 1–15 dan submenunya |
| Class | `MahasiswaManager` | `mahasiswa.py` | Mengelola data mahasiswa (kunci = NIM) |
| Class | `AlatManager` | `alat.py` | Mengelola data alat, kategori, dan pemeliharaan (kunci = kode alat) |
| Class | `TransaksiManager` | `transaksi.py` | Membuat transaksi, memproses pengembalian, riwayat, dan statistik (kunci = ID seperti `TRX001`) |
| Class | `Mahasiswa` | `mahasiswa.py` | Data mahasiswa dan daftar transaksi aktifnya |
| Class | `Alat` | `alat.py` | Data alat beserta kondisi dan statusnya |
| Class | `Transaksi` | `transaksi.py` | Satu peminjaman: tanggal, batas kembali, status, dan daftar alat |
| Class | `DetailPeminjaman` | `transaksi.py` | Catatan satu alat di dalam transaksi |
| Class | `PenyimpananMahasiswa` | `mahasiswa.py` | Baca dan tulis `mahasiswa.csv` |
| Class | `PenyimpananAlat` | `alat.py` | Baca dan tulis `alat.csv` dan `kategori.csv` |
| Class | `PenyimpananTransaksi` | `transaksi.py` | Baca dan tulis `transaksi.csv` dan `detail.csv` |
| Enum | `StatusTransaksi` | `transaksi.py` | `DIPINJAM`, `SEBAGIAN_DIKEMBALIKAN`, `SELESAI` |
| Enum | `KondisiAlat` | `alat.py` | `BAIK`, `RUSAK_RINGAN`, `RUSAK_BERAT` |
| Enum | `StatusAlat` | `alat.py` | `TERSEDIA`, `DIPINJAM`, `PEMELIHARAAN` |

### 🗃️ Struktur Data yang Dipakai

| Struktur | Dipakai untuk |
|----------|---------------|
| `dict` | Tempat menyimpan data tiap manager dan daftar menu |
| `list` | Daftar alat dalam transaksi dan hasil pencarian |
| `set` | Kategori alat dan ID transaksi aktif mahasiswa (tidak boleh ganda) |
| `tuple` | Pasangan `(nama, jumlah)` pada statistik |
| File `csv` | Penyimpanan data supaya tidak hilang saat program ditutup |


## 🚀 Cara Menjalankan

### 🔧 Yang Dibutuhkan

- **Python 3.8 atau lebih baru** (sudah dicoba di Python 3.13)
- Terminal yang bisa menampilkan warna dan karakter Unicode (Windows Terminal, PowerShell, macOS Terminal, atau terminal Linux)
- Tidak perlu `pip install` apa pun
- Atau buka `main.py` di editor (misalnya VS Code), lalu klik tombol play di pojok kanan atas untuk Run

### ▶️ Langkah-langkah

```bash
# 1. Masuk ke folder proyek
cd Project2_FIX

# 2. Jalankan program
python main.py          # Windows
python3 main.py         # macOS / Linux
```

### 💡 Contoh Alur Pemakaian

File CSV awal hanya berisi judul kolom, jadi **isi data dulu**:

1. **Menu 1** → tambah mahasiswa (NIM, nama, No. HP).
2. **Menu 2** → tambah alat. Contoh: kode `MKS`, jumlah `3` → otomatis jadi `MKS-01`, `MKS-02`, `MKS-03`.
3. **Menu 3** → buat peminjaman (NIM, kode alat dipisah koma, lama pinjam).
4. **Menu 5** → kembalikan alat (pilih transaksi, kode alat, kondisi, tanggal).
5. **Menu 14 dan 15** → lihat dan selesaikan pemeliharaan jika ada alat yang dikembalikan dalam keadaan rusak.
6. **Menu 4, 10, 13** → lihat transaksi, riwayat, dan statistik.

> 💾 Data tersimpan otomatis ke folder `Data_Sistem/`, jadi tetap ada saat program dibuka lagi.
>
> ⚠️ Jangan membuka file CSV di Excel saat program berjalan, karena penyimpanan bisa gagal.


## 🤝 Pembagian Kontribusi

| Anggota | File yang Dikerjakan | Isi Tugas |
|---------|----------------------|-----------|
| **Farrel Muflif Muzzaki** | `menu_app.py`, `main.py` | Menu utama dan submenu, alur input pengguna, menu tantangan, serta pintu masuk program |
| **Gisma Dian Utami** | `mahasiswa.py`, `alat.py`, `transaksi.py` | Enum dan class data: `Mahasiswa`, `Alat`, `DetailPeminjaman`, `Transaksi` |
| **Nourin Akbar Pratama** | `tampilan.py`, `README.md` | Tampilan terminal, penjelasan repository |
| **Azzahra Hendar Asafira** | `mahasiswa.py`, `alat.py`, `transaksi.py` | `MahasiswaManager`, `AlatManager`, `TransaksiManager`, penyimpanan CSV, serta pemeriksaan aturan |

<div align="center">

**Created by Kelompok 3**

</div>