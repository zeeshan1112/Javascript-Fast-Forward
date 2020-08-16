# Javascript: Patterns

The academic definition is a general, reusable solution to a commonly occurring problem within a given context in software design.

Patterns are split into 3 categories:
1. Creational - create new things
2. Structural - structure your code
3. Behavioral - use for behaviours in code

#### What is a callback and its role?
In its simplest terms, a callback function is a function that is called inside of another function. In other words, whenever you pass a function in the arguments and run it inside the function, you're doing the callback pattern.

Example:
```javascript
const calc = () => {
    return 4 * 4;
}

const printCalc = (callback) => {
    console.log(callback());
}

printCalc(calc); //should print 16 
```
## Creational Patterns
* Control creation process of an object
* Applicable to many languages
* Patterns explored - classes, constructor, singleton, factory & abstract factory

### Class Design Pattern
The prototype class pattern allows us to define a blueprint for a specific type of item, and then reuse it by creating a new object from that class.

Example:
```javascript
class Car {
    constructor(doors, engine, color) {
        this.doors = doors;
        this.engine = engine;
        this.color = color;
    }
}

const civic = new Car(4, 'V6', 'grey');
console.log(civic);
```
So this is how you use a class to create a new object. And basically the class is the prototype or the blueprint for that new object.

### Constructor Pattern
Similar to the class prototype pattern, the constructor pattern is one step further from the class pattern, where we leverage a class created to create an extended class from it.

Example:
```javascript
class SUV extends Car {
    constructor(doors, engine, color) {
        super(doors, engine, color);
        this.wheels = 4;
    }
}

const cx5 = new SUV(4, "V8", 'red');
console.log(cx5);
```
So when you want to create multiple sub-categories of a class, the constructor pattern is a great way to do it.

### Singleton Pattern
In singleton pattern, we allow only one instance of the class to be created.

Example:
```javascript
let instance = null;

class Car {
    constructor(doors, engine, color) {
        if (!instance) {
            this.doors = doors;
            this.engine = engine;
            this.color = color;
            instance = this;        
        } else {
            return instance;
        }
    }
}
const civic = new Car(4, 'V6', 'grey');
const honda = new Car(2, "V8", 'red');

console.log(civic);
console.log(honda); //civic instance will be returned
```
And as you can see, we've already created an instance of that car, therefore, it's going to return the same instance. So, basically what it does, it checks for instance of that class car and if there's already one, then just return the instance that we have.

### Factory Pattern
The factory pattern is great when you want to create, say, a mechanism to create other objects. This can be useful when you want a factory to handle most of your classes and then simply use this factory method to create your new objects.

Example:
```javascript
class Car {
    constructor(doors, engine, color) {
        this.doors = doors;
        this.engine = engine;
        this.color = color;   
    }
}

class carFactory {
    createCar(type) {
        switch(type) {
            case 'civic':
                return new Car(4, 'V6', 'grey')
            case 'honda':
                return new Car(2, "V8", 'red')
        }
    }
}

const factory = new carFactory();
const myHonda = factory.createCar('honda');

console.log(myHonda);
```
So basically factory is creating multiple classes for us automatically based on the type that we're passing to that factory. This is very efficient in big, large applications where you want to quickly create new objects through a factory or one function where you're passing a type and then it create the objects for you. For example, used for users, the types of users that you want to create in an application.

### Abstract Factory Pattern

In Abstract factory Pattern, you are able to create multiple factories, classes et cetera.

Example:
```javascript
class Car {
    constructor(doors, engine, color) {
        this.doors = doors;
        this.engine = engine;
        this.color = color;   
    }
}

class CarFactory {
    createCar(type) {
        switch(type) {
            case 'civic':
                return new Car(4, 'V6', 'grey')
            case 'honda':
                return new Car(2, "V8", 'red')
        }
    }
}

class SUV {
    constructor(doors, engine, color) {
        this.doors = doors;
        this.engine = engine;
        this.color = color;   
    }
}

class SuvFactory {
    createCar(type) {
        switch(type) {
            case 'cx5':
                return new Car(4, 'V6', 'grey')
            case 'sante fe':
                return new Car(2, "V8", 'red')
        }
    }
}

const carFactory = new CarFactory();
const suvFactory = new SuvFactory();

const autoManufacturer = (type, model) => {
    switch(type) {
        case 'car':
            return carFactory.createCar(model);
        case 'suv':
            return suvFactory.createCar(model);
    }
}

const cx5 = autoManufacturer('suv', 'cx5');

console.log(cx5);
```
In the above example, we've created a SUV which was CX5 and we create a CX5, which has four doors, V6 in gray. And this is basically how you would use an abstract factory to create a whole bunch of cars.