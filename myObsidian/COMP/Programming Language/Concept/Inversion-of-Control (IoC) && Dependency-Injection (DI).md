---
aliases: [IoC, DI]
tags:
  - concept
---
The **`Inversion-of-Control` (IoC)** pattern, is about providing _any kind_ of `callback` (which controls reaction), instead of acting ourself directly (in other words, inversion and/or redirecting control to external handler/controller). The **`Dependency-Injection` (DI)** pattern is a more specific version of IoC pattern, and is all about removing dependencies from your code.

> Every `DI` implementation can be considered `IoC`, but one should not call it `IoC`, because implementing Dependency-Injection is harder than callback (Don't lower your product's worth by using general term "IoC" instead).

For DI example, say your application has a text-editor component, and you want to provide spell checking. Your standard code would look something like this:

```csharp
public class TextEditor {

    private SpellChecker checker;

    public TextEditor() {
        this.checker = new SpellChecker();
    }
}
```

What we've done here creates a dependency between the `TextEditor` and the `SpellChecker`. In an IoC scenario we would instead do something like this:

```csharp
public class TextEditor {

    private IocSpellChecker checker;

    public TextEditor(IocSpellChecker checker) {
        this.checker = checker;
    }
}
```

In the first code example we are instantiating `SpellChecker` (`this.checker = new SpellChecker();`), which means the `TextEditor` class directly depends on the `SpellChecker` class.

In the second code example we are creating an abstraction by having the `SpellChecker`dependency class in `TextEditor`'s constructor signature (not initializing dependency in class). This allows us to call the dependency then pass it to the TextEditor class like so:

```csharp
SpellChecker sc = new SpellChecker(); // dependency
TextEditor textEditor = new TextEditor(sc);
```

Now the client creating the `TextEditor` class has control over which `SpellChecker`implementation to use because we're injecting the dependency into the `TextEditor`


IOC 全名**控制反转** Inverse of Control，它是一种**编程原则**，它的设计和架构可以实现**组件间的解耦**，核心思想是**将控制权转移出去**。

这里面提到了几个点：

-   编程原则：它是一种**理论**，而非具体的某种技术落地
-   组件间的解耦：所谓**耦合**，就是上面提到的**对象间的依赖关系**；**解耦**，就是**解除了对象间的依赖关系**。
    -   提到解耦，有可能面试官会继续问“什么是解耦”，也有可能不会问 “为什么用 Spring ”了
-   控制权的转移：IOC 为了实现解耦，将原有的对象间的**主动依赖改为被动接收型依赖**（由直接 **new 变为 set** ）

## IOC与DI的区别

-   **IOC 是一种思想、编程原则，DI 是 IOC 思想的一种实现方式。**
-   **IOC 的实现方式有依赖查找（ Dependency lookup ）和依赖注入（ Dependency Injection ）。**
