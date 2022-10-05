<sup>Bu belge, Kotlin'in resmî rehberindeki [Basic syntax](https://kotlinlang.org/docs/basic-syntax.html) başlıklı kısmın çevirisidir. Son güncelleme: 05.10.2022<sup>
    
Bu belgede temel söz dizimi öğelerinin örnekleri yer almaktadır. Her kısmın sonunda ilgili konunun detaylı açıklamalarına yönlendiren bir bağlantı bulabilirsiniz.

Ayrıca, Kotlin'in tüm temel konularını JetBrains Academy üzerinden erişebileceğiniz ücretsiz [Kotlin Temelleri patikası](https://hyperskill.org/join/fromdocstoJetSalesStat?redirect=true&next=/tracks/18) ile öğrenebilirsiniz.

## Paket tanımlama ve içe dahil etme (import)

```kotlin
package my.demo

import kotlin.text.*

// ...
```

Dizinler ile paketleri eşleştirmek gerekli değildir. Kaynak dosyalar dosya sistemine isteğe bağlı olarak yerleştirilebilir.

Bkz. [Paketler](packages.md).

## Program başlangıç noktası

Kotlin'de bir programın başlangıç noktası `main` fonksiyonudur.

```kotlin
fun main() {
    println("Merhaba Dünya!")
}
```

`main` fonksiyonu, String argümanlar da alabilir.

```kotlin
fun main(args: Array<String>) {
    println(args.contentToString())
}
```

## Standart çıktı'ya (Standart output) yazdırma

`print` fonlsiyonu aldığı argümanı standart çıktıya yazdırır.

```kotlin
fun main() {
//örnekBaşlangıcı
    print("Merhaba ")
    print("Dünya!")
//örnekSonu
}
```

`println` fonksiyonu aldığı argümanları yazdırır ve alt satıra geçer. Böylece daha sonra ekrana yazdırılacaklar yeni satırda görünür.

```kotlin
fun main() {
//örnekBaşlangıcı
    println("Merhaba dünya!")
    println(42)
//örnekSonu
}
```

## Fonksiyonlar

İki adet `Int`parametresi alan ve `Int` değeri döndüren bir fonksiyon:

```kotlin
//örnekBaşlangıcı
fun sum(a: Int, b: Int): Int {
    return a + b
}
//örnekSonu

fun main() {
    print("3 ve 5'in toplamı: ")
    println(sum(3, 5))
}
```

Fonksiyonun gövdesi yerine bir deyim (expression) kullanılabilir. Bu deyim dönüş değeri olarak kullanılır.

```kotlin
//örnekBaşlangıcı
fun sum(a: Int, b: Int) = a + b
//örnekSonu

fun main() {
    println("19 ve 23'ün toplamı: ${sum(19, 23)}")
}
```

Anlamlı bir değer döndürmeyen bir fonksiyon:

```kotlin
//örnekBaşlangıcı
fun printSum(a: Int, b: Int): Unit {
    println("$a ve $b sayılarının toplamı: ${a + b}")
}
//örnekSonu

fun main() {
    printSum(-1, 8)
}
```

`Unit` dönüş tipi yazılmayabilir.

```kotlin
//örnekBaşlangıcı
fun printSum(a: Int, b: Int) {
    println("$a ve $b sayılarının toplamı: ${a + b}")
}
//örnekSonu

fun main() {
    printSum(-1, 8)
}
```

Bkz. [Fonksiyonlar](functions.md).
