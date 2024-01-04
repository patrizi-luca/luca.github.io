---
title: The Gang Of Four 
subtitle: Key Questions for Senior Software Developer (Part II)
category: Programming C++
---

## Unveiling the Design Patterns Legacy: 
## The Gang of Four's Timeless Contributions

In the realm of software engineering, the Gang of Four (GoF) holds a revered status as the architects of 
one of the most influential texts in the field: "Design Patterns: Elements of Reusable Object-Oriented Software." 
Published in 1994, this seminal work was penned by Erich Gamma, Richard Helm, Ralph Johnson, and John Vlissides – collectively known as the Gang of Four. 
Their book serves as a cornerstone for developers seeking to elevate their understanding of object-oriented design 
by presenting a catalog of proven solutions to recurring design problems.

## Main Concepts:

1. Design Patterns as Solutions:
At its core, the Gang of Four's book introduces the concept of design patterns – general, reusable solutions to common software design problems. The authors identified and documented 23 such patterns, each encapsulating best practices for various aspects of object-oriented design. These patterns go beyond specific implementations and provide a higher-level view, guiding developers in crafting flexible, maintainable, and scalable software.

2. Abstraction of Expertise:
The Gang of Four's approach involves abstracting the expertise gained by experienced developers into these design patterns. By distilling successful design practices into patterns, the book empowers both novice and seasoned developers to apply these solutions effectively. This abstraction of expertise serves as a bridge, allowing the collective wisdom of experienced designers to be shared and applied across diverse projects.

3. Classification of Patterns:
The 23 design patterns are classified into three main categories: Creational, Structural, and Behavioral. Creational patterns address object creation mechanisms, Structural patterns focus on composition of classes and objects, and Behavioral patterns concentrate on communication between objects. This classification aids developers in understanding the context and purpose of each pattern, enabling them to make informed decisions during the design process.

## Practical Significance:

1. Flexibility and Adaptability:
The Gang of Four's design patterns promote the principles of flexibility and adaptability in software design. By embracing these patterns, developers gain the ability to create systems that can evolve gracefully in response to changing requirements. This adaptability is crucial in the dynamic landscape of software development.

2. Code Reusability:
One of the primary goals of the design patterns outlined by the Gang of Four is code reusability. Through the use of these patterns, developers can encapsulate functionalities in a modular and reusable manner. This not only reduces redundancy but also enhances maintainability and promotes a more efficient development process.

3. Common Language for Design:
The book establishes a common language for discussing design choices. Design patterns provide a shared vocabulary that facilitates communication among developers. This common understanding is instrumental in fostering collaboration and ensures a smoother exchange of ideas within development teams.

## Famous Design Patterns
Beyond the foundational concepts of design patterns, this masterpiece introduces a repertoire of solutions to common problems. Let's embark on a journey to explore some of the most famous design patterns that have left an indelible mark on the world of software engineering.

### Singleton Pattern: The Lone Guardian of Instances
- *Intent:* Ensure a class has only one instance and provide a global point of access to it.
- *Use case:* When you want to control access to a single instance of a class, and you want to provide a global point of access to that instance.
- *Implementation:* Typically involves creating a class with a private constructor, a private static instance, and a public static method that returns the instance. The instance is created only if it doesn't exist yet, otherwise, the existing instance is returned.
```
#include <iostream>

class Singleton {
private:
    // Private constructor to prevent instantiation
    Singleton() {}

    // Static instance variable
    static Singleton* instance;

public:
    // Public method to access the instance
    static Singleton* get_instance() {
        if (!instance) {
            instance = new Singleton();
        }
        return instance;
    }

    // Example method to demonstrate the singleton instance
    void display_message() {
        std::cout << "Hello from Singleton!" << std::endl;
    }
};

// Initializing the instance to nullptr
Singleton* Singleton::instance = nullptr;

// Example usage:
int main() {
    Singleton* singletonInstance1 = Singleton::get_instance();
    Singleton* singletonInstance2 = Singleton::get_instance();

    std::cout << "Are instances the same? " << (singletonInstance1 == singletonInstance2 ? "Yes" : "No") << std::endl;

    // Using the singleton instance
    singletonInstance1->display_message();

    return 0;
}
```

### Observer Pattern:
- *Intent:* Define a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.
- *Use case:* When you have an object (subject) whose state changes, and you want to notify and update other objects (observers) that are dependent on its state.
- *Implementation:* Involves a subject that maintains a list of observers, and when its state changes, it notifies all registered observers.
```
#include <iostream>
#include <vector>

// Observer interface
class Observer {
public:
    virtual void update() = 0;
};

// Subject
class Subject {
private:
    std::vector<Observer*> observers;

public:
    // Methods for managing observers
    void add_observer(Observer* observer) {
        observers.push_back(observer);
    }

    void remove_observer(Observer* observer) {
        // Implementation of observer removal
    }

    // Notify all observers
    void notify_observers() {
        for (Observer* observer : observers) {
            observer->update();
        }
    }
};

// Concrete Observer
class ConcreteObserver : public Observer {
public:
    // Implementation of the update method
    void update() override {
        std::cout << "Subject's state has changed!" << std::endl;
    }
};

// Example usage:
int main() {
    Subject subject;
    ConcreteObserver observer;

    // Register the observer
    subject.add_observer(&observer);

    // Notify observers
    subject.notify_observers();

    return 0;
}
   
```
### Factory Method Pattern:
- *Intent:* Define an interface for creating an object but let subclasses alter the type of objects that will be created.
- *Use case:* When you want to delegate the responsibility of instantiating an object to its subclasses, allowing a class to specify its instantiated objects at runtime.
- *Implementation:* Involves an interface or an abstract class with a method for creating objects, and concrete subclasses that implement this method to produce objects of a specific type.
```
#include <iostream>

// Product interface
class Product {
public:
    virtual std::string display() = 0;
};

// Concrete Products
class ConcreteProductA : public Product {
public:
    std::string display() override {
        return "Product A";
    }
};

class ConcreteProductB : public Product {
public:
    std::string display() override {
        return "Product B";
    }
};

// Creator interface
class Creator {
public:
    virtual Product* create_product() = 0;
};

// Concrete Creators
class ConcreteCreatorA : public Creator {
public:
    // Factory method to create ConcreteProductA
    Product* create_product() override {
        return new ConcreteProductA();
    }
};

class ConcreteCreatorB : public Creator {
public:
    // Factory method to create ConcreteProductB
    Product* create_product() override {
        return new ConcreteProductB();
    }
};

// Example usage:
int main() {
    Creator* creatorA = new ConcreteCreatorA();
    Product* productA = creatorA->create_product();
    std::cout << productA->display() << std::endl;  // Output: Product A

    return 0;
}

```
### Command Pattern: Encapsulating Requests
- *Intent:* Encapsulate a request as an object, thereby allowing for parameterization of clients with different requests, queuing of requests, and logging of the requests.
- *Use case:* When you want to decouple the sender and receiver of a request and parameterize objects with operations.
```
     #include <iostream>

     // Command interface
     class Command {
     public:
         virtual void execute() = 0;
     };

     // Concrete Command
     class ConcreteCommand : public Command {
     public:
         void execute() override {
             std::cout << "Executing command" << std::endl;
             // Additional command-specific logic here
         }
     };

     // Invoker
     class Invoker {
     private:
         Command* command;

     public:
         void set_command(Command* cmd) {
             command = cmd;
         }

         void execute_command() {
             command->execute();
         }
     };

     // Example usage:
     int main() {
         ConcreteCommand concreteCommand;
         Invoker invoker;
         invoker.set_command(&concreteCommand);
         invoker.execute_command();

         return 0;
     }
     
```
### Strategy Pattern: Dynamic Algorithms
- *Intent:* Define a family of algorithms, encapsulate each one, and make them interchangeable. Clients can vary the algorithm independently from the context that uses it.
- *Use case:* When you want to define a family of algorithms, encapsulate each algorithm, and make them interchangeable.
```
     #include <iostream>

     // Strategy interface
     class Strategy {
     public:
         virtual void algorithm() = 0;
     };

     // Concrete Strategies
     class ConcreteStrategyA : public Strategy {
     public:
         void algorithm() override {
             std::cout << "Executing algorithm A" << std::endl;
         }
     };

     class ConcreteStrategyB : public Strategy {
     public:
         void algorithm() override {
             std::cout << "Executing algorithm B" << std::endl;
         }
     };

     // Context
     class Context {
     private:
         Strategy* strategy;

     public:
         void set_strategy(Strategy* stg) {
             strategy = stg;
         }

         void execute_strategy() {
             strategy->algorithm();
         }
     };

     // Example usage:
     int main() {
         ConcreteStrategyA strategyA;
         ConcreteStrategyB strategyB;

         Context context;
         context.set_strategy(&strategyA);
         context.execute_strategy();

         context.set_strategy(&strategyB);
         context.execute_strategy();

         return 0;
     }
     
```
