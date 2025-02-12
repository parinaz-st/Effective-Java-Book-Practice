## 🔹 Why Use a Builder Instead of Constructors?

### 🚫 Avoids Telescoping Constructors
Without a builder, you'd need multiple constructors like:

```java
public NutritionFacts(int servingSize, int servings) { ... }
public NutritionFacts(int servingSize, int servings, int calories) { ... }
public NutritionFacts(int servingSize, int servings, int calories, int fat) { ... }
```

This becomes hard to manage when there are many parameters.
✅ Improves Readability
Compare:
```java
NutritionFacts facts = new NutritionFacts(240, 8, 100, 0, 35, 27);
```
It’s unclear what each number represents.

With a builder:
```java
NutritionFacts facts = new NutritionFacts.Builder(240, 8)
                                 .calories(100)
                                 .sodium(35)
                                 .carbohydrate(27)
                                 .build();
```
Allows Immutability

The NutritionFacts object is immutable because all fields are final and cannot be changed after creation.
```java
private final int servingSize;
private final int servings;
```
More Flexible than JavaBeans

JavaBeans (setters) require multiple method calls and do not guarantee an object is properly initialized before use.
The builder ensures a fully initialized object when build() is called.

🔹 How It Works

The Builder class contains all fields (optional ones have default values).
It provides chained setter-like methods (calories(), sodium(), etc.) that return this for method chaining.
The build() method creates an instance of NutritionFacts by passing this (the builder) to the private constructor.
The NutritionFacts constructor assigns values from the builder.

This pattern is widely used in frameworks like Spring Boot, Lombok (@Builder), and even Java's own StringBuilder.