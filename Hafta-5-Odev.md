# Ruby Ödevi: Hafta 5

Bu ödevde terminalde bir klasör oluşturacak, içine dört Ruby dosyası yazacak ve her birini çalıştıracaksınız.

---

## 1. Klasörü ve ilk dosyayı oluşturma

Terminali açınız ve aşağıdaki komutları sırayla yazınız. Okul bilgisayarında değilseniz ilk satırda `cd` ile kendi seçtiğiniz bir klasöre gidiniz.

```bash
cd /mnt/c/Users/Vagrant/Desktop   # okul bilgisayarında masaüstüne gider
mkdir Hafta5                      # Hafta5 adında bir klasör oluşturur
cd Hafta5                         # Hafta5 klasörüne girer
touch main.rb                     # boş bir main.rb dosyası oluşturur
code main.rb                      # main.rb dosyasını VS Code editöründe açar
```

## 2. Kodu kaydetme ve çalıştırma

Her dosya için aynı adımları izleyiniz:

1. Kodu VS Code editöründe yazınız.
2. **Ctrl + S** tuşlarıyla dosyayı kaydediniz.
3. Terminalde `ruby` komutuyla çalıştırınız:

```bash
ruby main.rb   # main.rb dosyasını çalıştırır
```

Kaydetmeyi unutursanız Ruby dosyanın eski halini çalıştırır.

---

## 3. main.rb: Merhaba

`puts` komutu kendisine verilen yazıyı ekrana yazar.

```ruby
puts "Merhaba"
```

**Ekrana yazılan:**

```
Merhaba
```

## 4. main2.rb: Metot ile merhaba

Yeni dosyayı oluşturup açınız:

```bash
touch main2.rb   # boş bir main2.rb dosyası oluşturur
code main2.rb    # main2.rb dosyasını VS Code editöründe açar
```

Metot, bir isim verilmiş kod parçasıdır. `def` ile başlar, `end` ile biter. Metot tanımlandığında çalışmaz, adı yazılınca çalışır.

```ruby
def merhaba
  puts "Merhaba"
end

merhaba
```

**Ekrana yazılan:**

```
Merhaba
```

## 5. main3.rb: Metot ile verilen mesajı yazma

```bash
touch main3.rb   # boş bir main3.rb dosyası oluşturur
code main3.rb    # main3.rb dosyasını VS Code editöründe açar
```

Metoda parantez içinde bir değer verilebilir. Burada `mesaj`, metoda verilen yazıyı tutar. Böylece aynı metot farklı yazılarla kullanılabilir.

```ruby
def yaz(mesaj)
  puts mesaj
end

yaz("Merhaba")
yaz("Ruby öğreniyorum")
```

**Ekrana yazılan:**

```
Merhaba
Ruby öğreniyorum
```

## 6. main4.rb: Değişkenler

```bash
touch main4.rb   # boş bir main4.rb dosyası oluşturur
code main4.rb    # main4.rb dosyasını VS Code editöründe açar
```

Değişken, bir değere verilen addır. `=` işaretiyle değer atanır. Yazının içinde bir değişkenin değerini göstermek için `#{ }` kullanılır.

```ruby
ad = "Deniz"        # yazı
yas = 19            # tam sayı
boy = 1.75          # ondalıklı sayı
ogrenci = true      # doğru ya da yanlış

puts ad
puts yas
puts boy
puts ogrenci

puts "Adım #{ad}, #{yas} yaşındayım."

yas = yas + 1       # değişkenin değeri değiştirilebilir
puts "Gelecek yıl #{yas} yaşında olacağım."
```

**Ekrana yazılan:**

```
Deniz
19
1.75
true
Adım Deniz, 19 yaşındayım.
Gelecek yıl 20 yaşında olacağım.
```

---

## Ek çalışma

Terminalde klasör ve dosya oluşturma, klasörler arasında gezinme ve WSL'de Windows sürücülerinin nerede durduğu hakkında daha fazla pratik için [Temel Seviye Dosya ve Dizin Kabuk Komutları](Hafta-5-Kabuk.md) sayfasına bakınız.
