# Packages in Java — Complete, Deep Notes

> Packages group related classes and interfaces, provide a namespace, and control visibility. These notes explain everything about packages: syntax, filesystem layout, import mechanics, access rules, classpath/modulepath, packaging (JARs), best practices, pitfalls, and useful examples. Suitable for beginners and interview preparation.

---

## Quick summary (TL;DR)

* A **package** is a named grouping of related classes and interfaces.
* Packages provide **namespacing** (avoid name collisions) and **visibility control**.
* Filesystem directories must mirror package names (e.g., `com.example.app` → `com/example/app`).
* The JVM finds classes using the **current directory**, the **CLASSPATH**, or `-classpath`/`--class-path`.
* Access levels interact with packages: **public**, **protected**, **private**, and **package-private** (default).
* Use `import` (or fully-qualified names) to reference package members; `static import` for static members.
* Java 9+ adds the **module system** with `module-info.java` and a modulepath (separate from classpath).

---

## 1. What is a package?

A package is a named container for classes, interfaces, enums, and annotation types.
It serves two main roles:

1. **Namespace management** — allows multiple classes with the same simple name to coexist in different packages (e.g., `java.util.List` vs `com.myapp.List`).
2. **Access control** — the package boundary is used by the compiler for package-private accessibility (no modifier) and affects `protected`.

You declare a package at the top of a source file:

```java
package com.mycompany.app; // must be first non-comment statement
```

If you omit a `package` statement, the class is placed in the *unnamed (default) package*, which has restrictions (e.g., classes in named packages cannot import classes from the unnamed package with `import`).

---

## 2. Filesystem layout and compilation

Java expects the **directory structure** to reflect the package name. Example:

```
src/
  com/
    mycompany/
      app/
        Main.java   // contains: package com.mycompany.app;
```

`Main.java` example:

```java
package com.mycompany.app;

public class Main {
    public static void main(String[] args) {
        System.out.println("Hello from com.mycompany.app.Main");
    }
}
```

### Compile & run from project root

From the `src` directory parent:

```bash
javac src/com/mycompany/app/Main.java
# produces: src/com/mycompany/app/Main.class

# set classpath (here we use src as classpath)
java -cp src com.mycompany.app.Main
```

Or from `src`:

```bash
cd src
javac com/mycompany/app/Main.java
java com.mycompany.app.Main
```

**Important:** The directory names are *case-sensitive* on case-sensitive filesystems. `com/MyCompany` ≠ `com/mycompany`.

---

## 3. How JVM finds your packages / classes

The run-time system looks for classes in a sequence of places:

1. **Current working directory** by default. If your package classes are in a subdirectory of the current directory (matching the package structure), the JVM can load them.
2. **CLASSPATH environment variable** — a list of directories/JARs (colon-separated on UNIX, semicolon-separated on Windows). If a directory on the classpath contains `com/mycompany/app/Main.class`, it can be found as `com.mycompany.app.Main`.
3. **-classpath / -cp option** (command-line) — overrides or supplements `CLASSPATH`. Prefer using `-cp` for clarity.

Examples:

```bash
# Using class files in build/classes
java -cp build/classes com.mycompany.app.Main

# Using a JAR
java -cp lib/myapp.jar com.mycompany.app.Main
```

If a class is inside a JAR file, include the JAR in the classpath:

```bash
java -cp "lib/foo.jar:lib/bar.jar:build/classes" com.example.Main    # Unix
java -cp "lib\foo.jar;lib\bar.jar;build\classes" com.example.Main    # Windows
```

---

## 4. `import` and fully-qualified names

To use types from other packages you can:

* Use **fully-qualified names**:

  ```java
  java.util.List<String> list = new java.util.ArrayList<>();
  ```
* Or **import** the type:

  ```java
  import java.util.List;
  import java.util.ArrayList;

  List<String> list = new ArrayList<>();
  ```

### Wildcard import

`import java.util.*;` imports all *public* classes in `java.util`. It does **not** import subpackages (see below).

**Best practice:** Import specific classes (or let an IDE handle it). Wildcard imports can pollute the namespace and obscure dependencies.

### `static import`

Allows using static members without type qualification:

```java
import static java.lang.Math.PI;
import static java.lang.Math.max;

double r = 2.0;
double area = PI * r * r;
int m = max(10, 20);
```

**Use sparingly** — static imports are convenient for constants and test code (e.g., `assertEquals`), but overuse harms readability.

---

## 5. Package visibility and access modifiers

Java has four levels of access:

1. **public** — accessible from anywhere (subject to module rules in modular projects).
2. **protected** — accessible within same package *and* by subclasses (even if they are in different packages). Note: when accessed from a subclass in a different package, `protected` access requires a reference of subclass type (more on this in examples).
3. **package-private** (default, no modifier) — accessible only by classes in the *same package*. This is extremely important: a class with no modifier is invisible outside its package (except via public methods/classes).
4. **private** — accessible only within the defining class (or interface default/private methods within same type).

### Examples

```java
package com.example.a;

public class PublicClass {                 // visible everywhere
    protected int protectedField;          // visible in package and subclasses
    int packagePrivateField;               // visible only within com.example.a
    private int privateField;              // visible only within this class
}
```

**Key rules & gotchas:**

* **Top-level classes** can only be `public` or package-private. You cannot declare a top-level class as `protected` or `private`.
* **Nested classes** (static or inner) can have all access modifiers.
* Subpackages are **not** the same as the parent package for access control. For example, `com.example` and `com.example.util` are distinct packages. A package-private type in `com.example` is *not* visible in `com.example.util`.
* `protected` gives package access *and* subclass access. But subclass access is not unconditional — the subclass must access the protected member through an instance of the subclass (or `this`). Accessing a protected member on an instance of the parent type from a different package is not allowed.

---

## 6. Naming conventions and package design

* Use **reverse domain name** as a prefix if you own a domain: `com.example`, `org.apache`. This avoids global name collisions.
* Keep package names **lowercase**. Use descriptive names for subpackages: `com.example.app.service`, `com.example.app.model`.
* Choose package structure to reflect **logical boundaries** and **module separation**, not necessarily just folder hierarchy. Example: `com.example.auth`, `com.example.orders`.
* Avoid overly deep package hierarchies unless they add clarity.

---

## 7. Default (unnamed) package

If you omit `package` in your source file, the class is placed in the **unnamed** package. Rules & downsides:

* Classes in the unnamed package cannot be imported by classes in named packages using `import`. (It is bad practice to use the unnamed package for production code.)
* Use unnamed package only for small demos or throwaway code.

---

## 8. Package declarations, package-info.java, and package annotations

* `package` declaration must be the first non-comment, non-blank line (before `import` and type declarations).
* `package-info.java` is a file used for package-level documentation and annotations. Example:

  ```java
  /**
   * Utilities and helper classes for Foo module.
   */
  @NonNullApi
  package com.example.foo;

  import org.springframework.lang.NonNullApi;
  ```

  This file is compiled into the package annotations and shows up in Javadoc.

---

## 9. Packages vs subpackages — they are different

A package `com.example` and `com.example.util` are separate namespaces. A class declared package-private in `com.example` is **not visible** to classes in `com.example.util`.

**Implication:** Don’t assume subpackages inherit access. Design packages with that in mind.

---

## 10. JAR files and packaging

**JAR (Java ARchive)** bundles compiled `.class` files and resources (properties, images) into one ZIP-like file.

* The JAR contains entries that mirror the package directories:

  ```
  com/example/app/Main.class
  com/example/app/Util.class
  ```
* To run a class from a JAR:

  ```bash
  java -cp myapp.jar com.example.app.Main
  ```
* To create a JAR:

  ```bash
  jar cfe myapp.jar com.example.app.Main -C build/classes .
  ```

  * `c` = create, `f` = file name, `e` = entry point (main class)
* Manifest (`META-INF/MANIFEST.MF`) can define `Main-Class` and classpath entries.

**Sealed JARs and package sealing (historical):**

* JAR files can be *sealed*, which restricts classes in a package to be loaded from the same JAR. This prevents classes in the same package being supplied by different JARs. Sealed packages are rarely used in modern development and are superseded by the module system for strong encapsulation.

---

## 11. ClassLoader basics and classpath vs modulepath

* The JVM uses **ClassLoaders** to find and load classes and resources. Each ClassLoader has a search path and parent loader. You can create custom ClassLoaders for advanced use (dynamic loading, hot deployment, plugin systems).
* **Classpath**: traditional mechanism (directories and JARs).
* **Modulepath** (Java 9+): used by the module system (`module-info.java`) for stronger encapsulation. Modules declare exported packages; non-exported packages are not accessible to code outside the module even if public.

When you migrate to modules:

* `module-info.java` declares `exports` and `requires`. Exports control which packages are visible to other modules.
* Classpath and modulepath are separate; you run modular applications with `--module-path` and `--module`.

Example module declaration:

```java
module com.example.app {
    requires com.google.guava;
    exports com.example.app.api;
}
```

---

## 12. `import` specifics & conflicts

* Multiple classes with the same simple name in different packages can be used via fully-qualified names or import one and fully-qualify the other.
* If you import two classes with the same simple name using wildcard imports (like `import pkg1.*; import pkg2.*;`), the compiler will fail when you refer to that simple name; you must use fully-qualified name or explicit import for one.
* Static import can import static fields/methods, either explicitly or via wildcard (`import static java.lang.Math.*;`).

---

## 13. Package-private and API design

* **Package-private** (default) is useful when you want classes or methods to be visible only within a package (e.g., implementation classes, helpers). This enables a package boundary as the unit of encapsulation: public API classes (in `...api` or root package) and package-private implementation classes (in `...impl`).
* Use `package-info.java` to document package-level contracts and intended usage (e.g., which classes are public API vs internal).

**Pattern:** put public API in `com.example.api` and implementation details in `com.example.internal` (or `impl`). This makes intent clear.

---

## 14. Common pitfalls and gotchas

* **Assuming subpackages are same package** — they are not.
* **Renaming packages** requires moving files in the filesystem (or refactor via IDE).
* **Classpath mistakes** — classes not found because classpath doesn't include base directory.
* **Mixing classpath and modulepath** incorrectly in Java 9+ — modules may not see classpath entries or vice versa.
* **Using default (unnamed) package in production** — makes modularization and visibility awkward.
* **Overusing wildcard imports** — decreases readability and may cause conflicts.
* **Circular package dependencies** — reduce cohesion and complicate modularization; prefer clean package dependency graphs.

---

## 15. Best practices

* Use reverse-domain package names for uniqueness: `io.yourorg.project`.
* Design packages by **cohesion** and **abstraction boundaries** — group related types and hide internals with package-private.
* Keep public API packages small and stable, and move helpers to internal packages.
* Use `package-info.java` for package-level docs and annotations.
* Prefer explicit imports (or let your IDE manage them).
* Use JAR manifests and build tools (Maven/Gradle) to handle classpath and packaging.
* When migrating to modules, carefully design `exports` and `requires` to preserve encapsulation.
* Avoid mixing class and module path unless you understand the implications.

---

## 16. Examples (practical)

### Example 1 — Two classes with same simple name

Project layout:

```
src/
  com/example/util/List.java
  my/app/List.java
  my/app/Main.java
```

`com/example/util/List.java`

```java
package com.example.util;
public class List { /* ... */ }
```

`my/app/List.java`

```java
package my.app;
public class List { /* ... */ }
```

`my/app/Main.java`

```java
package my.app;

import com.example.util.List; // imports com.example.util.List

public class Main {
    public static void main(String[] args) {
        List utilList = new List();            // refers to com.example.util.List due to import
        my.app.List localList = new my.app.List(); // fully-qualified for local one
    }
}
```

### Example 2 — package-private visibility

`com/example/internal/Helper.java`:

```java
package com.example.internal;
class Helper {                   // package-private
    static String secret() { return "42"; }
}
```

`com/example/app/Main.java`:

```java
package com.example.app;
import com.example.internal.Helper; // NOT allowed if Helper is package-private
// compile error — Helper is not public
```

If `Main` is in `com.example.internal`, it can access `Helper`.

### Example 3 — compile & run with classpath

```
javac -d out src/com/example/util/*.java src/my/app/*.java
java -cp out my.app.Main
```

`-d out` tells `javac` to put compiled classes into `out`, preserving package directories.

---

## 17. Packaging into a JAR with packages

Build classes into `build/classes` (retaining package dirs). Then:

```bash
jar cfe myapp.jar my.app.Main -C build/classes .
# run
java -jar myapp.jar
```

The `-C build/classes .` includes all package directories under `build/classes`.

---

## 18. Module system brief (Java 9+)

If your project uses modules, you define a `module-info.java` at module root:

```
src/
  module-info.java
  com/example/app/Main.java
```

Example `module-info.java`:

```java
module com.example.app {
    requires java.sql;              // depends on java.sql module
    exports com.example.app.api;    // only this package is visible to other modules
}
```

The module system restricts access at module granularity: even `public` types in non-exported packages are *not* accessible to other modules.

Run modular app:

```bash
javac -d mods/com.example.app src/module-info.java src/com/example/app/*.java
java --module-path mods -m com.example.app/com.example.app.Main
```

---

## 19. When to use packages vs modules

* Packages are the basic namespace and visibility mechanism inside the JVM and source code.
* Modules (Java 9+) provide stronger encapsulation across JARs and runtime packages — use modules for large systems wanting explicit dependency declarations and strong encapsulation.

---

## 20. Final checklist (practical tips)

* [ ] Directory structure mirrors package names.
* [ ] `package` statement is first non-comment line.
* [ ] Avoid using the unnamed package for production code.
* [ ] Use explicit imports and `package-info.java` for documentation.
* [ ] Be mindful of package-private access — design APIs accordingly.
* [ ] Keep module exports minimal if using Java modules.
* [ ] Use build tools (Maven/Gradle) to manage classpath and packaging.

---

### References for further study (recommended)

* Java Language Specification — section on packages and types.
* `jar` documentation and `javac`/`java` command-line docs.
* Java Platform Module System (JPMS) tutorials for modularization.

---


# `static` in Java — Complete Deep Dive (with examples + interview exercises)

Everything you need to know about `static`. Explanations, how and why it works, memory/initialization details, common patterns, pitfalls, and interview-style exercises with answers. Paste directly into your notes.

---

## Quick summary (TL;DR)

* `static` marks **class-level** members (fields, methods, nested classes, initialization blocks).
* A `static` member belongs to the **class**, not to any particular instance. There's exactly one copy per class loader.
* `static` members are initialized when the **class is initialized**, not when instances are created.
* `static` methods cannot access instance fields/methods directly (they have no `this`).
* `static` methods are **hidden**, not overridden; they use **static binding**.
* `static` nested classes do not have an implicit reference to an outer instance.
* `static` is heavily used for constants, utility methods, singletons (holder idiom), and shared state (be careful with concurrency).

---

## Table of contents

1. What `static` means
2. `static` fields (variables) — behavior & memory
3. `static` methods — binding, rules, limitations
4. `static` initialization blocks — when to use
5. `static` nested classes vs inner classes
6. `static` imports
7. `static` and inheritance, hiding vs overriding
8. `static` and final (constants)
9. `static` and concurrency (thread-safety concerns)
10. Class loading & initialization order (where `static` fits)
11. `static` and serialization / reflection / classloaders
12. Common patterns using `static`
13. Pitfalls & best practices
14. Examples (complete runnable snippets)
15. Interview exercise questions (with answers & explanations)

---

## 1 — What `static` means

`static` makes a member belong to the **class itself** rather than to instances (objects) of the class.

* For a `static` **field**, there is one shared value per class (per classloader).
* For a `static` **method**, the method can be called without creating an object: `ClassName.method(...)`.
* For a `static` **nested class**, the nested class doesn't capture an instance of the outer class (no implicit `Outer.this`).

Think of `static` as "there is one copy shared across all objects (and even when there are no objects)".

---

## 2 — `static` fields (class variables)

### Characteristics

* Single copy per class (per classloader).
* Initialized when class is loaded/initialized.
* Accessed via `ClassName.field` (but `instance.field` also works syntactically — but not recommended).
* Useful for constants, caches, counters, shared resources.

### Memory location

* The reference to the class and its `static` fields live in the JVM area for class metadata (Method Area or Metaspace depending on JVM). The actual objects referenced live on the heap.

### Example: simple counter

```java
public class Box {
    public static int count = 0;
    public Box() { count++; }
}
```

All `Box` instances increment the same `count`.

### `static` variable visibility

* You can use access modifiers: `public static`, `private static`, etc.
* `private static` is a common pattern for encapsulated shared state.

### Initialization

* If a `static` field is not explicitly initialized, it gets a default (0, `false`, `null`).
* You can initialize inline or in a static block.

---

## 3 — `static` methods

### Rules & properties

* Belong to class. Call with `ClassName.method(...)`.
* Cannot use non-static (instance) fields/methods directly — no `this`.
* Can access static fields and other static methods.
* Cannot be abstract (since abstract requires subclass instance behavior).
* Can be `synchronized`, `final`, or `private`, etc.

### Static binding (hiding)

* `static` methods are **resolved at compile time** based on the reference type. They are *hidden* not overridden.
* Example:

```java
class Parent {
    static void f() { System.out.println("Parent"); }
}
class Child extends Parent {
    static void f() { System.out.println("Child"); }
}
Parent p = new Child();
p.f(); // prints "Parent" (static binding)
```

This differs from instance methods, which use dynamic dispatch.

### Use-cases

* Utility/helper methods (e.g., `Math.max`).
* Factory methods.
* Entry point (`public static void main(String[] args)`).

---

## 4 — `static` initialization blocks

A `static` block runs once when the class is initialized. Useful for complex static initialization.

```java
public class Config {
    public static final Map<String, String> map = new HashMap<>();
    static {
        // complex initialization, error handling, reading config, etc.
        map.put("appName", "MyApp");
    }
}
```

Multiple static blocks execute in textual order. They run when the class is initialized (first actively used).

---

## 5 — `static` nested classes vs non-static (inner) classes

* **Static nested class**: declared `static` inside another class. It behaves like a top-level class, but its name is scoped in the outer class. It **does not** have an implicit reference to an instance of the outer class.
* **Inner class (non-static)**: every instance implicitly points to the outer instance. You need an outer instance to instantiate it.

Example:

```java
class Outer {
    static class StaticNested { }
    class Inner { }
}
Outer.StaticNested s = new Outer.StaticNested(); // OK
Outer.Inner i = new Outer().new Inner();       // needs an outer instance
```

**Common use**: `static` nested classes implement helper types, builders, or the *Initialization-on-demand holder* for singletons.

---

## 6 — `static` import

`import static` imports static members so you can refer to them without class qualification:

```java
import static java.lang.Math.*;

double r = 2;
double area = PI * r * r; // no Math.PI
```

Use sparingly — avoid making code ambiguous.

---

## 7 — `static` & inheritance — hiding vs overriding

* `static` members are inherited, but static methods are **hidden** if declared again in subclass. This is called *method hiding*.
* Instance fields can also be shadowed by subclass static/instance fields (you can define a field with same name in subclass — it hides the parent field for references of the subclass type).

Example of hiding:

```java
class A { static void m() { System.out.println("A"); } }
class B extends A { static void m() { System.out.println("B"); } }
A a = new B();
a.m(); // prints "A"
B.m(); // prints "B"
```

Note: shadowing / hiding can create confusion. Prefer unique names or avoid hiding.

---

## 8 — `static` + `final` (constants)

`public static final` is how you create compile-time constants (if type and value are compile-time constants).

```java
public class Constants {
    public static final int MAX = 100;
    public static final String NAME = "App"; // String literal is compile-time constant
}
```

* `static final` primitive or `String` constants are inlined at compile-time into code that references them (if accessed from other classes). That means changing the constant value and not recompiling users leads to stale values — recompile clients.
* For complex objects as constants, prefer `public static final` but remember it's not immutable unless the object itself is immutable.

---

## 9 — `static` & concurrency (thread-safety concerns)

Because `static` fields are shared across threads, they are a source of concurrency bugs if mutable.

Common patterns:

* `private static final` immutable objects — safe.
* `private static volatile int x` — `volatile` ensures visibility, but is not atomic for increments (`x++`).
* Use `AtomicInteger`, `synchronized`, or other concurrency constructs for atomic updates.

Example (unsafe)

```java
public class Counter {
    public static int count = 0;     // not thread-safe
    public static void inc() { count++; }
}
```

Example (safe)

```java
public class Counter {
    private static final AtomicInteger count = new AtomicInteger(0);
    public static void inc() { count.incrementAndGet(); }
}
```

Static `synchronized` methods lock on `Class` object (`ClassName.class`), making them a way to synchronize across all instances:

```java
public static synchronized void foo() { ... } 
// locks ClassName.class
```

---

## 10 — Class loading & initialization order

Important for understanding when `static` members are created/executed.

### Rough order:

1. Load class binary (bytecode) into JVM (loading).
2. Link — verification + prepare (allocates static fields and sets default values).
3. Initialize — execute static initializers and static blocks in textual order and run superclass initializers first (if not already initialized).

A class is initialized when it is *first actively used* — common triggers:

* Creating an instance (`new`)
* Accessing a `static` field (unless it's a compile-time constant)
* Invoking a `static` method
* Using reflection to call `Class.forName(...)` often triggers initialization

**Note**: `Class.forName("pkg.ClassName")` initializes class; `ClassLoader.loadClass("pkg.ClassName")` may only load but not initialize.

---

## 11 — `static` & serialization / reflection / classloaders

* `static` fields are part of class state, not instance state, so **serialization of an instance does not include static fields**. After deserialization, static fields are whatever the runtime/classloader currently holds (or default).
* Reflection can access and modify static fields (e.g., `Field.set(null, value)` for static field).
* Classloaders: static data is per classloader. If you have two classloaders loading the same class name, they have separate static fields.

---

## 12 — Common patterns using `static`

* **Utility classes** (private constructor + static methods): `java.lang.Math`
* **Constants**: `public static final` fields in `interface` or `class`.
* **Singleton holder idiom**: `static` nested class that lazily holds the instance:

```java
public class Singleton {
    private Singleton() {}
    private static class Holder { static final Singleton INSTANCE = new Singleton(); }
    public static Singleton getInstance() { return Holder.INSTANCE; }
}
```

* **Caches** / shared resources (but manage concurrency carefully).
* **Factory methods**: `public static MyClass create(...)`.

---

## 13 — Pitfalls & best practices

### Pitfalls

* Shared mutable `static` fields → concurrency bugs and test interference.
* Relying on `static` initialization order across classes (can introduce subtle bugs).
* Declaring constants as `public static final` mutable objects → false immutability.
* Assuming `static` fields are unique across entire JVM — not true when multiple classloaders are involved.

### Best practices

* Minimize mutable `static` state. Prefer instance state, dependency injection.
* Make utility classes final, with private constructor to prevent instantiation.
* Use `static final` for immutable constants only; recompile clients after changes.
* Use `Atomic*` classes or synchronization for static mutable fields.
* Avoid hiding static methods across class hierarchies.

---

## 14 — Examples (runnable snippets)

### Example 1 — Static field & counter

```java
public class Box {
    public static int count = 0;
    public Box() { count++; }
    public static void main(String[] args) {
        new Box();
        new Box();
        System.out.println(Box.count); // prints 2
    }
}
```

### Example 2 — Static block initialization

```java
public class Config {
    public static final Map<String, String> props;
    static {
        props = new HashMap<>();
        props.put("appName", "Sample");
        // maybe read from file, handle exceptions etc.
    }
}
```

### Example 3 — Static method hiding demo

```java
class Parent {
    static void hello() { System.out.println("Parent"); }
    void instanceHello() { System.out.println("Parent instance"); }
}
class Child extends Parent {
    static void hello() { System.out.println("Child"); }
    @Override
    void instanceHello() { System.out.println("Child instance"); }
}
public class Test {
    public static void main(String[] args) {
        Parent p = new Child();
        p.hello();          // Parent (static binding)
        p.instanceHello();  // Child instance (dynamic dispatch)
    }
}
```

### Example 4 — Static nested class holder singleton

```java
public class Singleton {
    private Singleton() {}
    private static class Holder {
        private static final Singleton INSTANCE = new Singleton();
    }
    public static Singleton getInstance() {
        return Holder.INSTANCE;
    }
}
```

### Example 5 — Static synchronized

```java
public class Util {
    public static synchronized void doSomething() {
        // synchronized on Util.class
    }
}
```

---

## 15 — Interview Exercises (frequently asked) — with answers & explanations

> Each exercise tests a common `static` concept: initialization order, hiding, threading, serialization, nested classes, etc.

---

### Q1 — Predict output: static initialization order

```java
class A {
    static { System.out.println("A static"); }
    { System.out.println("A instance"); }
    A() { System.out.println("A ctor"); }
}

class B extends A {
    static { System.out.println("B static"); }
    { System.out.println("B instance"); }
    B() { System.out.println("B ctor"); }
}

public class Test {
    public static void main(String[] args) {
        System.out.println("Main start");
        new B();
        new B();
    }
}
```

**What prints (in order)?**

**Answer & Explanation**

```
A static
B static
Main start
A instance
B instance
A ctor
B ctor
A instance
B instance
A ctor
B ctor
```

* Class A initialized first (parent). Then B. Static blocks run once per class.
* For each `new B()`: instance initializers and constructors: parent instance initializer/ctor run (A instance/ctor) then child.

---

### Q2 — Static method hiding vs instance overriding

```java
class Parent { static void s() { System.out.println("Parent.s"); } void i() { System.out.println("Parent.i"); } }
class Child extends Parent { static void s() { System.out.println("Child.s"); } @Override void i() { System.out.println("Child.i"); } }
Parent p = new Child();
p.s();
p.i();
```

**What prints? Why?**

**Answer & Explanation**

```
Parent.s
Child.i
```

* `p.s()` calls `Parent.s` due to static binding (method hiding).
* `p.i()` calls `Child.i` via dynamic dispatch.

**Key point:** static methods are not polymorphic.

---

### Q3 — Static field shadowing and access

```java
class A { static int x = 10; }
class B extends A { static int x = 20; }
System.out.println(A.x); // ?
System.out.println(B.x); // ?
A a = new B();
System.out.println(a.x); // ?
```

**Answer & Explanation**

```
10
20
10
```

* `A.x` = 10, `B.x` = 20.
* `a.x` uses compile-time type `A` so prints `A.x`. Static fields are resolved by type, not runtime instance.

---

### Q4 — Static and serialization

```java
public class S implements Serializable {
    public static int s = 5;
    public int x;
    public S(int x) { this.x = x; }
}
S obj = new S(10);
obj.s = 15;
serialize(obj); // to file
S.s = 100;      // change static after serialize
S des = deserialize(); // reads object back
System.out.println(des.s);
```

**What prints?**

**Answer & Explanation**

`100`

* Static fields are not serialized with the instance. They are part of the class, not instance state. After deserialization, static value is whatever the class currently has in the JVM.

---

### Q5 — Static nested class vs inner class instantiation

```java
class Outer {
    static class StaticNested { void f() { System.out.println("static"); } }
    class Inner { void f() { System.out.println("inner"); } }
}
Outer.StaticNested n = new Outer.StaticNested();
Outer.Inner i = new Outer().new Inner();
n.f();
i.f();
```

**What prints?**

**Answer & Explanation**

```
static
inner
```

* Static nested class can be instantiated without an outer instance. Inner requires an outer instance.

---

### Q6 — Thread-safety: static counter

Given:

```java
public class Counter {
    public static int count = 0;
    public static void inc() { count++; }
}
```

If 100 threads each call `Counter.inc()` concurrently 1000 times (total 100k increments), is final `count` necessarily 100000? Why/why not? How to fix?

**Answer & Explanation**

* Not guaranteed. `count++` is not atomic (read-modify-write). Race conditions mean final value may be less.
* Fix: use synchronization:

  * `public static synchronized void inc() { count++; }` (locks on Class object), **or**
  * use `private static final AtomicInteger count = new AtomicInteger(0); public static void inc() { count.incrementAndGet(); }`.

---

### Q7 — Static final constant inlining

```java
public class C {
    public static final int F = 42;
}

// In other code compiled earlier:
System.out.println(C.F); // prints 42
```

If you change `C.F` to 43 and update only `C.class` (not the other class), what happens when you run old program?

**Answer & Explanation**

* The referencing class may still print `42` because compile-time constants are inlined into the bytecode of referencing classes. You must recompile dependents to see updated value.

---

### Q8 — Static initialization circular dependency

```java
class A {
    static int a = B.b + 1;
}
class B {
    static int b = A.a + 1;
}
System.out.println(A.a + " " + B.b);
```

**What happens?**

**Answer & Explanation**

* This leads to default initialization and likely results in zeros and increments depending on order. It's an example of risky circular static initialization and should be avoided. The exact outcome depends on which class triggers initialization first. Such circular dependencies are fragile and error-prone.

---

### Q9 — Static synchronized lock test

```java
public class Test {
    public static synchronized void A() {
        // locks Test.class
        // sleep for a while
    }
    public synchronized void B() {
        // locks instance
    }
}
```

If Thread1 calls `Test.A()` and Thread2 calls `new Test().B()`, can they run concurrently?

**Answer & Explanation**

* Yes. `A()` locks `Test.class`; `B()` locks the instance. Different locks, so they can proceed concurrently. If B were static synchronized, it would lock the same `Test.class` and cause mutual exclusion.

---

### Q10 — Static & Classloader uniqueness

If two classloaders load the same class name `com.example.Foo`, each will have its own `static` fields. What are the implications?

**Answer & Explanation**

* There will be two separate copies of `com.example.Foo` in JVM (one per classloader), each with separate static fields. This allows class isolation (used in application servers/plugin systems) but can cause confusion if you expect a single static singleton across the JVM.

---

## 16 — Extra practice exercises (no immediate answer given)

Try these on your own (good for interviews):

1. Create two classes `A` and `B` where `A` has a static block that calls a static method in `B` and `B` has a static block that calls a static method in `A`. Instantiate one class and reason about initialization order and outputs.
2. Write a utility class with `private` constructor and only static methods. Show how you prevent instantiation and how IDEs warn when wrongly instantiating.
3. Implement a thread-safe static lazy singleton WITHOUT `synchronized` on the getter using the static nested holder idiom — explain why it’s thread-safe.
4. Show what happens when you `import static` two classes that have same static member name — how to disambiguate?
5. Write code where a subclass hides a static field of parent and then access via parent reference vs subclass reference — explain results.

---

## Final quick checklist (what to remember)

* `static` = class-level (one copy).
* `static` fields are shared; be careful with mutability & concurrency.
* `static` methods are hidden, not overridden — static binding.
* `static` nested classes have no outer instance reference.
* Static initialization order matters. Use static blocks for complex init.
* Use `public static final` for constants, but remember inlining.
* Minimize mutable `static` state; prefer DI and instance-level state when possible.

