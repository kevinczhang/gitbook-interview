---
description: >-
  Design patterns systematically names, explains and evaluates an important and
  recurring design in object-oriented system
---

# Design Patterns

## Type of design patterns

1. Creational: concern process of object creation

* Apply to class: Factory Method
* Apply to objects: Abstract Factory, Builder, Prototype, Singleton

2\. Structural: deal with composition of classes or object.

* Apply to class: Adapter (class)
* Apply to object: Adapter (object), Bridge, Composite, Decorator, Facade, Flyweight, Proxy

3\. Behavioral: characterize the ways in which classes or objects interact and distribute responsibility.

* Apply to class: Interpreter, Template Method
* Apply to object: Chain of Responsibility, Command, Iterator, Mediator, Memento, Observer, State, Strategy, Visitor

## Examples:

### Singleton Class

It is used to control the number of objects created by preventing external instantiation and modification.

This concept can be generalized to systems that operate more efficiently when only one object exists, or that restrict the instantiation to a certain number of objects, such as:

1. private constructor - no other class can instantiate a new object.
2. private reference - no external modification.
3. public static method is the only place that can get an object.

Eager Mode:

```java
public final class AmericaPresident {
	private static final AmericaPresident thePresident = new AmericaPresident();
 
	private AmericaPresident() {}
 
	public static AmericaPresident getPresident() {
		return thePresident;
	}
}
```

Lazy Mode:

```java
public final class AmericaPresident {
	private static AmericaPresident thePresident;
 
	private AmericaPresident() {}
 
	public static AmericaPresident getPresident() {
		if (thePresident == null) {
			thePresident = new AmericaPresident();
		}
		return thePresident;
	}
}
```

### Factory Method

Factory design pattern is used for creating an object based on different parameters. The example below is about creating human in a factory.

```java
interface Human {
	public void Talk();
	public void Walk();
}
 
 
class Boy implements Human{
	@Override
	public void Talk() {
		System.out.println("Boy is talking...");		
	}
 
	@Override
	public void Walk() {
		System.out.println("Boy is walking...");
	}
}
 
class Girl implements Human{
 
	@Override
	public void Talk() {
		System.out.println("Girl is talking...");	
	}
 
	@Override
	public void Walk() {
		System.out.println("Girl is walking...");
	}
}
 
public class HumanFactory {
	public static Human createHuman(String m){
		Human p = null;
		if(m.equals("boy")){
			p = new Boy();
		}else if(m.equals("girl")){
			p = new Girl();
		}
 
		return p;
	}
}
```
