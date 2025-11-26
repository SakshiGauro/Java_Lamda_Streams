# Type Inference/Diamond Operator

Before Java 7, when creating generic objects, you had to **repeat the generic type** on both sides of the assignment:

```java
Map<String, Integer> inputMap = new HashMap<String, Integer>();
```

Starting from **Java 7**, the compiler can **infer the generic type automatically**, allowing you to use the **diamond operator** (`<>`) to simplify object creation:

```java
Map<String, Integer> inputMap = new HashMap<>();
```

---

### Key Points
- Java 7 introduced **type inference** for generic class instantiation.
- The diamond operator (`<>`) helps avoid redundant type declarations.
- Cleaner, shorter, and less error-prone code.
- **Limitation (Java 7 & 8):**
  - The diamond operator **cannot** be used with **anonymous inner classes.**
- **Java 9 Fix:**
  - The restriction was removed; diamond operator can now be used with anonymous inner classes.

---

