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