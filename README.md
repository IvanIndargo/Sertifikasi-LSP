# Library Management System

Aplikasi manajemen perpustakaan ini merupakan aplikasi perpustakaan yang dirancang menggunakan program **C# WinForms** yang terhubung langsung dengan database **MySQL**. Aplikasi ini menyediakan berbagai fitur untuk manajemen perpustakaan.

---

## Fitur Utama

* **Kelola Buku**
  Kelola data buku (Kode Buku, Judul Buku, Penulis, Penerbit, Tahun Terbit, Kategori, Stok Buku)

* **Kelola Anggota**
  Kelola data anggota yang terdaftar di dalam manajemen perpustakaan

* **Peminjaman Buku**
  Proses peminjaman dengan perhitungan otomatis pengembalian tempo (7 hari)

* **Pengembalian Buku**
  Proses pengembalian dengan perhitungan denda otomatis

* **Riwayat & Laporan**
  Lihat riwayat peminjaman lengkap

---

## Konsep yang Diterapkan

### 1️⃣ Object-Oriented Programming (OOP)

* Class di setiap form: `Book`, `Member`, `Borrowing`, dll
* Method: Functions dan Procedures dalam setiap class

---

### 2️⃣ Encapsulation

* Membungkus fungsi dan data ke dalam satu class (contoh di `Book.cs`)
* Akses data dilakukan melalui method atau property (`get`, `set`)

---

### 3️⃣ Abstraction

* Menyembunyikan detail rumit dan hanya menampilkan fungsi penting

Contoh:

```csharp
decimal fine = borrowing.CalculateFine();
```

---

### 4️⃣ Inheritance

* Class mewarisi class lain
* Contoh:

```csharp
public partial class MemberForm : Form
```

* `MemberForm` mewarisi class `Form` dari WinForms

---

### 5️⃣ Polymorphism

Method memiliki nama yang sama tetapi perilakunya dapat berbeda tergantung class atau kondisi saat dipanggil.

* Virtual method: `HitungDenda()` di class `Borrowing`
* Semua tindakan menggunakan event `Click`, tetapi aksi yang dijalankan berbeda tergantung tombol:

  * `btnAdd_Click`
  * `btnUpdate_Click`
  * `btnDelete_Click`

---

### Struktur Proejct

```
LibraryManagementSystemIvan/
│
├── LibraryManagementSystem/
│   ├── Forms/
│   │   ├── MainForm.cs
│   │   ├── BookForm.cs
│   │   ├── MemberForm.cs
│   │   ├── BorrowForm.cs
│   │   ├── ReturnForm.cs
│   │   └── HistoryForm.cs
│   │
│   ├── Models/
│   │   ├── Book.cs
│   │   ├── Member.cs
│   │   └── Borrowing.cs
│   │
│   ├── Data/
│   │   ├── DatabaseConnection.cs
│   │   ├── BookRepository.cs
│   │   ├── MemberRepository.cs
│   │   └── BorrowRepository.cs
│   │
│   ├── Program.cs
│   ├── App.config
│   └── LibraryManagementSystem.csproj
│
└── Database/
    └── LibraryManagementDb.sql
```

## Database Management

* **Database**: MySQL
* Konsep yang digunakan:

  * CRUD Operations (Create, Read, Update, Delete)
  * Transaction handling
  * Indexes untuk meningkatkan performa query

Operasi database dipisahkan ke dalam **Repository** untuk menjaga arsitektur tetap rapi.

---

## Data Structures

* Array dan List untuk manajemen buku dan anggota

---

## Prosedur & Function

* **Procedure**

  * Digunakan untuk operasi database (INSERT, UPDATE, DELETE)

* **Function**

  * Digunakan untuk perhitungan denda
  * Perhitungan stok
  * Validasi input

* **Helper Methods**

  * Digunakan untuk reusable code
    
## Screenshot Fitur

<img width="1918" height="1056" alt="image" src="https://github.com/user-attachments/assets/e33dcffc-8e32-4039-a7eb-65c20b4fb3bf" />

* Dashboard utama untuk menampilkan data total anggota, total buku, total peminjaman, dll

<img width="1919" height="1059" alt="image" src="https://github.com/user-attachments/assets/415ce142-dcaa-4764-8e1a-754083d41802" />

* Form tempat manajemen buku dimana terdapat fitur menambah buku dan penampilan data buku yang ada

<img width="1919" height="1061" alt="image" src="https://github.com/user-attachments/assets/d8144a92-7a8e-4ec0-bb4e-134be178a445" />

* Form tempat manajemen anggota dimana terdapat fitur menambah anggota dan penampilan anggota yang terdaftar

<img width="1917" height="1057" alt="image" src="https://github.com/user-attachments/assets/99c4248f-e41a-4329-8832-53f718f1a618" />

* Form tempat peminjaman buku

<img width="1919" height="1066" alt="image" src="https://github.com/user-attachments/assets/35e10cdb-2b4a-495c-8f68-4085d24c4866" />

* Form pengembalian buku

<img width="1919" height="1058" alt="image" src="https://github.com/user-attachments/assets/a54a8dfc-38c7-4628-ab63-6bb6d2a457aa" />

* Form tempat menampilkan riwayat laporan peminjaman dan pengembalian

## ER_Diagram
<img width="1859" height="479" alt="image" src="https://github.com/user-attachments/assets/cecc2fa9-97c6-42ff-9cb1-8410cb21aff7" />

## SQL Query
```Text
CREATE DATABASE IF NOT EXISTS `LSP` CHARACTER SET = utf8mb4 COLLATE = utf8mb4_unicode_ci;
USE `LSP`;

-- Drop tabel jika tabel telah digunakan
DROP TABLE IF EXISTS `Borrowings`;
DROP TABLE IF EXISTS `Books`;
DROP TABLE IF EXISTS `Members`;

-- Membuat tabel buku
CREATE TABLE `Books` (
  `BookId` INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
  `BookCode` VARCHAR(50) NOT NULL UNIQUE,
  `Title` VARCHAR(200) NOT NULL,
  `Author` VARCHAR(100) NOT NULL,
  `Publisher` VARCHAR(100) NOT NULL,
  `PublishYear` INT NOT NULL,
  `Category` VARCHAR(50) NOT NULL,
  `Stock` INT NOT NULL DEFAULT 0,
  `AvailableStock` INT NOT NULL DEFAULT 0,
  `CreatedDate` DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

-- Membuat tabel member
CREATE TABLE `Members` (
  `MemberId` INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
  `MemberCode` VARCHAR(50) NOT NULL UNIQUE,
  `FullName` VARCHAR(100) NOT NULL,
  `Address` VARCHAR(255) NOT NULL,
  `PhoneNumber` VARCHAR(20) NOT NULL,
  `Email` VARCHAR(100),
  `JoinDate` DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  `IsActive` TINYINT(1) NOT NULL DEFAULT 1
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

-- Membuat tabel peminjaman
CREATE TABLE `Borrowings` (
  `BorrowingId` INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
  `BorrowingCode` VARCHAR(50) NOT NULL UNIQUE,
  `MemberId` INT NOT NULL,
  `BookId` INT NOT NULL,
  `BorrowDate` DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  `DueDate` DATETIME NOT NULL,
  `ReturnDate` DATETIME NULL,
  `Fine` DECIMAL(18,2) NOT NULL DEFAULT 0,
  `Status` VARCHAR(20) NOT NULL DEFAULT 'Dipinjam',
  CONSTRAINT `fk_borrowings_members` FOREIGN KEY (`MemberId`) REFERENCES `Members`(`MemberId`) ON UPDATE CASCADE ON DELETE RESTRICT,
  CONSTRAINT `fk_borrowings_books` FOREIGN KEY (`BookId`) REFERENCES `Books`(`BookId`) ON UPDATE CASCADE ON DELETE RESTRICT
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

-- Inputan data untuk tabel buku
INSERT INTO `Books` (`BookCode`, `Title`, `Author`, `Publisher`, `PublishYear`, `Category`, `Stock`, `AvailableStock`) VALUES
('BK001', 'Jaringan Komputer Dasar', 'Andrew Tanenbaum', 'Network Press', 2022, 'Teknologi', 5, 5),
('BK002', 'Keamanan Sistem Informasi', 'William Stallings', 'Security Media', 2023, 'Teknologi', 4, 4),
('BK003', 'Pemrograman Web dengan PHP', 'Rasmus Lerdorf', 'Web Publisher', 2022, 'Teknologi', 6, 6),
('BK004', 'Pemrograman Java Lanjutan', 'James Gosling', 'Java Press', 2023, 'Teknologi', 3, 3),
('BK005', 'Rekayasa Perangkat Lunak', 'Ian Sommerville', 'SE Books', 2024, 'Teknologi', 5, 5),
('BK006', 'Kecerdasan Buatan', 'Stuart Russell', 'AI Publisher', 2024, 'Teknologi', 4, 4),
('BK007', 'Data Mining dan Big Data', 'Jiawei Han', 'Data Science Press', 2023, 'Teknologi', 3, 3),
('BK008', 'Statistika untuk Penelitian', 'Sudjana', 'Statistik Media', 2022, 'Pendidikan', 6, 6),
('BK009', 'Metodologi Penelitian', 'Sugiyono', 'Research Press', 2023, 'Pendidikan', 8, 8),
('BK010', 'Pengantar Ekonomi Mikro', 'N. Gregory Mankiw', 'Economy Press', 2022, 'Ekonomi', 5, 5),
('BK011', 'Akuntansi Dasar', 'Donald Kieso', 'Accounting Publisher', 2023, 'Ekonomi', 4, 4),
('BK012', 'Manajemen Sumber Daya Manusia', 'Gary Dessler', 'Management Press', 2024, 'Manajemen', 6, 6);

-- Inputan data untuk tabel member
INSERT INTO `Members` (`MemberCode`, `FullName`, `Address`, `PhoneNumber`, `Email`, `IsActive`) VALUES
('MBR001', 'Ivan Indargo', 'Jl. Merdeka No. 123, Malang', '0887368262837', 'Iindargo@email.com', 1);

SET @BorrowDate = DATE_SUB(NOW(), INTERVAL 5 DAY);
SET @DueDate = DATE_ADD(NOW(), INTERVAL 2 DAY);

-- Inputan data untuk peminjaman
INSERT INTO `Borrowings` (`BorrowingCode`, `MemberId`, `BookId`, `BorrowDate`, `DueDate`, `Status`) VALUES
(CONCAT('BRW', DATE_FORMAT(NOW(), '%Y%m%d'), '0001'), 1, 1, @BorrowDate, @DueDate, 'Dipinjam'),
(CONCAT('BRW', DATE_FORMAT(NOW(), '%Y%m%d'), '0002'), 2, 3, @BorrowDate, @DueDate, 'Dipinjam');

-- Update stock untuk buku yang dipinjam
UPDATE `Books` SET `AvailableStock` = `AvailableStock` - 1 WHERE `BookId` IN (1, 3);

-- Pembuatan index untuk performa query lebih bagus
CREATE INDEX `IX_Books_BookCode` ON `Books`(`BookCode`);
CREATE INDEX `IX_Books_Title` ON `Books`(`Title`(100));
CREATE INDEX `IX_Members_MemberCode` ON `Members`(`MemberCode`);
CREATE INDEX `IX_Members_FullName` ON `Members`(`FullName`(100));
CREATE INDEX `IX_Borrowings_Status` ON `Borrowings`(`Status`);
CREATE INDEX `IX_Borrowings_BorrowDate` ON `Borrowings`(`BorrowDate`);

-- Procedure untuk update status peminjaman
Drop procedure if exists UpdateLateStatus;
DELIMITER $$
CREATE PROCEDURE `UpdateLateStatus`()
BEGIN
  UPDATE `Borrowings`
  SET `Status` = 'Terlambat'
  WHERE `ReturnDate` IS NULL
    AND `DueDate` < NOW()
    AND `Status` != 'Terlambat';
END$$
DELIMITER ;

SELECT 'Database LSP berhasil dibuat dan diinisialisasi!' AS Info;
SELECT 'Total Books: ' AS Label, COUNT(*) AS TotalBooks FROM `Books`;
SELECT 'Total Members: ' AS Label, COUNT(*) AS TotalMembers FROM `Members`;
SELECT 'Total Borrowings: ' AS Label, COUNT(*) AS TotalBorrowings FROM `Borrowings`;
```
## Struktur Tabel
📘 Tabel Books

Menyimpan data buku yang tersedia di perpustakaan.

Kolom utama:

BookId → Primary Key

BookCode → Kode unik buku

Title, Author, Publisher

PublishYear, Category

Stock → Total stok buku

AvailableStock → Stok tersedia

CreatedDate → Tanggal input data

👤 Tabel Members

Menyimpan data anggota perpustakaan.

Kolom utama:

MemberId → Primary Key

MemberCode → Kode unik anggota

FullName, Address, PhoneNumber, Email

JoinDate → Tanggal bergabung

IsActive → Status keaktifan anggota

🔄 Tabel Borrowings

Menyimpan data transaksi peminjaman buku.

Kolom utama:

BorrowingId → Primary Key

BorrowingCode → Kode transaksi

MemberId → Relasi ke tabel Members

BookId → Relasi ke tabel Books

BorrowDate, DueDate, ReturnDate

Fine → Denda keterlambatan

Status → Status peminjaman (Dipinjam / Terlambat / Dikembalikan)

Relasi (Foreign Key):

MemberId → Members(MemberId)

BookId → Books(BookId)

---

# TEST CASE

## Library Management System Ivan
---

## Pengujian Kelola Buku

**Test Case ID** : TC-01
**Nama Fitur** : Kelola Buku

| Komponen              | Deskripsi                                      |
| --------------------- | ---------------------------------------------- |
| Langkah Pengujian     | Admin membuka menu **Buku**                    |
| Data Input            | Data buku                                      |
| Hasil yang Diharapkan | Data buku dapat dikelola (tambah, ubah, hapus) |
| Hasil Aktual          | Sesuai                                         |
| Status                | **Lulus**                                      |

---

## Pengujian Kelola Anggota

**Test Case ID** : TC-02
**Nama Fitur** : Kelola Anggota

| Komponen              | Deskripsi                           |
| --------------------- | ----------------------------------- |
| Langkah Pengujian     | Admin membuka menu **Anggota**      |
| Data Input            | Data anggota                        |
| Hasil yang Diharapkan | Data anggota tampil di DataGridView |
| Hasil Aktual          | Sesuai                              |
| Status                | **Lulus**                           |

---

## Pengujian Peminjaman Buku

**Test Case ID** : TC-03
**Nama Fitur** : Peminjaman Buku

| Komponen              | Deskripsi                              |
| --------------------- | -------------------------------------- |
| Langkah Pengujian     | Pilih anggota dan buku, lalu simpan    |
| Data Input            | Anggota aktif dan buku tersedia        |
| Hasil yang Diharapkan | Transaksi peminjaman berhasil disimpan |
| Hasil Aktual          | Sesuai                                 |
| Status                | **Lulus**                              |

---

## Pengujian Pengembalian Buku

**Test Case ID** : TC-04
**Nama Fitur** : Pengembalian Buku

| Komponen              | Deskripsi                                          |
| --------------------- | -------------------------------------------------- |
| Langkah Pengujian     | Klik tombol **Kembalikan** pada data peminjaman    |
| Data Input            | Data peminjaman aktif                              |
| Hasil yang Diharapkan | Status peminjaman berubah menjadi **Dikembalikan** |
| Hasil Aktual          | Sesuai                                             |
| Status                | **Lulus**                                          |

---

## Pengujian Riwayat Peminjaman

**Test Case ID** : TC-05
**Nama Fitur** : Riwayat Peminjaman

| Komponen              | Deskripsi                                       |
| --------------------- | ----------------------------------------------- |
| Langkah Pengujian     | Admin membuka menu **Riwayat**                  |
| Data Input            | Data dari tabel `t_Peminjaman`                  |
| Hasil yang Diharapkan | Data riwayat peminjaman dan pengembalian tampil |
| Hasil Aktual          | Sesuai                                          |
| Status                | **Lulus**                                       |

---

