# Other Miscellaneous Updates
Java 8 introduced several highly useful additions to Collections, Iterators, Strings, Math, Arrays, and utility classes.
Most of these improvements became possible because of **default methods** added to interfaces, allowing the JDK team to evolve APIs without breaking existing implementations.

This section summarizes the most important additions and includes code examples with explanations.

### Overview of New & Enhanced Methods
- **Collections & Iteration**
  - `List` → `replaceAll()`, `sort()`
  - `Iterator` → `forEachRemaining()`
  - `Iterable` → `forEach()`, `spliterator()`
  - `Collection` → `stream()`, `parallelStream()`, `removeIf()`
- **Comparator Enhancements**
  - `reversed()`
  - `thenComparing()`
  - `naturalOrder()`, `reverseOrder()`
  - `nullsFirst()`, `nullsLast()`
- **Arrays API**
  - `setAll()`
  - `parallelSetAll()`
  - `parallelSort()`
  - `parallelPrefix()`
- **String Utility**
  - `String.join()`
- **Math Additions**
  - `addExact()`, `subtractExact()`, `multiplyExact()`
  - `incrementExact()`, `decrementExact()`, `negateExact()`
  - `floorMod()`, `floorDiv()`, `toIntExact()`
  - Prevent overflow → throws `ArithmeticException`
- **Number Wrapper Enhancements**
  - `sum()`, `min()`, `max()` across Integer, Long, Float, etc.
- **Boolean Enhancements**
  - `logicalAnd(a,b)`
  - `logicalOr(a,b)`
  - `logicalXor(a,b)`
- **Objects Utility**
  - `Objects.isNull()`
  - `Objects.nonNull()`

---

## Coding examples: MiscellaneousExamples
### List.replaceAll()
```java
private static void listReplaceAll() {
    List<String> departmentList = new ArrayList<>();
    departmentList.add("Supply");
    departmentList.add("HR");
    departmentList.add("Sales");
    departmentList.add("Marketing");
    departmentList.add("Insurance");
    departmentList.add("Security");
    departmentList.add("Finance");
    System.out.println("Before List: " + departmentList);
    departmentList.replaceAll(element -> element.toUpperCase());
    System.out.println("List after replaceAll operation: " + departmentList);
}
```

**Explanation**
- `replaceAll()` applies a lambda to each element and replaces it in-place.
- Useful for bulk transformation (uppercase, trim, normalize, etc.).

**Output:**
```java
Before List: [Supply, HR, Sales, Marketing, Insurance, Security, Finance]
List after replaceAll operation: [SUPPLY, HR, SALES, MARKETING, INSURANCE, SECURITY, FINANCE]
```

---

### List.sort()
```java
private static void listSort() {
    List<String> departmentList = new ArrayList<>();
    departmentList.add("Supply");
    departmentList.add("HR");
    departmentList.add("Sales");
    departmentList.add("Marketing");
    departmentList.add("Insurance");
    departmentList.add("Security");
    departmentList.add("Finance");
    System.out.println("Before List: " + departmentList);
    departmentList.sort(Comparator.naturalOrder());
    System.out.println("List after sort operation: " + departmentList);
}
```

**Explanation**
- Comparator.naturalOrder() sorts strings alphabetically.
- sort() is now a default method on List.

**Output:**
```java
Before List: [Supply, HR, Sales, Marketing, Insurance, Security, Finance]
List after sort operation: [Finance, HR, Insurance, Marketing, Sales, Security, Supply]
```

---

### Iterator.forEachRemaining()
```java
private static void forEachRemaining() {
        List<String> departmentList = new ArrayList<>();
        departmentList.add("Supply");
        departmentList.add("HR");
        departmentList.add("Sales");
        departmentList.add("Marketing");
        departmentList.add("Insurance");
        departmentList.add("Security");
        departmentList.add("Finance");
        departmentList.iterator().forEachRemaining(System.out::println);
}
```

**Explanation**
- Processes the remaining elements of an iterator.
- This is a more functional alternative to a `while(iterator.hasNext())`.

**Output:**
```java
Supply
HR
Sales
Marketing
Insurance
Security
Finance
```

---

### Iterable.forEach()
```java
private static void forEach() {
  List<String> departmentList = new ArrayList<>();
  departmentList.add("Supply");
  departmentList.add("HR");
  departmentList.add("Sales");
  departmentList.add("Marketing");
  departmentList.add("Insurance");
  departmentList.add("Security");
  departmentList.add("Finance");
  departmentList.forEach(System.out::println);
}
```

**Explanation**
- A default method added to `Iterable`.
- Much cleaner than classic `for(String s : list)` loops.

**Output:**
```java
Supply
HR
Sales
Marketing
Insurance
Security
Finance
```

---

### Map Enhancements (Mini Version)
```java
private static void mapEnhancements() {
        Map<String, String> map = new HashMap<>();
        map.put("India", "Delhi");
        map.put("USA", "Washington DC");
        map.put("Japan", "Tokyo");
        map.put("China", "Beijing");
        map.put("Germany", "Berlin");
        map.put("England", "London");

        map.forEach((country, capital) -> System.out.println("The capital of " + country + " is: " + capital));

        map.entrySet().stream().sorted(Entry.comparingByKey()).forEachOrdered(System.out::println);
        map.entrySet().stream().sorted(Entry.comparingByValue()).forEachOrdered(System.out::println);
        System.out.println(map.getOrDefault("Russia", "No Data present"));
        map.computeIfAbsent("Spain", name -> "Madrid");
        map.entrySet().stream().sorted(Entry.comparingByValue()).forEachOrdered(System.out::println);
}
```

**Explanation**
- `forEach()` prints all entries.
- `comparingByKey/Value()` sorts based on key or value.
- `getOrDefault()` avoids null returns.
- `computeIfAbsent()` adds `"Spain" → "Madrid"` if missing.

**Output:**
```java
The capital of USA is: Washington DC
The capital of Japan is: Tokyo
The capital of China is: Beijing
The capital of England is: London
The capital of Germany is: Berlin
The capital of India is: Delhi
China=Beijing
England=London
Germany=Berlin
India=Delhi
Japan=Tokyo
USA=Washington DC
China=Beijing
Germany=Berlin
India=Delhi
England=London
Japan=Tokyo
USA=Washington DC
No Data present
China=Beijing
Germany=Berlin
India=Delhi
England=London
Spain=Madrid
Japan=Tokyo
USA=Washington DC
```

---

### Spliterator
```java
private static void spliterator() {
    List<String> departmentList = new ArrayList<>();
    departmentList.add("Supply");
    departmentList.add("HR");
    departmentList.add("Sales");
    departmentList.add("Marketing");
    departmentList.add("Insurance");
    departmentList.add("Security");
    departmentList.add("Finance");

    ArrayList<String> newList = new ArrayList<>();
    Spliterator<String> splitr = departmentList.spliterator();
    while (splitr.tryAdvance((value) -> newList.add(value.toUpperCase())))
      ;

    Spliterator<String> newSplitr = newList.spliterator();
    while (newSplitr.tryAdvance(System.out::println))
      ;
}
```

**Explanation**
- `Spliterator` supports parallel processing (splitting + iterating).
- `tryAdvance()` processes one element at a time.

**Output:**
```java
SUPPLY
HR
SALES
MARKETING
INSURANCE
SECURITY
FINANCE
```

---

### String.join()
```java
private static void stringJoin() {
    String departments = String.join(", ", "Supply", "HR", "Sales");
    System.out.println(departments);
}
```

**Explanation**
- Joins strings using a delimiter → `Supply, HR, Sales`.
- Cleaner than manual concatenation.

**Output:**
```java
Supply, HR, Sales
```

---

### Objects.isNull() & nonNull()
```java
private static void objectsNullCheck() {
        List<String> departmentList = new ArrayList<>();
        departmentList.add("Supply");
        departmentList.add("HR");
        departmentList.add("Sales");
        departmentList.add("Marketing");
        departmentList.add("Insurance");
        departmentList.add("Security");
        departmentList.add("Finance");
        departmentList.add(null);
        long nullCount = departmentList.stream().filter(Objects::isNull).count();
        long nonNullCount = departmentList.stream().filter(Objects::nonNull).count();
        System.out.println("Total null values in the list are: " + nullCount);
        System.out.println("Total non-null values in the list are: " + nonNullCount);
}
```

**Explanation**
- `Objects.isNull` → equivalent to `x == null`.
- `Objects.nonNull` → equivalent to `x != null`.
- Very useful inside Streams.

**Output:**
```java
Total null values in the list are: 1
Total non-null values in the list are: 7
```

---

### Boolean.logicalAnd / logicalOr / logicalXor
```java
private static void booleanMethods() {
        Boolean checkAnd = Boolean.logicalAnd(10>5, "Eazy".equals("Eazy"));
        Boolean checkOr = Boolean.logicalOr(10>5, "Eazy".equals("Eazy Bytes"));
        Boolean checkXor = Boolean.logicalXor(false,true);
        System.out.println(checkAnd);
        System.out.println(checkOr);
        System.out.println(checkXor);
}
```

**Explanation**
- Pure logical operations—no auto-unboxing issues.
- `XOR` → true only when values differ.

**Output:**
```java
true
true
true
```

---

### Number Methods (sum, max, min)
```java
private static void numberMethods(){
        int sum = Integer.sum(234, 4565);
        int max = Integer.max(234, 4565);
        int min = Integer.min(234, 4565);
        System.out.println(sum);
        System.out.println(max);
        System.out.println(min);
}
```

**Explanation**
- Utility methods on Integer, Long, Float...
- Cleaner than `Math.min()` for primitive wrappers.

**Output:**
```java
4799
4565
234 
```

---
### Math Methods (Overflow-Safe)

```java
private static void mathMethods() {
        long sum = Math.addExact(1234, 45456);
        long sub = Math.subtractExact(1234, 45456);
        long mul = Math.multiplyExact(1234, 45456);
        long inc = Math.incrementExact(45456);
        long dec = Math.decrementExact(1234);
        long neg = Math.negateExact(1234);
        int toInt = Math.toIntExact(12346576);
        int floorDiv = Math.floorDiv(45456,1234);
        int floorMod = Math.floorMod(45456,1234);
        float nextDown = Math.nextDown(12);
        System.out.println(sum);
        System.out.println(sub);
        System.out.println(mul);
        System.out.println(inc);
        System.out.println(dec);
        System.out.println(neg);
        System.out.println(toInt);
        System.out.println(floorDiv);
        System.out.println(floorMod);
        System.out.println(nextDown);
}
```

**Explanation**
- `addExact`, `subtractExact`, etc. detect **overflow** → throw `ArithmeticException`.
- `toIntExact(long)` ensures values fit in `int`.
- `floorDiv` and `floorMod` behave better than `/` and `%` for negative numbers

**Output:**
```java
46690
-44222
56092704
45457
1233
-1234
12346576
36
1032
11.999999 
```

---

### Arrays Methods
```java
private static void arrayMethods() {
        int[] array = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12,
        13, 14, 15, 16, 17, 18, 19, 20 };
        Arrays.setAll(array, ele -> {
        return array[ele] = array[ele]*2;
        });
        System.out.println(Arrays.toString(array));

        int[] unsortedArr = { 3,78, 7, 91, 20, 1, 8, 54 };
        Arrays.parallelSort(unsortedArr);
        System.out.println(Arrays.toString(unsortedArr));

        Arrays.parallelPrefix(array, (first,second)->{
        return first + second;
        });

        System.out.println(Arrays.toString(array));
}
```

**Explanation**
- `setAll()` → transforms each element (*2 in this case).
- `parallelSort()` → uses multi-threading for large arrays.
- `parallelPrefix()` → cumulative sum-like processing.

**Output:**
```java
[2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40]
[1, 3, 7, 8, 20, 54, 78, 91]
[2, 6, 12, 20, 30, 42, 56, 72, 90, 110, 132, 156, 182, 210, 240, 272, 306, 342, 380, 420]
```

---