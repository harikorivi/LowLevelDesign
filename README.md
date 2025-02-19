# Low Level Design
Discuss and Sharing the learning Notes


## SOLID Principles Overview

SOLID is an acronym that stands for five fundamental principles of object-oriented programming (OOP) and software design:
S - Single Responsibility Principle (SRP)
O - Open-Closed Principle (OCP)
L - Liskov Substitution Principle (LSP)
I - Interface Segregation Principle (ISP)
D - Dependency Inversion Principle (DIP)
These principles aim to promote cleaner, more robust, and updatable code by providing guidelines for designing classes, modules, and systems.

Single Responsibility Principle (SRP)

Definition: A class should have only one reason to change, meaning it should have a single responsibility or purpose.
Goal: To ensure that a class is focused on performing a specific task and is not overloaded with multiple, unrelated responsibilities.
Benefits:
Easier maintenance and updates
Reduced coupling between classes
Improved cohesion within classes
Example:

### // Bad practice: Multiple responsibilities in one class
```
public class Employee {
    public void calculateSalary() { ... }
    public void saveEmployeeData() { ... }
    public void generateReport() { ... }
}
```
### // Good practice: Separate classes for each responsibility
```
public class SalaryCalculator {
    public void calculateSalary() { ... }
}
public class EmployeeRepository {
    public void saveEmployeeData() { ... }
}
public class ReportGenerator {
    public void generateReport() { ... }
}
```
## Open-Closed Principle (OCP)

**Definition:** Software entities (classes, modules, functions, etc.) should be open for extension but closed for modification.
**Goal:** To allow for the addition of new functionality without altering existing code.
**Benefits:**
Increased flexibility and extensibility
Reduced risk of introducing bugs into existing code
Improved maintainability
### Example:

### // Bad practice: Modifying existing code to add new functionality
```
public class Shape {
    public void draw() {
        if (this instanceof Circle) {
            // Draw circle
        } else if (this instanceof Rectangle) {
            // Draw rectangle
        }
    }
}
```
### // Good practice: Using inheritance and polymorphism to extend functionality
```
public abstract class Shape {
    public abstract void draw();
}
public class Circle extends Shape {
    @Override
    public void draw() {
        // Draw circle
    }
}
public class Rectangle extends Shape {
    @Override
    public void draw() {
        // Draw rectangle
    }
}
```
## Liskov Substitution Principle (LSP)

**Definition:** Derived classes should be substitutable for their base classes.
**Goal:** To ensure that derived classes behave as expected when used in place of their base classes.
**Benefits:**
Improved code reliability and predictability
Reduced errors due to incorrect assumptions about subclass behavior
**Example:**

### // Bad practice: Violating LSP
```
public class Bird {
    public void fly() { ... }
}
public class Penguin extends Bird {
    @Override
    public void fly() {
        throw new UnsupportedOperationException("Penguins cannot fly");
    }
}
```
### // Good practice: Designing classes to adhere to LSP
```
public abstract class Bird {
    public abstract void makeSound();
}
public class FlyingBird extends Bird {
    @Override
    public void makeSound() {
        System.out.println("Chirp");
    }
    public void fly() { ... }
}
public class NonFlyingBird extends Bird {
    @Override
    public void makeSound() {
        System.out.println("Honk");
    }
}
```
## Interface Segregation Principle (ISP)

**Definition:** Clients should not be forced to depend on interfaces they do not use.
**Goal:** To avoid bloated interfaces that contain methods that are not relevant to all clients.
**Benefits:**
Reduced coupling between clients and interfaces
Improved flexibility and maintainability
**Example:**

### // Bad practice: Fat interface
```
public interface Printer {
    void print();
    void scan();
    void fax();
}
public class BasicPrinter implements Printer {
    @Override
    public void print() { ... }
    @Override
    public void scan() {
        throw new UnsupportedOperationException();
    }
    @Override
    public void fax() {
        throw new UnsupportedOperationException();
    }
}
```
### // Good practice: Segregated interfaces
```
public interface Printable {
    void print();
}
public interface Scannable {
    void scan();
}
public interface Faxable {
    void fax();
}
public class BasicPrinter implements Printable {
    @Override
    public void print() { ... }
}
```
## Dependency Inversion Principle (DIP)

**Definition:** High-level modules should not depend on low-level modules, but both should depend on abstractions.
**Goal:** To decouple high-level modules from low-level modules and promote flexibility and testability.
**Benefits:**
Reduced coupling between modules
Improved flexibility and maintainability
Easier testing
**Example:**

### // Bad practice: Tight coupling
```
public class PaymentProcessor {
    private final PayPalPaymentGateway paymentGateway;
    public PaymentProcessor() {
        paymentGateway = new PayPalPaymentGateway();
    }
    public void processPayment() {
        paymentGateway.processPayment();
    }
}
```
### // Good practice: Dependency inversion
```
public interface PaymentGateway {
    void processPayment();
}
public class PayPalPaymentGateway implements PaymentGateway {
    @Override
    public void processPayment() { ... }
}
public class PaymentProcessor {
    private final PaymentGateway paymentGateway;
    public PaymentProcessor(PaymentGateway paymentGateway) {
        this.paymentGateway = paymentGateway;
    }
    public void processPayment() {
        paymentGateway.processPayment();
    }
}
```
