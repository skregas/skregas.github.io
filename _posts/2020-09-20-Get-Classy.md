---
layout: post
title: "Becoming Flutter: Time to Get Classy"
tags: [flutter, ui, mobile, learning, class, objects]
---

Exploring the idea that I need to use a class for the cards in the deck, and perhaps even a class for the card deck itself. Why? so the flipped state can be set on individual objects, even while they are part of a larger container (List, card deck, etc).

Thus, the recent lessons have been on the use of classes in Flutter. As you might expect, the idea behind classes and the syntax is quite similar to other programming languages. If you have some expereince with OOP (Object-Oriented Programming) in another language, this content will feel familiar to you.

Starting off, good design principles suggest defining new classes in their own seperate files. In Flutter case, we have `lib/main.dart` as the location dfor the entry point for our app. And that's where we want to put new class. Make a new file in this location, using the name of the class, in lowercase, for the name of the file. In my case, `lib/card.dart`

On to defining the class itself. Open up the new file in your favorite editor and start the class definition with the keyword `class`. Again, `class` is a reserved word with special meaning to Flutter. It tells the compiler, 'Hey, this declares a class I intend to use later on'

Following the `class` keyword is the name of the class itself. Make this descriptive, usually a noun. Use CamelCase for multiple words. Follow the class name with open and close curly brackets, `{}`. The body of the class will go inside these brackets.

The benefit of using classes is to bundle data and functions together in something called an **_object_**. When an object gets created, it is called an **_instance_** of a class. For example, use a Car class to create a Car object called myCar. myCar would then be an _instance_ of Car.
```
class Car {
    void drive() {
        print("wheels turning");
    }
}


//... elsewhere in the code...
// create an object of class Car
Car myCar = Car()
```

#### The Four Pillars of classes

###### Abstraction
This bundling together of data and methods to operate on that data is called **_abstraction_**. The way an object behaves is hidden behind the class definition. Thus, user code can use and pass around an object without caring too much about _how_ it behaves, only that it does what is expected. Using the Car class above as an example, as a user of that class, I would expect it to perform operations like start, accelerate, turn, and stop.



##### Encapsulation
What if you wanted to change something within the class from outside the class. What if the Car class above had only 4 gears and you wanted to add a 5th? You could set a variable, let's call it `numOfGears` equal to 5.
Thing is, you shouldn't be able to change class attributes from outside the class without explicity requesting the class to make the change. We can use _encapsulation_ to achieve this interface, or communication between the class and the outside world. We can start by making variables inside the class private. This means they are only accessable inside the class; any attempts to change private variables will be flagged as an error.
The next step is to provide _getters_ and _setters_. These are methods tha allow access to private class variables. This way, the class defines and controls what it exposes, the user code being none the wiser.


##### Inheritance
You are probably familiar with the idea that humans inherit genes from thier parents; things like eye color, hair color, maybe a personality trait or two. The same is possible in code. Inheritance allows us to define some general piece of functionality, and reuse it in sub-classes, that is classes that _inherit_ from a parent class. Let's go back to the Car example. Car is a generic class. It defines attributes and functions that every car has, like drive, number of seats, number or wheels, etc. But what if we want to produce a different kind of car? We want to avoid writing out the same definitions as the generic Car. That's where inheritance comes in. Our new class, let's call it `ElectricCar` inherits from Car by using the keyword `extend`:

`class ElectricCar extends Car`

This way, we can reuse everything defined in Car, and add new functionality for our ElectricCar. Let's add a battery level and a recharge method:

```
class ElectricCar extends Car {
    int batteryLevel = 100;

    void recharge() {
        batteryLevel = 100;
    }
}

```

Great! Now the electric car can do everything it does without reinventing the attributes and behaviors of a generic car.


##### Polymorphism
[//]: # (Greek: many forms, changing shape)
[//]: # (extends inheritance by customizing the inherited methods)
[//]: # (override parent's behavior, using the best parts, and also
providing  own custom version)

Inheritance is all well and good. We get lots of good traits from our parents and anscestors, and we get lots of things we may like to change, or we simply improve upon what our parents could do. We can do the same thing in code. Changing the behavior of inherited methods in a child class is called _polymorphism_, from the Greek meaning "many forms", or "changing shapes". We can change the form or the shape of a child class to customize and improve it.

Using our Car class once again, let's see how this works. Our Car class provides some generic car basics, but we want a self-driving car. So we can inherit the drive method, but we also want the car to steer for us, to our intended destination. We want to customize the drive method to include this new behavior.

```
car SelfDrivingCar extends Car {
    String destination;

    @override
    void drive() {
        super.drive()

        print("steering towards $destination");
    }

    SelfDrivingCar(String userSetDestination) {
        destination = userSetDestination;
    }
}

```
Let's look at what's happening here. We inherit from Car as before, so we can use the drive method. But this time, we use the the '@' symbol with the keyword `override` to change the method for our needs. Then, we call the parent drive method using the keyword `super`

We also defined a new variable `destination`. This stores where we want the car to go. This variable is used in the constructor, when we create a new SelfDrivingCar:

`SelfDrivingCar myAuto = SelfDrivingCar("1 Infinite Loop")`

Now the myAuto knows where to go!. Because we inherited the drive method, all we have to do is:

`myAuto.drive()`

and the wheels will turn, and the car will steer towards the destination.

-----
Returning to the card deck app, I've split out the individual cards and the deck into their own files and classes:
> myCard.dart -> MyCard class
>
> cardDeck.dart -> CardDeck class. Contains and manages a collection of myCards

I need to modify the CoverFlow widget to recognize the card deck. Tapping each card _should_ result in only that card flipping. Still learning, still learning.

UPDATE: With some modifications (removing the redundant myCard class), each card now flips independently of the other cards. Yes!

Now on to testing, fix what breaks, and continue the journey.
Thanks for reading! Take a deep breath, a break from the desk, and stay real.
