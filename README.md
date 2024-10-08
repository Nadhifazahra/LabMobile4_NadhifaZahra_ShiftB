# Pertemuan 4 Toko Kita

Nadhifa Zahra Kurniawan  
<br>Shift B

## Registrasi Page

**a. Tampilan Form Registrasi**  
<img src="https://github.com/user-attachments/assets/a30ca997-f006-4247-8c53-51f224ffc38e" width="300"> <img src="https://github.com/user-attachments/assets/836f897c-977b-4c61-accd-db261a6de3e1" width="300"><br>
Sebelum melakukan login, pengguna harus melakukan registrasi terlebih dahulu. Tampilan registrasi didapat dari kode berikut:
```
Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text("Registrasi Nadhifa"),
      ),
      body: SingleChildScrollView(
        child: Padding(
          padding: const EdgeInsets.all(8.0),
          child: Form(
            key: _formKey,
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                _namaTextField(),
                _emailTextField(),
                _passwordTextField(),
                _passwordKonfirmasiTextField(),
                _buttonRegistrasi()
              ],
            ),
          ),
        ),
      ),
    );
  }
```

**b. Registrasi Berhasil**  
<img src="https://github.com/user-attachments/assets/75173947-8799-43a4-b766-d1a45749bc67" width="300"><br>
Jika registrasi berhasil, akan muncul pop-up seperti gambar di atas. Pop-up ini dihasilkan oleh kode berikut:  

```dart
RegistrasiBloc.registrasi(
  nama: _namaTextboxController.text,
  email: _emailTextboxController.text,
  password: _passwordTextboxController.text
).then((value) {
  showDialog(
    context: context,
    barrierDismissible: false,
    builder: (BuildContext context) => SuccessDialog(
      description: "Registrasi berhasil, silahkan login",
      okClick: () {
        Navigator.pop(context);
      },
    )
  );
});
```
c. Registrasi Gagal<br>
<img src="https://github.com/user-attachments/assets/cd5a107b-5386-459f-ab66-3d7d1ba8d12d" width="300"><br>
Jika inputan form registrasi tidak sesuai, maka akan muncul peringatan seperti pada gambar. Peringatan tersebut didapat dari widget sebagai berikut:
```dart
 Widget _namaTextField() {
    return TextFormField(
      decoration: const InputDecoration(labelText: "Nama"),
      keyboardType: TextInputType.text,
      controller: _namaTextboxController,
      validator: (value) {
        if (value!.length < 3) {
          return "Nama harus diisi minimal 3 karakter";
        }
        return null;
      },
    );
  }

  //Membuat Textbox email
  Widget _emailTextField() {
    return TextFormField(
      decoration: const InputDecoration(labelText: "Email"),
      keyboardType: TextInputType.emailAddress,
      controller: _emailTextboxController,
      validator: (value) {
        //validasi harus diisi
        if (value!.isEmpty) {
          return 'Email harus diisi';
        }
        //validasi email
        Pattern pattern =
            r'^(([^<>()[\]\\.,;:\s@\"]+(\.[^<>()[\]\\.,;:\s@\"]+)*)|(\".+\"))@((\[[0 - 9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zAZ]{2,}))$';
        RegExp regex = RegExp(pattern.toString());
        if (!regex.hasMatch(value)) {
          return "Email tidak valid";
        }
        return null;
      },
    );
  }

  //Membuat Textbox password
  Widget _passwordTextField() {
    return TextFormField(
      decoration: const InputDecoration(labelText: "Password"),
      keyboardType: TextInputType.text,
      obscureText: true,
      controller: _passwordTextboxController,
      validator: (value) {
        //jika karakter yang dimasukkan kurang dari 6 karakter
        if (value!.length < 6) {
          return "Password harus diisi minimal 6 karakter";
        }
        return null;
      },
    );
  }

  //membuat textbox Konfirmasi Password
  Widget _passwordKonfirmasiTextField() {
    return TextFormField(
      decoration: const InputDecoration(labelText: "Konfirmasi Password"),
      keyboardType: TextInputType.text,
      obscureText: true,
      validator: (value) {
        //jika inputan tidak sama dengan password
        if (value != _passwordTextboxController.text) {
          return "Konfirmasi Password tidak sama";
        }
        return null;
      },
    );
  }
```

## Login Page
a. Tampilan form login<br>
<img src="https://github.com/user-attachments/assets/3b29147a-0e22-42d9-8253-f4fa10e38cf7" width="300">
<img src="https://github.com/user-attachments/assets/b69835b2-bab2-4a8e-9f7d-d24791aab2b8" width="300"><br>
Setelah registrasi berhasil, button 'OK' di pop up registrasi sukses akan mengarahkan ke login page. Login page berisi form dengan kolom email dan password. Jika login berhasil, button 'Login' akan langsung mengarahkan ke Produk Page. Tampilan login didapat dari kode berikut:
```
 Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Login Nadhifa'),
      ),
      body: SingleChildScrollView(
        child: Padding(
          padding: const EdgeInsets.all(8.0),
          child: Form(
            key: _formKey,
            child: Column(
              children: [
                _emailTextField(),
                _passwordTextField(),
                _buttonLogin(),
                const SizedBox(
                  height: 30,
                ),
                _menuRegistrasi()
              ],
            ),
          ),
        ),
      ),
    );
  }
```

b. Login gagal <br>
<img src="https://github.com/user-attachments/assets/c3a756e8-ce96-425d-9e3d-4b7889f5387a" width="300"><br>
Jika email atau password salah, maka akan menampilkan pop up peringatan login gagal. Pop up ini dihasilkan dari kode berikut:
```
else {
        showDialog(
            context: context,
            barrierDismissible: false,
            builder: (BuildContext context) => const WarningDialog(
                  description: "Login gagal, silahkan coba lagi",
                ));
      }
    }, onError: (error) {
      print(error);
      showDialog(
          context: context,
          barrierDismissible: false,
          builder: (BuildContext context) => const WarningDialog(
                description: "Login gagal, silahkan coba lagi",
              ));
    });
  }
```


## Produk Page
<img src="https://github.com/user-attachments/assets/d9592233-2bca-4bf5-8cda-4ef0c80449b4" width="300">
Setelah login berhasil, akan menampilkan Produk Page yang masih kosong. Pada halaman ini terdapat button + untuk menambahkan produk dan sidebar untuk logout. Tampilan produk page didapat dari kode berikut
``` dart
class _ProdukPageState extends State<ProdukPage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('List Produk Nadhifa'),
        actions: [
          Padding(
              padding: const EdgeInsets.only(right: 20.0),
              child: GestureDetector(
                child: const Icon(Icons.add, size: 26.0),
                onTap: () async {
                  Navigator.push(context,
                      MaterialPageRoute(builder: (context) => ProdukForm()));
                },
              ))
        ],
      ),
      drawer: Drawer(
        child: ListView(
          children: [
            ListTile(
              title: const Text('Logout'),
              trailing: const Icon(Icons.logout),
              onTap: () async {
                await LogoutBloc.logout().then((value) => {
                      Navigator.of(context).pushAndRemoveUntil(
                          MaterialPageRoute(builder: (context) => LoginPage()),
                          (route) => false)
                    });
              },
            )
          ],
        ),
      ),
      body: FutureBuilder<List>(
        future: ProdukBloc.getProduks(),
        builder: (context, snapshot) {
          if (snapshot.hasError) print(snapshot.error);
          return snapshot.hasData
              ? ListProduk(
                  list: snapshot.data,
                )
              : const Center(
                  child: CircularProgressIndicator(),
                );
        },
      ),
    );
  }
}
```


## Tambah Produk
<img src="https://github.com/user-attachments/assets/99c0f16d-9af9-4b1b-ac8f-61e8deacdda2" width="300">
<img src="https://github.com/user-attachments/assets/998a7369-60c1-43ba-a821-a1b92961f345" width="300">
<img src="https://github.com/user-attachments/assets/c975049a-546e-4b84-b510-6ad731f3e445" width="300">

## Detail Produk
<img src="https://github.com/user-attachments/assets/ed900d3a-7c78-4f6c-a05c-cdb663023a0a" width="300">

## Ubah Produk
<img src="https://github.com/user-attachments/assets/95574d5b-6f7d-416a-9cc7-aff4a6c3370c" width="300">
<img src="https://github.com/user-attachments/assets/69aeaccb-45a3-4872-a50f-63cfe776fceb" width="300">

## Hapus Produk
<img src="https://github.com/user-attachments/assets/89d6a85e-b4d3-4e0d-9671-61a4108b191e" width="300">
