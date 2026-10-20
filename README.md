# Sundanese Corpus

Korpus adalah kumpulan data bahasa yang dikumpulkan dan ditata secara sistematis agar dapat dipelajari dan digunakan kembali. Dalam korpus ujaran, rekaman suara dilengkapi dengan transkripsi dan informasi pendukung yang membantu pembaca memahami tuturan serta konteksnya.

**Sundanese Corpus** menghimpun tuturan bahasa Sunda dalam sebuah repositori data publik. Di dalamnya tersedia potongan audio WAV, transkripsi, anotasi, dan metadata yang saling terhubung. Repositori ini ditujukan bagi siapa pun yang ingin mempelajari tuturan bahasa Sunda, melakukan analisis bahasa, atau mengembangkan teknologi pengolahan suara.

## Struktur folder

```text
Sundanese-Corpus/
├── README.md
├── audio/
│   └── <kelompok>/
│       └── *.WAV
├── annotation/
│   └── annotation_<kelompok>.csv
├── metadata/
│   └── metadata_<kelompok>.csv
├── consent/
│   └── consent_form/
└── documentation/
```

Bagian `<kelompok>` menunjukkan penutur atau kelompok rekaman. Satu kelompok dapat berisi tuturan dari satu penutur maupun percakapan beberapa penutur.

| Folder | Isi |
| --- | --- |
| `audio/` | Potongan audio WAV, disusun berdasarkan penutur atau kelompok rekaman. |
| `annotation/` | Transkripsi dan label yang menjelaskan isi setiap potongan audio. |
| `metadata/` | Informasi tentang penutur, topik, durasi, lingkungan, dan kualitas rekaman. |
| `consent/` | Dokumentasi persetujuan penutur. |
| `documentation/` | Dokumentasi pendukung pengumpulan dan pengolahan korpus. |

## Penamaan dan hubungan antarberkas

Nama berkas membantu mengenali penutur, topik, dan urutan potongan tanpa harus membuka audionya. Pola yang digunakan adalah `SXX_TXX_NNN.WAV`:

| Bagian | Penjelasan |
| --- | --- |
| `SXX` | Kode unik penutur dalam korpus. |
| `TXX` | Kode topik pembicaraan, dengan pemetaan yang sama untuk seluruh penutur. |
| `NNN` | Nomor urut potongan dalam kelompok rekaman. |

### Kode topik

| Kode | Topik |
| --- | --- |
| `T01` | Perkenalan |
| `T02` | Aktivitas Sehari-hari |
| `T03` | Keluarga |
| `T04` | Makanan |
| `T05` | Pendidikan |
| `T06` | Pekerjaan |
| `T07` | Perjalanan |

Kode topik berlaku sama untuk semua penutur dan kelompok rekaman. Ketika pembicaraan beralih ke topik lain, bagian `TXX` pada nama WAV mengikuti topik tersebut. Nama yang sama juga dicatat pada kolom `File` di kedua CSV.

Nomor `NNN` tetap mengikuti urutan potongan dalam rekaman meskipun topiknya berganti. Untuk topik baru, gunakan kode berikutnya dan pertahankan kode yang sudah ada. Nama topik pada kolom `Topic` dan `Label Topik` mengacu pada tabel di atas.

### Menghubungkan audio dan CSV

Gunakan kolom `File` untuk mencocokkan audio dengan anotasi dan metadatanya. Kolom ini hanya memuat nama WAV, tanpa awalan folder. Berkas audionya dapat ditemukan melalui pola `audio/<kelompok>/<File>`.

Setiap potongan audio memiliki satu baris anotasi dan satu baris metadata dalam kelompok yang sama. Baris CSV mengikuti nomor urut potongan, sehingga kode penutur dapat muncul bergantian dalam sebuah percakapan. Beberapa nomor mungkin dilewati; daftar pada kolom `File` menunjukkan berkas yang tersedia.

## Kolom anotasi

Anotasi menjelaskan apa yang diucapkan, siapa yang berbicara, serta konteks pembicaraannya.

| Kolom | Penjelasan | Contoh nilai |
| --- | --- | --- |
| `File` | Nama berkas audio yang dirujuk oleh anotasi. | `SXX_TXX_NNN.WAV` |
| `Transkripsi` | Teks tuturan pada potongan audio. | `Kumaha damang?` |
| `Label Speaker` | Kode penutur utama pada potongan. | `SXX` |
| `Label Bahasa` | Bahasa atau dialek utama tuturan. | `Sunda` |
| `Label Topik` | Topik pembicaraan dalam bahasa Indonesia, ditentukan dari konteks tuturan. | `Perkenalan`, `Pendidikan` |
| `Label Kejadian Khusus` | Kejadian yang ditandai pada audio. `none` berarti tidak ada kejadian khusus yang dicatat; `overlap` menunjukkan penutur berbicara secara bersamaan. | `none`, `overlap` |

## Kolom metadata

Metadata memberikan informasi pendukung tentang penutur dan kondisi rekaman. Informasi ini dapat digunakan untuk memilih data yang sesuai dengan kebutuhan analisis.

| Kolom | Penjelasan | Contoh nilai |
| --- | --- | --- |
| `File` | Nama berkas audio yang dijelaskan oleh baris metadata. | `SXX_TXX_NNN.WAV` |
| `Speaker` | Kode penutur, sesuai `Label Speaker` dan awalan nama WAV. | `SXX` |
| `Gender` | Label gender penutur: `M` untuk laki-laki dan `F` untuk perempuan. | `M`, `F` |
| `Language/Dialect` | Bahasa atau dialek utama rekaman. | `Sunda` |
| `Topic` | Kategori pembicaraan, sesuai `Label Topik` pada anotasi. | `Keluarga`, `Makanan` |
| `Duration` | Durasi audio dalam **detik**, dengan titik sebagai pemisah desimal. | `4.25` |
| `Environment` | Lingkungan tempat rekaman dibuat. Nilai `Indoor` dan `indoor` sama-sama berarti di dalam ruangan. | `Indoor`, `Outdoor` |
| `Quality` | Penilaian kualitas audio saat peninjauan data. | `Good`, `Acceptable` |


## Konvensi data

- **Transkripsi:** mengikuti pendekatan verbatim. Improvisasi, pengulangan, kata pengisi, dan campuran bahasa dipertahankan agar cara penutur berbicara tetap tercermin dalam teks. Ejaan mengikuti konvensi korpus tanpa mengubah susunan tuturan.
- **Pemotongan:** batas audio mempertimbangkan jeda dan keutuhan kata. Durasi setiap potongan tersedia pada kolom `Duration`.
- **Konsistensi:** nama berkas, kode penutur, bahasa, dan topik saling sesuai antara audio, anotasi, dan metadata.
