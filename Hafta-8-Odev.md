# Ruby Çalışma Ödevi: Hafta 8

## Sağa yaslı dik üçgen

Kullanıcıdan bir tam sayı (`n`) alıp `*` karakterleriyle `n` satırlık, sağa yaslı bir dik üçgen çizen bir program yazınız. Programda **tek bir `while` döngüsü** kullanınız.

Bu bir **çalışma ödevidir**, teslim edilmeyecektir. Konuyu pekiştirmek için kendiniz çalışınız. Çözüm sayfanın ilerisinde verilmiştir. Çözüme bakmadan önce programı kendiniz yazmaya çalışmanız tavsiye edilmektedir.

Negatif değer girilme ihtimalini düşünmeyiniz. Programınızı 1 ile 50 arasındaki değerlerle deneyiniz.

**İpucu:** Ruby'de bir yazıyı bir sayıyla çarparsanız yazı o kadar kez yan yana yazılmaktadır. Terminalde aşağıdaki kodu çalıştırıp deneyiniz:

```ruby
puts "q" * 4      # qqqq
puts " " * 3 + "*" # üç boşluk, sonra bir yıldız
```

---

## Programı oluşturma ve çalıştırma

Hafta 5'teki gibi masaüstünde bir klasör açıp içinde `main.rb` dosyasını oluşturunuz:

```bash
cd /mnt/c/Users/vagrant/Desktop   # okul bilgisayarında masaüstüne gitmektedir
mkdir Hafta8                      # Hafta8 adında bir klasör oluşturmaktadır
cd Hafta8                         # Hafta8 klasörüne girmektedir
touch main.rb                     # boş bir main.rb dosyası oluşturmaktadır
code main.rb                      # main.rb dosyasını VS Code editöründe açmaktadır
```

Programınızı iki şekilde çalıştırabilirsiniz:

```bash
ruby main.rb            # program, sayıyı yazıp Enter'a basmanızı beklemektedir
echo "4" | ruby main.rb # 4 sayısı programa doğrudan verilmektedir
```

---

## Uyarı: Girdiyi `echo` ve `|` ile verme

Programınızdaki `gets`, **standart girişten** bir satır okumaktadır. Standart giriş normalde klavyedir. Bu yüzden `ruby main.rb` yazdığınızda program durmakta ve sizin bir sayı yazıp Enter'a basmanızı beklemektedir.

Aynı girdiyi her seferinde elle yazmak yerine komutla da verebilirsiniz:

- `echo` kendisine verilen yazıyı ekrana yazmakta ve sonuna bir satır sonu (Enter) eklemektedir.
- `|` işaretine **pipe** (boru) denilmektedir. Pipe, solundaki komutun ekrana yazacağı şeyi ekrana yazdırmamakta, sağındaki programın standart girişine vermektedir.

Yani `echo "4" | ruby main.rb` komutunda `echo`'nun yazdığı `4` ve Enter, `main.rb`'ye klavyeden yazılmış gibi gelmektedir. `gets` bu satırı okumaktadır.

**1. `echo` tek başına**

```bash
echo "Merhaba"
```

Çıktı:

```
Merhaba
```

**2. `gets` ile okuyan bir program**

`selam.rb` dosyasına aşağıdaki kodu yazınız:

```ruby
ad = gets.chomp
puts "Merhaba #{ad}"
```

Önce elle çalıştırınız: `ruby selam.rb` yazınız, program beklerken `Deniz` yazıp Enter'a basınız. Sonra aynı girdiyi `echo` ile veriniz:

```bash
echo "Deniz" | ruby selam.rb
```

Çıktı:

```
Merhaba Deniz
```

İki yolun sonucu aynıdır. Farkı şudur: `echo` ile verdiğinizde program sizi beklememekte ve girdi (`Deniz`) ekranda ayrıca görünmemektedir. Ekranda yalnızca programın çıktısı görünmektedir.

**3. Birden fazla girdi**

Her `gets` bir satır okumaktadır. Program iki kez `gets` çağırıyorsa iki satır vermeniz gerekmektedir. `toplam.rb`:

```ruby
a = gets.to_i
b = gets.to_i
puts a + b
```

`printf` ile `\n` (satır sonu) koyarak iki satırı tek komutta verebilirsiniz:

```bash
printf "3\n5\n" | ruby toplam.rb
```

Çıktı:

```
8
```

**Dikkat:** `echo "3 5" | ruby toplam.rb` yazarsanız iki sayı tek satırda gitmektedir. İlk `gets` `3 5` satırının tamamını okumakta, `to_i` bundan `3` çıkarmaktadır. İkinci `gets` okuyacak satır bulamamakta, `b` de `0` olmaktadır. Bu durumda ekranda `8` yerine `3` yazılmaktadır.

Bu ödevde program tek bir sayı okuduğu için `echo "4" | ruby main.rb` yeterlidir.

---

## Örnekler

**Örnek 1**

```bash
echo "1" | ruby main.rb
```

Çıktı:

```
*
```

**Örnek 2**

```bash
echo "2" | ruby main.rb
```

Çıktı:

```
 *
**
```

**Örnek 3**

```bash
echo "4" | ruby main.rb
```

Çıktı:

```
   *
  **
 ***
****
```

**Örnek 4**

```bash
echo "10" | ruby main.rb
```

Çıktı:

```
         *
        **
       ***
      ****
     *****
    ******
   *******
  ********
 *********
**********
```

Her satırın son karakteri yıldızdır, yıldızdan sonra boşluk yoktur.

---

## Kodlamadan önce düşününüz

Kodu yazmadan önce algoritmayı kâğıt üzerinde kurunuz:

- Program kaç satır yazacak?
- Her satırda kaç boşluk, kaç yıldız var?

`n = 4` için satırları tabloya dökünüz:

| Satır (`i`) | Boşluk sayısı | Yıldız sayısı | Ekrana yazılan |
| --- | --- | --- | --- |
| 1 | 3 | 1 | `   *` |
| 2 | 2 | 2 | `  **` |
| 3 | 1 | 3 | ` ***` |
| 4 | 0 | 4 | `****` |

Tablodan şu kural çıkmaktadır: `i`. satırda **`n - i` boşluk** ve **`i` yıldız** vardır. Satır sayısı da `n`'dir.

---

## Çözüm

```ruby
# frozen_string_literal: true

n = gets.to_i
i = 1
while i <= n
  puts ' ' * (n - i) + '*' * i
  i += 1
end
```

**Satır satır açıklama**

1. `n = gets.to_i`: Kullanıcının yazdığı sayıyı okumakta ve tam sayıya çevirmektedir.
2. `i = 1`: Kaçıncı satırda olduğumuzu tutan sayaç 1'den başlamaktadır.
3. `while i <= n`: Sayaç `n`'yi geçene kadar döngü çalışmakta, yani `n` satır yazılmaktadır.
4. `' ' * (n - i)`: Satırın başına `n - i` tane boşluk koymaktadır.
5. `'*' * i`: Boşlukların arkasına `i` tane yıldız eklemektedir. İki parça `+` ile birleştirilip `puts` ile yazılmaktadır.
6. `i += 1`: Bir sonraki satıra geçilmektedir.

---

## Sık yapılan hatalar

Aşağıdaki hatalı programlar `echo "3" | ruby main.rb` ile çalıştırılmıştır. Programınız beklenmedik bir çıktı veriyorsa önce bu listeyi kontrol ediniz.

**1. `to_i` unutulursa**

```ruby
n = gets
```

`gets` girilen değeri yazı (String) olarak okumaktadır. `i <= n` karşılaştırmasında sayı ile yazı karşılaştırılamadığı için program hata vermektedir:

```
comparison of Integer with String failed (ArgumentError)
```

Doğrusu `n = gets.to_i` şeklindedir.

**2. Parantez unutulursa**

```ruby
puts ' ' * n - i + '*' * i
```

Ruby önce `' ' * n` işlemini yapmakta ve bir yazı elde etmektedir. Ardından bu yazıdan `i` sayısını çıkarmaya çalışmaktadır. Yazıdan sayı çıkarılamadığı için program hata vermektedir:

```
undefined method `-' for "   ":String (NoMethodError)
```

Doğrusu `' ' * (n - i)` şeklindedir. Önce parantezin içi hesaplanmakta, sonra boşluk o kadar kez yazılmaktadır.

**3. `+` yerine virgül kullanılırsa**

```ruby
puts ' ' * (n - i), '*' * i
```

`puts` virgülle ayrılmış her değeri ayrı bir satıra yazmaktadır. Bu yüzden boşluklar ve yıldızlar alt alta düşmektedir:

```
  
*
 
**

***
```

Doğrusu iki parçayı `+` ile birleştirmektir.

**4. `i += 1` unutulursa**

```ruby
while i <= n
  puts ' ' * (n - i) + '*' * i
end
```

`i` hiç artmadığı için `i <= n` koşulu hep doğru kalmakta ve döngü sonsuza kadar çalışmaktadır. Ekran aynı satırla dolmaktadır:

```
  *
  *
  *
...
```

Sonsuz döngüye giren bir programı terminalde **Ctrl + C** tuşlarıyla durdurabilirsiniz.

**5. Sayaç yanlış başlatılırsa**

```ruby
i = 0
```

Sayaç 0'dan başlarsa döngü `n` yerine `n + 1` kez çalışmaktadır. İlk satırda hiç yıldız olmadığı için çıktının başına yalnızca boşluklardan oluşan fazladan bir satır eklenmektedir:

```
   
  *
 **
***
```

**6. Koşulda `<=` yerine `<` yazılırsa**

```ruby
while i < n
```

Döngü `i` değeri `n`'ye eşit olduğunda durmaktadır. Bu yüzden en alttaki, yıldızlarla dolu son satır yazılmamaktadır:

```
  *
 **
```

---

## Kendiniz deneyiniz

Aşağıdaki şekilleri de birer programla çiziniz. Her birinde yine kullanıcıdan `n` alınız ve tek bir `while` döngüsü kullanınız. Her şekil için `Hafta8` klasöründe ayrı bir dosya oluşturunuz (örneğin `touch sola.rb`) ve programınızı verilen komutla çalıştırınız. Programlarınızı yine 1 ile 50 arasındaki değerlerle deneyiniz.

1. **Sola yaslı dik üçgen:** Yıldızlar sola dayalıdır, satır başında boşluk yoktur.

   **Örnek 1**

   ```bash
   echo "4" | ruby sola.rb
   ```

   Çıktı:

   ```
   *
   **
   ***
   ****
   ```

   **Örnek 2**

   ```bash
   echo "6" | ruby sola.rb
   ```

   Çıktı:

   ```
   *
   **
   ***
   ****
   *****
   ******
   ```

2. **Sağa yaslı ters dik üçgen:** Sağa yaslı üçgenin baş aşağı hâli. En uzun satır en üsttedir. (İpucu: sayacı `n`'den başlatıp azaltınız.)

   **Örnek 1**

   ```bash
   echo "4" | ruby saga_ters.rb
   ```

   Çıktı:

   ```
   ****
    ***
     **
      *
   ```

   **Örnek 2**

   ```bash
   echo "6" | ruby saga_ters.rb
   ```

   Çıktı:

   ```
   ******
    *****
     ****
      ***
       **
        *
   ```

3. **Sola yaslı ters dik üçgen:** Sola yaslı üçgenin baş aşağı hâli. Satır başında boşluk yoktur, en uzun satır en üsttedir.

   **Örnek 1**

   ```bash
   echo "4" | ruby sola_ters.rb
   ```

   Çıktı:

   ```
   ****
   ***
   **
   *
   ```

   **Örnek 2**

   ```bash
   echo "6" | ruby sola_ters.rb
   ```

   Çıktı:

   ```
   ******
   *****
   ****
   ***
   **
   *
   ```

4. **Piramit:** Yıldızlar ortalanmıştır. `i`. satırda kaç yıldız olduğunu tabloyla bulunuz. (İpucu: 1, 3, 5, 7 …)

   **Örnek 1**

   ```bash
   echo "4" | ruby piramit.rb
   ```

   Çıktı:

   ```
      *
     ***
    *****
   *******
   ```

   **Örnek 2**

   ```bash
   echo "6" | ruby piramit.rb
   ```

   Çıktı:

   ```
        *
       ***
      *****
     *******
    *********
   ***********
   ```

5. **Sayı üçgeni:** Yıldız yerine sayılar yazılmaktadır. Her satır, bir öncekinin sonuna yeni bir sayı eklenerek oluşmaktadır. (İpucu: döngüden önce boş bir yazı (`''`) tanımlayıp her adımda `i.to_s` ekleyiniz.)

   **Örnek 1**

   ```bash
   echo "4" | ruby sayi.rb
   ```

   Çıktı:

   ```
   1
   12
   123
   1234
   ```

   **Örnek 2**

   ```bash
   echo "6" | ruby sayi.rb
   ```

   Çıktı:

   ```
   1
   12
   123
   1234
   12345
   123456
   ```

6. **İçi boş kare:** `n × n` boyutunda bir kare. İlk ve son satır dolu, aradaki satırlarda yalnızca kenarlarda yıldız vardır. (İpucu: döngünün içinde `if` ile ilk ve son satırı ayırınız.) Bu şekilde `n`'nin 4 ile 50 arasında olduğunu varsayınız.

   **Örnek 1**

   ```bash
   echo "4" | ruby kare.rb
   ```

   Çıktı:

   ```
   ****
   *  *
   *  *
   ****
   ```

   **Örnek 2**

   ```bash
   echo "6" | ruby kare.rb
   ```

   Çıktı:

   ```
   ******
   *    *
   *    *
   *    *
   *    *
   ******
   ```
