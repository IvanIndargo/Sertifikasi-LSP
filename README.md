# 📚 Library Management System

Aplikasi manajemen perpustakaan ini merupakan aplikasi perpustakaan yang dirancang menggunakan program **C# WinForms** yang terhubung langsung dengan database **MySQL**. Aplikasi ini menyediakan berbagai fitur untuk manajemen perpustakaan.

---

## ✨ Fitur Utama

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

## 🧠 Konsep yang Diterapkan

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

## 🗄️ Database Management

* **Database**: MySQL
* Konsep yang digunakan:

  * CRUD Operations (Create, Read, Update, Delete)
  * Transaction handling
  * Indexes untuk meningkatkan performa query

Operasi database dipisahkan ke dalam **Repository** untuk menjaga arsitektur tetap rapi.

---

## 🧩 Data Structures

* Array dan List untuk manajemen buku dan anggota

---

## ⚙️ Prosedur & Function

* **Procedure**

  * Digunakan untuk operasi database (INSERT, UPDATE, DELETE)

* **Function**

  * Digunakan untuk perhitungan denda
  * Perhitungan stok
  * Validasi input

* **Helper Methods**

  * Digunakan untuk reusable code
 
<img width="1918" height="1056" alt="image" src="https://github.com/user-attachments/assets/e33dcffc-8e32-4039-a7eb-65c20b4fb3bf" />

