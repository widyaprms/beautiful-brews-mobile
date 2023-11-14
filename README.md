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

* **ThemeData**: *Widget* yang digunakan untuk mengonfigurasi tema umum aplikasi termasuk warna, tipe teks, dan elemen desain lainnya.

* **ColorScheme**: *Widget* yang digunakan untuk menentukan skema warna untuk ThemeData.



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
3. Men-*define* tipe pada class `ShopItem` untuk menambahkan teks dan card dengan menambahkan kode sebagai berikut.
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
    ShopItem("Lihat Item", Icons.checklist, const Color.fromARGB(255, 226, 101, 143)),
    ShopItem("Tambah Item", Icons.add_shopping_cart, const Color.fromARGB(255, 191, 62, 214)),
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


---
## Tugas 8
>1.  Jelaskan perbedaan antara `Navigator.push()` dan `Navigator.pushReplacement()`, disertai dengan contoh mengenai penggunaan kedua metode tersebut yang tepat!

* `Navigator.push()`: Method `push()` menambahkan suatu *route* ke dalam *stack route* yang dikelola oleh `Navigator`. Method ini menyebabkan *route* yang ditambahkan berada pada paling atas *stack*, sehingga *route* yang baru saja ditambahkan tersebut akan muncul dan ditampilkan kepada pengguna.
Contoh penggunaan method `push()`:
```text
...
    if (item.name == "Tambah Produk") {
        Navigator.push(context,
            MaterialPageRoute(builder: (context) => const ShopFormPage()));
    }
...
```

* `Navigator.pushReplacement()`: Method `pushReplacement()` menghapus *route* yang sedang ditampilkan kepada pengguna dan menggantinya dengan suatu *route*. Method ini menyebabkan aplikasi untuk berpindah dari *route* yang sedang ditampilkan kepada pengguna ke suatu *route* yang diberikan. Pada *stack route* yang dikelola `Navigator`, *route* lama pada atas *stack* akan digantikan secara langsung oleh *route* baru yang diberikan tanpa mengubah kondisi elemen *stack* yang berada di bawahnya.
Contoh penggunaan method `pushReplacement()`:
```text
...
    onTap: () {
        Navigator.pushReplacement(
        context,
        MaterialPageRoute(
            builder: (context) => MyHomePage(),
        ));
    },
...
```

Walaupun `push()` dan `pushReplacement()` sekilas terlihat mirip, namun perbedaan kedua method tersebut terletak pada apa yang dilakukan kepada *route* yang berada pada atas *stack*. `push()` akan menambahkan *route* baru diatas *route* yang sudah ada pada atas *stack*, sedangkan `pushReplacement()` menggantikan *route* yang sudah ada pada atas *stack* dengan *route* baru tersebut. 


>2. Jelaskan masing-masing *layout* widget pada Flutter dan konteks penggunaannya masing-masing!
* **Container**: *Widget* ini digunakan untuk membuat kotak yang dapat menampung *widget* lainnya. Container dapat diatur ukurannya, warnanya, dan margin-nya. Container juga dapat digunakan untuk mengatur tata letak *widget* lainnya.

* **Row dan Column**: *Widget* ini digunakan untuk menempatkan *widget* secara horizontal (Row) atau vertikal (Column). Row dan Column dapat digunakan untuk mengatur tata letak *widget* lainnya.

* **Padding**: *Widget* ini digunakan untuk menambahkan ruang kosong di sekitar *widget* lainnya. Padding dapat digunakan untuk mengatur jarak antara *widget* lainnya.

* **Align**: *Widget* ini digunakan untuk mengatur posisi *widget* dalam kotak induknya. Align dapat digunakan untuk mengatur posisi *widget* secara horizontal dan vertikal.

* **ListView**: *Widget* ini digunakan untuk membuat daftar item yang dapat di-scroll. ListView dapat digunakan untuk menampilkan daftar item yang panjang.

* **GridView**: *Widget* ini digunakan untuk membuat tampilan grid. GridView dapat digunakan untuk menampilkan daftar item dalam bentuk grid.

* **Wrap**: *Widget* ini digunakan untuk menempatkan*widget* dalam baris-baris yang dapat di-wrap. Wrap dapat digunakan untuk mengatur tata letak *widget* yang fleksibel.


>3. Sebutkan apa saja elemen input pada form yang kamu pakai pada tugas kali ini dan jelaskan mengapa kamu menggunakan elemen input tersebut!
* `TextFormField` untuk Nama Item
```text
TextFormField(
  decoration: InputDecoration(
    hintText: "Nama Item",
    labelText: "Nama Item",
    border: OutlineInputBorder(
      borderRadius: BorderRadius.circular(5.0),
    ),
  ),
  onChanged: (String? value) {
    setState(() {
      _name = value!;
    });
  },
  validator: (String? value) {
    if (value == null || value.isEmpty) {
      return "Nama tidak boleh kosong!";
    }
    return null;
  },
)
```
Elemen input ini digunakan untuk mengumpulkan nama item. `onChanged` digunakan untuk menyimpan nilai yang diinput ke dalam variabel `_name` dan akan dijalankan setiap ada perubahan isi `TextFormField`. Sedangkan, `validator` akan melakukan validasi isi `TextFormField` untuk memastikan bahwa input tidak kosong.

* `TextFormField` untuk Jumlah
```text
TextFormField(
  decoration: InputDecoration(
    hintText: "Jumlah",
    labelText: "Jumlah",
    border: OutlineInputBorder(
      borderRadius: BorderRadius.circular(5.0),
    ),
  ),
  onChanged: (String? value) {
    setState(() {
      _amount = int.parse(value!);
    });
  },
  validator: (String? value) {
    if (value == null || value.isEmpty) {
      return "Jumlah tidak boleh kosong!";
    }
    if (int.tryParse(value) == null) {
      return "Jumlah harus berupa angka!";
    }
    return null;
  },
)
```
Elemen input ini digunakan untuk mengumpulkan jumlah item. `onChanged` digunakan untuk menyimpan nilai yang diinput ke dalam variabel `_amount` dan akan dijalankan setiap ada perubahan isi `TextFormField`. Sedangkan, `validator` akan melakukan validasi isi `TextFormField` untuk memastikan bahwa input tidak kosong dan harus berupa angka.

* `TextFormField` untuk Deskripsi
```text
TextFormField(
  decoration: InputDecoration(
    hintText: "Deskripsi",
    labelText: "Deskripsi",
    border: OutlineInputBorder(
      borderRadius: BorderRadius.circular(5.0),
    ),
  ),
  onChanged: (String? value) {
    setState(() {
      _description = value!;
    });
  },
  validator: (String? value) {
    if (value == null || value.isEmpty) {
      return "Deskripsi tidak boleh kosong!";
    }
    return null;
  },
)
```
Elemen input ini digunakan untuk mengumpulkan deskripsi item. `onChanged` digunakan untuk menyimpan nilai yang diinput ke dalam variabel `_description` dan akan dijalankan setiap ada perubahan isi `TextFormField`. Sedangkan, `validator` akan melakukan validasi isi `TextFormField` untuk memastikan bahwa input tidak kosong.


>4. Bagaimana penerapan *clean architecture* pada aplikasi Flutter?

Clean Architecture pada aplikasi Flutter adalah suatu pola arsitektur yang digunakan untuk membangun aplikasi dengan memisahkan kode menjadi beberapa lapisan. Lapisan tersebut antara lain: *Domain Layer*, *Application Layer*, *Infrastructure Layer*, dan *Presentation Layer*.

Lapisan-lapisan tersebut memiliki fungsi masing-masing, yaitu:
* **Domain Layer**: Lapisan ini berisi definisi dari bisnis logic aplikasi. Lapisan ini tidak bergantung pada lapisan lainnya dan dapat digunakan kembali pada aplikasi lainnya.
* **Application Layer**: Lapisan ini berisi implementasi dari use case aplikasi. Lapisan ini bergantung pada lapisan *Domain Layer*.
* **Infrastructure Layer**: Lapisan ini berisi implementasi dari teknologi yang digunakan pada aplikasi seperti database, jaringan, dan lain-lain. Lapisan ini bergantung pada lapisan *Domain Layer* dan *Application Layer*.
* **Presentation Layer**: Lapisan ini berisi implementasi dari tampilan aplikasi. Lapisan ini bergantung pada lapisan *Domain Layer*, *Application Layer*, dan *Infrastructure Layer*.


>5. Jelaskan bagaimana cara kamu mengimplementasikan *checklist* di atas secara *step-by-step*! (bukan hanya sekadar mengikuti tutorial)
- [x] Memakai minimal tiga elemen input, yaitu `name`, `amount`, `description`. Tambahkan elemen input sesuai dengan model pada aplikasi tugas Django yang telah kamu buat.
1. Membuat berkas baru dengan nama `beautiful_brews_form.dart` dan menambahkan kode berikut.
```text
...
class _ShopFormPageState extends State<ShopFormPage> {
    final _formKey = GlobalKey<FormState>();
    String _name = "";
    int _amount = 0;
    String _description = "";

    @override
    Widget build(BuildContext context) {
        return Scaffold(
          appBar: AppBar(
            title: const Center(
              child: Text(
                'Form Tambah Item',
              ),
            ),
            backgroundColor: Colors.indigo,
            foregroundColor: Colors.white,
          ),
          drawer: const LeftDrawer(),
          body: Form(
            key: _formKey,
            child: SingleChildScrollView(
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                  children: [
                    Padding(
                      padding: const EdgeInsets.all(8.0),
                      child: TextFormField(
                        decoration: InputDecoration(
                          hintText: "Nama Item",
                          labelText: "Nama Item",
                          border: OutlineInputBorder(
                            borderRadius: BorderRadius.circular(5.0),
                          ),
                        ),
                        onChanged: (String? value) {
                          setState(() {
                            _name = value!;
                          });
                        },
                        validator: (String? value) {
                          if (value == null || value.isEmpty) {
                            return "Nama tidak boleh kosong!";
                          }
                          return null;
                        },
                      ),
                    ),
                  Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: TextFormField(
                      decoration: InputDecoration(
                        hintText: "Jumlah",
                        labelText: "Jumlah",
                        border: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(5.0),
                        ),
                      ),
                      onChanged: (String? value) {
                        setState(() {
                          _amount = int.parse(value!);
                        });
                      },
                      validator: (String? value) {
                        if (value == null || value.isEmpty) {
                          return "Jumlah tidak boleh kosong!";
                        }
                        if (int.tryParse(value) == null) {
                          return "Jumlah harus berupa angka!";
                        }
                        return null;
                      },
                    ),
                  ),
                  Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: TextFormField(
                      decoration: InputDecoration(
                        hintText: "Deskripsi",
                        labelText: "Deskripsi",
                        border: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(5.0),
                        ),
                      ),
                      onChanged: (String? value) {
                        setState(() {
                          _description = value!;
                        });
                      },
                      validator: (String? value) {
                        if (value == null || value.isEmpty) {
                          return "Deskripsi tidak boleh kosong!";
                        }
                        return null;
                      },
                    ),
                  ),
...
```

- [x] Memiliki sebuah tombol `Save`.
1. Menambahkan kode berikut pada berkas `beautiful_brews_form.dart` dibawah kode yang paling terakhir ditulis.
```text
...
  Align(
  alignment: Alignment.bottomCenter,
  child: Padding(
    padding: const EdgeInsets.all(8.0),
    child: ElevatedButton(
      style: ButtonStyle(
        backgroundColor:
            MaterialStateProperty.all(Colors.indigo),
      ),
      onPressed: () {
        if (_formKey.currentState!.validate()) {
          showDialog(
            context: context,
            builder: (context) {
              return AlertDialog(
                title: const Text('Item berhasil tersimpan'),
                content: SingleChildScrollView(
                  child: Column(
                    crossAxisAlignment:
                        CrossAxisAlignment.start,
                    children: [
                      Text('Nama: $_name'),
                      Text('Jumlah: $_amount'),
                      Text('Deskripsi: $_description'),
                    ],
                  ),
                ),
                actions: [
                  TextButton(
                    child: const Text('OK'),
                    onPressed: () {
                      Navigator.pop(context);
                    },
                  ),
                ],
              );
            },
          );
        _formKey.currentState!.reset();
        }
      },
      child: const Text(
        "Save",
        style: TextStyle(color: Colors.white),
      ),
    ),
  ),
),
```

- [x] Setiap elemen input di formulir juga harus divalidasi dengan ketentuan sebagai berikut:
    - Setiap elemen input tidak boleh kosong.
    - Setiap elemen input harus berisi data dengan tipe data atribut modelnya.
1. Membuat `validator` untuk setiap input berupa `String` pada form.
```text
validator: (String? value) {
  if (value == null || value.isEmpty) {
    return "Nama tidak boleh kosong!";
  }
  return null;
},
```

2. Membuat `validator` untuk setiap input berupa `Integer` pada form.
```text
validator: (String? value) {
  if (value == null || value.isEmpty) {
    return "Jumlah tidak boleh kosong!";
  }
  if (int.tryParse(value) == null) {
    return "Jumlah harus berupa angka!";
  }
  return null;
},
```


- [x] Mengarahkan pengguna ke halaman form tambah item baru ketika menekan tombol `Tambah Item` pada halaman utama.
1. Membuat berkas dengan nama `shop_card.dart` dan menambahkan kode sebagai berikut untuk membuat `Navigator` yang akan melakukan push page `ShopFormPage` ke dalam stack.
```text
  if (item.name == "Tambah Item") {
  Navigator.push(
  context,
  MaterialPageRoute(
    builder: (context) => const ShopFormPage(),
  ));
}
```

- [x] Memunculkan data sesuai isi dari formulir yang diisi dalam sebuah `pop-up` setelah menekan tombol `Save` pada halaman formulir tambah item baru.
1. Membuka berkas `beautiful_brews_form.dart` lalu menambahkan fungsi `showDialog()` pada bagian `onPressed()`` dan munculkan widget `AlertDialog` pada fungsi tersebut.
```text
  onPressed: () {
  if (_formKey.currentState!.validate()) {
    showDialog(
      context: context,
      builder: (context) {
        return AlertDialog(
          title: const Text('Item berhasil tersimpan'),
          content: SingleChildScrollView(
            child: Column(
              crossAxisAlignment:
                  CrossAxisAlignment.start,
              children: [
                Text('Nama: $_name'),
                Text('Jumlah: $_amount'),
                Text('Deskripsi: $_description'),
              ],
            ),
          ),
          actions: [
            TextButton(
              child: const Text('OK'),
              onPressed: () {
                Navigator.pop(context);
              },
            ),
          ],
        );
      },
    );
  _formKey.currentState!.reset();
  }
},
```

- [x] Membuat sebuah drawer pada aplikasi dengan ketentuan sebagai berikut:
    - Drawer minimal memiliki dua buah opsi, yaitu `Halaman Utama` dan `Tambah Item`.
    1. Membuat folder baru dengan nama `widgets` dan membuat berkas baru di dalamnya dengan nama `left_drawer.dart`, lalu tambahkan kode berikut.
    ```text
        import 'package:flutter/material.dart';
        import 'package:beautiful_brews/screens/menu.dart';
        import 'package:beautiful_brews/screens/beautiful_brews_form.dart';


        class LeftDrawer extends StatelessWidget {
        const LeftDrawer({super.key});

        @override
        Widget build(BuildContext context) {
            return Drawer(
            child: ListView(
                children: [
                const DrawerHeader(
                    decoration: BoxDecoration(
                    color: Colors.indigo,
                    ),
                    child: Column(
                    children: [
                        Text(
                        'BeautyBrews Co.',
                        textAlign: TextAlign.center,
                        style: TextStyle(
                            fontSize: 30,
                            fontWeight: FontWeight.bold,
                            color: Colors.white,
                        ),
                        ),
                        Padding(padding: EdgeInsets.all(10)),
                        Text("Catat seluruh keperluan belanjamu di sini!",
                                style: TextStyle(
                                fontSize: 15.0,
                                fontWeight: FontWeight.normal,
                                color: Colors.white
                            ),
                            ),
                    ],
                    ),
                ),
                ListTile(
                    leading: const Icon(Icons.home_outlined),
                    title: const Text('Halaman Utama'),
                    // Bagian redirection ke MyHomePage
                    onTap: () {
                    Navigator.pushReplacement(
                        context,
                        MaterialPageRoute(
                            builder: (context) => MyHomePage(),
                        ));
                    },
                ),
                ListTile(
                    leading: const Icon(Icons.add_shopping_cart),
                    title: const Text('Tambah Item'),
                    // Bagian redirection ke ItemFormPage
                    onTap: () {
                    Navigator.pushReplacement(
                        context,
                        MaterialPageRoute(
                            builder: (context) => const ShopFormPage(),
                        ));
                    },
                ),
                ],
            ),
            );
        }
     }

    ```
    - Ketika memiih opsi `Halaman Utama`, maka aplikasi akan mengarahkan pengguna ke halaman utama.
    1. Menambahkan `Navigator.pushReplacement()` didalam fungsi `onTap` pada widget ListTile 'Halaman Utama' sehingga pada saat ditekan akan menghapus route yang sedang ditampilkan kepada pengguna dan menggantinya dengan route ke Halaman Utama. 
    ```text
    onTap: () {
    Navigator.pushReplacement(
      context,
      MaterialPageRoute(
       builder: (context) => MyHomePage(),
      ));
    },
    ```
    - Ketika memiih opsi (`Tambah Item`), maka aplikasi akan mengarahkan pengguna ke halaman form tambah item baru.
    1. Menambahkan `Navigator.pushReplacement()` didalam fungsi `onTap` pada widget ListTile 'Tambah Item' sehingga pada saat ditekan akan menghapus route yang sedang ditampilkan kepada pengguna dan menggantinya dengan route ke Tambah Item. 
    ```text
    onTap: () {
    Navigator.pushReplacement(
      context,
      MaterialPageRoute(
        builder: (context) => const ShopFormPage(),
      ));
    },
```
