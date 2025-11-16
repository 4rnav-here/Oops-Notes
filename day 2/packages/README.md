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
