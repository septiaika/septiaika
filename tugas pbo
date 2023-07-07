import os
import sys
from PyQt5.QtWidgets import QApplication, QMainWindow, QLabel, QPushButton, QLineEdit, QMessageBox
from PyQt5.QtCore import Qt
#class obat untuk menyimpan nama obat
class Obat:
    def __init__(self, nama_obat):
        self.nama_obat = nama_obat

#class puskesmas untuk menyimpan tambahan obat, ambil obat
class Puskesmas:
    def __init__(self, kapasitas):
        self.obat = []
        self.kapasitas = kapasitas
# untuk menambah obat 
    def tambah_obat(self, nama_obat):
        if self.is_full(): #memanggil method is_full 
            return False, 'Lemari obat penuh. Tidak dapat menambahkan obat.'
        else:
            self.obat.append(Obat(nama_obat))
            return True, f"Obat {nama_obat} telah ditambahkan ke dalam lemari obat."
#untuk mengambil obat
    def ambil_obat(self, nama_obat): 


            for obat in self.obat:
                if obat.nama_obat.lower() == nama_obat.lower():

                    self.obat.remove(obat)
                    return True, f"Obat {obat.nama_obat} telah diambil dari lemari obat."
            return False, f"Tidak ditemukan obat dengan nama {nama_obat}."
#untuk cek jumlah obat
    def is_empty(self):
        return len(self.obat) == 0

    def is_full(self):
        return len(self.obat) == self.kapasitas

    def size(self):
        return len(self.obat)
#untuk menampilkan obat
    def tampilkan_obat(self):
        data = 'Data Obat di Lemari Obat\n'.center(25)
        data += '_______________________________\n'.center(25)


        for i, obat in enumerate(self.obat):
            data += f"{obat.nama_obat:<12}\n".center(20)
        return data

#untuk menampilkan tampilan Qmainwindow
class MainWindow(QMainWindow):
    def __init__(self, kapasitas_puskesmas):
        super().__init__()

        self.setWindowTitle('Aplikasi Pengambilan Obat')
        self.setGeometry(200, 200, 400, 400)
#untuk memanggil variabel
        self.puskesmas = Puskesmas(kapasitas_puskesmas)

        self.label = QLabel(self)
        self.label.setGeometry(50, 50, 300, 150)
        self.label.setAlignment(Qt.AlignTop | Qt.AlignCenter)

        self.label1 = QLabel('Masukkan Nama Obat:', self)
        self.label1.setGeometry(50, 160, 300, 30)
        self.label1.setAlignment(Qt.AlignLeft | Qt.AlignVCenter)

        self.pushButtonTambah = QPushButton('Tambah Obat', self)
        self.pushButtonTambah.setGeometry(50, 220, 300, 50)


        self.pushButtonTampilkan = QPushButton('Tampilkan Obat di Lemari', self)
        self.pushButtonTampilkan.setGeometry(50, 290, 300, 50)


        self.pushButtonAmbil = QPushButton('Ambil Obat', self)
        self.pushButtonAmbil.setGeometry(50, 360, 300, 50)

        self.lineEdit = QLineEdit(self)
        self.lineEdit.setGeometry(50, 190, 300, 30)

        #konsep signal dan slot
        self.pushButtonAmbil.clicked.connect(self.ambil_obat_clicked)
        self.pushButtonTampilkan.clicked.connect(self.tampilkan_obat_clicked)
        self.pushButtonTambah.clicked.connect(self.tambah_obat_clicked)

    def tambah_obat_clicked(self):
        nama_obat = self.lineEdit.text()
        success, message = self.puskesmas.tambah_obat(nama_obat)
        if success:
            QMessageBox.information(self, 'Informasi', message)
            self.lineEdit.clear()
        else:
            QMessageBox.warning(self, 'Peringatan', message)

    def tampilkan_obat_clicked(self):
        data = self.puskesmas.tampilkan_obat()
        self.label.setText(data)

    def ambil_obat_clicked(self):
        nama_obat = self.lineEdit.text()
        success, message = self.puskesmas.ambil_obat(nama_obat)
        if success:
            QMessageBox.information(self, 'Informasi', message)
        else:
            QMessageBox.warning(self, 'Peringatan', message)
        self.lineEdit.clear()
#untuk  menjalankan aplikasi
if __name__ == '__main__':
    os.system('cls')
    app = QApplication(sys.argv)
    kapasitas_puskesmas = int(input("Masukkan kapasitas lemari obat: "))
    window = MainWindow(kapasitas_puskesmas)
    window.show()
    sys.exit(app.exec_())
