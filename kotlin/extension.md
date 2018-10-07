### Sort list of enums by ordinality

```kotlin
fun <T : Enum<*>> List<T>.sortByOrdinal(): List<T>{
    return this.sortedBy {
        it.ordinal
    }
}
```
