# Map Enchancements

Java 8 added several powerful default methods to the `Map` interface, making common operations (iteration, sorting, computing values) much easier and more expressive.

Below is a breakdown of the most useful additions, followed by example code with explanations.

### Key Enhancements in Map (Java 8)

| Method                     | Purpose                                                |
| -------------------------- | ------------------------------------------------------ |
| `forEach()`                | Iterate over key–value pairs easily                    |
| `Entry.comparingByKey()`   | Sort map entries by key                                |
| `Entry.comparingByValue()` | Sort map entries by value                              |
| `getOrDefault()`           | Return default value if key not found                  |
| `computeIfAbsent()`        | Compute value only if key is missing                   |
| `computeIfPresent()`       | Compute value only if key exists                       |
| `compute()`                | Compute and replace value for any key (present or not) |
| `remove(key, value)`       | Remove entry only if key & value match                 |
| `replace()`                | Replace value if key exists                            |
| `replaceAll()`             | Replace all values using a function                    |

---

## Coding Example: 

### Creating and Printing the Map Using forEach()
```java
Map<String, String> map = new HashMap<>();
map.put("India", "Delhi");
map.put("USA", "Washington");
map.put("Japan", "Tokyo");
map.put("China", "Beijing");
map.put("Germany", "Berlin");
map.put("England", "London");

map.forEach((country, capital) -> System.out.println("The capital of " + country + " is: " + capital));
```

**Explanation:**
- `forEach()` is a Java 8 default method on `Map`.
- It accepts a lambda that receives `(key, value)`.
- Makes iteration cleaner than using an iterator or entrySet loop.

**Output:** 
```java
The capital of USA is: Washington
The capital of Japan is: Tokyo
The capital of China is: Beijing
The capital of England is: London
The capital of Germany is: Berlin
The capital of India is: Delhi
```

---

### Sorting Entries by Key and Value
```java
map.entrySet().stream().sorted(Entry.comparingByKey()).forEachOrdered(System.out::println);

map.entrySet().stream().sorted(Entry.comparingByValue()).forEachOrdered(System.out::println);
```

**Explanation:**
- `entrySet().stream()` converts the map to a stream of entries.
- `comparingByKey()` sorts alphabetically by country name.
- `comparingByValue()` sorts alphabetically by capital city.
- `forEachOrdered()` preserves the sorted order when printing.

**Output:**
```java
// sorting by key 
China=Beijing
England=London
Germany=Berlin
India=Delhi
Japan=Tokyo
USA=Washington
// sorting by value 
China=Beijing
Germany=Berlin
India=Delhi
England=London
Japan=Tokyo
USA=Washington
```

---

### Using getOrDefault()
```java
System.out.println(map.getOrDefault("Russia", "No Data present"));
```

**Explanation:**
- If `"Russia"` is missing, Java prints `"No Data present"` instead of `null`.
- Avoids extra null checks.

**Output:**
```java
No Data present
```

---

### Adding Values Conditionally with computeIfAbsent()
```java
map.computeIfAbsent("Spain", name -> "Madrid");
```

**Explanation:**
- If `"Spain"` is **not** in the map, compute `"Madrid"` and insert it.
- If `"Spain"` already exists, nothing happens.

---

### Updating Existing Keys with computeIfPresent()
```java
map.computeIfPresent("USA", (k, v) -> "Washington DC");
```

**Explanation:**
- Runs only if `"USA"` exists.
- Replaces the value `"Washington"` → `"Washington DC"`.

---

### Computing/Replacing Any Key Using compute()
```java
map.compute("India", (key, val) -> "New " + val);
```

**Explanation:**
- Always runs, whether key exists or not.
- Prefixes `"New "` to India’s capital → `"New Delhi"`.

---

### Removing an Entry Conditionally
```java
map.remove("England", "London");
```

**Explanation:**
- Removes the entry **only if key AND value match exactly.**
- Safer than `remove(key)` because it prevents accidental removal.

---

### Transforming All Values Using replaceAll()
```java
map.replaceAll((country, capital) -> capital.toUpperCase());
```

**Explanation:**
- Converts every capital city name to uppercase.
- Applies the lambda to every entry in the map.

---

### Replacing a Single Value Using replace()
```java
map.replace("India", "Delhi");
```

**Explanation:**
- Replaces the value **only if** the key "India" exists.

---

### Final Sorted Output
```java
map.entrySet().stream().sorted(Entry.comparingByValue()).forEachOrdered(System.out::println);
```

**Explanation:**
- Final pass prints the updated map, sorted by value (capital city).

**Output:**
```java
China=BEIJING
Germany=BERLIN
India=Delhi
Spain=MADRID
Japan=TOKYO
USA=WASHINGTON DC
```

---
