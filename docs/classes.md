[//]: # (title: Sınıflar)

Kotlin'de sınıflar `class` deyimi ile tanımlanır.

```kotlin
class Person { /*...*/ }
```

Sınıflar sınıf adı, sınıf başlığı (parametrelerini, birincil contructor'ını ve diğer bilgileri) ve süslü parantezler ile kapsamı belirtilmiş sınıf gövdesinden oluşur. Başlık ve gövde kısmı isteğe bağlıdır. Sınıfın gövdesi yoksa süslü parantezler kaldırılabilir.

```kotlin
class Empty
```

## Constructor

Kotlin'de sınıflar tek bir _birincil constructor_ ve bir ya da birden fazla _ikincil contructor_ alabilir. Birincil constructor sınıf başlığına aittir ve sınıf adından ve isteğe bağlı olan tip parametresinden sonra gelir.

```kotlin
class Person constructor(firstName: String) { /*...*/ }
```

Birincil constructor herhangi bir annotation veya görünürlük düzenleyicisine (visibility modifier) sahip değilse `constructor` deyimi kaldırılabilir:

```kotlin
class Person(firstName: String) { /*...*/ }
```

Birincil constructor herhangi bir kod içeremez. Başlatma komutları `init` deyimi ile tanımlanan _başlatma bloklarının_ içine yazılabilir.

Sınıftan bir örnek oluşturulurken başlatma blokları sınıfın gövdesinde yazılı olduğu sırada, property tanımlamalarıyla ayrılmış şekilde çalıştırılır.

```kotlin
//sampleStart
class InitOrderDemo(name: String) {
    val firstProperty = "Birinci property: $name".also(::println)
    
    init {
        println("İlk bailatma bloğu çıktısı: $name")
    }
    
    val secondProperty = "İkinci property: ${name.length}".also(::println)
    
    init {
        println("İkinci başlatma bloğu çıktısı: ${name.length}")
    }
}
//sampleEnd

fun main() {
    InitOrderDemo("hello")
}
```
{kotlin-runnable="true"}

Birincil constructor parametreleri başlatma blokları içinde kullnılabilir. Ayrıca, sınıfın gövdesindeki property tanımlamalarında da kullanılabilirler.

```kotlin
class Customer(name: String) {
    val customerKey = name.uppercase()
}
```

