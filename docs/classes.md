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

Kotlin, property tanımlamak ve bu property'leri birincil constructor'dan başlatmak için yalın bir sözdizimine sahiptir.

```kotlin
class Person(val firstName: String, val lastName: String, var age: Int)
```

Bu tanımlamalarda sınıf property'lerine varsayılan değerler de atayabiliriz.

```kotlin
class Person(val firstName: String, val lastName: String, var isEmployed: Boolean = true)
```

Sınıf property'leri tanımlarken son virgül ([trailing comma](coding-conventions.md#trailing-commas)) kullanabilirsiniz.

```kotlin
class Person(
    val firstName: String,
    val lastName: String,
    var age: Int, // son virgül
) { /*...*/ }
```

Sıradan property'ler gibi, birincil constructor'da tanımlanan property'ler de değeri değişebilir (`var`) veya değeri yalnızca okunabilir (`val`) olabilir.

Bir constructor'ın anotasyonları veya görünürlük düzenleyicisi var `constructor` deyiminin kullanılması gerekir. Düzenleyiciler bu deyimin önüne yazılır.

```kotlin
class Customer public @Inject constructor(name: String) { /*...*/ }
```

Görünürlük düzenleyicileri hakkında daha fazla bilgi için: [visibility modifiers](visibility-modifiers.md#constructors).

### İkincil constructor'lar

Sınıflarda _ikincil constructor'lar_ tanımlanabilir. Bu constructor'ların önüne `constructor` deyimi yazılır:

```kotlin
class Person(val pets: MutableList<Pet> = mutableListOf())

class Pet {
    constructor(owner: Person) {
        owner.pets.add(this) // adds this pet to the list of its owner's pets
    }
}
```

Bir sınıfta birincil constructor varsa ikincil constructor'ların hepsinin doğrudan veya diğer ikincil constructor'lar üzerinden dolaylı olarak birincil constructor'ı işaret etmesi gerekir. Aynı sınıf içerisindeki başka bir constructor'ı işaret etme işlemi `this` deyimi ile sağlanır:

```kotlin
class Person(val name: String) {
    val children: MutableList<Person> = mutableListOf()
    constructor(name: String, parent: Person) : this(name) {
        parent.children.add(this)
    }
}
```

