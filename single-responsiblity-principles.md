# Single Responsibility Principle (SRP)

* Definition
* Real-life analogy (Restaurant)
* Why SRP matters?
* Benefits of SRP
* Common mistakes when violating SRP
* Is SRP just for classes?

---

## Definition

A class should have only one reason to change. This means that the class should have only one job, one responsibility, and one purpose.

If a class takes more than one responsibility, then the responsibilities become coupled, and changes to one might break the other.

---

## Real-Life Analogy: Restaurant

A restaurant has waiters, chefs, receptionists, security, etc. Everyone has a single responsibility. They do their own job.

For example:

* The chef is responsible for making food.
* The receptionist does their own job, such as collecting money and answering customer queries.
* The waiter is responsible for serving customers.
* Security is responsible for security.

Everyone has their own responsibility.

---

## Why Does SRP Matter?

For example, consider a code compiler:

* Add driver code
* Syntax processing
* Code runs with test cases
* Store the output in the database
* Return the necessary things

A coordinator coordinates all these modules.

For example, if I have a coordinator class named `Run`, it should not look like this:

```text
class Run {
    run() {},
    add_driver() {},
    syntax_processing() {},
    ......
    .....
}
```

Every class has a try-catch block, so it becomes messy if everything is written inside one file.

For 3 to 4 months later, if the code compiler has an issue, then I need to check everything code by code. First, I will check the add driver code. If the bug is inside that, I will fix that. Then I will move to syntax processing, and then move on to the next one, and so on.

To avoid doing this, I can create separate classes or methods for performing the above-listed tasks.

For example:

* I have an add driver code class.
* I have a syntax processing class.
* I have a class for running code with test cases.
* I have a class for storing the output.
* I have a class for returning the necessary things.

Each responsibility can have its own class or method.

---

# Benefits of SRP

* Improved maintainability
* Better test coverage
* Lower risk in changes
* Reusable modules

For example, in the future, we can build an IDE. Then we don't need to write everything from scratch. We can use existing code, like syntax processing and returning the necessary things.

---

# Common Mistakes When Violating SRP

* Putting DB logic and business logic in the same class
* UI code coupled with logic

---

# Is SRP Just for Classes?

* It could be decided by the developer or the team.

You could have a responsibility like:

* `RUN`
* `SUBMIT`

It should be defined by developer to developer how they want to define these things depending on their use case.
