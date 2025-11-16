# 🚀 **Class Objects and oops basics**

# 🧭 Table of Contents

- [🚀 **Class Objects and oops basics**](#-class-objects-and-oops-basics)
- [🧭 Table of Contents](#-table-of-contents)
- [Introduction](#introduction)
- [Classes and Objects](#classes-and-objects)
  - [What is a Class?](#what-is-a-class)
    - [Important properties:](#important-properties)
  - [What is an Object?](#what-is-an-object)
- [State, Identity, Behavior](#state-identity-behavior)
    - [✔ **State**](#-state)
    - [✔ **Identity**](#-identity)
    - [✔ **Behavior**](#-behavior)
- [Object Creation \& Memory (`new`, references)](#object-creation--memory-new-references)
  - [`new` creates objects at runtime](#new-creates-objects-at-runtime)
    - [Java memory layout (simplified):](#java-memory-layout-simplified)
    - [Example](#example)
- [Constructors](#constructors)
  - [Purpose](#purpose)
  - [Types of constructors](#types-of-constructors)
  - [Rules](#rules)
- [References, Aliasing \& Java Pass-by-Value](#references-aliasing--java-pass-by-value)
  - [Java is ALWAYS pass-by-value](#java-is-always-pass-by-value)
    - [✔ For primitives:](#-for-primitives)
    - [✔ For objects:](#-for-objects)
    - [Aliasing:](#aliasing)
- [Dot Operator (`.`) \& `this` Keyword](#dot-operator---this-keyword)
    - [Use cases of `this`:](#use-cases-of-this)
- [Primitive vs Reference Types](#primitive-vs-reference-types)
  - [Primitives:](#primitives)
  - [Reference Types:](#reference-types)
  - [Autoboxing:](#autoboxing)
    - [Pitfall:](#pitfall)
- [Methods: Parameters, Arguments \& Overloading](#methods-parameters-arguments--overloading)
  - [Key Terms](#key-terms)
- [`equals()`, `hashCode()`, Identity vs Equality](#equals-hashcode-identity-vs-equality)
  - [`==`](#)
  - [`equals()`](#equals)
  - [`hashCode()`](#hashcode)
- [`toString()`](#tostring)
- [Copying (Shallow, Deep, Cloneable)](#copying-shallow-deep-cloneable)
    - [Shallow Copy:](#shallow-copy)
    - [Deep Copy:](#deep-copy)
    - [`Cloneable` issues:](#cloneable-issues)
- [Immutability (Deep Explanation)](#immutability-deep-explanation)
- [Garbage Collection](#garbage-collection)
    - [GC roots:](#gc-roots)
- [`static`, `final`, `volatile`, `transient`](#static-final-volatile-transient)
    - [`static`](#static)
    - [`final`](#final)
    - [`volatile`](#volatile)
    - [`transient`](#transient)
- [Access Modifiers \& Encapsulation](#access-modifiers--encapsulation)
- [Inheritance, Polymorphism \& Abstraction](#inheritance-polymorphism--abstraction)
    - [Inheritance:](#inheritance)
    - [Polymorphism:](#polymorphism)
    - [Abstraction:](#abstraction)
- [Interfaces vs Abstract Classes](#interfaces-vs-abstract-classes)
    - [Use an Interface when:](#use-an-interface-when)
    - [Use an Abstract class when:](#use-an-abstract-class-when)
- [Inner Classes, Anonymous Classes, Lambdas](#inner-classes-anonymous-classes-lambdas)
- [Design Principles (SOLID, DRY, KISS)](#design-principles-solid-dry-kiss)
    - [S — Single responsibility](#s--single-responsibility)
    - [O — Open/Closed](#o--openclosed)
    - [L — Liskov substitution](#l--liskov-substitution)
    - [I — Interface segregation](#i--interface-segregation)
    - [D — Dependency inversion](#d--dependency-inversion)
- [Common Pitfalls \& Gotchas](#common-pitfalls--gotchas)
- [Code Recipes](#code-recipes)
    - [Constructor chaining:](#constructor-chaining)
    - [Correct equals:](#correct-equals)
- [🔥 **Interview Questions \& Answers (60+ Deep Explanations)**](#-interview-questions--answers-60-deep-explanations)
- [🧩 **1. What is the difference between a class and an object?**](#-1-what-is-the-difference-between-a-class-and-an-object)
    - [**Class**](#class)
    - [**Object**](#object)
    - [Key Interview Line:](#key-interview-line)
- [🧩 **2. What does the `new` keyword do? Explain step-by-step.**](#-2-what-does-the-new-keyword-do-explain-step-by-step)
    - [Key Interview Line:](#key-interview-line-1)
- [🧩 **3. Is Java pass-by-value or pass-by-reference?**](#-3-is-java-pass-by-value-or-pass-by-reference)
    - [Example:](#example-1)
    - [Example (mutating state):](#example-mutating-state)
    - [Interview Line:](#interview-line)
- [🧩 **4. Difference between `==` and `equals()`?**](#-4-difference-between--and-equals)
    - [`==`](#-1)
    - [`equals()`](#equals-1)
    - [Interview Line:](#interview-line-1)
- [🧩 **5. Explain the contract between `equals()` and `hashCode()`.**](#-5-explain-the-contract-between-equals-and-hashcode)
    - [If two objects are equal:](#if-two-objects-are-equal)
    - [If hashCodes differ:](#if-hashcodes-differ)
    - [Collections affected:](#collections-affected)
    - [Interview Line:](#interview-line-2)
- [🧩 **6. What is the difference between overloading and overriding?**](#-6-what-is-the-difference-between-overloading-and-overriding)
    - [Overloading (compile-time)](#overloading-compile-time)
    - [Overriding (runtime)](#overriding-runtime)
    - [Interview Line:](#interview-line-3)
- [🧩 **7. What is dynamic method dispatch?**](#-7-what-is-dynamic-method-dispatch)
    - [Interview Line:](#interview-line-4)
- [🧩 **8. What is constructor chaining?**](#-8-what-is-constructor-chaining)
    - [Rules:](#rules-1)
    - [Interview Line:](#interview-line-5)
- [🧩 **9. Why can’t constructors be inherited?**](#-9-why-cant-constructors-be-inherited)
    - [Interview Line:](#interview-line-6)
- [🧩 **10. Why does Java not support multiple inheritance?**](#-10-why-does-java-not-support-multiple-inheritance)
    - [Interview Line:](#interview-line-7)
- [🧩 **11. What is an abstract class vs interface?**](#-11-what-is-an-abstract-class-vs-interface)
    - [Abstract class:](#abstract-class)
    - [Interface:](#interface)
    - [Interview Line:](#interview-line-8)
- [🧩 **12. What is encapsulation?**](#-12-what-is-encapsulation)
    - [Interview Line:](#interview-line-9)
- [🧩 **13. What is the Liskov Substitution Principle?**](#-13-what-is-the-liskov-substitution-principle)
    - [Interview Line:](#interview-line-10)
- [🧩 **14. What is the purpose of `super` keyword?**](#-14-what-is-the-purpose-of-super-keyword)
    - [Interview Line:](#interview-line-11)
- [🧩 **15. Why is `String` immutable?**](#-15-why-is-string-immutable)
    - [Interview Line:](#interview-line-12)
- [🧩 **16. What is the String Pool?**](#-16-what-is-the-string-pool)
    - [Interview Line:](#interview-line-13)
- [🧩 **17. What is a package?**](#-17-what-is-a-package)
- [🧩 **18. What is coupling and cohesion?**](#-18-what-is-coupling-and-cohesion)
    - [Coupling](#coupling)
    - [Cohesion](#cohesion)
- [🧩 **19. What is immutability? How do you implement it?**](#-19-what-is-immutability-how-do-you-implement-it)
- [🧩 **20. What is a static block?**](#-20-what-is-a-static-block)
- [🧩 **21. What is a static nested class?**](#-21-what-is-a-static-nested-class)
- [🧩 **22. What is an inner class?**](#-22-what-is-an-inner-class)
- [🧩 **23. What are anonymous classes?**](#-23-what-are-anonymous-classes)
- [🧩 **24. What is a lambda expression?**](#-24-what-is-a-lambda-expression)
- [🧩 **25. What is a functional interface?**](#-25-what-is-a-functional-interface)
- [🧩 **26. What is method hiding?**](#-26-what-is-method-hiding)
- [🧩 **27. What is method shadowing?**](#-27-what-is-method-shadowing)
- [🧩 **28. What is the difference between composition and inheritance?**](#-28-what-is-the-difference-between-composition-and-inheritance)
    - [Composition:](#composition)
    - [Inheritance:](#inheritance-1)
- [🧩 **29. Explain polymorphism with an example.**](#-29-explain-polymorphism-with-an-example)
- [🧩 **30. What is an interface default method?**](#-30-what-is-an-interface-default-method)
- [🧩 **31. What is `Object` class? Why is it important?**](#-31-what-is-object-class-why-is-it-important)
- [🧩 **32. What is final keyword used for?**](#-32-what-is-final-keyword-used-for)
- [🧩 **33. What is covariance and contravariance?**](#-33-what-is-covariance-and-contravariance)
    - [Covariant return types:](#covariant-return-types)
- [🧩 **34. What is an enum in Java?**](#-34-what-is-an-enum-in-java)
- [🧩 **35. Why is multiple inheritance of classes not allowed?**](#-35-why-is-multiple-inheritance-of-classes-not-allowed)
- [🧩 **36. What is the diamond problem?**](#-36-what-is-the-diamond-problem)
- [🧩 **37. What is serialization?**](#-37-what-is-serialization)
- [🧩 **38. Difference between shallow and deep cloning?**](#-38-difference-between-shallow-and-deep-cloning)
- [🧩 **39. What are marker interfaces?**](#-39-what-are-marker-interfaces)
- [🧩 **40. What is Garbage Collection (GC)?**](#-40-what-is-garbage-collection-gc)
- [🧩 **41. What is finalize() method?**](#-41-what-is-finalize-method)
- [🧩 **42. What is the difference between fail-fast and fail-safe?**](#-42-what-is-the-difference-between-fail-fast-and-fail-safe)
- [🧩 **43. Explain the Java Memory Model (JMM).**](#-43-explain-the-java-memory-model-jmm)
- [🧩 **44. What is volatile?**](#-44-what-is-volatile)
- [🧩 **45. What is the difference between synchronized and volatile?**](#-45-what-is-the-difference-between-synchronized-and-volatile)
- [🧩 **46. What is a race condition?**](#-46-what-is-a-race-condition)
- [🧩 **47. What is a deadlock?**](#-47-what-is-a-deadlock)
- [🧩 **48. What is composition over inheritance?**](#-48-what-is-composition-over-inheritance)
- [🧩 **49. What is a POJO and a JavaBean?**](#-49-what-is-a-pojo-and-a-javabean)
- [🧩 **50. What is a singleton class?**](#-50-what-is-a-singleton-class)
- [🧩 **51. What is dependency injection?**](#-51-what-is-dependency-injection)
- [🧩 **52. What is tight coupling?**](#-52-what-is-tight-coupling)
- [🧩 **53. What is loose coupling?**](#-53-what-is-loose-coupling)
- [🧩 **54. What is the difference between composition and aggregation?**](#-54-what-is-the-difference-between-composition-and-aggregation)
    - [Composition:](#composition-1)
    - [Aggregation:](#aggregation)
- [🧩 **55. Explain method overriding rules.**](#-55-explain-method-overriding-rules)
- [🧩 **56. Explain the concept of upcasting and downcasting.**](#-56-explain-the-concept-of-upcasting-and-downcasting)
    - [Upcasting:](#upcasting)
    - [Downcasting:](#downcasting)
- [🧩 **57. Why should you minimize mutable state?**](#-57-why-should-you-minimize-mutable-state)
- [🧩 **58. What is an immutable object? Give real examples.**](#-58-what-is-an-immutable-object-give-real-examples)
- [🧩 **59. What is the difference between `this` and `super`?**](#-59-what-is-the-difference-between-this-and-super)
- [🧩 **60. What is a factory method?**](#-60-what-is-a-factory-method)
- [🧩 **61. Why are arrays covariant but generics are invariant?**](#-61-why-are-arrays-covariant-but-generics-are-invariant)
- [🧩 **62. What is the difference between early binding and late binding?**](#-62-what-is-the-difference-between-early-binding-and-late-binding)
- [🧩 **63. What is the difference between class loading and object creation?**](#-63-what-is-the-difference-between-class-loading-and-object-creation)
- [🧩 **64. What is an adapter pattern?**](#-64-what-is-an-adapter-pattern)
- [🧩 **65. What is the purpose of the Builder Pattern?**](#-65-what-is-the-purpose-of-the-builder-pattern)
- [🧩 **66. What is cloning? Why is it tricky?**](#-66-what-is-cloning-why-is-it-tricky)
- [🧩 **67. What is method reference?**](#-67-what-is-method-reference)
- [🧩 **68. Explain polymorphism using real-world examples.**](#-68-explain-polymorphism-using-real-world-examples)
- [🧩 **69. Explain dependency inversion principle (DIP).**](#-69-explain-dependency-inversion-principle-dip)
- [🧩 **70. Explain interface segregation principle (ISP).**](#-70-explain-interface-segregation-principle-isp)
- [🧩 **71. Explain DRY principle.**](#-71-explain-dry-principle)
- [🧩 **72. Explain KISS principle.**](#-72-explain-kiss-principle)
- [🧩 **73. What is the role of access modifiers in design?**](#-73-what-is-the-role-of-access-modifiers-in-design)
- [🧩 **74. What is polymorphic behavior in Collections API?**](#-74-what-is-polymorphic-behavior-in-collections-api)
- [🧩 **75. Why should mutable objects not be keys in HashMap?**](#-75-why-should-mutable-objects-not-be-keys-in-hashmap)
- [🧩 **76. Explain “open for extension, closed for modification.”**](#-76-explain-open-for-extension-closed-for-modification)
- [🧩 **77. Why is composition preferred over inheritance?**](#-77-why-is-composition-preferred-over-inheritance)
- [🧩 **78. Why should subclass not violate invariants of superclass?**](#-78-why-should-subclass-not-violate-invariants-of-superclass)
- [🧩 **79. What is the role of equals and compareTo?**](#-79-what-is-the-role-of-equals-and-compareto)
- [🧩 **80. What is the difference between clone() and copying constructor?**](#-80-what-is-the-difference-between-clone-and-copying-constructor)
- [✔ **END OF INTERVIEW SECTION**](#-end-of-interview-section)

---

# Introduction

Java is primarily an **object-oriented programming language** where:

* Classes define a **new data type**
* Objects are **runtime entities**
* Memory is **managed automatically**
* References, not objects themselves, are passed around
* Behavior and state are encapsulated

This document covers OOP concepts deeply and precisely, suitable for:

* Technical interviews
* Exams
* Revision
* Understanding language internals

---

# Classes and Objects

## What is a Class?

A **class** is a template that describes:

1. **Fields** (data/state)
2. **Methods** (behavior)
3. **Constructors**
4. **Nested types**
5. **Access modifiers**
6. **Static and instance initialization blocks**

### Important properties:

* Exists **in bytecode** after compilation.
* **Does not occupy memory** per instance — only objects do.
* Has metadata stored in the **Method Area** or **Metaspace** (JVM dependent).

---

## What is an Object?

An object is:

* A **runtime instance** of a class
* Holds **its own copy** of instance fields
* Occupies memory in the **heap**
* Has identity, state, behavior

---

# State, Identity, Behavior

### ✔ **State**

Values stored inside fields.
Example:

```java
class Car {
  String color;
  int speed;
}
```

### ✔ **Identity**

Each object has its **own identity** (reference value).

```
Car c1 = new Car();   // identity: ref value e.g. 0xA12F31
Car c2 = new Car();   // different identity: 0xB9911A
```

### ✔ **Behavior**

Defined by methods:

```java
void accelerate() { speed += 10; }
```

---

# Object Creation & Memory (`new`, references)

## `new` creates objects at runtime

`new` performs these steps:

1. Allocates memory in heap
2. Assigns default values (0, null, false)
3. Calls the constructor
4. Returns a **reference**

### Java memory layout (simplified):

```
+----------------+
|  Stack         | → stores reference variables
+----------------+
|  Heap          | → stores objects
+----------------+
|  Method Area   | → class metadata
+----------------+
```

### Example

```java
Box b;        // reference only, null by default if field
b = new Box(); // actual object created
```

---

# Constructors

## Purpose

* Initialize object state
* Execute logic during creation
* Ensure valid state

## Types of constructors

* Default constructor (only if no constructor exists)
* Parametrized constructors
* Copy constructors
* Private constructors (Singleton)

## Rules

* Must match class name
* Cannot have return type
* Can overload

---

# References, Aliasing & Java Pass-by-Value

## Java is ALWAYS pass-by-value

Even for objects.

### ✔ For primitives:

Value is copied.

### ✔ For objects:

The **reference** is copied.

```
Original object on heap unchanged
Parameter just receives a COPY of the reference
```

### Aliasing:

```java
Box b1 = new Box();
Box b2 = b1;  // both refer to same object
```

Changing through b2 affects b1.

---

# Dot Operator (`.`) & `this` Keyword

* Used to access members: `obj.field`, `obj.method()`
* `this` refers to the current object instance

### Use cases of `this`:

* Disambiguate field names
* Pass current object
* Invoke constructor chaining (`this(...)`)

---

# Primitive vs Reference Types

## Primitives:

Stored directly, fast, not objects.

| Type    | Size          |
| ------- | ------------- |
| int     | 4B            |
| double  | 8B            |
| boolean | JVM dependent |
| char    | 2B            |

## Reference Types:

Store an address to heap object.

## Autoboxing:

Java converts primitives ↔ wrappers automatically.

### Pitfall:

```java
Integer a = 128;
Integer b = 128;
a == b → false  // outside Integer cache range
```

---

# Methods: Parameters, Arguments & Overloading

## Key Terms

* **Parameter** → variable in method definition
* **Argument** → actual value passed

```java
int square(int x) // x is parameter
square(10)        // 10 is argument
```

---

# `equals()`, `hashCode()`, Identity vs Equality

## `==`

* Reference comparison

## `equals()`

* Logical comparison
* Must override to compare real content

## `hashCode()`

* Equal objects MUST have equal hashcodes

---

# `toString()`

Override to provide readable representation.

---

# Copying (Shallow, Deep, Cloneable)

### Shallow Copy:

Copies references, not objects.

### Deep Copy:

Clones everything recursively.

### `Cloneable` issues:

* Poor design
* Should avoid
* Better alternatives: copy constructors

---

# Immutability (Deep Explanation)

Immutable objects:

* Cannot change state
* Safe for multithreading
* Used in many APIs (String, wrapper classes)

To create immutable classes:

1. Make class final
2. Make fields private + final
3. Defensive copies

---

# Garbage Collection

GC frees unreachable objects.

### GC roots:

* Local variables
* Static fields
* Active threads

---

# `static`, `final`, `volatile`, `transient`

### `static`

* Belongs to class
* Shared across all objects

### `final`

* Variable: cannot reassign
* Method: cannot override
* Class: cannot extend

### `volatile`

* Ensures visibility across threads

### `transient`

* Skips field in serialization

---

# Access Modifiers & Encapsulation

| Modifier  | Scope              |
| --------- | ------------------ |
| private   | class only         |
| default   | package            |
| protected | package + subclass |
| public    | everywhere         |

Encapsulation = hide data + expose behavior.

---

# Inheritance, Polymorphism & Abstraction

### Inheritance:

Reuse parent class functionality.

### Polymorphism:

Method behavior depends on actual object type.

### Abstraction:

Hiding implementation details.

---

# Interfaces vs Abstract Classes

### Use an Interface when:

* You need multiple inheritance
* Only need method signatures

### Use an Abstract class when:

* Need constructors
* Need shared state

---

# Inner Classes, Anonymous Classes, Lambdas

* Inner classes access outer class
* Anonymous classes created inline
* Lambdas implement functional interfaces

---

# Design Principles (SOLID, DRY, KISS)

### S — Single responsibility

### O — Open/Closed

### L — Liskov substitution

### I — Interface segregation

### D — Dependency inversion

---

# Common Pitfalls & Gotchas

* Using `==` for string comparison
* Forgetting to override `hashCode()`
* Mutable static fields
* Returning internal mutable objects
* Autoboxing hazards

---

# Code Recipes

### Constructor chaining:

```java
this(x, y)
```

### Correct equals:

```java
@Override
public boolean equals(Object o) {...}
```
---

# 🔥 **Interview Questions & Answers (60+ Deep Explanations)**

> These answers are intentionally long, detailed, and “interview-perfect.”
> Suitable for FAANG/MAANG, top product companies, and high-level Java interviews.

---

# 🧩 **1. What is the difference between a class and an object?**

### **Class**

* A blueprint/template
* Exists in **metaspace/method area**
* No memory allocated per instance
* Defines:

  * Fields
  * Methods
  * Constructors
  * Nested classes

### **Object**

* Runtime entity
* Stored in **heap**
* Has:

  * Identity (reference)
  * State (field values)
  * Behavior (invoked methods)

### Key Interview Line:

> *A class is a logical construct; an object is a physical entity with memory.*

---

# 🧩 **2. What does the `new` keyword do? Explain step-by-step.**

`new` performs:

1. **Allocates memory** in heap
2. **Initializes all fields** with default values
3. **Executes instance initializers**
4. **Executes constructor**
5. **Returns a reference** (pointer-like)
6. **Assigns to a variable** (reference variable holds the pointer)

### Key Interview Line:

> *`new` always allocates at runtime. Reference is stored in stack; object is in heap.*

---

# 🧩 **3. Is Java pass-by-value or pass-by-reference?**

**Java is 100% pass-by-value.**

But for objects, the value that is passed is **the reference value**.

### Example:

```java
void change(Box b) { b = new Box(); } 
```

Caller’s reference doesn’t change → only the copy changes.

### Example (mutating state):

```java
void mutate(Box b) { b.size = 10; }
```

State is changed → both references point to SAME object.

### Interview Line:

> *Object parameters are pass-by-value, but the value is a reference, leading to pass-by-reference-like behavior.*

---

# 🧩 **4. Difference between `==` and `equals()`?**

### `==`

* For primitives → compares **values**
* For objects → compares **references** (identity)

### `equals()`

* Logical equality
* Must be overridden
* Default in `Object` behaves like `==`

### Interview Line:

> *Use `==` for identity, `equals()` for semantic equality.*

---

# 🧩 **5. Explain the contract between `equals()` and `hashCode()`.**

### If two objects are equal:

`equals(a, b) == true`
→ `a.hashCode() == b.hashCode()`

### If hashCodes differ:

→ objects are GUARANTEED not equal.

### Collections affected:

* HashMap
* HashSet
* Hashtable
* LinkedHashMap

### Interview Line:

> *Violating this contract breaks hashing structures — objects become “lost.”*

---

# 🧩 **6. What is the difference between overloading and overriding?**

### Overloading (compile-time)

* Same name
* Different parameters
* Resolved by compiler
* No inheritance needed

### Overriding (runtime)

* Same signature
* Inheritance required
* Dynamic dispatch

### Interview Line:

> *Overloading is static polymorphism; overriding is dynamic polymorphism.*

---

# 🧩 **7. What is dynamic method dispatch?**

* The **actual object type**, NOT reference type, decides which method runs at runtime.

Example:

```java
Animal a = new Dog();
a.sound(); // Dog's overridden method runs
```

### Interview Line:

> *Dynamic dispatch enables runtime polymorphism.*

---

# 🧩 **8. What is constructor chaining?**

Calling one constructor from another using:

* `this(...)` within the same class
* `super(...)` in subclass

### Rules:

* Must be first statement
* Constructor chain always ends at `Object()`

### Interview Line:

> *Constructor chaining ensures consistent initialization.*

---

# 🧩 **9. Why can’t constructors be inherited?**

Because:

* Their names must match the class name
* Superclass and subclass have different names
* Semantically makes no sense

### Interview Line:

> *Constructors belong to classes, not objects; inheritance applies to objects.*

---

# 🧩 **10. Why does Java not support multiple inheritance?**

To avoid:

* Ambiguity (Diamond problem)
* Method resolution conflicts

Instead:

* Java uses **interfaces** for multiple type inheritance
* Java 8+ uses **default methods** to handle behavior inheritance

### Interview Line:

> *Java avoids complexity by allowing multiple inheritance of type, not behavior.*

---

# 🧩 **11. What is an abstract class vs interface?**

### Abstract class:

* Can have state (fields)
* Can have concrete and abstract methods
* Can have constructors
* Single inheritance only

### Interface:

* No instance variables
* Public abstract methods (before Java 8)
* Default + static methods allowed (after Java 8)
* Multiple inheritance allowed

### Interview Line:

> *Use abstract classes for shared state; interfaces for capabilities.*

---

# 🧩 **12. What is encapsulation?**

Encapsulation = data hiding + exposing behavior.

How?

* Private fields
* Public getters/setters
* Validation inside setters

### Interview Line:

> *Encapsulation protects internal invariants of the object.*

---

# 🧩 **13. What is the Liskov Substitution Principle?**

A child class must be completely substitutable for its parent without altering program correctness.

Example of violation:

* Rectangle → Square relationship
* Changing width changes height unexpectedly

### Interview Line:

> *Subclass should never break the parent’s expected behavior.*

---

# 🧩 **14. What is the purpose of `super` keyword?**

Used to:

* Call parent constructor
* Access parent’s fields
* Access parent method

### Interview Line:

> *`super` gives direct access to superclass behavior.*

---

# 🧩 **15. Why is `String` immutable?**

Benefits:

* Security (classloaders, file paths)
* Thread-safety
* Hashcode caching
* Cannot modify data inside string pool

### Interview Line:

> *String immutability is one of Java’s most important design choices.*

---

# 🧩 **16. What is the String Pool?**

A pool of **interned** String objects in heap/metaspace.
If two strings have the same value, they can share the same reference.

Example:

```java
String s1 = "hello";
String s2 = "hello";
s1 == s2 // true (same pool instance)
```

### Interview Line:

> *The string pool reduces memory usage and speeds up comparison.*

---

# 🧩 **17. What is a package?**

A namespace to organize classes and avoid naming collisions.

---

# 🧩 **18. What is coupling and cohesion?**

### Coupling

* Degree of interdependence
* Low coupling = good design

### Cohesion

* Degree to which elements belong together
* High cohesion = better modules

---

# 🧩 **19. What is immutability? How do you implement it?**

Make class:

* final
* fields: private final
* no setters
* deep copies in constructor
* deep copies when returning objects

---

# 🧩 **20. What is a static block?**

Executes when class loads.

Used to:

* Initialize static fields
* Configure class-level resources

---

# 🧩 **21. What is a static nested class?**

A static class inside another class.
Doesn’t require outer class instance.

---

# 🧩 **22. What is an inner class?**

Has access to outer instance.
Good for logically grouped entities.

---

# 🧩 **23. What are anonymous classes?**

Used for one-time implementations.
Example:

```java
Runnable r = new Runnable() {
  public void run() {}
};
```

---

# 🧩 **24. What is a lambda expression?**

Functional-style anonymous function.
Requires a functional interface.

---

# 🧩 **25. What is a functional interface?**

Interface with exactly one abstract method.
Example:

```java
@FunctionalInterface
interface Calculator {
  int calc(int a, int b);
}
```

---

# 🧩 **26. What is method hiding?**

Static methods are **hidden**, not overridden.

---

# 🧩 **27. What is method shadowing?**

Field hiding in subclass.

---

# 🧩 **28. What is the difference between composition and inheritance?**

### Composition:

"Has-a"
More flexible, preferred for reuse.

### Inheritance:

"Is-a"
Tightly coupled, fragile hierarchies.

---

# 🧩 **29. Explain polymorphism with an example.**

```java
Animal a = new Dog();
a.sound(); // Dog’s sound
```

---

# 🧩 **30. What is an interface default method?**

Java 8 introduced default methods to let interfaces evolve without breaking old code.

---

# 🧩 **31. What is `Object` class? Why is it important?**

Root of all classes.

Provides:

* `equals()`
* `hashCode()`
* `toString()`
* `clone()`
* `wait()`, `notify()`, `notifyAll()`

---

# 🧩 **32. What is final keyword used for?**

* Final variable → cannot reassign
* Final method → cannot override
* Final class → cannot extend

---

# 🧩 **33. What is covariance and contravariance?**

### Covariant return types:

Subclass can override method with narrower return type.

Example:

```java
Animal foo() { ... }
@Override
Dog foo() { ... }
```

---

# 🧩 **34. What is an enum in Java?**

A special class for constants.

---

# 🧩 **35. Why is multiple inheritance of classes not allowed?**

To avoid ambiguity in:

* Method resolution
* Diamond problem

---

# 🧩 **36. What is the diamond problem?**

Ambiguity when two parent classes define same method.

---

# 🧩 **37. What is serialization?**

Converting object → byte stream.

---

# 🧩 **38. Difference between shallow and deep cloning?**

Already explained earlier.

---

# 🧩 **39. What are marker interfaces?**

Interfaces without methods.
Examples:

* Serializable
* Cloneable

---

# 🧩 **40. What is Garbage Collection (GC)?**

Automatic memory management.

GC is triggered when:

* Memory is needed
* Minor or major GC cycles

---

# 🧩 **41. What is finalize() method?**

Deprecated.
Unreliable cleanup.

---

# 🧩 **42. What is the difference between fail-fast and fail-safe?**

Fail-fast iterators throw ConcurrentModificationException.
Fail-safe iterators operate on copy.

---

# 🧩 **43. Explain the Java Memory Model (JMM).**

Defines:

* Happens-before relationships
* Visibility rules
* Reordering constraints

---

# 🧩 **44. What is volatile?**

Guarantees visibility, prevents caching.
Does not guarantee atomicity.

---

# 🧩 **45. What is the difference between synchronized and volatile?**

| Feature    | synchronized      | volatile                   |
| ---------- | ----------------- | -------------------------- |
| Atomicity  | Yes               | No                         |
| Visibility | Yes               | Yes                        |
| Locks      | Yes               | No                         |
| Usage      | Critical sections | Single variable visibility |

---

# 🧩 **46. What is a race condition?**

Two threads accessing shared variable unpredictably.

---

# 🧩 **47. What is a deadlock?**

Threads wait forever for each other’s locks.

---

# 🧩 **48. What is composition over inheritance?**

Prefer composition because:

* More flexible
* No tight coupling
* Easier to test

---

# 🧩 **49. What is a POJO and a JavaBean?**

POJO: Plain Old Java Object
JavaBean: POJO + getter/setter + default constructor + serializable

---

# 🧩 **50. What is a singleton class?**

One instance per application.

Example:

```java
class Singleton {
  private static final Singleton INSTANCE = new Singleton();
  private Singleton() {}
  public static Singleton getInstance() { return INSTANCE; }
}
```

---

# 🧩 **51. What is dependency injection?**

Injecting dependencies instead of creating them inside class.

---

# 🧩 **52. What is tight coupling?**

A depends heavily on B → changes in B break A.

---

# 🧩 **53. What is loose coupling?**

Dependency via interfaces, not concrete classes.

---

# 🧩 **54. What is the difference between composition and aggregation?**

### Composition:

Strong ownership
Child cannot exist without parent

### Aggregation:

Weak ownership
Child can exist independently

---

# 🧩 **55. Explain method overriding rules.**

* Same signature
* Return type covariant
* Cannot reduce visibility
* Must not throw broader checked exceptions

---

# 🧩 **56. Explain the concept of upcasting and downcasting.**

### Upcasting:

Child → Parent
Safe

```java
Animal a = new Dog();
```

### Downcasting:

Parent → Child
Risky
Use `instanceof`

---

# 🧩 **57. Why should you minimize mutable state?**

* Hard to reason
* Prone to bugs
* Not thread-safe
* Breaks encapsulation

---

# 🧩 **58. What is an immutable object? Give real examples.**

Examples:

* String
* Integer
* LocalDate

Safe in:

* Maps
* Multithreading

---

# 🧩 **59. What is the difference between `this` and `super`?**

`this` → current object
`super` → immediate parent

---

# 🧩 **60. What is a factory method?**

Static method returning objects, often used instead of constructors.

Example:

```java
LocalDate.now();
List.of(...);
```

---

# 🧩 **61. Why are arrays covariant but generics are invariant?**

Arrays allow:

```java
Object[] arr = new String[10];
```

But generics do not:

```
List<Object> ≠ List<String>
```

To avoid runtime type errors.

---

# 🧩 **62. What is the difference between early binding and late binding?**

Early binding → compile time (static methods, overloading)
Late binding → runtime (overriding)

---

# 🧩 **63. What is the difference between class loading and object creation?**

Class loading happens once per class.
Object creation happens per instance.

---

# 🧩 **64. What is an adapter pattern?**

Wrapper that converts interface of one class into another.

---

# 🧩 **65. What is the purpose of the Builder Pattern?**

Simplifies complex object creation, avoids telescoping constructors.

---

# 🧩 **66. What is cloning? Why is it tricky?**

Cloning is duplicating objects.
Problematic because:

* Default is shallow
* Requires manual deep copy
* `Cloneable` contract is broken

---

# 🧩 **67. What is method reference?**

Lambda shorthand:

```java
System.out::println
```

---

# 🧩 **68. Explain polymorphism using real-world examples.**

Example: Shape
Circle, Square, Rectangle all override `draw()`

At runtime:

```java
Shape s = new Circle();
s.draw(); // Circle's draw
```

---

# 🧩 **69. Explain dependency inversion principle (DIP).**

High-level modules must not depend on low-level modules; both depend on abstractions.

---

# 🧩 **70. Explain interface segregation principle (ISP).**

Make small, specific interfaces — not “god interfaces”.

---

# 🧩 **71. Explain DRY principle.**

Do not repeat code — use methods, abstraction, composition.

---

# 🧩 **72. Explain KISS principle.**

Keep It Simple, Stupid → avoid over-engineering.

---

# 🧩 **73. What is the role of access modifiers in design?**

They enforce encapsulation and information hiding.

---

# 🧩 **74. What is polymorphic behavior in Collections API?**

List can refer to:

* ArrayList
* LinkedList
* Vector

---

# 🧩 **75. Why should mutable objects not be keys in HashMap?**

Because hashCode can change → break lookup, object becomes lost.

---

# 🧩 **76. Explain “open for extension, closed for modification.”**

Add new behavior via inheritance or composition without editing existing code.

---

# 🧩 **77. Why is composition preferred over inheritance?**

* Less coupling
* More flexibility
* Can change behavior at runtime
* Avoids fragile base-class problem

---

# 🧩 **78. Why should subclass not violate invariants of superclass?**

It breaks software correctness (Liskov violation).

---

# 🧩 **79. What is the role of equals and compareTo?**

`equals()` → logical equality
`compareTo()` → ordering for sorting

---

# 🧩 **80. What is the difference between clone() and copying constructor?**

Copy constructor → safer, explicit, type-safe
clone() → messy, shallow by default

---

# ✔ **END OF INTERVIEW SECTION**

---
