[//]: # (title: Kapsam fonksiyonları)

<sup>Bu belge, Kotlin'in resmi dökümantasyonundaki [Scope functions](https://kotlinlang.org/docs/scope-functions.html) başlıklı kısmın çevirisidir. Son güncelleme: 19.09.2022<sup>


Kotlin'in standart kütüphanesi, bir kod bloğunu bir nesnenin (object) bağlamında (context) çalıştırmak için tasarlanmış birkaç fonksiyon içerir. Bu fonksiyonları bir nesne üzerinde çağırır ve [lambda gösterimi](lambdas.md) kullanırsanız geçici bir kapsam (scope) oluşur. Bu tür fonksiyonlara _kapsam fonksiyonları_ (scope functions) adı verilir. Beş adet kapsam fonksiyonu vardır: `let`, `run`, `with`, `apply` ve `also`.

Bu fonksiyonların hepsi temel olarak aynı şekilde çalışır; bir nesne üzerinde kod bloğu çalıştırırlar. Nesnenin kod bloğu içinde kullanılabilirliği ve tüm ifadenin döndürdüğü sonuca göre birbirlerinden ayrışırlar.

Aşağıdaki örnekte bir kapsam fonksiyonunun kullanımını görmektesiniz:

```kotlin
data class Person(var name: String, var age: Int, var city: String) {
    fun moveTo(newCity: String) { city = newCity }
    fun incrementAge() { age++ }
}

fun main() {
//örnekBaşlangıcı
    Person("Ali", 20, "İstanbul").let {
        println(it)
        it.moveTo("Ankara")
        it.incrementAge()
        println(it)
    }
//örnekSonu
}
```

Aynı kodu `let` kullanmadan yazdığınızda bir değişken tanımlamanız ve kullanmak istediğinizde bu değişkeni tekrar yazmanız gerekir.

```kotlin
data class Person(var name: String, var age: Int, var city: String) {
    fun moveTo(newCity: String) { city = newCity }
    fun incrementAge() { age++ }
}

fun main() {
//örnekBaşlangıcı
    val alice = Person("Ali", 20, "İstanbul")
    println(alice)
    alice.moveTo("Ankara")
    alice.incrementAge()
    println(alice)
//örnekSonu
}
```

Kapsam fonksiyonları teknik açıdan yeni beceriler sunmaz ancak yazdığınız kodun daha okunaklı ve öz olmasını sağlar.

Birbirine benzer yapılarından dolayı sizin durumunuza uygun olan kapsam fonksiyonunu seçmek zor olabilir. Bu seçim, yapmak istediğinize ve projedeki kullanımlara bağlı olarak değişir. Aşağıda kapsam fonksiyonları arasındaki farklardan ve nasıl kullanıldıklarından söz edeceğiz.

## Fonksiyon seçimi

|Fonksiyon|Nesne referansı|Dönüş değeri|Uzantı (extension) fonksiyon mu?|
|---|---|---|---|
|`let`|`it`|Lambda|Evet|
|`run`|`this`|Lambda|Evet|
|`run`|-|Lambda|Hayır: bağlam nesnesi olmadan çağrılır.|
|`with`|`this`|Lambda|Hayır: bağlam nesnesini argüman olarak alır.|
|`apply`|`this`|Bağlam nesnesi|Evet|
|`also`|`it`|Bağlam nesnesi|Evet|