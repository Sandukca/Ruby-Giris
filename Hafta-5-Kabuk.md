# Temel Seviye Dosya ve Dizin Kabuk Komutları: Hafta 5

Bu çalışmada masaüstünüzde terminalden klasör ve dosya oluşturacak, klasörler arasında gezinecek ve WSL'de Windows sürücülerinin nerede durduğunu göreceksiniz.

Komutların yanındaki `#` işaretinden sonraki kısım açıklamadır, terminal onu çalıştırmamaktadır. Komutları yazarken açıklamayı yazmanıza gerek yoktur.

**Kullanılan komutlar**

| Komut | Görevi |
| --- | --- |
| `pwd` | Şu an hangi klasörde olduğunuzu yazmaktadır (*print working directory*). |
| `ls` | Bulunduğunuz klasörün içindekileri listelemektedir. |
| `cd klasor` | Verilen klasöre girmektedir (*change directory*). |
| `cd ..` | Bir üst klasöre çıkmaktadır. |
| `mkdir ad` | Yeni bir klasör oluşturmaktadır (*make directory*). |
| `touch ad` | Boş bir dosya oluşturmaktadır. |

---

## 1. Terminalden masaüstüne gitme

Terminal açıldığında genellikle Linux tarafındaki ev klasörünüzde (`/home/kullanici_adi`) başlamaktadır. Bu klasör Windows masaüstünüz değildir. Önce nerede olduğunuza bakınız, sonra masaüstüne gidiniz:

```bash
pwd                                   # şu anki klasörü yazmaktadır, örneğin /home/ogrenci
cd /mnt/c/Users/Vagrant/Desktop       # okul bilgisayarında masaüstüne gitmektedir
pwd                                   # artık /mnt/c/Users/Vagrant/Desktop yazmalı
ls                                    # masaüstündeki klasör ve dosyaları listelemektedir
```

Kendi bilgisayarınızda `Vagrant` yerine Windows kullanıcı adınızı yazınız. Kullanıcı adınızı bilmiyorsanız şu komutla görebilirsiniz:

```bash
ls /mnt/c/Users                       # Windows'taki kullanıcı klasörlerini listelemektedir
```

**İpucu:** Yolun bir kısmını yazıp **Tab** tuşuna basarsanız terminal adı kendisi tamamlamaktadır. Böylece yazım hatası yapma ihtimaliniz azalmaktadır.

**Not:** Bazı bilgisayarlarda masaüstü OneDrive içindedir. `Desktop` bulunamazsa `cd /mnt/c/Users/KullaniciAdi/OneDrive/Desktop` yolunu deneyiniz.

## 2. Aynı anda 3 klasör oluşturma

`mkdir` komutuna birden fazla ad verirseniz hepsini tek seferde oluşturmaktadır. Adları aralarında boşluk bırakarak yazınız:

```bash
mkdir klasor1 klasor2 klasor3         # üç klasörü birlikte oluşturmaktadır
ls                                    # klasor1  klasor2  klasor3 görünmeli
```

Aynı işi daha kısa yazmanın bir yolu da vardır. `{1..3}` ifadesi kabuk tarafından `1 2 3` olarak açılmaktadır:

```bash
mkdir klasor{1..3}                    # mkdir klasor1 klasor2 klasor3 ile aynıdır
```

Klasörler zaten varsa bu ikinci komut `File exists` hatası vermektedir. Bu bir sorun değildir, klasörlerin oluşturulmuş olduğunu göstermektedir.

**Dikkat:** Adlarda boşluk ve Türkçe karakter kullanmayınız. `mkdir yeni klasor` komutu tek bir klasör değil, `yeni` ve `klasor` adında iki klasör oluşturmaktadır.

## 3. Aynı anda 3 dosya oluşturma

`touch` komutu da birden fazla ad alabilir:

```bash
touch dosya1.txt dosya2.txt dosya3.txt   # üç boş dosyayı birlikte oluşturmaktadır
ls                                       # klasörler ve dosyalar birlikte görünmeli
```

## 4. Dosya ile klasörün farkı

Masaüstünüze fareyle bakınız (açık pencereleri küçültünüz ya da **Windows + D** tuşlarına basınız). Terminalden oluşturduğunuz üç klasör ve üç dosya orada görünmelidir.

- **Klasör** sarı klasör simgesiyle görünmektedir. Çift tıklayınca içi açılmakta ve içinde başka dosya ve klasörler bulunabilir.
- **Dosya** belge simgesiyle görünmektedir. Çift tıklayınca bir programla (örneğin Not Defteri) açılmaktadır. Dosyanın içinde başka dosya bulunmamakta, yazı ya da veri bulunmaktadır.
- Dosya adının sonundaki `.txt` gibi kısma **uzantı** denilmektedir. Uzantı, dosyanın ne tür bir dosya olduğunu ve hangi programla açılacağını göstermektedir. Klasörlerin uzantısı olmamaktadır.

Aynı farkı terminalde de görebilirsiniz:

```bash
ls -F                                 # klasörlerin sonuna / koymaktadır: dosya1.txt  klasor1/
ls -l                                 # satırın ilk harfi d ise klasör, - ise dosyadır
```

`ls -l` çıktısının bir bölümü şöyle görünmektedir:

```
-rwxrwxrwx 1 ogrenci ogrenci    0 Nov 10 10:00 dosya1.txt
drwxrwxrwx 1 ogrenci ogrenci 4096 Nov 10 10:00 klasor1
```

Ortadaki sayı boyuttur. Yeni oluşturduğunuz dosyalar boş olduğu için boyutları `0`'dır.

Masaüstü klasörünü terminalden doğrudan Windows Gezgini'nde de açabilirsiniz:

```bash
explorer.exe .                        # bulunduğunuz klasörü Windows Gezgini'nde açmaktadır
```

Buradaki `.` işareti "bulunduğum klasör" demektir.

## 5. Klasörlerin içine girip dosya oluşturma

Her klasöre sırayla giriniz, içinde bir dosya oluşturunuz ve `cd ..` ile masaüstüne geri dönünüz. Her adımda `pwd` ile nerede olduğunuzu kontrol ediniz:

```bash
cd klasor1                            # klasor1'e girmektedir
pwd                                   # .../Desktop/klasor1 yazmalı
touch not1.txt                        # klasor1'in içinde not1.txt oluşturmaktadır
ls                                    # not1.txt görünmeli
cd ..                                 # bir üst klasöre, yani masaüstüne dönmektedir
pwd                                   # .../Desktop yazmalı

cd klasor2
touch not2.txt
cd ..

cd klasor3
touch not3.txt
cd ..
```

Hepsini bitirdikten sonra masaüstünden her klasörün içine bakınız:

```bash
ls klasor1 klasor2 klasor3            # her klasörün içindekileri ayrı ayrı listelemektedir
```

Fareyle de klasörleri çift tıklayıp açınız. Her klasörün içinde bir dosya görmelisiniz.

**Yol mantığı:** `..` her zaman "bir üst klasör", `.` her zaman "bulunduğum klasör" demektir. `cd ..` komutunu masaüstündeyken çalıştırırsanız `/mnt/c/Users/Vagrant` klasörüne çıkılmaktadır. Masaüstüne dönmek için `cd Desktop` yazınız.

## 6. WSL'de Windows sürücüleri nerede durmaktadır?

Okul bilgisayarlarında Windows'un içinde bir Linux (Ubuntu) çalışmaktadır. Buna **WSL** (*Windows Subsystem for Linux*) denilmektedir. Aynı bilgisayarda iki işletim sistemi aynı dosyalara iki farklı yazımla ulaşmaktadır.

### Windows: her disk bir harfle başlamaktadır

Windows'ta her diskin ve sürücünün kendi harfi vardır: `C:` sistem diski, `D:` ikinci disk ya da USB bellek gibi. Her yol bir sürücü harfiyle başlamakta ve klasörler ters bölü `\` ile ayrılmaktadır:

```
C:\Users\Vagrant\Desktop
```

Yani Windows'ta tek bir başlangıç noktası yoktur, her sürücü ayrı bir ağacın köküdür.

### Linux/Unix: her şey tek bir ağaçtadır

Linux, macOS gibi Unix türü sistemlerde sürücü harfi yoktur. Bütün dosyalar **kök** denen tek bir klasörün (`/`) altındadır ve klasörler düz bölü `/` ile ayrılmaktadır. Bilgisayara yeni bir disk takıldığında o disk ağaçtaki bir klasöre **bağlanmaktadır** (*mount*). Diskin içi artık o klasörün içi gibi görünmektedir.

WSL, Windows'un sürücülerini `/mnt` klasörünün altına bağlamaktadır. Sürücü harfi küçük harfle klasör adı olmaktadır:

| Windows'ta | WSL'de (Linux tarafında) |
| --- | --- |
| `C:\` | `/mnt/c` |
| `D:\` | `/mnt/d` |
| `C:\Users\Vagrant\Desktop` | `/mnt/c/Users/Vagrant/Desktop` |

Bu yüzden 1. adımda masaüstüne `cd /mnt/c/Users/Vagrant/Desktop` ile gittiniz. İkisi de aynı klasördür, yalnızca yazılışları farklıdır.

Terminalde kendiniz görünüz:

```bash
ls /                                  # Linux ağacının kökü: bin, etc, home, mnt, usr ...
ls /mnt                               # Windows sürücüleri: c (varsa d, e ...)
ls /mnt/c                             # C: sürücüsünün içi: Users, Windows, Program Files ...
```

Son komutun çıktısını Windows Gezgini'nde açtığınız `C:` sürücüsüyle karşılaştırınız. Aynı klasörleri görmelisiniz.

İki yazım arasında çevirmek için `wslpath` komutu kullanılmaktadır:

```bash
wslpath -w /mnt/c/Users               # Linux yolunu Windows yazımına çevirmektedir: C:\Users
wslpath 'C:\Users'                    # Windows yolunu Linux yazımına çevirmektedir: /mnt/c/Users
```

Windows yolunu yazarken tek tırnak `' '` kullanınız. Tırnak olmadan kabuk ters bölüleri silmektedir.

### Linux'un kendi ev klasörü

`/mnt` altındaki klasörler Windows'un diskidir. Linux'un kendi dosyaları ise ayrı bir sanal diskte durmaktadır. Terminali açtığınızda başladığınız ev klasörü buradadır:

```bash
cd ~                                  # ~ işareti ev klasörünüz demektir
pwd                                   # /home/kullanici_adi yazmaktadır
```

Bu klasör Windows masaüstünde ya da `C:` sürücüsünde görünmemektedir. Windows Gezgini'nden ulaşmak isterseniz adres çubuğuna `\\wsl$` yazınız ya da ev klasöründeyken terminalde `explorer.exe .` komutunu çalıştırınız.

### Dikkat edilecek farklar

- **Bölü işareti:** Windows `\`, Linux `/` kullanmaktadır. Terminalde her zaman `/` yazınız.
- **Büyük/küçük harf:** Linux'ta `Desktop` ile `desktop` iki ayrı addır. Windows bunları genellikle aynı kabul etmektedir. Windows'tan gelen bu alışkanlık terminalde hataya yol açmaktadır. Adları her zaman doğru harflerle yazınız.
- **WSL olmayan sistemler:** Doğrudan Linux kurulu bir bilgisayarda `/mnt/c` bulunmamaktadır. Takılan diskler genellikle `/media` ya da `/mnt` altında, macOS'ta ise `/Volumes` altında görünmektedir. Fikir aynıdır: her disk tek ağaçtaki bir klasöre bağlanmaktadır.

---

## Temizlik

Bu çalışmada oluşturduklarınızı silmek isterseniz masaüstündeyken şu komutları çalıştırınız:

```bash
rm dosya1.txt dosya2.txt dosya3.txt   # üç dosyayı silmektedir
rm -r klasor1 klasor2 klasor3         # üç klasörü içindekilerle birlikte silmektedir
```

**Dikkat:** Terminalden silinen dosyalar Geri Dönüşüm Kutusu'na gitmemekte, doğrudan silinmektedir. `rm` komutunu çalıştırmadan önce adları kontrol ediniz.
