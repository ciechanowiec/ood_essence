# The Essence of Object-Oriented Design

## Table of Contents

1. [Object](#Object)
	* [Definition of Object](#Definition-of-Object)
	* [Messaging](#Messaging)
	* [Externals vs Internals](#Externals-vs-Internals)
2. [Encapsulation](#Encapsulation)
	* [Definition of Encapsulation](#Definition-of-Encapsulation)
	* [Giving Access to Data](#Giving-Access-to-Data)
	* [Real World Analogy](#Real-World-Analogy)
	* [Comparison to Functional Software Design](#Comparison-to-Functional-Software-Design)
4. [Nouns Instead of Verbs](#Nouns-Instead-of-Verbs)

## Description
This document explains the basics of object-oriented design in software development.

## Object

#### Definition of Object
Object-oriented design is a software development approach that solves the problem by creating a system of interacting *objects*. 

Every object is a composition of data and operations that manipulate the data. That data is contained in object's *fields*, which represent its properties. The operations are, in turn, represented by object's *methods*, which are algorithms that manipulate the data stored in the object. Such bundle of data and operations results in situation, when every object is exclusively responsible for its own manipulation.

> The object-oriented view is one of a world of interacting objects. Each object has responsibility for its own actions. In the procedural paradigm, data objects are considered passive and are acted upon by the program. In the object-oriented paradigm, data objects are active. Objects and the code that manipulates them are bundled together, making each object responsible for its own manipulation
> 
> *\-  N. Dale, J. Lewis, Computer Science Illuminated, 2020, p. 295-296.*

In other words, an object is an entity that (i) has state and (ii) is characterized by the actions that it suffers and that it requires of other objects. It is something that exists in time and space, and may be affected by the activity of other objects or affect them itself (*G. Booch, Object-Oriented Development, "IEEE Transactions on Software Engineering", vol. SE-12, No. 2, February 1986, p. 215*).

#### Messaging
Objects communicate with one another by sending messages, i.e., by invoking one another’s subprograms (*N. Dale, J. Lewis, op. cit., p. 283*). Three following types of messages can be specified (*D. West, Object Thinking, 2004, p. 155*):
1) **imperative message**, which directs an object to make some change to itself. No response is expected or required. The object is assumed to have made the appropriate change;
2) **informational message**, which is similar to an imperative in the sense that no response is expected. It differs from an imperative in that there is also no expectation that the receiving object will do anything at all in response to the message;
3) **interrogatory message**, which is any request for a service. The object always returns an object (a typed value) that encapsulates the result requested. The returned object can be simple (a character or a string) or arbitrarily complex.

#### Externals vs Internals
Every object has two parts, and so may be viewed from two different ways: there is an outside view and an inside view, object's externals and internals. Whereas the outside view of an object serves to capture the abstract behavior of the object, the inside view indicates how that behavior is implemented. Thus, by seeing only the outside view, one object can interact with another without knowing how the other is represented or implemented. When designing a system, we first concern ourselves with the outside view. The outside view of an object is its specification (*G. Booch, op. cit., p. 216*). 

## Encapsulation

#### Definition of Encapsulation
The data stored in an object can be accessed or modified only through the methods of that object. The data stored in an object must not be accessed neither modified directly by another object, i.e. bypassing the methods of the object, in which that data is stored. Hiding object's data in such a way is called _encapsulation_.
> (...) that _encapsulation_ is a language feature that enforces information hiding. A module’s implementation is hidden in a separate block with a formally specified interface. An object knows things about itself, but not about any other object. If one object needs information about another object, it must request that information from that object. (...)
> 
> The only way to manipulate the data fields of [an object] (...) is through the methods (subprograms) defined in the [object] (...)
> 
> *\-  N. Dale, J. Lewis, op. cit., p. 314.*
> 
#### Giving Access to Data
As a rule, an object should have the responsibility of making data it stores available to other objects that need it. For example, a `Student` object can store data such as name and address, and an object that uses the `Student` object should be able to retrieve this information. The discussed responsibility of giving access to the internal object's data is usually implemented by methods named with `Get` preceding the name of the data, e.g. `GetName` or `GetEmailAddress` (*N. Dale, J. Lewis, op. cit., p. 284*). 

Nevertheless, giving access to the internal object's data must not break encapsulation. It means that any action performed upon the data retrieved from a given object must not affect the original data stored in an object. For instance, changing by a querying object the data (e.g. name) retrieved from the `Student` object must not change the data stored in that source object. However, the `Student` object may have a method that will allow another object to modify the data (e.g. name) stored inside the `Student` object.

#### Real World Analogy
The idea of encapsulation has many real world analogies, such as an automobile engine:
> (...) [Encapsulation] and information hiding are actually quite natural activities. We employ [encapsulation] (...) daily and tend to develop models of reality by identifying the objects and operations that exist at each level of interaction. Thus, when driving a car, we consider the accelerator, gauges, steering wheel, and brake (among other objects) as well as the operations we can perform upon them and the effect of those operations. When repairing an automobile engine, we consider objects at a lower level of abstraction, such as the fuel pump, carburetor, and distributor.
> 
> Similarly, a program that implements a model of reality (as all of them should) may be viewed as a set of objects that interact with one another
> 
> *G. Booch, op. cit., p. 213*

#### Comparison to Functional Software Design
One of the side-effects of functional software design is that all relevant data ends up being global to the entire system, so that any change to that data affects the whole program. Alternately, in the object-oriented software design, thanks to encapsulation, the effect of changing the given data tends to be much more localized (*G. Booch, op. cit., p. 213*).

The main difference between functional software design and object-oriented software design can be shown on the example of calculating student's grade point average (GPA). In the first case we would concentrate on developing a program procedure, which task will be to calculate the GPA for for the provided data, while in the second case we would concentrate on developing a separate `Student` object that will be responsible for calculating its own GPA. The distinction is both subtle and profound. The final code for the calculation may look the same, but it is executed in different ways. In a program based on a functional software design, the program calls the subprogram that calculates the GPA, passing the `Student` object as a parameter. In an object-oriented program, a message is sent to the object to calculate its GPA. There are no parameters because the object to which the message is sent knows its own data (*N. Dale, J. Lewis, op. cit., p. 294*).

## Nouns Instead of Verbs
One of effective approaches for understanding object-oriented design is to think in terms of nouns instead of verbs. Here is how it was explained in an Apple's guide for developers from 1988:
> If procedures and functions are verbs and pieces of data are nouns, a procedure-oriented program is organized around verbs and an object-oriented program is organized around nouns. Imagine that you had a program that operated on dogs, mice, and cats. Further, imagine that the program needed to implement eating and running methods for the dogs, mice, and cats
> 
> *- Apple Computer (publisher), Programmers Introduction to the Macintosh Family, 1988, p. 142.*

As an example of verb-oriented (procedure-oriented) way of thinking the authors of the mentioned guide presented the following pseudocode:
```
dog = RECORD
mouse = RECORD
cat = RECORD
PROCEDURE Eat(animal)
	IF animal = dog THEN eat this way
	IF animal = mouse THEN eat another way
	IF animal = cat THEN eat a third way
END
PROCEDURE Run(animal)
	IF animal = dog THEN run this way
	IF animal = mouse THEN run another way
	IF animal = cat THEN run a third way
END
```
*- Apple Computer (publisher), op. cit., p. 143.*

While the noun-oriented (object-oriented) program looked like this:
```
dog = OBJECT
	PROCEDURE Eat
	PROCEDURE Run
END
mouse = OBJECT
	PROCEDURE Eat
	PROCEDURE Run
END
cat = OBJECT
	PROCEDURE Eat
	PROCEDURE Run
END
```
*- Apple Computer (publisher), op. cit., p. 143.*
