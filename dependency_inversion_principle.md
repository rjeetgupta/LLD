# Dependency Inversion Principle (DIP)

## Definition

The **Dependency Inversion Principle (DIP)** states:

> **High-level modules should not depend on low-level modules. Both should depend on abstractions. Abstractions should not depend on details. Details should depend on abstractions.**

In simple words:

**Instead of depending directly on a specific implementation, depend on an interface (abstraction).**

---

# Real-Life Example: Recommendation System

Let's understand DIP with a **Netflix-like recommendation system**.

Imagine you are building a recommendation system for a streaming platform such as Netflix.

Netflix may recommend movies or shows based on different algorithms:

* **Recent-based recommendation** — recommends content based on what the user recently watched.
* **Trending-based recommendation** — recommends currently trending content.
* **Genre-based recommendation** — recommends content based on the user's preferred genre.

### The Problem

Suppose our main recommendation system directly depends on the trending algorithm:

```java
class RecommendationAlgorithm {

    private TrendingRecommendation trendingRecommendation;

    public RecommendationAlgorithm() {
        this.trendingRecommendation = new TrendingRecommendation();
    }

    public void recommend() {
        trendingRecommendation.recommend();
    }
}
```

This creates **tight coupling**.

If tomorrow we want to use `GenreRecommendation` instead of `TrendingRecommendation`, we have to modify the `RecommendationAlgorithm` class.

And if we add another algorithm, such as:

* `RecentRecommendation`
* `PopularRecommendation`
* `PersonalizedRecommendation`

the high-level class keeps changing.

This violates the idea of depending on abstractions rather than concrete implementations.

---

# Applying Dependency Inversion Principle

To solve this problem, we introduce an abstraction:

```java
interface RecommendationStrategy {
    void recommend();
}
```

Now, every recommendation algorithm implements this interface.

```java
class TrendingRecommendation implements RecommendationStrategy {

    @Override
    public void recommend() {
        System.out.println("Recommending trending movies...");
    }
}
```

```java
class GenreRecommendation implements RecommendationStrategy {

    @Override
    public void recommend() {
        System.out.println("Recommending movies based on genre...");
    }
}
```

```java
class RecentRecommendation implements RecommendationStrategy {

    @Override
    public void recommend() {
        System.out.println("Recommending recently watched movies...");
    }
}
```

Now our high-level `RecommendationAlgorithm` class depends only on the abstraction:

```java
class RecommendationAlgorithm {

    private RecommendationStrategy recommendationStrategy;

    public RecommendationAlgorithm(RecommendationStrategy recommendationStrategy) {
        this.recommendationStrategy = recommendationStrategy;
    }

    public void recommend() {
        recommendationStrategy.recommend();
    }
}
```

We can now choose the required recommendation strategy from outside:

```java
public class Main {

    public static void main(String[] args) {

        RecommendationAlgorithm recommendationAlgorithm =
                new RecommendationAlgorithm(
                        new TrendingRecommendation()
                );

        recommendationAlgorithm.recommend();
    }
}
```

Tomorrow, if we want to use genre-based recommendations, we don't need to modify `RecommendationAlgorithm`.

We simply provide a different implementation:

```java
RecommendationAlgorithm recommendationAlgorithm =
        new RecommendationAlgorithm(
                new GenreRecommendation()
        );
```

Or we can use recent-based recommendations:

```java
RecommendationAlgorithm recommendationAlgorithm =
        new RecommendationAlgorithm(
                new RecentRecommendation()
        );
```

---

# The Story in Simple Words

Imagine you are the **manager of Netflix's recommendation system**.

Your job is simple:

> "Give me a recommendation."

You don't care **how** the recommendation is generated.

You don't need to know whether the recommendation comes from:

* Trending data
* Recent history
* Genre preferences
* Personalized AI
* Some future algorithm

You only need to know that the recommendation strategy can perform:

```java
recommend()
```

That's why you define an interface:

```java
interface RecommendationStrategy {
    void recommend();
}
```

Now the manager depends on this interface instead of depending on a specific algorithm.

So the relationship becomes:

```text
RecommendationAlgorithm
          |
          v
RecommendationStrategy
          ^
          |
   -------------------
   |        |        |
   v        v        v
Trending  Genre    Recent
```

The **high-level module** (`RecommendationAlgorithm`) depends on the **abstraction** (`RecommendationStrategy`).

The **low-level modules** (`TrendingRecommendation`, `GenreRecommendation`, and `RecentRecommendation`) also depend on that abstraction by implementing it.

This is **Dependency Inversion Principle**.

---

# Benefits of DIP

### 1. Loose Coupling

The high-level class is not tightly coupled to a particular implementation.

```java
RecommendationStrategy
```

is the abstraction, so we can replace the implementation easily.

---

### 2. Easy to Add New Implementations

Suppose tomorrow we introduce:

```java
class PersonalizedRecommendation implements RecommendationStrategy {

    @Override
    public void recommend() {
        System.out.println("Recommending personalized movies...");
    }
}
```

We don't need to modify `RecommendationAlgorithm`.

We simply pass the new implementation:

```java
new RecommendationAlgorithm(
    new PersonalizedRecommendation()
);
```

---

### 3. Easier Unit Testing

Because the high-level class depends on an interface, we can easily provide a **mock implementation** during testing.

For example:

```java
class MockRecommendation implements RecommendationStrategy {

    @Override
    public void recommend() {
        System.out.println("Mock recommendation");
    }
}
```

Then:

```java
RecommendationAlgorithm algorithm =
        new RecommendationAlgorithm(
                new MockRecommendation()
        );
```

This makes unit testing much easier.

---

### 4. Abstractions Control the Relationship

The high-level module defines what it needs through an abstraction:

```java
interface RecommendationStrategy {
    void recommend();
}
```

The concrete implementations follow that contract.

This allows the high-level business logic to remain independent of implementation details.

---

### 5. Supports the Open/Closed Principle

DIP works very well with the **Open/Closed Principle (OCP)**.

We can add new recommendation strategies without modifying the existing `RecommendationAlgorithm` class.

For example:

```text
New Requirement
      |
      v
PersonalizedRecommendation
      |
      v
RecommendationStrategy
      |
      v
RecommendationAlgorithm
```

We are **extending the system without modifying the high-level module**.

---

# Key Takeaway

The main idea of DIP is:

> **Depend on abstractions, not concrete implementations.**

Instead of:

```text
RecommendationAlgorithm
        |
        v
TrendingRecommendation
```

we should have:

```text
RecommendationAlgorithm
        |
        v
RecommendationStrategy
        ^
        |
TrendingRecommendation
```

This gives us **loose coupling, flexibility, easier testing, and easier extension of the system**.
