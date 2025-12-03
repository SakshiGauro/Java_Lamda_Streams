# SUPPLIER FUNCTIONAL INTERFACE

Supplier interface returns a value without accepting any
input.

It is defined in:
```java
java.util.function.Supplier<T>
```

### Supplier API Overview
#### Type Parameter
- `<T>` → Output type

#### Single Abstract Method (SAM)
- `T get()`
- returns a value of type `T`

No static and chaining methods are available in Supplier functional interface. The reason is that it will not accept any input so there is no meaning of chaining in it.

---

## Coding Example: SupplierExample
```java
// Creating a Supplier
Supplier<Integer> getCurrDayOfMonth = () -> LocalDate.now().getDayOfMonth();

// invoking get method inside the Supplier
System.out.println("Today's day of the month is: "+getCurrDayOfMonth.get());

// Creating a Supplier
Supplier<String> getCurrDay = () -> LocalDate.now().getDayOfWeek().name();

// invoking get method inside the Supplier
System.out.println("Today's day is: "+getCurrDay.get());
```
1. Creating a Suppliers 
- `Supplier<Integer>` → this Supplier will give you an Integer
- `()` -> → it takes no input
- `LocalDate.now().getDayOfMonth()` → returns today’s date (1–31)
- `LocalDate.now().getDayOfWeek().name()` → returns the day name: "MONDAY", "TUESDAY", etc.

2. `.get()` method
- `.get()` Calls the Supplier
- Returns today's date number

**Output**
```java
Today's day of the month is: 3
Today's day is: WEDNESDAY
```

---
|**Concept**| 	**Consumer**	                 | **Supplier**                |
|----|--------------------------------|-----------------------------|
|Purpose| 	Takes input, performs action	 | Produces data (no input)    |
|Method	| `accept(T t)`                  | 	`get()`                    |
|Returns?| 	**Nothing (void)**            | 	A value                    |
|Inputs?| 	Yes                           | 	No                         |
|Chaining| 	Yes (`andThen`)               | 	No                         |
|Analogy	| **Setter** in POJO classes     | 	**Getter** in POJO classes |

---