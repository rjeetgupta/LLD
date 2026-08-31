# Open-Closed Principle (OCP)

* Definition
* Real-Life Analogy (Adapter)
* Real-World Example
* When Should You Apply OCP?
* Misconceptions About OCP

---

## Definition

The **Open-Closed Principle (OCP)** states:

> **Software entities (classes, modules, and functions) should be open for extension but closed for modification.**

In simple words:

* You should be able to **add new behavior** to a class or function.
* You should be able to do this **without changing its existing code**.

### Example

Imagine a class that is used in **multiple places or multiple microservices**.

You should be careful when modifying this class because your changes might **break existing functionality**.

The problem is that we may not know:

* Where the class is being used.
* How it is being used.
* What assumptions other parts of the system have about its behavior.

So, instead of modifying the existing class every time we need to add new behavior, we should design it in a way that allows us to **extend its behavior without changing the existing implementation**.

---

## Real-Life Analogy (Adapter)

The **power adapters used in India are different from those used in the EU or the USA**.

For example, if you travel from India to the EU, you may find that your Indian charger cannot be plugged directly into a European power socket.

Instead of modifying or breaking your charger, you can buy a **travel adapter**.

The adapter allows your existing charger to work with the new socket **without modifying the charger itself**.

So:

> **Existing charger + new adapter = new compatibility without changing the existing charger.**

This is similar to the Open-Closed Principle.

We keep the existing code unchanged and **extend its behavior through a new implementation or extension**.

---

## Real-World Example

Let's take an example of **tax calculation in an invoicing system**.

### Requirement

Initially:

* We only need to calculate tax for **India**.

Later, the business expands:

* We need to support **the US**.
* We need to support **the EU**.
* In the future, we may need to support more countries.

### Initial Implementation

We can define a common `TaxCalculator` interface:

```java
interface TaxCalculator {
    double amountAfterTax(double amount);
}

class IndianTax implements TaxCalculator {

    @Override
    public double amountAfterTax(double amount) {
        return amount * 1.18;
    }
}
```

Our `InvoiceService` can use the `TaxCalculator` abstraction:

```java
class InvoiceService {

    private final TaxCalculator taxCalculator;

    public InvoiceService(TaxCalculator taxCalculator) {
        this.taxCalculator = taxCalculator;
    }

    public double calculate(double amount) {
        return taxCalculator.amountAfterTax(amount);
    }
}
```

Now, when we need to support the US, we can add a new implementation:

```java
class UsTax implements TaxCalculator {

    @Override
    public double amountAfterTax(double amount) {
        return amount * 1.10;
    }
}
```

And for the EU:

```java
class EuTax implements TaxCalculator {

    @Override
    public double amountAfterTax(double amount) {
        return amount * 1.20;
    }
}
```

Now we can use different tax calculators:

```java
public class Main {

    public static void main(String[] args) {

        TaxCalculator indianTax = new IndianTax();
        InvoiceService indiaInvoice = new InvoiceService(indianTax);

        System.out.println(indiaInvoice.calculate(100));

        TaxCalculator usTax = new UsTax();
        InvoiceService usInvoice = new InvoiceService(usTax);

        System.out.println(usInvoice.calculate(100));
    }
}
```

### What did we achieve?

When we added support for the US and EU, we **did not have to modify the existing `IndianTax` implementation**.

We simply **extended the system by adding new implementations**.

That's the basic idea behind OCP:

> **Add new behavior by extending the system instead of repeatedly modifying existing, stable code.**

---

## When Should You Apply OCP?

You should consider applying OCP:

* When you have **business rules that are likely to change or expand**.
* When you are building a **plugin system**.
* When you expect multiple implementations of the same behavior.
* When your codebase is becoming a **"God class"** with lots of conditions.
* When you frequently need to modify the same class to support new variations.

For example, if you repeatedly have code like:

```java
if (country.equals("INDIA")) {
    // India tax
} else if (country.equals("USA")) {
    // US tax
} else if (country.equals("EU")) {
    // EU tax
}
```

and new countries are continuously being added, that could be a good signal to introduce an abstraction and apply OCP.

---

## Misconceptions About OCP

| Misconception                                    | Reality                                                                             |
| ------------------------------------------------ | ----------------------------------------------------------------------------------- |
| OCP means never touching old code.               | No, you can refactor old code to support OCP.                                       |
| OCP leads to more classes, so it is an overkill. | Extra classes are fine if they improve maintainability.                             |
| OCP makes code harder to read.                   | If done right, OCP provides more flexibility and makes the code easier to maintain. |
