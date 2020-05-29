# SIMPLE FTP SERVER AND CLIENT

ATAKAN TÜRKAY 170401009

## Açıklama

Python kütüphanelerine ekstra scapy kütüphanesi kullanılmıştır.

FTP CLIENT AND SERVER KOMUTLARI :
 
```bash
--CONNECTION
CLIENT "FTP_CLIENT_HANDSHAKE" İSTEĞİNİ YAPARAK SERVERE BAĞLANTI İSTEĞİ YAPAR
EĞER SERVER "FTP_SERVER_HANDSHAKE_OK" MESAJI YOLLARSA BAĞLANTI BAŞLAR. 
MENÜ AÇILIR. SERVER WHITELISTINE CLIENT IP ADRESINI KAYDEDER.ÇÜNKÜ İŞLEMLERDE İSTEKLERİN
YANI SIRA İSTEĞİ KİMİN YAPTIĞINA DA BAKAR.

--GET
"GET FILENAME" | BU İSTEĞİ SERVERA YAPAR VE SERVERİ DİNLEMEYE BAŞLAR.
DOSYAYI İSTER EĞER SERVERDE DOSYA YOK İSE "GET_ERROR" MESAJI ALIR VE BUNU EKRANA BASAR.
EĞER SERVERDEN "GET_INFO" MESAJI GELİRSE. MESAJIN İÇERİĞİNDEKİ LİSTEDEN DOSYA BİLGİLERİNİ
(BOYUT,HASH,CHUNKSIZE...)
TEMP BİR "CLASS DOSYA" YAPISINA KAYDEDER.SERVER DOSYAYI RAM UZERİNDE BİR DICTIONARYE ONCEDEN
TANIMLI CHUNKSIZE ILE CHUNKLERE PARCALAR VE HAFIZADA TUTAR.AMAC O CHUNKLERI TEKER TEKER YOLLAYIP
OLUMLU BİR DÖNÜT ALMAKTIR.
SERVER "GET_FILEPART CHUNK_NUMARASI CHUNK" OLARAK DOSYA PARÇALARINI YOLLAR VE CLIENT GELEN DOSYALARI
ONAYLAR "GET_FILEPART_OK " İLE.
FTP SERVER ONAY MESAJLARINI ALDIKÇA DICTIONARY ÜZERİNDEN ONAYLI YOLLANMIŞ VERİLERİ SİLER. DICTIONARY
UZUNLUĞU 0 OLDUĞU ZAMAN TÜM PARÇALAR DOĞRU ŞEKİLDE ATILMIŞ DEMEKTİR.
BU AŞAMADA CLIENT TÜM DOSYALARI ALIĞINDA "CLASS DOSYA" YAPISINA BİRLEŞTİR EMRİ VERİR VE ALINAN TÜM
PARÇALAR BİRLEŞTİRİLİR. DOSYA YAZILIR. OLUŞAN DOSYA HASHI İLE SERVERİN YOLLADIĞI BİLGİ KARŞILAŞTIRILIR.
EĞER HATA VARSA EKRANA BASILIR. YOKSA MENÜYE DÖNER. FTP SERVERE "GET_FINISH_BASARILI" MESAJI GÖNDERİLİR
VE SERVER TEKRARDAN STANDBY POZİSYONUNA GEÇER.


--PUT
GET İLE BENZER MANTIKTA ÇALIŞMAKTADIR.

```


## default chunksize = 512 byte
## windows üzerinde listen yaparken problemler yaşadığım için delay koymak zorunda kaldım. 0.001sn
## Asyncsniffer kullandım. bunu hız düşüklüğünün sebebi olarak düşünüyorum.