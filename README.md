# Veritaban-Y-netim-Sistemi-dev-2

CREATE DATABASE KutuphaneDB;
USE KutuphaneDB;

-- ÜYELER Tablosu
CREATE TABLE Uyeler (
    UyeID INT PRIMARY KEY AUTO_INCREMENT,
    Ad VARCHAR(50) NOT NULL,
    Soyad VARCHAR(50) NOT NULL,
    Telefon VARCHAR(15),
    Eposta VARCHAR(100) UNIQUE,
    Emanet_Tarih DATE
);

-- ADRESLER Tablosu
CREATE TABLE Adresler (
    AdresID INT PRIMARY KEY AUTO_INCREMENT,
    Sehir VARCHAR(50) NOT NULL,
    Ilce VARCHAR(50) NOT NULL,
    Cadde VARCHAR(100),
    PostaKodu VARCHAR(10)
);

-- KÜTÜPHANE Tablosu
CREATE TABLE Kutuphane (
    KutuphaneID INT PRIMARY KEY AUTO_INCREMENT,
    Ad VARCHAR(100) NOT NULL,
    Aciklama TEXT,
    Sehir VARCHAR(50)
);

-- KİTAPLAR Tablosu
CREATE TABLE Kitaplar (
    KitapID INT PRIMARY KEY AUTO_INCREMENT,
    KitapAdi VARCHAR(255) NOT NULL,
    SayfaSayisi INT,
    YayinTarihi DATE
);

-- YAZARLAR Tablosu
CREATE TABLE Yazarlar (
    YazarID INT PRIMARY KEY AUTO_INCREMENT,
    Ad VARCHAR(50) NOT NULL,
    Soyad VARCHAR(50) NOT NULL
);

-- KATEGORİLER Tablosu
CREATE TABLE Kategoriler (
    KategoriID INT PRIMARY KEY AUTO_INCREMENT,
    KategoriAdi VARCHAR(100) NOT NULL
);

-- EMANETLER Tablosu (Ödünç Verme)
CREATE TABLE Emanetler (
    EmanetID INT PRIMARY KEY AUTO_INCREMENT,
    UyeID INT,
    KitapID INT,
    Emanet_Tarih DATE NOT NULL,
    Teslim_Tarih DATE,
    FOREIGN KEY (UyeID) REFERENCES Uyeler(UyeID) ON DELETE CASCADE,
    FOREIGN KEY (KitapID) REFERENCES Kitaplar(KitapID) ON DELETE CASCADE
);

-- Kitap ve Yazar Arasındaki İlişki (Çoktan çoğa)
CREATE TABLE KitapYazar (
    KitapID INT,
    YazarID INT,
    PRIMARY KEY (KitapID, YazarID),
    FOREIGN KEY (KitapID) REFERENCES Kitaplar(KitapID) ON DELETE CASCADE,
    FOREIGN KEY (YazarID) REFERENCES Yazarlar(YazarID) ON DELETE CASCADE
);

-- Kitap ve Kategori Arasındaki İlişki (Çoktan çoğa)
CREATE TABLE KitapKategori (
    KitapID INT,
    KategoriID INT,
    PRIMARY KEY (KitapID, KategoriID),
    FOREIGN KEY (KitapID) REFERENCES Kitaplar(KitapID) ON DELETE CASCADE,
    FOREIGN KEY (KategoriID) REFERENCES Kategoriler(KategoriID) ON DELETE CASCADE
);
