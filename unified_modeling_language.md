# Unified Modeling Language (UML)

## What is UML?

**UML (Unified Modeling Language)** is a standardized visual language used to **model and document the design of software systems**.

It provides a set of diagrams that help us represent different aspects of a system. UML makes it easier to **communicate ideas among stakeholders**, understand the system’s design, and visualize how different parts of the system interact with each other.

In simple words:

> **UML is a visual way of representing how a software system is designed and how it works.**

---

## Why Do We Use UML?

Imagine that we are developing an **online shopping application**.

Before writing the actual code, we need to understand:

* Who will use the system?
* What can a customer do?
* How will customers place an order?
* How will the payment process work?
* What data do we need to store?
* How will different parts of the system communicate with each other?

If we try to explain all of this only through words, it can become difficult to understand.

Instead, we can use **UML diagrams** to visually represent these requirements and designs.

For example:

A customer wants to buy a product.

**Customer → Select Product → Add to Cart → Make Payment → Place Order**

We can represent this process using a UML diagram. Developers, testers, business analysts, project managers, and other stakeholders can then look at the diagram and understand the system more easily.

---

# Types of UML Diagrams

UML diagrams are officially divided into **two main categories**:

1. **Structural Diagrams**
2. **Behavioral Diagrams**

### 1. Structural Diagrams

Structural diagrams describe the **static structure** of a system.

They answer questions such as:

> **What things exist in the system, and how are they related to each other?**

Examples include:

* Class Diagram
* Object Diagram
* Component Diagram
* Deployment Diagram
* Package Diagram
* Composite Structure Diagram
* Profile Diagram

### 2. Behavioral Diagrams

Behavioral diagrams describe the **behavior and dynamic aspects** of a system.

They answer questions such as:

> **How does the system behave, and how do its different parts interact over time?**

Examples include:

* Use Case Diagram
* Activity Diagram
* State Machine Diagram
* Sequence Diagram
* Communication Diagram
* Interaction Overview Diagram
* Timing Diagram

---

# A Simple Story to Understand UML

Let's say we are building an **Online Food Delivery System**.

A customer opens the application and searches for a restaurant.

The customer selects food and adds it to the cart. Then, the customer makes a payment and places the order.

After that, the restaurant receives the order and starts preparing the food. A delivery person picks up the order and delivers it to the customer.

We can represent different parts of this story using different UML diagrams.

### Use Case Diagram

Shows **what users can do** with the system.

> Customer → Search Restaurant
> Customer → Order Food
> Customer → Make Payment
> Customer → Track Order

### Class Diagram

Shows the **structure of the system**.

For example:

> Customer
> Order
> Restaurant
> Food
> Payment
> DeliveryPerson

It can also show how these classes are related.

### Sequence Diagram

Shows **how objects interact with each other over time**.

For example:

> Customer → Application → Restaurant → Payment Service → Delivery Service

### Activity Diagram

Shows the **flow of activities**.

For example:

> Select Food → Add to Cart → Checkout → Make Payment → Place Order → Prepare Food → Deliver Food

### State Machine Diagram

Shows how an object **changes its state**.

For example, an order might move through these states:

> **Created → Confirmed → Preparing → Ready → Out for Delivery → Delivered**

So, the same software system can be viewed from different perspectives using different UML diagrams.

---

# Summary

**UML = Unified Modeling Language**

It is a **standardized visual language** used to model and document software systems.

UML helps us:

* Understand software design
* Communicate with stakeholders
* Visualize system structure
* Describe system behavior
* Document software systems
* Identify relationships between different components

UML diagrams are broadly divided into two categories:

**1. Structural Diagrams** → Describe **what the system is**

**2. Behavioral Diagrams** → Describe **what the system does and how it behaves**
