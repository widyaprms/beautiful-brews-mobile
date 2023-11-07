# BeautyBrews Co.
```text
Arini Widya Pramesti
2206830271
PBP E
```

## Tugas 7
>1. Apa perbedaan utama antara *stateless* dan *stateful widget* dalam konteks pengembangan aplikasi Flutter?
* **Stateless Widget** : *Stateless Widget* adalah salah satu jenis *widget* pada Flutter yang tidak dapat merespon terhadap interaksi pengguna dan tidak menampilkan perubahan data. *Stateless Widget* hanya bertugas untuk menampilkan sesuatu secara statis. 
Dalam Flutter, *Stateless Widget* tidak memiliki objek *State* terkait yang berisi data yang dapat diubah. Oleh karena itu, ketika state berubah, *Stateless Widget* tidak akan membangun ulang tampilannya dengan menggunakan data yang baru.

* **Stateful Widget** : *Stateful Widget* adalah salah satu jenis *widget* pada Flutter yang memungkinkan perubahan data pada *widget* tersebut. Ketika suatu *widget* dapat merespon terhadap interaksi pengguna dan menampilkan perubahan data, maka *widget* tersebut disebut sebagai *stateful widget*. 
Dalam Flutter, *Stateful Widget* memiliki objek *State* terkait yang berisi data yang dapat diubah. Ketika *state* berubah, *Stateful Widget* akan membangun ulang tampilannya dengan menggunakan data yang baru.



>2. Sebutkan seluruh *widget* yang kamu gunakan untuk menyelesaikan tugas ini dan jelaskan fungsinya masing-masing.

* **MaterialApp**: *Widget* ini adalah titik awal aplikasi Flutter yang menggunakan material design dan digunakan untuk mengatur tema serta navigasi pada aplikasi.

* **Scaffold**: *Widget* yang digunakan untuk memberikan struktur dasar untuk tampilan layar dengan app bar, body, dan floating action button.

* **AppBar**: *Widget* yang digunakan untuk menampilkan app bar pada bagian atas layar yang biasanya berisi judul dan aksi.

* **Text**: *Widget* yang digunakan untuk menampilkan string teks dengan gaya tertentu pada layar.

* **SingleChildScrollView**: *Widget* yang digunakan untuk membungkus seluruh konten halaman sehingga dapat discroll jika konten melebihi ruang layar.

* **Padding**: *Widget* yang digunakan untuk menambahkan jarak di sekeliling widget anaknya.

* **Column**: *Widget* yang digunakan untuk mengatur anak-anaknya dalam kolom vertikal.

* **GridView**: *Widget* yang digunakan untuk mengatur anak-anaknya dalam grid dua dimensi.

* **Icon**: *Widget* yang digunakan untuk menampilkan ikon yang terkait dengan item toko.

* **InkWell**: *Widget* yang digunakan untuk memberikan area responsif terhadap sentuhan sehingga item toko dapat ditekan.

* **Container**: *Widget* yang digunakan untuk mengelompokkan ikon dan teks dalam card.

* **Material**: *Widget* yang digunakan untuk memberikan efek visual pada InkWell.

* **SnackBar**: *Widget* yang muncul di bagian bawah layar untuk memberikan pesan sementara kepada pengguna.

* **ShopItem**: Bukan merupakan *widget*, tetapi sebuah kelas yang memodelkan data yang akan digunakan oleh *widget*.

* **ShopCard**: *Widget* yang dibuat khusus untuk menampilkan informasi dari objek ShopItem.

* *ThemeData*: *Widget* yang digunakan untuk mengonfigurasi tema umum aplikasi termasuk warna, tipe teks, dan elemen desain lainnya.

* ColorScheme: *Widget* yang digunakan untuk menentukan skema warna untuk ThemeData.



>3. Jelaskan bagaimana cara kamu mengimplementasikan *checklist* di atas secara *step-by-step* (bukan hanya sekadar mengikuti tutorial)

- [x] Membuat sebuah program Flutter baru dengan tema *inventory* seperti tugas-tugas sebelumnya.
1. Masuk ke direktori tempat proyek Flutter disimpan, lalu *generate* proyek Flutter baru bernama **beautiful_brews** dengan menjalankan perintah dibawah ini.
```text
flutter create beautiful_brews
cd beautiful_brews
``` 
2. Mengubah sifat *widget* halaman dari *stateful* menjadi *stateless* dengan mengubah kode yang sudah ada menjadi sebagai berikut.
```text
class MyHomePage extends StatelessWidget {
    MyHomePage({Key? key}) : super(key: key);

    @override
    Widget build(BuildContext context) {
        return Scaffold(
            ...
        );
    }
}
```
3. Men-*define* tipe pada class ShhopItem untuk menambahkan teks dan card dengan menambahkan kode sebagai berikut.
```text
class ShopItem {
  final String name;
  final IconData icon;
  final Color color;  // Data field tambahan

  ShopItem(this.name, this.icon, this.color);
}
```

- [x] Membuat tiga tombol sederhana dengan ikon dan teks untuk:
    - Melihat daftar item (`Lihat Item`)
    - Menambah item (`Tambah Item`)
    - Logout (`Logout`)

1. Menambahkan kode berikut dibawah kode `MyHomePage({Key? key}) : super(key: key);` untuk menambahkan barang-barang yang dijual (nama, harga, dan icon barang tersebut).
```text
final List<ShopItem> items = [
    ShopItem("Lihat Produk", Icons.checklist, const Color.fromARGB(255, 226, 101, 143)),
    ShopItem("Tambah Produk", Icons.add_shopping_cart, const Color.fromARGB(255, 191, 62, 214)),
    ShopItem("Logout", Icons.logout, Colors.blue),
];
```

- [x] Memunculkan Snackbar dengan tulisan:
    - "Kamu telah menekan tombol Lihat Item" ketika tombol `Lihat Item` ditekan.
    - "Kamu telah menekan tombol Tambah Item" ketika tombol `Tambah Item` ditekan.
    - "Kamu telah menekan tombol Logout" ketika tombol `Logout` ditekan.
    
1. Menambahkan kode berikut pada `InkWell` di dalam `ShopCard` untuk memberikan interaksi dan menampilkan SnackBar ketika card ditekan.
```text
...
 child: InkWell(
        // Area responsive terhadap sentuhan
        onTap: () {
          // Memunculkan SnackBar ketika diklik
          ScaffoldMessenger.of(context)
            ..hideCurrentSnackBar()
            ..showSnackBar(SnackBar(
                content: Text("Kamu telah menekan tombol ${item.name}!")));
        },
...
 ),
```

