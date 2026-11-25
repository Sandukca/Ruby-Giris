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

## Örnekler

**Girdi:** `1`

```
*
```

**Girdi:** `2`

```
 *
**
```

**Girdi:** `4`

```
   *
  **
 ***
****
```

**Girdi:** `10`

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

2. **Ters dik üçgen:** Sağa yaslı üçgenin baş aşağı hâli. En uzun satır en üsttedir. (İpucu: sayacı `n`'den başlatıp azaltınız.)

   ```bash
   echo "4" | ruby ters.rb
   ```

   Çıktı:

   ```
   ****
    ***
     **
      *
   ```

3. **Piramit:** Yıldızlar ortalanmıştır. `i`. satırda kaç yıldız olduğunu tabloyla bulunuz. (İpucu: 1, 3, 5, 7 …)

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

4. **Sayı üçgeni:** Yıldız yerine sayılar yazılır. Her satır bir öncekinin sonuna yeni bir sayı eklenerek oluşur. (İpucu: döngüden önce boş bir yazı (`''`) tanımlayıp her adımda `i.to_s` ekleyiniz.)

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

5. **İçi boş kare:** `n × n` boyutunda bir kare. İlk ve son satır dolu, aradaki satırlarda yalnızca kenarlarda yıldız vardır. (İpucu: döngünün içinde `if` ile ilk ve son satırı ayırınız.)

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
