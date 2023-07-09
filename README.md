# Super_Cashier-Project_Pacmann-

Program SuperCashier adalah sistem kasir mandiri sederhana untuk supermarket yang memungkinkan pelanggan memasukkan informasi barang, jumlah, dan harga yang ingin dibeli.

# Background
Pemilik sebuah supermarket di suatu kota ingin meningkatkan efisiensi bisnisnya dengan memperkenalkan kasir self-service. Dengan ini, pelanggan dapat membeli barang langsung dari supermarket, mulai dari memesan produk, memasukkan jumlah item, hingga menginputkan harga belanjaan. Dengan adanya inovasi ini, supermarket tersebut dapat menjangkau pasar yang lebih luas, sehingga pelanggan dari luar kota pun dapat melakukan pembelian barang-barang dari supermarket tersebut.

# Feature Requirement
Berikut adalah langkah-langkah yang dapat dilakukan oleh pelanggan:

1. Pelanggan dapat memasukkan ID mereka.
2. Pelanggan dapat memasukkan nama barang, jumlah barang, dan harga barang.
3. Jika terdapat kesalahan dalam input, pelanggan dapat melakukan hal berikut:
   a. Memperbarui nama barang.
   b. Memperbarui jumlah barang.
   c. Memperbarui harga barang.
4. Jika pelanggan ingin membatalkan sebuah item belanjaan, mereka dapat melakukan salah satu dari dua opsi berikut:
   a. Menghapus salah satu item dari daftar belanja.
   b. Menghapus seluruh transaksi dan mengulang dari awal.
5. Setelah selesai, pelanggan dapat memeriksa daftar belanjaan mereka.
6. Pelanggan dapat memeriksa total harga pembelian.

# Flowchart
![alt text](https://github.com/robbyarihidayat/Super_Cashier-Project_Pacmann-/blob/main/Screenshot%202023-07-09%20at%202.50.29%20PM.png?raw=true))





# Fungsi
1. Class Transaction :

class Transaction:
    def __init__(self):
        """"
        Fungsi ini adalah untuk menginisiasi dictionary item yang akan diinputkan pembeli
        dan variabel total belanja yang akan di bayarkan pembeli
        """
        self.order_list = {}

2. add_item() :

def add_item(self, item_info):
        """
        Fungsi ini adalah untuk menambahkan item baru ke dalam daftar transaksi.
        """
        try:
            name, qty, price = item_info
            if name not in self.order_list:
                self.order_list[name] = [qty, price]
            else:
                self.order_list[name][0] += qty
        except ValueError:
            print("Input data harus berisi nama item, jumlah item, dan harga item dalam format [nama, jumlah, harga]")

3. delete_item() :
 
  def delete_item(self, name):
        """
        Fungsi ini adalah untuk menghapus item dari daftar transaksi berdasarkan nama item.
        """
        try:
            del self.order_list[name]
        except KeyError:
            print(f"Item {name} tidak ditemukan dalam transaksi")

update_item_name() , update_item_qty() , update_item_price() :
def update_item_name(self, name, update_name):
        """
        Fungsi ini adalah untuk mengubah nama item pada daftar transaksi.
        yang dihasilkan.
        """
        try:
            self.order_list[update_name] = self.order_list.pop(name)
        except KeyError:
            print(f"Item {name} tidak ditemukan dalam transaksi")

4. check_order() :

def update_item_qty(self, name, update_qty):
        """
        Fungsi ini adalah untuk mengubah jumlah item pada daftar transaksi.
        """
        try:
            self.order_list[name][0] = update_qty
        except KeyError:
            print(f"Item {name} tidak ditemukan dalam transaksi")
    def update_item_price(self, name, update_price):
        """
        Fungsi ini adalah untuk mengubah harga item pada daftar transaksi.
        """
        try:
            self.order_list[name][1] = update_price
        except KeyError:
            print(f"Item {name} tidak ditemukan dalam transaksi")



5. total_price(). Memiliki fungsi untuk menghitung total belanjaan pelanggan beserta dengan diskonnya. Diskon yang diperoleh pelanggan akan mengikuti ketentuan sebagai berikut:

Jika total belanja diatas Rp 200.000 maka akan mendapatkan diskon 5%.

Jika total belanja diatas Rp 300.000 maka akan mendapatkan diskon 8%.

Jika total belanja diatas Rp 500.000 maka akan mendapatkan diskon 10% 
  
   def check_order(self):
        """
        Fungsi ini adalah untuk mengecek daftar item yang telah dibeli dan total harga.
        """
        if not self.order_list:
            print("Belum ada item yang dibeli")
        else:
            print("Item yang dibeli adalah:")
            print("| No | Nama item | Jumlah item | Harga/item | Total harga |")
            print("-" * 65)
            total_price = 0
            for index, (name, item_info) in enumerate(self.order_list.items(), start=1):
                qty, price = item_info
                total = qty * price
                print(f"| {index:<2} | {name:<9} | {qty:<11} | {price:>10,.0f} | {total:>11,.0f} |")
                total_price += total
            print("-" * 65)
            return total_price

    def total_price(self):
        """
        Fungsi ini adalah untuk menghitung total harga yang harus dibayar dan mengeluarkan diskon jika diperlukan.
        Dengan kondisional sebagai berikut. 
            a. Jika total belanja di atas Rp 200.000 akan mendapatkan diskon 5%
            b. Jika total belanja di atas Rp 300.000 akan mendapatkan diskon 8%
            c. Jika total belanja di atas Rp 500.000 akan mendapatkan dikon 10%
            d. Jika di bawah Rp 200.000 maka akan langsung menampilkan total harga belanja
        """
        total_price = self.check_order()
        if total_price > 500000:
            discount = 0.1
            print(f'Total belanja kamu di atas Rp 500000 \nSelamat kamu mendapatkan diskon sebesar 10%')
        elif total_price > 300000:
            discount = 0.08
            print(f'Total belanja kamu di atas Rp 300000 \nSelamat kamu mendapatkan diskon sebesar 8%')
        elif total_price > 200000:
            discount = 0.05
            print(f'Total belanja kamu di atas Rp 200000 \nSelamat kamu mendapatkan diskon sebesar 5%')
        else:
            discount = 0

        discounted_price = total_price * discount
        total_discounted_price = total_price - discounted_price
        print(f"Total belanja yang harus dibayarkan adalah {total_discounted_price:,.0f}")
        return total_discounted_price


6. reset_transaction()
   def reset_transaction(self):
        """
        Fungsi ini adalah untuk menghapus semua item pada daftar transaksi.
        """
        self.order_list = {}
        print("Semua item berhasil dihapus!")

# Test Case
 1) Pada case pertama berikut, customer ingin membeli 2 Ayam Goreng seharga @20,000 dan 3 Pasta Gigi seharga @15,000


2) Case 2 berikut ternyata customer salah membeli item Pasta Gigi, sehingga harus menghapus nama barang beserta jumlah dan harganya.


3) Setelah menghapus semua belanjaan di keranjang, customer membeli lagi barang-barang berikut dan langsung ingin membayarnya ke kasir.

2 Ayam Goreng @20,000
3 Pasta Gigi @15,000
1 Mainan Mobil @200,000
5 Mie Instan @3,000


# Kesimpulan 
Setelah melalui beberapa test case, sistem kasir self-service terbukti berjalan dengan baik. Namun, untuk meningkatkan efektivitas dan efisiensi, terdapat beberapa pengembangan yang dapat dilakukan pada sistem kasir self-service.

1. Database Harga: Membangun database harga akan membantu menghindari kecurangan (fraud) dan memudahkan manajemen harga produk. Dengan menggunakan database harga, Anda dapat menyimpan informasi harga produk secara terpusat, sehingga memudahkan pembaruan harga dan pengelolaan stok.

2. Data Transaksi: Membangun fitur penyimpanan data transaksi setiap pembeli akan membantu dalam melacak riwayat pembelian, menganalisis pola pembelian, dan menyediakan informasi penting untuk keperluan akuntansi dan analisis bisnis. Anda dapat menyimpan data transaksi dalam basis data terpisah atau menggunakan sistem manajemen basis data (Database Management System) untuk menyimpan dan mengelola data secara efisien.

3. User Interface (UI) / Graphical User Interface (GUI): Membangun antarmuka pengguna (user interface) yang intuitif dan user-friendly dapat meningkatkan pengalaman pengguna. Dengan menggunakan GUI, pengguna dapat dengan mudah berinteraksi dengan sistem kasir self-service melalui tampilan visual yang lebih menarik dan interaktif. Ini akan membantu pengguna dalam melakukan pembelian dengan lebih cepat dan mudah.

4. Pengoptimalan Kode: Melakukan pengoptimalan pada kode juga penting untuk meningkatkan efisiensi sistem. Anda dapat mempertimbangkan teknik-teknik seperti caching, penggunaan struktur data yang efisien, dan penggunaan algoritma yang lebih efektif untuk mempercepat kinerja sistem.

Dengan melakukan pengembangan-pengembangan tersebut, sistem kasir self-service akan menjadi lebih canggih, efisien, dan user-friendly, serta dapat memberikan manfaat yang lebih besar bagi pengguna dan pemilik bisnis.


































