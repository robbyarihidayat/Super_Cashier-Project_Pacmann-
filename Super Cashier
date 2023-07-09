class Transaction:
    def __init__(self):
        """"
        Fungsi ini adalah untuk menginisiasi dictionary item yang akan diinputkan pembeli
        dan variabel total belanja yang akan di bayarkan pembeli
        """
        self.order_list = {}
        
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

    def delete_item(self, name):
        """
        Fungsi ini adalah untuk menghapus item dari daftar transaksi berdasarkan nama item.
        """
        try:
            del self.order_list[name]
        except KeyError:
            print(f"Item {name} tidak ditemukan dalam transaksi")

    def update_item_name(self, name, update_name):
        """
        Fungsi ini adalah untuk mengubah nama item pada daftar transaksi.
        yang dihasilkan.
        """
        try:
            self.order_list[update_name] = self.order_list.pop(name)
        except KeyError:
            print(f"Item {name} tidak ditemukan dalam transaksi")

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

    def reset_transaction(self):
        """
        Fungsi ini adalah untuk menghapus semua item pada daftar transaksi.
        """
        self.order_list = {}
        print("Semua item berhasil dihapus!")
