# Kabuk Betiği Pratikleri: Hafta 5

Bu pratiklerde masaüstünüzde terminalden klasör ve dosya oluşturacak, klasörler arasında gezinecek ve WSL'de Windows sürücülerinin nerede durduğunu göreceksiniz.

Komutların yanındaki `#` işaretinden sonraki kısım açıklamadır, terminal onu çalıştırmaz. Komutları yazarken açıklamayı yazmanıza gerek yoktur.

**Kullanılan komutlar**

| Komut | Ne yapar |
| --- | --- |
| `pwd` | Şu an hangi klasörde olduğunuzu yazar (*print working directory*). |
| `ls` | Bulunduğunuz klasörün içindekileri listeler. |
| `cd klasor` | Verilen klasöre girer (*change directory*). |
| `cd ..` | Bir üst klasöre çıkar. |
| `mkdir ad` | Yeni bir klasör oluşturur (*make directory*). |
| `touch ad` | Boş bir dosya oluşturur. |

---

## 1. Terminalden masaüstüne gitme

Terminali açtığınızda genellikle Linux tarafındaki ev klasörünüzde (`/home/kullanici_adi`) başlarsınız. Bu klasör Windows masaüstünüz değildir. Önce nerede olduğunuza bakınız, sonra masaüstüne gidiniz:

```bash
pwd                                   # şu anki klasörü yazar, örneğin /home/ogrenci
cd /mnt/c/Users/Vagrant/Desktop       # okul bilgisayarında masaüstüne gider
pwd                                   # artık /mnt/c/Users/Vagrant/Desktop yazmalı
ls                                    # masaüstündeki klasör ve dosyaları listeler
```

Kendi bilgisayarınızda `Vagrant` yerine Windows kullanıcı adınızı yazınız. Kullanıcı adınızı bilmiyorsanız şu komutla görebilirsiniz:

```bash
ls /mnt/c/Users                       # Windows'taki kullanıcı klasörlerini listeler
```

**İpucu:** Yolun bir kısmını yazıp **Tab** tuşuna basarsanız terminal adı kendisi tamamlar. Böylece yazım hatası yapmazsınız.

**Not:** Bazı bilgisayarlarda masaüstü OneDrive içindedir. `Desktop` bulunamazsa `cd /mnt/c/Users/KullaniciAdi/OneDrive/Desktop` yolunu deneyiniz.

## 2. Aynı anda 3 klasör oluşturma

`mkdir` komutuna birden fazla ad verirseniz hepsini tek seferde oluşturur. Adları aralarında boşluk bırakarak yazınız:

```bash
mkdir klasor1 klasor2 klasor3         # üç klasörü birlikte oluşturur
ls                                    # klasor1  klasor2  klasor3 görünmeli
```

Aynı işi daha kısa yazmanın bir yolu da vardır. `{1..3}` ifadesi kabuk tarafından `1 2 3` olarak açılır:

```bash
mkdir klasor{1..3}                    # mkdir klasor1 klasor2 klasor3 ile aynıdır
```

Klasörler zaten varsa bu ikinci komut `File exists` hatası verir. Bu bir sorun değildir, klasörlerin oluşturulmuş olduğunu gösterir.

**Dikkat:** Adlarda boşluk ve Türkçe karakter kullanmayınız. `mkdir yeni klasor` komutu tek bir klasör değil, `yeni` ve `klasor` adında iki klasör oluşturur.

## 3. Aynı anda 3 dosya oluşturma

`touch` komutu da birden fazla ad alabilir:

```bash
touch dosya1.txt dosya2.txt dosya3.txt   # üç boş dosyayı birlikte oluşturur
ls                                       # klasörler ve dosyalar birlikte görünmeli
```

## 4. Dosya ile klasörün farkı

Masaüstünüze fareyle bakınız (açık pencereleri küçültünüz ya da **Windows + D** tuşlarına basınız). Terminalden oluşturduğunuz üç klasör ve üç dosya orada görünmelidir.

- **Klasör** sarı klasör simgesiyle görünür. Çift tıklayınca içi açılır ve içinde başka dosya ve klasörler bulunabilir.
- **Dosya** belge simgesiyle görünür. Çift tıklayınca bir programla (örneğin Not Defteri) açılır. Dosyanın içinde başka dosya olmaz, yazı ya da veri olur.
- Dosya adının sonundaki `.txt` gibi kısma **uzantı** denir. Uzantı, dosyanın ne tür bir dosya olduğunu ve hangi programla açılacağını gösterir. Klasörlerin uzantısı olmaz.

Aynı farkı terminalde de görebilirsiniz:

```bash
ls -F                                 # klasörlerin sonuna / koyar: dosya1.txt  klasor1/
ls -l                                 # satırın ilk harfi d ise klasör, - ise dosyadır
```

`ls -l` çıktısının bir bölümü şöyle görünür:

```
-rwxrwxrwx 1 ogrenci ogrenci    0 Nov 10 10:00 dosya1.txt
drwxrwxrwx 1 ogrenci ogrenci 4096 Nov 10 10:00 klasor1
```

Ortadaki sayı boyuttur. Yeni oluşturduğunuz dosyalar boş olduğu için boyutları `0`'dır.

Masaüstü klasörünü terminalden doğrudan Windows Gezgini'nde de açabilirsiniz:

```bash
explorer.exe .                        # bulunduğunuz klasörü Windows Gezgini'nde açar
```

Buradaki `.` işareti "bulunduğum klasör" demektir.

## 5. Klasörlerin içine girip dosya oluşturma

Her klasöre sırayla giriniz, içinde bir dosya oluşturunuz ve `cd ..` ile masaüstüne geri dönünüz. Her adımda `pwd` ile nerede olduğunuzu kontrol ediniz:

```bash
cd klasor1                            # klasor1'e girer
pwd                                   # .../Desktop/klasor1 yazmalı
touch not1.txt                        # klasor1'in içinde not1.txt oluşturur
ls                                    # not1.txt görünmeli
cd ..                                 # bir üst klasöre, yani masaüstüne döner
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
ls klasor1 klasor2 klasor3            # her klasörün içindekileri ayrı ayrı listeler
```

Fareyle de klasörleri çift tıklayıp açınız. Her klasörün içinde bir dosya görmelisiniz.

**Yol mantığı:** `..` her zaman "bir üst klasör", `.` her zaman "bulunduğum klasör" demektir. `cd ..` komutunu masaüstündeyken çalıştırırsanız `/mnt/c/Users/Vagrant` klasörüne çıkarsınız. Masaüstüne dönmek için `cd Desktop` yazınız.

## 6. WSL'de Windows sürücüleri nerede durur?

Okul bilgisayarlarında Windows'un içinde bir Linux (Ubuntu) çalışır. Buna **WSL** (*Windows Subsystem for Linux*) denir. Aynı bilgisayarda iki işletim sistemi aynı dosyalara iki farklı yazımla ulaşır.

### Windows: her disk bir harfle başlar

Windows'ta her diskin ve sürücünün kendi harfi vardır: `C:` sistem diski, `D:` ikinci disk ya da USB bellek gibi. Her yol bir sürücü harfiyle başlar ve klasörler ters bölü `\` ile ayrılır:

```
C:\Users\Vagrant\Desktop
```

Yani Windows'ta tek bir başlangıç noktası yoktur, her sürücü ayrı bir ağacın köküdür.

### Linux/Unix: her şey tek bir ağaçtadır

Linux, macOS gibi Unix türü sistemlerde sürücü harfi yoktur. Bütün dosyalar **kök** denen tek bir klasörün (`/`) altındadır ve klasörler düz bölü `/` ile ayrılır. Bilgisayara yeni bir disk takıldığında o disk ağaçtaki bir klasöre **bağlanır** (*mount*). Diskin içi artık o klasörün içi gibi görünür.

WSL, Windows'un sürücülerini `/mnt` klasörünün altına bağlar. Sürücü harfi küçük harfle klasör adı olur:

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

İki yazım arasında çevirmek için `wslpath` komutu kullanılır:

```bash
wslpath -w /mnt/c/Users               # Linux yolunu Windows yazımına çevirir: C:\Users
wslpath 'C:\Users'                    # Windows yolunu Linux yazımına çevirir: /mnt/c/Users
```

Windows yolunu yazarken tek tırnak `' '` kullanınız. Tırnak olmadan kabuk ters bölüleri siler.

### Linux'un kendi ev klasörü

`/mnt` altındaki klasörler Windows'un diskidir. Linux'un kendi dosyaları ise ayrı bir sanal diskte durur. Terminali açtığınızda başladığınız ev klasörü buradadır:

```bash
cd ~                                  # ~ işareti ev klasörünüz demektir
pwd                                   # /home/kullanici_adi yazar
```

Bu klasör Windows masaüstünde ya da `C:` sürücüsünde görünmez. Windows Gezgini'nden ulaşmak isterseniz adres çubuğuna `\\wsl$` yazınız ya da ev klasöründeyken terminalde `explorer.exe .` komutunu çalıştırınız.

### Dikkat edilecek farklar

- **Bölü işareti:** Windows `\`, Linux `/` kullanır. Terminalde her zaman `/` yazınız.
- **Büyük/küçük harf:** Linux'ta `Desktop` ile `desktop` iki ayrı addır. Windows bunları genellikle aynı kabul eder. Windows'tan gelen bu alışkanlık terminalde hataya yol açar. Adları her zaman doğru harflerle yazınız.
- **WSL olmayan sistemler:** Doğrudan Linux kurulu bir bilgisayarda `/mnt/c` olmaz. Takılan diskler genellikle `/media` ya da `/mnt` altında görünür. macOS'ta ise `/Volumes` altında görünür. Fikir aynıdır: her disk tek ağaçtaki bir klasöre bağlanır.

---

## Temizlik

Pratikte oluşturduklarınızı silmek isterseniz masaüstündeyken şu komutları çalıştırınız:

```bash
rm dosya1.txt dosya2.txt dosya3.txt   # üç dosyayı siler
rm -r klasor1 klasor2 klasor3         # üç klasörü içindekilerle birlikte siler
```

**Dikkat:** Terminalden silinen dosyalar Geri Dönüşüm Kutusu'na gitmez, doğrudan silinir. `rm` komutunu çalıştırmadan önce adları kontrol ediniz.
