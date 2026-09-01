# Liskov Substitution Principle (LSP)

* Definition
* Classic Example: Rectangle and Square
* Notification System Example
* Why Does LSP Matter?
* How to Spot an LSP Violation?
* Key Principles

---

## Definition

The **Liskov Substitution Principle (LSP)** states:

> **If S is a subtype of T, then objects of type T should be replaceable with objects of type S without altering the correctness of the program.**

### In Simple Terms

If **Class B** is a subtype of **Class A**, you should be able to use **B** anywhere you would use **A**, and the program should continue to behave correctly.

For example:

```java
T obj = new T();

// We should also be able to do:
T obj = new S();
```

The important point is that replacing the parent class with its child class **should not break the expected behavior of the program**.

---

## Classic Example: Rectangle and Square

Let's take a simple example of a `Rectangle`:

```java
class Rectangle {
    int height;
    int width;

    void setHeight(int height) {
        this.height = height;
    }

    void setWidth(int width) {
        this.width = width;
    }
}
```

Now, we might think that a `Square` should extend `Rectangle` because mathematically, a square is a type of rectangle.

```java
class Square extends Rectangle {
    @Override
    void setHeight(int height) {
        this.height = height;
        this.width = height;
    }

    @Override
    void setWidth(int width) {
        this.width = width;
        this.height = width;
    }
}
```

Now consider the following code:

```java
Rectangle rect = new Square();

rect.setHeight(2);
rect.setWidth(4);
```

For a normal `Rectangle`, we expect:

```text
Height = 2
Width  = 4
```

But because `rect` is actually a `Square`, calling `setWidth(4)` also changes the height to `4`.

So we get:

```text
Height = 4
Width  = 4
```

This means that replacing a `Rectangle` with a `Square` changes the expected behavior.

Therefore, **the inheritance relationship violates LSP**.

### The Lesson

The problem is not that a square is not mathematically a rectangle.

The problem is that **a `Square` does not behave like a `Rectangle` from the perspective of the `Rectangle` interface**.

LSP is about **behavior**, not just about whether the relationship makes sense conceptually.

---

# Notification System Example

Let's understand LSP using a more practical example.

Imagine that we are building a notification system for an application.

We have a base class called `Notification`:

```java
class Notification {

    public void sendNotification() {
        System.out.println("Notification Sent");
    }
}
```

Now we create different types of notifications:

```java
class EmailNotification extends Notification {

    @Override
    public void sendNotification() {
        System.out.println("Email Sent");
    }
}

class TextNotification extends Notification {

    @Override
    public void sendNotification() {
        System.out.println("Text Message Sent");
    }
}

class WhatsAppNotification extends Notification {

    @Override
    public void sendNotification() {
        System.out.println("WhatsApp Message Sent");
    }
}
```

Now our application can work with the parent type:

```java
public class Main {

    public static void main(String[] args) {

        Notification notification = new EmailNotification();
        notification.sendNotification();

        notification = new TextNotification();
        notification.sendNotification();

        notification = new WhatsAppNotification();
        notification.sendNotification();
    }
}
```

The output would be:

```text
Email Sent
Text Message Sent
WhatsApp Message Sent
```

This follows LSP because we can replace the `Notification` object with any of its valid subtypes without breaking the expected behavior.

---

# A Story to Understand LSP

Imagine you run an **online shopping company**.

Whenever a customer places an order, your system sends a notification.

Initially, you only support email notifications.

So you create:

```java
class Notification {

    public void sendNotification() {
        System.out.println("Email Sent");
    }
}
```

Later, your business team says:

> "We also want to send notifications through SMS and WhatsApp."

So you create:

```java
class TextNotification extends Notification {

    @Override
    public void sendNotification() {
        System.out.println("SMS Sent");
    }
}

class WhatsAppNotification extends Notification {

    @Override
    public void sendNotification() {
        System.out.println("WhatsApp Sent");
    }
}
```

Your existing notification service looks like this:

```java
class NotificationService {

    public void notifyCustomer(Notification notification) {
        notification.sendNotification();
    }
}
```

Now you can pass any notification:

```java
NotificationService service = new NotificationService();

service.notifyCustomer(new EmailNotification());
service.notifyCustomer(new TextNotification());
service.notifyCustomer(new WhatsAppNotification());
```

The service doesn't care which specific notification it receives.

It simply expects:

> "Give me a `Notification`, and I will send it."

And every subtype fulfills that promise.

This is the essence of **LSP**.

---

# But What If We Violate LSP?

Now imagine that someone creates this class:

```java
class SilentNotification extends Notification {

    @Override
    public void sendNotification() {
        throw new UnsupportedOperationException(
            "This notification cannot be sent"
        );
    }
}
```

We can technically write:

```java
Notification notification = new SilentNotification();

notification.sendNotification();
```

The code compiles because `SilentNotification` is a subtype of `Notification`.

But at runtime, the program fails.

That means `SilentNotification` **cannot properly substitute `Notification`**.

Therefore, it violates LSP.

### The Important Question

Whenever you create a subclass, ask:

> **"Can this subclass be used anywhere the parent class is expected without breaking the program's expected behavior?"**

If the answer is **no**, you probably have an LSP violation.

---

# Why Does LSP Matter?

LSP is important because it makes inheritance and polymorphism **safe and predictable**.

Without LSP, we may end up writing code like this:

```java
if (notification instanceof SilentNotification) {
    // special handling
}
```

or:

```java
if (notification instanceof TextNotification) {
    // do something different
}
```

When we constantly need to check the concrete type of an object, it is often a sign that our abstraction is not designed correctly.

With proper LSP, we can simply write:

```java
notification.sendNotification();
```

and trust that every valid subtype will behave correctly.

### Benefits of LSP

* Makes polymorphism reliable.
* Reduces unnecessary `if-else` and type checking.
* Makes code easier to extend.
* Makes existing code less likely to break when new subtypes are introduced.
* Improves maintainability.
* Encourages better abstractions.
