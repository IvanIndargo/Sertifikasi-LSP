Library Management System
Aplikasi manajemen perpustakaan ini merupakan aplikasi perpustakaan yang dirancang menggunakan program C# WinForms yang terhubung langsung dengan database MySQL. Aplikasi ini menyediakan berbagai fitur untuk manajemen perpustakaan.
Fitur Utama
•	Kelola Buku - Kelola data buku (Kode Buku, Judul Buku, Penulis, Penerbit, Tahun Terbit, Kategori, Stok Buku)
•	Kelola Anggota - Kelola data anggota yang terdaftar di dalam manajemen perpustakaan
•	Peminjaman Buku - Proses peminjaman dengan perhitungan otomatis pengembalian tempo (7 hari)
•	Pengembalian Buku - Proses pengembalian dengan perhitungan denda otomatis
•	Riwayat & Laporan - Lihat riwayat peminjaman lengkap
Konsep yang Diterapkan
Object-Oriented Programming (OOP)
•	Class di setiap form: Book, Member, Borrowing, dll
•	Method: Functions dan Procedures dalam setiap class
Encapsulation
•	Membungkus fungsi dan data ke 1 class (contoh di form book.cs)
•	Akses dilakukan melalui method atau property (get, set)
Abstraction
•	menyembunyikan detail rumit dan hanya menampilkan fungsi penting 
(decimal fine = borrowing.CalculateFine();
Inheritance
•	class mewarisi class lain (public partial class MemberForm : Form) mewarisi class form dari winform.
Polymorphism
Method namanya sama tapi perilakunya bisa berbeda tergantung class atau kondisi saat dipanggil
•	Virtual method: HitungDenda() di class Borrowing
•	Semua tindakan yang 'click' tetapi tindakan yang ditangani itu berbeda tergantung apa tindakan yang akan di lakukan, seperti private void btnAdd_Click(object sender, EventArgs e) private void btnUpdate_Click(object sender, EventArgs e) private void btnDelete_Click(object sender, EventArgs e)
Database Management
•	Database: MySQL
•	Konsep yang digunakan:
•	CRUD Operations (Create, Read, Update, Delete)
•	Transaction handling
•	Indexes untuk meningkatkan performa query
Operasi database dipisahkan ke dalam Repository untuk menjaga arsitektur tetap rapi.
Data Structures
•	Array dan List untuk manajemen buku dan anggota
Prosedur & Function
•	Procedure untuk perhitungan database (INSERT, UPDATE, DELETE)
•	Function untuk perhitungan denda, stok, validasi input
•	Helper methods untuk reusable code
