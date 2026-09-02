# Interface Segregation Principle (ISP)

* Definition
* Example (Uber)
* Benefits of ISP
* When to Apply ISP?

---

## Definition

The **Interface Segregation Principle (ISP)** states:

> **Clients should not be forced to depend on interfaces that they do not use.**

In simple words:

* Don't create large, **bloated** interfaces.
* Break large interfaces into **smaller, more specific interfaces**.
* A class should only implement the methods that are relevant to it.

---

## Example: Uber

Imagine we are building an **Uber-like application**.

There are two main types of users:

* **Rider** → Books a ride and pays for the ride.
* **Driver** → Accepts the ride, drives the rider, and ends the ride.

A common mistake would be to create one large interface:

```java
interface UberInterface {
    void bookRide();
    void payRide();
    void acceptRide();
    void drive();
    void endRide();
}
```

Now imagine that both `Rider` and `Driver` have to implement this interface.

The `Rider` doesn't need `acceptRide()`, `drive()`, or `endRide()`.

Similarly, the `Driver` doesn't need `bookRide()` or `payRide()`.

This violates the **Interface Segregation Principle** because both classes are forced to depend on methods they don't use.

### Applying ISP

Instead of creating one large interface, we can split it into smaller and more specific interfaces:

```java
interface RiderInterface {
    void bookRide();
    void payRide();
}

interface DriverInterface {
    void acceptRide();
    void drive();
    void endRide();
}

class Rider implements RiderInterface {

    public void bookRide() {
        // Book a ride
    }

    public void payRide() {
        // Pay for the ride
    }
}

class Driver implements DriverInterface {

    public void acceptRide() {
        // Accept the ride
    }

    public void drive() {
        // Drive the rider
    }

    public void endRide() {
        // End the ride
    }
}
```

### Story to Remember ISP

Think about what happens when you use Uber.

As a **rider**, you open the app, enter your destination, book a ride, and pay for it.

You don't need to:

* Accept a ride request
* Drive the car
* End the driver's trip

Those responsibilities belong to the **driver**.

Similarly, a driver doesn't need to implement the functionality for booking or paying for their own ride.

So, instead of giving both users one **huge interface**, we give them only the interfaces relevant to their responsibilities.

That's the main idea behind the **Interface Segregation Principle**:

> **"Don't force a class to implement methods that it doesn't need."**

---

## Benefits of ISP

### 1. Modularity and Flexibility

Smaller interfaces make the application more modular and flexible.

Each interface focuses on a specific responsibility.

### 2. Improved Testability

Smaller interfaces are easier to mock and test.

For example, if a class only depends on `PaymentInterface`, we only need to mock the payment-related behavior instead of mocking a large interface with many unrelated methods.

### 3. Prevents Irrelevant Implementations

ISP prevents classes from accidentally implementing methods that are irrelevant to them.

This results in cleaner and more meaningful implementations.

### 4. Easier to Understand

Smaller interfaces are easier to read, understand, and maintain.

Developers can quickly understand what a class is responsible for by looking at the interfaces it implements.

---

## When to Apply ISP?

You should consider applying ISP:

* When an interface is doing **too many things**.
* When an interface contains many unrelated methods.
* When some classes implementing an interface don't need certain methods.
* When some classes are forced to provide empty implementations for methods they don't use.
* When some classes implementing an interface throw exceptions such as `UnsupportedOperationException` for certain methods.

### Simple Rule

If you see a class implementing an interface and saying:

> **"I don't need this method."**

that's a good signal that the interface may need to be **split into smaller, more specific interfaces**.

---

## In One Line

**ISP = Keep interfaces small, focused, and specific to the needs of their clients.**
