class Bioskop:
    def __init__(self):
        self.films = {
            '1': {'judul': 'Avengers', 'harga': 50000, 'studio': ['A', 'B'], 'jadwal': ['10:00', '13:00', '16:00']},
            '2': {'judul': 'Superman', 'harga': 55000, 'studio': ['C'], 'jadwal': ['11:00', '14:00', '17:00']}
        }
        self.kursi = {
            'A': 50, 'B': 40, 'C': 30
        }

    def tampilkan_film(self):
        for kode, film in self.films.items():
            print(f"{kode}. {film['judul']} - Rp{film['harga']}")

    def pilih_film(self, kode):
        return self.films.get(kode)

    def pesan_tiket(self, film, studio, jadwal, jumlah):
        if self.kursi[studio] >= jumlah:
            total_harga = film['harga'] * jumlah
            self.kursi[studio] -= jumlah
            return total_harga, True
        return 0, False

def main():
    bioskop = Bioskop()

    while True:
        print("\n--- Sistem Penjualan Tiket ---")
        bioskop.tampilkan_film()
        
        kode_film = input("Pilih kode film: ")
        film = bioskop.pilih_film(kode_film)
        
        if film:
            print(f"\nFilm: {film['judul']}")
            print("Studio tersedia:", film['studio'])
            print("Jadwal:", film['jadwal'])
            
            studio = input("Pilih studio: ")
            jadwal = input("Pilih jadwal: ")
            jumlah_tiket = int(input("Jumlah tiket: "))
            
            total, berhasil = bioskop.pesan_tiket(film, studio, jadwal, jumlah_tiket)
            
            if berhasil:
                print(f"\nPembayaran: Rp{total}")
                print("Tiket berhasil dipesan!")
            else:
                print("Maaf, kursi tidak mencukupi.")
        
        lanjut = input("\nIngin memesan lagi? (y/n): ")
        if lanjut.lower() != 'y':
            break

if __name__ == "__main__":
    main()
