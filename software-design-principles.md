# PRINCIPLES OF SOFTWARE DESIGN

* DRY
* KISS
* YAGNI

## DRY (Don't Repeat Yourself)

* It means that each piece of knowledge or logic should have a single, unambiguous representation within the system.

For example: We have two functions where a logic of finding even and odd is being used in those two functions, then I will create a separate class for it and use this class in those functions because when I need to change some logic or add some logic, then it is easier to change it at once only.

### Importance

* Reduce redundancy
* Easier maintenance
* Single point of change

### How to apply?

* Identify repetitive code
* Extract common functionality
* Leverage libraries and frameworks
* Refactor code regularly

## When not to use the DRY principle?

* Premature abstraction
* Performance-critical code
* Sacrificing readability
* Legacy code

# KISS (Keep It Simple, Stupid)

* A design should be kept as simple as possible. Complexity should only be introduced when absolutely necessary.

### Importance

* Easier debugging
* Improved readability
* Better maintenance
* Faster development

# YAGNI (You Aren't Gonna Need It)

* Always implement things when you actually need them, never when you just foresee that you might need them.

Example: Start with a single payment.

### Importance

* Reduced waste
* Simplified codebase
* Faster development

### What not to follow?

* Well-known requirements
* Performance-critical areas
