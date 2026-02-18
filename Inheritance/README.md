## 1️⃣ Introduction to Inheritance

Inheritance is one of the four fundamental principles of **Object-Oriented Programming (OOP)**:

* Encapsulation
* Abstraction
* Polymorphism
* **Inheritance**

### 🔹 Definition

Inheritance is a mechanism in which one class **acquires the properties and behaviors** (fields and methods) of another class.

* **Superclass (Base Class)** → The class whose properties are inherited.
* **Subclass (Derived Class)** → The class that inherits.

Inheritance promotes:

* Code reuse
* Maintainability
* Logical hierarchy
* Extensibility

---

## 2️⃣ Basic Syntax of Inheritance

To inherit a class in Java, use the `extends` keyword:

```java
class SubclassName extends SuperclassName {
    // body of subclass
}
```

### ⚠️ Important Rules

* A subclass can inherit from **only one superclass**.
* Java **does NOT support multiple inheritance through classes**.
* A subclass can itself become a superclass (multilevel hierarchy allowed).
* ❌ No class can be a superclass of itself.
* A subclass inherits all members except those declared `private`.

---

## 3️⃣ Access to Superclass Members

Although a subclass includes all members of its superclass:

* It **cannot access private members** of the superclass.
* Access depends on the **access modifier**.

| Modifier  | Accessible in Subclass? |
| --------- | ----------------------- |
| private   | ❌ No                    |
| default   | ✔ Within same package   |
| protected | ✔ Yes                   |
| public    | ✔ Yes                   |

---

## 4️⃣ Superclass Reference Variable & Subclass Object

### 🔹 Key Concept

> It is the **type of reference variable**, not the object type, that determines accessible members.

```java
Superclass ref = new Subclass();
```

Example:

```java
plainbox = weightbox;
// (superclass)  (subclass)

SUPERCLASS ref = new SUBCLASS();
```

### Important Rule

Even if the object is of type `Subclass`, the reference can access **only members defined in Superclass**.

---

## 5️⃣ Using the `super` Keyword

The `super` keyword refers to the **immediate superclass**.

It has **two major uses**:

---

### 5.1 Calling Superclass Constructor

```java
BoxWeight(double w, double h, double d, double m) {
    super(w, h, d); // Calls superclass constructor
    weight = m;
}
```

### Key Points

* `super()` must be the **first statement** in subclass constructor.
* It always refers to the **immediate superclass constructor**.
* Works in multilevel inheritance.
* If not explicitly used, the **default (no-arg) constructor** of superclass is called automatically.

### Constructor Execution Order

Constructors execute in **top-down order**:

1. Superclass constructor
2. Subclass constructor

Reason:

A superclass has no knowledge of subclass. So it must complete initialization first.

---

### 5.2 Accessing Hidden Members

If subclass hides a superclass member:

```java
super.member;
```

Example:

```java
class Dog extends Animal {
    @Override
    void sound() {
        super.sound(); // Calls superclass method
        System.out.println("Dog barks");
    }
}
```

---

## 6️⃣ Constructor Chaining

Constructor chaining happens when:

* A constructor calls another constructor (same class using `this()`)
* Or calls superclass constructor using `super()`

Example:

```java
class Animal {
    Animal(String name) {
        System.out.println("Animal constructor called");
    }
}

class Dog extends Animal {
    Dog(String name) {
        super(name);
        System.out.println("Dog constructor called");
    }
}
```

### Output:

```
Animal constructor called
Dog constructor called
```

---

## 7️⃣ Clone Constructor Example with `super`

```java
class Box {
    private double width;
    private double height;
    private double depth;

    Box(Box ob) {
        width = ob.width;
        height = ob.height;
        depth = ob.depth;
    }
}

class BoxWeight extends Box {
    double weight;

    BoxWeight(BoxWeight ob) {
        super(ob);  // Calls Box(Box ob)
        weight = ob.weight;
    }
}
```

### Important Note

* `super(ob)` can pass a `BoxWeight` object.
* Since `BoxWeight` IS-A `Box`, it works.
* Superclass only accesses its own members.

---

## 8️⃣ Types of Inheritance in Java

---

### 8.1 Single Inheritance

One subclass inherits from one superclass.

```java
class Animal {
    String name;
    void eat() {
        System.out.println(name + " is eating.");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println(name + " is barking.");
    }
}
```

---

### 8.2 Multilevel Inheritance

Class derived from another derived class.

```java
class Animal { }
class Dog extends Animal { }
class Labrador extends Dog { }
```

Labrador inherits from both Dog and Animal.

---

### 8.3 Hierarchical Inheritance

Multiple subclasses inherit from one superclass.

```java
class Animal { }

class Dog extends Animal { }

class Cat extends Animal { }
```

---

### 8.4 Multiple Inheritance (Via Interfaces Only)

Java does NOT allow:

```java
class A extends B, C  ❌
```

Because of the **Diamond Problem**.

But supports multiple inheritance using interfaces:

```java
interface Animal {
    void eat();
}

interface Pet {
    void play();
}

class Dog implements Animal, Pet {
    public void eat() { }
    public void play() { }
}
```

---

## 9️⃣ Method Overriding

### Definition

When subclass provides its own implementation of a superclass method.

Rules:

* Same method name
* Same parameters
* Same return type

Example:

```java
class Animal {
    void sound() {
        System.out.println("Animal makes sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Dog barks");
    }
}
```

---

## 🔹 Dynamic Method Dispatch

```java
Animal myDog = new Dog();
myDog.sound();  // Dog barks
```

Method call decided at runtime → **Late Binding**

---

## 1️⃣0️⃣ The `final` Keyword with Inheritance

The keyword `final` has three uses.

---

### 10.1 final Variable (Constant)

```java
final int MAX = 100;
```

Cannot be changed.

---

### 10.2 Prevent Method Overriding

```java
final void show() { }
```

* Cannot be overridden.
* Allows **compile-time binding (Early Binding)**.
* Compiler may inline method → Performance improvement.

### Early vs Late Binding

| Binding Type  | When Resolved |
| ------------- | ------------- |
| Late Binding  | Runtime       |
| Early Binding | Compile Time  |

Normally, Java uses **late binding**.

But final methods use **early binding**.

---

### 10.3 Prevent Inheritance

```java
final class A { }
```

* Cannot be subclassed.
* All methods become implicitly final.
* ❌ Cannot declare class as both `abstract` and `final`.

---

## 1️⃣1️⃣ Static Methods and Inheritance

* Static methods can be inherited.
* But overriding them is meaningless.
* Parent static method always executes.
* That’s why static interface methods:

  * Cannot be inherited
  * Must have a body

---

## 1️⃣2️⃣ Important Concept: Polymorphism & Variables

⚠️ **Polymorphism does NOT apply to instance variables.**

Only methods are polymorphic.

Variables are resolved at compile time.

---

## 1️⃣3️⃣ Access Control in Inheritance

---

### Private

```java
private String name;
```

* Not accessible in subclass.

---

### Protected

```java
protected String name;
```

* Accessible in subclass.

---

### Public

```java
public String name;
```

* Accessible everywhere.

---

## 1️⃣4️⃣ Advantages of Inheritance

✔ Code Reuse
✔ Maintainability
✔ Extensibility
✔ Enables Polymorphism
✔ Reduces redundancy

---

## 1️⃣5️⃣ Challenges of Inheritance

❌ Tight Coupling
❌ Fragile Base Class Problem
❌ Complex Deep Hierarchies
❌ Sometimes composition is better

---

## 1️⃣6️⃣ Best Practices

### 🔹 1. Favor Composition Over Inheritance

Use "has-a" instead of "is-a" where appropriate.

### 🔹 2. Keep Hierarchies Shallow

Avoid deep inheritance chains.

### 🔹 3. Use Interfaces

For flexibility and polymorphism.

### 🔹 4. Avoid Overuse

Only use when strong "is-a" relationship exists.

### 🔹 5. Encapsulation

Keep fields private.
Use getters and setters.

---

## 1️⃣7️⃣ Important Summary Points

* Java supports **single inheritance through classes**
* Multiple inheritance allowed only through **interfaces**
* Subclass inherits everything except private members
* `super()` calls immediate superclass constructor
* Constructors execute top to bottom
* Reference type determines accessible members
* `final` prevents overriding and inheritance
* Static methods are inherited but not polymorphic
* Polymorphism applies to methods, not variables

---

# ✅ Final Conclusion

Inheritance enables:

* Logical class hierarchy
* Code reuse
* Method overriding
* Runtime polymorphism

However:

* Use it carefully
* Avoid deep hierarchies
* Prefer composition when suitable

By mastering:

* `extends`
* `super`
* Constructor chaining
* Method overriding
* `final`
* Access control

You can fully understand and implement inheritance in Java effectively.

# 🎯 Frequently Asked Interview Questions on Inheritance (With Detailed Answers)

This section covers **conceptual clarity, tricky edge cases, runtime behavior, and practical understanding** of inheritance in Java. These questions are commonly asked in **technical interviews (especially for Java backend roles)**.

---

# 🔹 1️⃣ What is Inheritance in Java?

### ✅ Answer:

Inheritance is an OOP mechanism in which one class (subclass) acquires the properties and behaviors (fields and methods) of another class (superclass) using the `extends` keyword.

It establishes an **IS-A relationship**.

Example:

```java
class Animal { }
class Dog extends Animal { }
```

Here:

* Dog **IS-A** Animal.

### Why Inheritance?

* Code reuse
* Polymorphism
* Maintainability
* Logical hierarchy
* Extensibility

---

# 🔹 2️⃣ Why Does Java Not Support Multiple Inheritance Through Classes?

### ✅ Answer:

Java does not support multiple inheritance through classes to avoid the **Diamond Problem**.

### Diamond Problem Explained:

If:

```
      A
     / \
    B   C
     \ /
      D
```

If both B and C override a method from A, and D extends both B and C:

* Which version should D inherit?

This creates ambiguity.

### How Java Solves It?

* Java supports multiple inheritance **through interfaces only**.
* Interfaces avoid ambiguity because:

  * No state (before Java 8)
  * With default methods, Java forces override if ambiguity exists.

---

# 🔹 3️⃣ What Is the Difference Between `extends` and `implements`?

| Feature           | extends           | implements               |
| ----------------- | ----------------- | ------------------------ |
| Used for          | Class inheritance | Interface implementation |
| Multiple allowed? | ❌ No              | ✔ Yes                    |
| Keyword used with | Class             | Interface                |

Example:

```java
class Dog extends Animal { }

class Dog implements Pet, Guard { }
```

---

# 🔹 4️⃣ What Gets Inherited in Java?

### Inherited:

* Public methods
* Protected methods
* Default methods (same package)
* Public/protected fields

### Not Inherited:

* Private members
* Constructors

⚠️ Note: Constructors are NOT inherited, but they are called during object creation.

---

# 🔹 5️⃣ What Is Constructor Chaining?

### ✅ Answer:

Constructor chaining ensures that superclass constructor runs before subclass constructor.

```java
class Animal {
    Animal() {
        System.out.println("Animal constructor");
    }
}

class Dog extends Animal {
    Dog() {
        System.out.println("Dog constructor");
    }
}
```

Output:

```
Animal constructor
Dog constructor
```

### Why?

Superclass must initialize itself first before subclass adds extra behavior.

---

# 🔹 6️⃣ What Happens If You Don’t Use `super()`?

If you don't explicitly call `super()`:

* Java automatically inserts `super()` (default constructor).
* But if superclass does NOT have a default constructor → Compilation error.

Example:

```java
class Animal {
    Animal(String name) { }
}

class Dog extends Animal {
    Dog() { }   // ❌ ERROR (no super call)
}
```

Must write:

```java
Dog() {
    super("Buddy");
}
```

---

# 🔹 7️⃣ Can a Superclass Reference Hold a Subclass Object?

### ✅ Yes

```java
Animal obj = new Dog();
```

This is called **Upcasting**.

### Important Rule:

> The reference type determines accessible members.

So:

```java
obj.bark(); ❌
```

Because `bark()` is not defined in Animal.

---

# 🔹 8️⃣ What Is Method Overriding?

### ✅ Answer:

When a subclass provides its own implementation of a method defined in superclass.

Rules:

* Same method name
* Same parameters
* Same return type
* Cannot reduce access level

Example:

```java
class Animal {
    void sound() { }
}

class Dog extends Animal {
    @Override
    void sound() { }
}
```

---

# 🔹 9️⃣ What Is Dynamic Method Dispatch?

When:

```java
Animal obj = new Dog();
obj.sound();
```

Java determines at runtime which method to call.

This is called:

* Runtime Polymorphism
* Late Binding

---

# 🔹 🔟 What Is the Difference Between Method Overriding and Overloading?

| Overriding           | Overloading           |
| -------------------- | --------------------- |
| Happens in subclass  | Happens in same class |
| Same signature       | Different parameters  |
| Runtime binding      | Compile-time binding  |
| Enables polymorphism | Does not              |

---

# 🔹 1️⃣1️⃣ Can We Override Static Methods?

### ❌ No (Not Really)

Static methods belong to class, not object.

They are resolved at compile time.

Example:

```java
class Animal {
    static void sound() {
        System.out.println("Animal");
    }
}

class Dog extends Animal {
    static void sound() {
        System.out.println("Dog");
    }
}
```

```java
Animal obj = new Dog();
obj.sound();   // Animal
```

This is method hiding, not overriding.

---

# 🔹 1️⃣2️⃣ Why Does Polymorphism Not Apply to Variables?

Variables are resolved at compile time.

```java
class Animal {
    int x = 10;
}

class Dog extends Animal {
    int x = 20;
}

Animal obj = new Dog();
System.out.println(obj.x);  // 10
```

Because:

* Variable binding is compile-time.
* Method binding is runtime.

---

# 🔹 1️⃣3️⃣ What Is the `super` Keyword Used For?

Two main purposes:

1. Call superclass constructor
2. Access hidden superclass members

Example:

```java
super();
super.methodName();
super.variableName;
```

---

# 🔹 1️⃣4️⃣ What Is the Use of `final` in Inheritance?

### 1️⃣ Final Method

Prevents overriding.

```java
final void show() { }
```

Enables:

* Early binding
* Possible inlining
* Performance improvement

---

### 2️⃣ Final Class

Prevents inheritance.

```java
final class A { }
```

Example:

* String class is final.

---

### 3️⃣ Final Variable

Creates constant.

---

# 🔹 1️⃣5️⃣ What Is the Fragile Base Class Problem?

When changes in superclass unexpectedly break subclass behavior.

Example:

* Adding new method in superclass
* Changing implementation logic

Because inheritance creates tight coupling.

---

# 🔹 1️⃣6️⃣ What Is the Difference Between IS-A and HAS-A Relationship?

### IS-A → Inheritance

```java
Dog extends Animal
```

Dog IS-A Animal.

### HAS-A → Composition

```java
class Car {
    Engine engine;
}
```

Car HAS-A Engine.

### Best Practice:

> Favor composition over inheritance.

---

# 🔹 1️⃣7️⃣ What Happens When Both Superclass and Subclass Have Same Variable?

Subclass hides superclass variable.

Use `super.variable` to access parent version.

---

# 🔹 1️⃣8️⃣ What Is Early Binding and Late Binding?

| Early Binding  | Late Binding       |
| -------------- | ------------------ |
| Compile-time   | Runtime            |
| Static methods | Overridden methods |
| Final methods  | Virtual methods    |

---

# 🔹 1️⃣9️⃣ Can a Class Be Both Abstract and Final?

❌ No.

* Abstract class needs subclass.
* Final class prevents subclassing.

Contradiction.

---

# 🔹 2️⃣0️⃣ What Are the Limitations of Inheritance?

* Tight coupling
* Reduced flexibility
* Deep hierarchies hard to manage
* Fragile base class problem

---

# 🔹 2️⃣1️⃣ What Is Upcasting and Downcasting?

### Upcasting (Safe)

```java
Animal obj = new Dog();
```

### Downcasting (Risky)

```java
Dog d = (Dog) obj;
```

Must ensure object is actually Dog.

Otherwise:

```
ClassCastException
```

---

# 🔹 2️⃣2️⃣ Why Are Constructors Not Inherited?

Because constructors initialize the class itself.

Subclass cannot inherit constructor of superclass, but it can call it using `super()`.

---

# 🔹 2️⃣3️⃣ What Is the Order of Constructor Execution in Multilevel Inheritance?

If:

```
A → B → C
```

When creating C object:

Execution order:

```
A constructor
B constructor
C constructor
```

---

# 🔹 2️⃣4️⃣ Can We Access Private Members Using super?

❌ No.

Private members are not visible to subclass.

Even `super` cannot access them directly.

---

# 🔹 2️⃣5️⃣ What Is the Most Important Rule in Inheritance for Interviews?

> The type of reference variable determines accessible members.
> The actual object determines which overridden method runs.

This single line explains:

* Polymorphism
* Dynamic dispatch
* Variable resolution
* Method overriding

---

# 🧠 Final Interview Strategy

If interviewer asks about inheritance:

Always mention:

* IS-A relationship
* Code reuse
* Constructor chaining
* super keyword
* Method overriding
* Dynamic dispatch
* final usage
* Diamond problem
* Composition vs inheritance

---

# ✅ Conclusion

If you fully understand:

* extends
* super
* constructor order
* overriding rules
* upcasting/downcasting
* final
* static method behavior
* polymorphism limitations

You are fully prepared for any Java inheritance interview question — from beginner to advanced level.

