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
- [🔨 **Constructors (Fully Explained)**](#-constructors-fully-explained)
- [✨ **What is a Constructor?**](#-what-is-a-constructor)
- [🎯 **Why Constructors Exist (Purpose)**](#-why-constructors-exist-purpose)
- [🧱 **Types of Constructors**](#-types-of-constructors)
  - [1️⃣ **Default Constructor**](#1️⃣-default-constructor)
    - [Key Points:](#key-points)
  - [2️⃣ **No-Argument Constructor (Explicit)**](#2️⃣-no-argument-constructor-explicit)
  - [3️⃣ **Parameterized Constructors**](#3️⃣-parameterized-constructors)
  - [4️⃣ **Copy Constructor**](#4️⃣-copy-constructor)
  - [5️⃣ **Private Constructor**](#5️⃣-private-constructor)
- [🧠 **Understanding `this` and `super` in Constructors**](#-understanding-this-and-super-in-constructors)
    - [`this(...)`](#this)
    - [Rules:](#rules)
    - [`super(...)`](#super)
    - [Rules:](#rules-1)
- [🏗️ **Constructor Overloading**](#️-constructor-overloading)
- [🔍 **Constructor Chaining (VERY IMPORTANT)**](#-constructor-chaining-very-important)
    - [Within same class:](#within-same-class)
    - [From parent class:](#from-parent-class)
- [⚠️ **Important Rules \& Gotchas**](#️-important-rules--gotchas)
    - [✔ Constructors are NOT methods](#-constructors-are-not-methods)
    - [✔ But constructors CAN be private, public, protected](#-but-constructors-can-be-private-public-protected)
    - [✔ Java does NOT allow constructor overloading based only on different return types](#-java-does-not-allow-constructor-overloading-based-only-on-different-return-types)
    - [✔ If your class has ANY constructor, default constructor disappears](#-if-your-class-has-any-constructor-default-constructor-disappears)
- [🔄 **Order of Execution During Object Creation**](#-order-of-execution-during-object-creation)
- [🧱 **Field Initialization Order**](#-field-initialization-order)
- [🔥 **What if a class has no constructors?**](#-what-if-a-class-has-no-constructors)
- [🧊 **What happens if you create an object without new?**](#-what-happens-if-you-create-an-object-without-new)
- [🏛️ **Deep Example: Class with multiple constructors**](#️-deep-example-class-with-multiple-constructors)
- [📚 **Summary (Important for Interviews)**](#-summary-important-for-interviews)
- [References, Aliasing \& Java Pass-by-Value — Detailed Explanation](#references-aliasing--java-pass-by-value--detailed-explanation)
  - [Short answer (TL;DR)](#short-answer-tldr)
  - [Why the phrasing matters: "pass-by-value of a reference"](#why-the-phrasing-matters-pass-by-value-of-a-reference)
  - [Memory diagram (simple)](#memory-diagram-simple)
  - [Examples and explanations](#examples-and-explanations)
    - [1) Mutating the object inside a method — changes are visible](#1-mutating-the-object-inside-a-method--changes-are-visible)
    - [2) Reassigning the parameter inside the method — caller unchanged](#2-reassigning-the-parameter-inside-the-method--caller-unchanged)
    - [3) Trying to swap two object references — doesn't work](#3-trying-to-swap-two-object-references--doesnt-work)
    - [4) Swapping actual contents — you *can* swap by mutating](#4-swapping-actual-contents--you-can-swap-by-mutating)
    - [5) Primitives are copied (pass-by-value) — changing parameter doesn't affect caller](#5-primitives-are-copied-pass-by-value--changing-parameter-doesnt-affect-caller)
    - [6) Arrays are objects (reference copies) — mutations visible](#6-arrays-are-objects-reference-copies--mutations-visible)
    - [7) Strings and wrappers: immutability \& autoboxing pitfalls](#7-strings-and-wrappers-immutability--autoboxing-pitfalls)
    - [8) `final` reference variables — final reference vs final object](#8-final-reference-variables--final-reference-vs-final-object)
  - [Practical consequences \& best practices](#practical-consequences--best-practices)
    - [1. Defensive copies for APIs](#1-defensive-copies-for-apis)
    - [2. Don’t try to swap references in a method](#2-dont-try-to-swap-references-in-a-method)
    - [3. Understand when changes are visible](#3-understand-when-changes-are-visible)
    - [4. Concurrency \& aliasing](#4-concurrency--aliasing)
  - [Common beginner pitfalls (summary)](#common-beginner-pitfalls-summary)
  - [Quick checklist / rules to remember](#quick-checklist--rules-to-remember)
- [🧠 **Exercises: Java References, Aliasing \& Pass-by-Value**](#-exercises-java-references-aliasing--pass-by-value)
- [🧩 **Exercise 1 — Basic Pass-By-Value for Objects**](#-exercise-1--basic-pass-by-value-for-objects)
    - [Code:](#code)
    - [❓ **What does it print?**](#-what-does-it-print)
    - [✅ **Answer: `20`**](#-answer-20)
    - [Explanation:](#explanation)
- [🧩 **Exercise 2 — Reassigning Inside Method**](#-exercise-2--reassigning-inside-method)
    - [Code:](#code-1)
    - [❓ **What does it print?**](#-what-does-it-print-1)
    - [✅ **Answer: `5`**](#-answer-5)
    - [Explanation:](#explanation-1)
- [🧩 **Exercise 3 — Swapping References (Trick Question)**](#-exercise-3--swapping-references-trick-question)
    - [Code:](#code-2)
    - [❓ **What does it print?**](#-what-does-it-print-2)
    - [✅ **Answer: `1 2`**](#-answer-1-2)
    - [Explanation:](#explanation-2)
- [🧩 **Exercise 4 — Swapping Values (Not References)**](#-exercise-4--swapping-values-not-references)
    - [Code:](#code-3)
    - [❓ **What does it print?**](#-what-does-it-print-3)
    - [✅ **Answer: `20 10`**](#-answer-20-10)
    - [Explanation:](#explanation-3)
- [🧩 **Exercise 5 — Arrays Are Objects**](#-exercise-5--arrays-are-objects)
    - [Code:](#code-4)
    - [❓ **What does it print?**](#-what-does-it-print-4)
    - [✅ **Answer: `99`**](#-answer-99)
    - [Explanation:](#explanation-4)
- [🧩 **Exercise 6 — Strings \& Immutability**](#-exercise-6--strings--immutability)
    - [Code:](#code-5)
    - [❓ **What does it print?**](#-what-does-it-print-5)
    - [✅ **Answer: `hello`**](#-answer-hello)
    - [Explanation:](#explanation-5)
- [🧩 **Exercise 7 — Autoboxing + Immutability Trap**](#-exercise-7--autoboxing--immutability-trap)
    - [Code:](#code-6)
    - [❓ **What does it print?**](#-what-does-it-print-6)
    - [✅ **Answer: `5`**](#-answer-5-1)
    - [Explanation:](#explanation-6)
- [🧩 **Exercise 8 — final Reference, Mutable Object**](#-exercise-8--final-reference-mutable-object)
    - [Code:](#code-7)
    - [❓ **What happens?**](#-what-happens)
    - [✅ **Output so far: `50`**](#-output-so-far-50)
    - [Explanation:](#explanation-7)
- [🧩 **Exercise 9 — Passing a null Reference**](#-exercise-9--passing-a-null-reference)
    - [Code:](#code-8)
    - [❓ **Output?**](#-output)
    - [❌ **Throws NullPointerException**](#-throws-nullpointerexception)
    - [Explanation:](#explanation-8)
- [🧩 **Exercise 10 — Method Returning a Modified Object**](#-exercise-10--method-returning-a-modified-object)
    - [Code:](#code-9)
    - [❓ **What does it print?**](#-what-does-it-print-7)
    - [✅ **Answer: `40 40`**](#-answer-40-40)
    - [Explanation:](#explanation-9)
- [🧩 **Exercise 11 — Defensive Copy Needed**](#-exercise-11--defensive-copy-needed)
    - [Code:](#code-10)
    - [❓ **What does it print?**](#-what-does-it-print-8)
    - [✅ **Answer: `[10, 20, 30]`**](#-answer-10-20-30)
    - [Explanation:](#explanation-10)
- [🧩 **Exercise 12 — True Pass-by-Value Visualization**](#-exercise-12--true-pass-by-value-visualization)
    - [Code:](#code-11)
    - [❓ **Output?**](#-output-1)
    - [Answer: `5`](#answer-5)
    - [Explanation:](#explanation-11)
- [🧩 **Exercise 13 — Mutating vs Reassigning Together**](#-exercise-13--mutating-vs-reassigning-together)
    - [Code:](#code-12)
    - [❓ **Output?**](#-output-2)
    - [✅ Answer: `50`](#-answer-50)
    - [Explanation:](#explanation-12)
- [🧩 **Exercise 14 — Multi-Level Aliasing**](#-exercise-14--multi-level-aliasing)
    - [Code:](#code-13)
    - [❓ **Output?**](#-output-3)
    - [Answer: `100`](#answer-100)
    - [Explanation:](#explanation-13)
- [🧩 **Exercise 15 — Changing Contents of a Passed Array of Objects**](#-exercise-15--changing-contents-of-a-passed-array-of-objects)
    - [Code:](#code-14)
    - [❓ **Output?**](#-output-4)
    - [Answer: `42`](#answer-42)
    - [Explanation:](#explanation-14)
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
    - [Rules:](#rules-2)
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

# 🔨 **Constructors (Fully Explained)**

A **constructor** in Java is a special block of code that runs **automatically** when an object is created.
Its main job is to **initialize the object**—that means setting up its initial state, allocating internal resources, or validating input.

---

# ✨ **What is a Constructor?**

A constructor is a method-like block that:

* Has **the same name as the class**
* Has **no return type** (not even `void`)
* Runs **automatically** when you call `new`
* Initializes the object’s fields or performs setup tasks

Example:

```java
class Car {
    String model;
    int year;

    Car() {                  // constructor
        model = "Unknown";
        year = 2000;
    }
}
```

When you do:

```java
Car c = new Car();
```

The constructor is executed **immediately**.

---

# 🎯 **Why Constructors Exist (Purpose)**

1. **Initialize object state**

   ```java
   Bike b = new Bike("Yamaha", 200);
   ```
2. **Ensure object is created in a valid state**

   * Example: preventing negative balance in a bank account
3. **Run code during creation**

   * Assign IDs
   * Connect to resources
   * Initialize default values
4. **Provide multiple ways to create an object**
   (overloaded constructors)

---

# 🧱 **Types of Constructors**

## 1️⃣ **Default Constructor**

A constructor **automatically provided by the compiler** *ONLY IF* you don’t write any constructor.

```java
class A {
    // compiler inserts:
    // A() {}
}
```

### Key Points:

* Exists only when you define **no constructor**
* Is **0-argument**
* Calls `super()` implicitly (parent constructor)

---

## 2️⃣ **No-Argument Constructor (Explicit)**

Even if you write your own no-arg constructor, it is *not* the compiler-provided one.

```java
class A {
    A() {
        System.out.println("My own no-arg constructor");
    }
}
```

---

## 3️⃣ **Parameterized Constructors**

Used when you want to initialize fields with specific values.

```java
class Student {
    String name;
    int roll;

    Student(String n, int r) {
        name = n;
        roll = r;
    }
}

Student s = new Student("Arnav", 42);
```

---

## 4️⃣ **Copy Constructor**

Used to create an object using another object’s data.

Java does **not** have a built-in copy constructor, the programmer writes it manually:

```java
class Point {
    int x, y;

    Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    // copy constructor
    Point(Point p) {
        this.x = p.x;
        this.y = p.y;
    }
}
```

---

## 5️⃣ **Private Constructor**

Used for:

* Singleton pattern
* Preventing object creation from outside
* Factory methods

Example:

```java
class Singleton {
    private static Singleton instance = new Singleton();

    private Singleton() {}  // private

    public static Singleton getInstance() {
        return instance;
    }
}
```

---

# 🧠 **Understanding `this` and `super` in Constructors**

### `this(...)`

Used to call *another constructor* in the same class.

```java
class Box {
    int w, h;

    Box() {
        this(10, 10);  // call another constructor
    }

    Box(int w, int h) {
        this.w = w;
        this.h = h;
    }
}
```

### Rules:

* Must be **first line** in constructor
* Only **one** `this(...)` call allowed

---

### `super(...)`

Used to call the parent class’s constructor.

```java
class Animal {
    Animal() {
        System.out.println("Animal created");
    }
}

class Dog extends Animal {
    Dog() {
        super(); // optional, inserted automatically
        System.out.println("Dog created");
    }
}
```

### Rules:

* Must be the **first line**
* If not written, Java inserts `super()` automatically
* Parent constructor *must* exist or be default

---

# 🏗️ **Constructor Overloading**

You can define multiple constructors with different parameter lists.

```java
class Time {
    int hour, minute;

    Time() {
        this(0, 0);
    }

    Time(int hour) {
        this(hour, 0);
    }

    Time(int hour, int minute) {
        this.hour = hour;
        this.minute = minute;
    }
}
```

Benefits:

* Multiple ways to create an object
* Code reuse (using `this(...)`)
* Cleaner and more flexible API

---

# 🔍 **Constructor Chaining (VERY IMPORTANT)**

### Within same class:

`this()`

### From parent class:

`super()`

Example of full chain:

```java
class A {
    A() { System.out.println("A"); }
}

class B extends A {
    B() { 
        super();  // calls A()
        System.out.println("B");
    }
}

class C extends B {
    C() {
        super();  // calls B()
        System.out.println("C");
    }
}
```

Output:

```
A
B
C
```

---

# ⚠️ **Important Rules & Gotchas**

### ✔ Constructors are NOT methods

* They don’t have return types
* They cannot return values
* They cannot be inherited
* They cannot be abstract
* They cannot be final
* They cannot be static

### ✔ But constructors CAN be private, public, protected

### ✔ Java does NOT allow constructor overloading based only on different return types

### ✔ If your class has ANY constructor, default constructor disappears

---

# 🔄 **Order of Execution During Object Creation**

When you do:

```java
Child obj = new Child();
```

Java performs:

1. Memory allocated for object
2. Parent class constructor called
3. Fields initialized (default values)
4. Instance initializers run
5. Child constructor executed

Visual flow:

```
superclass constructor
↓
instance initializers
↓
current class constructor
```

---

# 🧱 **Field Initialization Order**

Order is:

1. Static fields (once)
2. Static blocks (once)
3. Instance fields
4. Instance initializer blocks
5. Constructor

Example:

```java
class A {
    int x = 10;

    {
        System.out.println("Initializer");
    }

    A() {
        System.out.println("Constructor");
    }
}
```

Output:

```
Initializer
Constructor
```

---

# 🔥 **What if a class has no constructors?**

Java automatically provides:

```java
ClassName() { super(); }
```

Only if:

* You define **no** constructor.

---

# 🧊 **What happens if you create an object without new?**

Possible through:

* Cloning
* Deserialization
* Reflection

Example:

```java
A obj = A.class.newInstance();  // deprecated but possible
```

---

# 🏛️ **Deep Example: Class with multiple constructors**

```java
class Account {
    String name;
    double balance;

    // default constructor
    Account() {
        this("Unknown", 0.0);
    }

    // parameterized
    Account(String name) {
        this(name, 0.0);
    }

    // full constructor
    Account(String name, double balance) {
        if (balance < 0) throw new IllegalArgumentException("No negative balance");
        this.name = name;
        this.balance = balance;
    }
}
```

This demonstrates:

* Overloading
* Validation
* `this()`
* Multiple creation paths

---

# 📚 **Summary (Important for Interviews)**

1. Constructors initialize objects
2. Must have same name as class
3. Cannot have return type
4. Cannot be inherited
5. Can be private
6. Only one `this()` or `super()` allowed
7. Must be first statement
8. Default constructor added only if none exist
9. Support overloading
10. Support constructor chaining
11. Play a major role in object creation flow

---


# References, Aliasing & Java Pass-by-Value — Detailed Explanation

This section explains *exactly* what Java does when you pass things into methods, how references work, what aliasing is, and why Java is **always** pass-by-value — even for objects. I'll use clear examples, ASCII memory diagrams, and point out common beginner pitfalls so you won't miss anything.

---

## Short answer (TL;DR)

* **Java is always pass-by-value.**
* For **primitives**, the *value* (the actual primitive) is copied.
* For **objects**, the *value that is copied* is the **reference** (i.e., the pointer/address to the object).
* That means: methods receive a **copy of the reference**, not the original reference variable nor a new object.
* Because the reference copy still points to the *same object*, mutating the object inside the method affects the caller’s object. But reassigning the parameter to a new object does **not** affect the caller’s reference.

---

## Why the phrasing matters: "pass-by-value of a reference"

Confusion arises because people see that objects *can be changed* inside methods and call it “pass-by-reference.” That’s wrong terminology for Java.

* Java does **not** give you the caller’s variable itself to manipulate.
* Java gives you a **copy** of the caller’s variable. For objects that variable’s *value* is a reference (an address-like value). So you get a copy of the address. Both the original and the copy point to the same object. That’s why mutations are visible through both.

Think of it like giving someone a photocopy of a map with an "X" marking a treasure chest (the object). They can go dig up the chest (mutate object) and it affects the real chest. But if they take a pen and draw a new "X" on their photocopy (reassign the map), your map is unchanged.

---

## Memory diagram (simple)

When you write:

```java
Box b1 = new Box(); // Box object created on heap
Box b2 = b1;        // b2 references same object
```

In memory (conceptual):

```
Stack                             Heap
------                            ----------------
b1  ──┐                           │ Box object     │
      └─> (0xA12) ───────────────>│ fields...      │
b2  ──┘                           ----------------
```

When you call `method(b1)`, Java copies the value stored in `b1` (0xA12) into the parameter variable (say `p`) on that method’s stack frame:

```
Caller stack               Callee stack              Heap
-----------                -------------             ----------------
b1 -> 0xA12                p -> 0xA12               │ Box object       │
                                                   │ fields...        │
```

`p` and `b1` are two separate variables that both hold the same value `0xA12` (the reference/address). Changing the object at `0xA12` is visible via either variable. Reassigning `p` to `0xBFF` only changes `p`, not `b1`.

---

## Examples and explanations

### 1) Mutating the object inside a method — changes are visible

```java
class Box {
    int value;
    Box(int v) { value = v; }
    void setValue(int v) { value = v; }
}

void mutate(Box b) {
    b.setValue(99);    // modifies the object that b refers to
}

Box x = new Box(10);
mutate(x);
System.out.println(x.value); // prints 99
```

**Why?** `mutate` received a copy of the reference pointing at the same Box. Calling `setValue` changes the object at that memory address.

---

### 2) Reassigning the parameter inside the method — caller unchanged

```java
void reassign(Box b) {
    b = new Box(42);   // reassigns local parameter variable b
}

Box x = new Box(10);
reassign(x);
System.out.println(x.value); // prints 10 — unchanged
```

**Why?** `reassign` changed its *local copy* of the reference to point to a new Box. The caller’s `x` still points to the original object.

---

### 3) Trying to swap two object references — doesn't work

A classic exam question:

```java
void swap(Box a, Box b) {
    Box temp = a;
    a = b;
    b = temp;
}

Box x = new Box(1);
Box y = new Box(2);
swap(x, y);
// x.value is still 1, y.value is still 2
```

**Explanation:** `swap` only swaps the **local copies of the references**. The caller’s variables still reference their original objects.

---

### 4) Swapping actual contents — you *can* swap by mutating

If you want to swap the contents, mutate the objects via their setters:

```java
void swapValues(Box a, Box b) {
    int t = a.value;
    a.value = b.value;
    b.value = t;
}
```

This works because you are mutating the objects at the referenced memory locations, visible to all references.

---

### 5) Primitives are copied (pass-by-value) — changing parameter doesn't affect caller

```java
void inc(int n) { n = n + 1; }

int x = 5;
inc(x);
System.out.println(x); // prints 5
```

The value `5` was copied into the method parameter; mutating the parameter doesn't touch the caller’s `x`.

---

### 6) Arrays are objects (reference copies) — mutations visible

```java
void setFirst(int[] arr) { arr[0] = 100; }

int[] a = {1,2,3};
setFirst(a);
System.out.println(a[0]); // prints 100
```

**Why?** `arr` is a copy of the reference to the same array. Mutating the array contents affects the single underlying array.

---

### 7) Strings and wrappers: immutability & autoboxing pitfalls

Strings are immutable; reassigning a String parameter makes the local variable refer to a new String, caller unchanged:

```java
void foo(String s) { s = s + " world"; }

String x = "hello";
foo(x);
System.out.println(x); // prints "hello"
```

For wrappers:

```java
void inc(Integer i) { i = i + 1; } // autoboxing creates new Integer
Integer n = 1;
inc(n);
System.out.println(n); // prints 1
```

Because `Integer` is immutable and `i = i + 1` creates a new Integer object assigned to the local copy.

Beware `NullPointerException` when unboxing `null`:

```java
Integer n = null;
int x = n; // NPE
```

---

### 8) `final` reference variables — final reference vs final object

`final` only prevents reassigning the reference, not mutating the referred object:

```java
final Box b = new Box(5);
b.setValue(10); // OK — object mutated
b = new Box(2); // compile error — cannot reassign final variable
```

---

## Practical consequences & best practices

### 1. Defensive copies for APIs

If you accept a mutable object from a caller and want to protect your internal state, **make a defensive copy**:

```java
class Person {
    private final Date dob;
    public Person(Date dob) {
        this.dob = new Date(dob.getTime()); // defensive copy
    }
    public Date getDob() {
        return new Date(dob.getTime());     // return copy
    }
}
```

Otherwise external code could mutate the `Date` you store inside the object.

### 2. Don’t try to swap references in a method

If API requires swapping, provide a container object or return a swapped pair (or use holder/array). Example: return a `Pair<Box, Box>`.

### 3. Understand when changes are visible

* Mutations of shared objects → visible to all references.
* Reassignments of local parameters → not visible to caller.

### 4. Concurrency & aliasing

Multiple threads holding references to the same mutable object can cause race conditions. Aliasing means shared mutable state — protect it with synchronization or use immutable objects.

---

## Common beginner pitfalls (summary)

* Thinking Java is pass-by-reference because you can mutate objects in methods. (It’s not.)
* Expecting parameter reassignment to change caller’s references. (It won’t.)
* Returning or storing a passed mutable object without defensive copying. (Leads to unintended mutation.)
* Believing `final` makes the object immutable. (It only makes reference non-reassignable.)
* Using `==` to compare Strings or wrapper values. (Use `equals()`.)

---

## Quick checklist / rules to remember

* Java = **pass-by-value**. Always.
* For objects: **value copied = reference**.
* Mutating object via reference inside method → visible to caller.
* Reassigning parameter variable inside method → **not** visible to caller.
* Use defensive copying to prevent aliasing problems.
* `final` affects reassignment of the reference, not object mutability.
Here are **carefully designed exercises** that help you *truly* understand Java references, aliasing, and pass-by-value.
Each exercise includes:

* The **code snippet**
* A **question** about what it prints or what happens
* The **detailed explanation + answer**

These are perfect for revision, interviews, and debugging intuition.

---

# 🧠 **Exercises: Java References, Aliasing & Pass-by-Value**

---

# 🧩 **Exercise 1 — Basic Pass-By-Value for Objects**

### Code:

```java
class Box {
    int value;
    Box(int v) { value = v; }
}

void change(Box b) {
    b.value = 20;
}

Box x = new Box(10);
change(x);
System.out.println(x.value);
```

### ❓ **What does it print?**

### ✅ **Answer: `20`**

### Explanation:

* `change()` receives a **copy of the reference** to the same Box.
* Both `b` and `x` point to the *same* object.
* Mutating `b.value` changes the object → visible through `x`.

---

# 🧩 **Exercise 2 — Reassigning Inside Method**

### Code:

```java
class Box {
    int value;
    Box(int v) { value = v; }
}

void reassign(Box b) {
    b = new Box(999);
}

Box x = new Box(5);
reassign(x);
System.out.println(x.value);
```

### ❓ **What does it print?**

### ✅ **Answer: `5`**

### Explanation:

* `b = new Box(999)` only changes the **local copy** of the reference.
* `x` remains pointing to the original object.
* No mutation was done on the original object.

---

# 🧩 **Exercise 3 — Swapping References (Trick Question)**

### Code:

```java
class Box {
    int value;
    Box(int v) { value = v; }
}

void swap(Box a, Box b) {
    Box temp = a;
    a = b;
    b = temp;
}

Box x = new Box(1);
Box y = new Box(2);
swap(x, y);
System.out.println(x.value + " " + y.value);
```

### ❓ **What does it print?**

### ✅ **Answer: `1 2`**

### Explanation:

* Only the **local copies** of the references were swapped.
* Caller variables (`x` and `y`) remain unchanged.
* Java parameter passing prevents true swapping in this way.

---

# 🧩 **Exercise 4 — Swapping Values (Not References)**

### Code:

```java
class Box {
    int value;
}

void swapValues(Box a, Box b) {
    int temp = a.value;
    a.value = b.value;
    b.value = temp;
}

Box x = new Box();
x.value = 10;
Box y = new Box();
y.value = 20;

swapValues(x, y);
System.out.println(x.value + " " + y.value);
```

### ❓ **What does it print?**

### ✅ **Answer: `20 10`**

### Explanation:

* You aren’t swapping the references.
* You’re swapping the *data inside* the objects.
* Both parameters point to same objects as caller does → mutation visible.

---

# 🧩 **Exercise 5 — Arrays Are Objects**

### Code:

```java
void setFirst(int[] arr) {
    arr[0] = 99;
}

int[] nums = {1, 2, 3};
setFirst(nums);
System.out.println(nums[0]);
```

### ❓ **What does it print?**

### ✅ **Answer: `99`**

### Explanation:

* Arrays are objects.
* `arr` holds a **copied reference**, but still points to same array.
* Changing the element mutates the shared array.

---

# 🧩 **Exercise 6 — Strings & Immutability**

### Code:

```java
void test(String s) {
    s = s + " world";
}

String x = "hello";
test(x);
System.out.println(x);
```

### ❓ **What does it print?**

### ✅ **Answer: `hello`**

### Explanation:

* Strings are immutable.
* `s = s + " world"` creates a *new* String.
* Local reference `s` changes → caller’s reference `x` unchanged.

---

# 🧩 **Exercise 7 — Autoboxing + Immutability Trap**

### Code:

```java
void increment(Integer i) {
    i = i + 1; 
}

Integer n = 5;
increment(n);
System.out.println(n);
```

### ❓ **What does it print?**

### ✅ **Answer: `5`**

### Explanation:

* `i = i + 1` → unboxes Integer → adds 1 → re-boxes into a NEW Integer.
* Local reference `i` changes to new object.
* Caller variable `n` still references old Integer object.

---

# 🧩 **Exercise 8 — final Reference, Mutable Object**

### Code:

```java
final Box b = new Box(10);
b.value = 50;
System.out.println(b.value);

b = new Box(20); // Line X
```

### ❓ **What happens?**

### ✅ **Output so far: `50`**

But at line X: **Compilation Error**

### Explanation:

* `final` reference cannot be reassigned.
* But the object it points to *can* be modified.

---

# 🧩 **Exercise 9 — Passing a null Reference**

### Code:

```java
void foo(Integer i) {
    System.out.println(i + 5);
}

Integer x = null;
foo(x);
```

### ❓ **Output?**

### ❌ **Throws NullPointerException**

### Explanation:

* `i + 5` → unboxing → `i.intValue()`
* Calling `.intValue()` on null → NPE

---

# 🧩 **Exercise 10 — Method Returning a Modified Object**

### Code:

```java
class Box {
    int value;
    Box(int v) { value=v; }
}

Box change(Box b) {
    b.value = 40;
    return b;
}

Box x = new Box(10);
Box y = change(x);

System.out.println(x.value + " " + y.value);
```

### ❓ **What does it print?**

### ✅ **Answer: `40 40`**

### Explanation:

* `change(x)` returns the same object reference.
* Both x and y refer to the same Box.

---

# 🧩 **Exercise 11 — Defensive Copy Needed**

### Code:

```java
class Student {
    List<Integer> marks;

    Student(List<Integer> marks) {
        this.marks = marks;
    }
}

List<Integer> m = new ArrayList<>(List.of(10, 20));
Student s = new Student(m);

m.add(30);
System.out.println(s.marks);
```

### ❓ **What does it print?**

### ✅ **Answer: `[10, 20, 30]`**

### Explanation:

* `Student` stored the reference the caller gave.
* Both share the same list → mutations visible.
* To fix this: make a defensive copy.

---

# 🧩 **Exercise 12 — True Pass-by-Value Visualization**

### Code:

```java
void foo(Box p) {
    p = new Box(100); // line A
}

Box x = new Box(5);
foo(x);
System.out.println(x.value);
```

### ❓ **Output?**

### Answer: `5`

### Explanation:

* At line A, only the **local copy** of the reference is changed.
* Caller’s reference not affected.

---

# 🧩 **Exercise 13 — Mutating vs Reassigning Together**

### Code:

```java
void foo(Box b) {
    b.value = 50;
    b = new Box(999);
}

Box x = new Box(10);
foo(x);
System.out.println(x.value);
```

### ❓ **Output?**

### ✅ Answer: `50`

### Explanation:

* First line: mutate underlying object → visible.
* Second line: reassign local reference → caller unaffected.

---

# 🧩 **Exercise 14 — Multi-Level Aliasing**

### Code:

```java
Box a = new Box(1);
Box b = a;
Box c = b;

a.value = 100;
System.out.println(c.value);
```

### ❓ **Output?**

### Answer: `100`

### Explanation:

All three variables refer to the same object.

---

# 🧩 **Exercise 15 — Changing Contents of a Passed Array of Objects**

### Code:

```java
class Box { int v; Box(int x){ v=x; } }

void modify(Box[] arr) {
    arr[0].v = 42;
}

Box[] boxes = { new Box(5), new Box(10) };
modify(boxes);

System.out.println(boxes[0].v);
```

### ❓ **Output?**

### Answer: `42`

### Explanation:

You mutated the object in the array, not the array reference.

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
