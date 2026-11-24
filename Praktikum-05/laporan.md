# Laporan Praktikum Pertemuan 5 Pemrograman Web 1

**Nama:** [Muhammad Nor Azkia Rabbani]  
**NIM:** [2510010182]  
**Kelas:** [3B Reguler banjarbaru pagi]  

---

## 1. Percobaan 1: Box Model

### Tabel Pengamatan
| No | Kondisi | Lebar Kotak A (px) | Lebar Kotak B (px) |
|---|---|---|---|
| 1 | padding 20px | 350 | 300 |
| 2 | padding 40px | 390 | 300 |

| No | Kondisi | Jarak judul-paragraf (px) |
|---|---|---|
| 3 | Block biasa | 30 |
| 4 | Di dalam flex column | 50 |

| No | Kondisi .menu a | Latar menimpa teks lain? (ya/tidak) |
|---|---|---|
| 5 | inline (bawaan) | ya |
| 6 | inline-block | tidak |

---

## 2. Percobaan 2: Flexbox Lab

### Tabel Pengamatan
| No | Properti dan Nilai | Pengamatan |
|---|---|---|
| 1 | `display: flex` | Item A, B, C berjejer secara horizontal ke samping dan tingginya memenuhi container (240px). |
| 2 | `justify-content: space-between` | Item A berada di ujung kiri, Item C di ujung kanan, dan Item B di tengah ruang sisa. |
| 3 | `justify-content: space-evenly` | Seluruh jarak antar item dan jarak ke tepi container berukuran sama rata. |
| 4 | `align-items: stretch` vs `center` | `stretch` membuat item memenuhi tinggi container (240px), sedangkan `center` membuat item setinggi kontennya dan berada di tengah vertikal. |
| 5 | `flex-direction: column` + `justify-content: center` | Main axis berubah menjadi vertikal sehingga item tersusun ke bawah dan terkumpul di tengah secara vertikal. |
| 6 | 8 item x 200px, `nowrap` vs `wrap` | Pada `nowrap` item dipaksa menyusut dalam 1 baris. Pada `wrap` item tetap 200px dan turun membuat baris baru. |
| 7 | `.b { flex-grow: 1 }` | Item B menyerap seluruh sisa ruang kosong container, sedangkan A dan C tetap selebar kontennya. |
| 8 | Lebar A/B/C (`flex: 0 0 200px`, `1`, `2`) | Lebar item terbagi proporsional sesuai rasio basis dan flex-grow yang diberikan di panel Computed. |
| 9 | `.c { order: -1 }` | Item C berpindah posisi tampil menjadi yang paling awal/kiri tanpa mengubah urutan di struktur HTML. |
| 10 | `.c { margin-left: auto }` | Item C terdorong ke ujung paling kanan karena margin otomatis menyerap sisa ruang di sebelah kirinya. |
| 11 | `gap: 24px` | Muncul jarak sebesar 24px tepat di antara item tanpa memberikan jarak pada tepi container. |

---

## 3. Percobaan 3: Positioning

### Tabel Pengamatan
| No | Eksperimen | Pengamatan |
|---|---|---|
| 1 | Header `sticky` saat digulir | Header tetap mengalir normal lalu menempel di bagian paling atas viewport saat layar digulir. |
| 2a | Header `fixed` tanpa `padding-top` body | Header keluar dari aliran dokumen sehingga konten paragraf pertama tertutup oleh header. |
| 2b | Header `fixed` dengan `padding-top: 64px` | Konten terdorong ke bawah sebesar 64px sehingga paragraf pertama tidak lagi tertutup header. |
| 3 | `.notif` tanpa `position: relative` | Badge merah melompat menempel di pojok kanan atas header karena mencari acuan induk non-static terdekat. |
| 4 | `.lapis-1` z-index 3, lalu `lapis-2` z-index 5 | Element dengan nilai `z-index` lebih tinggi akan menumpuk di lapisan paling depan. |
| 5 | Header `z-index: 1` | Header tertutup oleh kotak lapis yang memiliki `z-index` lebih besar (3 dan 5) saat digulir melewati header. |
| 6 | Tombol Bantuan di layar 375px | Tombol Bantuan tetap konsisten melayang menempel di pojok kanan bawah layar ponsel. |

---

## 4. Percobaan 4: Dashboard SIAKAD Mini

### Jawaban Pertanyaan Analisis

1. **Mengapa `box-sizing: border-box` ditulis di awal stylesheet?**  
   Aturan `border-box` memastikan bahwa ukuran total suatu elemen mencakup `content`, `padding`, dan `border`. Hal ini mencegah ukuran elemen membengkak saat diberi padding/border sehingga mempermudah perhitungan layout dan mencegah tata letak web rusak/pecah.

2. **Mengapa pada P2 eksperimen 4 item terkumpul di tengah secara vertikal?**  
   Saat `flex-direction: column` diaktifkan, *main axis* berpindah dari arah horizontal (kiri-kanan) menjadi vertikal (atas-bawah). Oleh karena itu, properti `justify-content: center` yang bertugas mengatur posisi di *main axis* akan memusatkan elemen secara vertikal di tengah container.

3. **Perhitungan lebar B dan C pada eksperimen 7 & perubahan `flex: 1 1 auto`:**  
   Pada basis 0px dengan sisa ruang 800px, rasio `1:2` membuat $B \approx 266.7\text{px}$ dan $C \approx 533.3\text{px}$. Jika `.b` diubah menjadi `flex: 1 1 auto`, item B akan memperhitungkan lebar konten aslinya terlebih dahulu sebelum membagi sisa ruang kosong.

4. **Mengapa pada P3 eksperimen 3 badge menempel ke header?**  
   Elemen dengan `position: absolute` akan mencari leluhur (*ancestor*) terdekat yang memiliki posisi non-static (`relative`, `absolute`, `fixed`, atau `sticky`). Ketika `position: relative` pada `.notif` dihapus, badge mencari acuan terdekat di atasnya yaitu `.header` yang memiliki `position: sticky`.

5. **Perbandingan `sticky` vs `fixed` untuk navbar dashboard:**  
   Saya memilih `position: sticky` untuk navbar dashboard. Alasan utamanya adalah elemen `sticky` tetap mempertahankan ruang fisiknya dalam aliran dokumen (*normal flow*) sehingga tidak menutupi konten di bawahnya saat pertama kali dimuat tanpa perlu menambahkan margin/padding manual pada body.

6. **Fungsi `flex: 1` pada `.wrapper`:**  
   Properti `flex: 1` pada `.wrapper` berfungsi untuk meregangkan kontainer utama agar menyerap seluruh sisa ruang vertikal di dalam body. Jika baris ini dihapus, `.wrapper` hanya setinggi isinya dan footer akan naik ke tengah layar jika konten sedang sedikit.

---

## 5. Kesimpulan

Dalam praktikum ini, saya telah mempelajari penggunaan CSS Box Model, Flexbox, dan Positioning untuk membangun tata letak web yang rapi dan responsif. Penggunaan `border-box` sangat membantu konsistensi ukuran elemen, sementara Flexbox memudahkan penyusunan layout seperti navbar, sidebar, dan kartu statistik. Teknik positioning (`sticky` dan `absolute`) juga berhasil diterapkan dengan baik pada komponen header dan badge notifikasi.