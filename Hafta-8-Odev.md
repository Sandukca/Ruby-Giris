# Ruby Ödevi: Hafta 8

## Sağa yaslı dik üçgen

Kullanıcıdan bir tam sayı (`n`) alıp `*` karakterleriyle `n` satırlık, sağa yaslı bir dik üçgen çizen bir program yazınız. Programda **tek bir `while` döngüsü** kullanınız.

**İpucu:** Ruby'de bir yazıyı bir sayıyla çarparsanız yazı o kadar kez yan yana yazılır. Terminalde aşağıdaki kodu çalıştırıp deneyiniz:

```ruby
puts "q" * 4      # qqqq
puts " " * 3 + "*" # üç boşluk, sonra bir yıldız
```

---

## Programı oluşturma ve çalıştırma

Hafta 5'teki gibi masaüstünde bir klasör açıp içinde `main.rb` dosyasını oluşturunuz:

```bash
cd /mnt/c/Users/Vagrant/Desktop   # okul bilgisayarında masaüstüne gider
mkdir Hafta8                      # Hafta8 adında bir klasör oluşturur
cd Hafta8                         # Hafta8 klasörüne girer
touch main.rb                     # boş bir main.rb dosyası oluşturur
code main.rb                      # main.rb dosyasını VS Code editöründe açar
```

Programınızı iki şekilde çalıştırabilirsiniz:

```bash
ruby main.rb            # program sayıyı bekler, siz yazıp Enter'a basarsınız
echo "4" | ruby main.rb # 4 sayısı programa doğrudan verilir
```

---

## Uyarı: Girdiyi `echo` ve `|` ile verme

Programınızdaki `gets`, **standart girişten** bir satır okur. Standart giriş normalde klavyedir. Bu yüzden `ruby main.rb` yazdığınızda program durur ve sizin bir sayı yazıp Enter'a basmanızı bekler.

Aynı girdiyi her seferinde elle yazmak yerine komutla da verebilirsiniz:

- `echo` kendisine verilen yazıyı ekrana yazar ve sonuna bir satır sonu (Enter) ekler.
- `|` işaretine **pipe** (boru) denir. Solundaki komutun ekrana yazacağı şeyi ekrana yazdırmaz, sağındaki programın standart girişine verir.

Yani `echo "4" | ruby main.rb` komutunda `echo`'nun yazdığı `4` ve Enter, `main.rb`'ye klavyeden yazılmış gibi gelir. `gets` bu satırı okur.

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

İki yolun sonucu aynıdır. Farkı şudur: `echo` ile verdiğinizde program sizi beklemez ve girdi (`Deniz`) ekranda ayrıca görünmez, yalnızca programın çıktısı görünür.

**3. Birden fazla girdi**

Her `gets` bir satır okur. Program iki kez `gets` çağırıyorsa iki satır vermeniz gerekir. `toplam.rb`:

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

**Dikkat:** `echo "3 5" | ruby toplam.rb` yazarsanız iki sayı tek satırda gider. İlk `gets` `3 5` satırının tamamını okur, `to_i` bundan `3` çıkarır. İkinci `gets` okuyacak satır bulamaz, `b` da `0` olur. Ekranda `8` yerine `3` görürsünüz.

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

Tablodan şu kural çıkar: `i`. satırda **`n - i` boşluk** ve **`i` yıldız** vardır. Satır sayısı da `n`'dir.

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

1. `n = gets.to_i`: Kullanıcının yazdığı sayıyı okur ve tam sayıya çevirir.
2. `i = 1`: Kaçıncı satırda olduğumuzu tutan sayaç 1'den başlar.
3. `while i <= n`: Sayaç `n`'yi geçene kadar döngü çalışır, yani `n` satır yazılır.
4. `' ' * (n - i)`: Satırın başına `n - i` tane boşluk koyar.
5. `'*' * i`: Boşlukların arkasına `i` tane yıldız ekler. İki parça `+` ile birleştirilip `puts` ile yazılır.
6. `i += 1`: Bir sonraki satıra geçer.

---

## Kendiniz deneyiniz

Aşağıdaki şekilleri de birer programla çiziniz. Her birinde yine kullanıcıdan `n` alınız ve tek bir `while` döngüsü kullanınız. Her şekil için `Hafta8` klasöründe ayrı bir dosya oluşturunuz (örneğin `touch sola.rb`) ve programınızı verilen komutla çalıştırınız.

1. **Sola yaslı dik üçgen:** Yıldızlar sola dayalıdır, satır başında boşluk yoktur.

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

2. **Sağa yaslı ters dik üçgen:** Sağa yaslı üçgenin baş aşağı hâli. En uzun satır en üsttedir. (İpucu: sayacı `n`'den başlatıp azaltınız.)

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

3. **Sola yaslı ters dik üçgen:** Sola yaslı üçgenin baş aşağı hâli. Satır başında boşluk yoktur, en uzun satır en üsttedir.

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

4. **Piramit:** Yıldızlar ortalanmıştır. `i`. satırda kaç yıldız olduğunu tabloyla bulunuz. (İpucu: 1, 3, 5, 7 …)

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

5. **Sayı üçgeni:** Yıldız yerine sayılar yazılır. Her satır bir öncekinin sonuna yeni bir sayı eklenerek oluşur. (İpucu: döngüden önce boş bir yazı (`''`) tanımlayıp her adımda `i.to_s` ekleyiniz.)

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

6. **İçi boş kare:** `n × n` boyutunda bir kare. İlk ve son satır dolu, aradaki satırlarda yalnızca kenarlarda yıldız vardır. (İpucu: döngünün içinde `if` ile ilk ve son satırı ayırınız.)

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
