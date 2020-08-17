**Table of Contents**

- [Javascript: Patterns](#Javascript:-Patterns)
    * [Creational Patterns](#Creational-Patterns)
        + [Class Design Pattern](#Class-Design-Pattern)
        + [Constructor Pattern](#Constructor-Pattern)
        + [Singleton Pattern](#Singleton-Pattern)
        + [Factory Pattern](#Factory-Pattern)
        + [Abstract Factory Pattern](#Abstract-Factory-Pattern)
    * [Structural Patterns](#Structural-Patterns)
        + [Module Pattern](#Module-Pattern)
        + [Mixins Pattern](#Mixins-Pattern)
        + [Facade Pattern](#Facade-Pattern)
        + [Flyweight Pattern](#Flyweight-Pattern)
        + [Decorator Pattern](#Decorator-Pattern)
        + [Model-View-Controller Pattern](#Model-View-Controller-Pattern)
        + [Model-View-Presenter Pattern](#Model-View-Presenter-Pattern)
        + [Model-View-ViewModel Pattern](#Model-View-ViewModel-Pattern)
    * [Behavioral Patterns](#Behavioral-Patterns)
        + [Observer Pattern](#Observer-Pattern)
        + [State Pattern](#State-Pattern)
        + [Chain of Responsibility](#Chain-of-Responsibility)
        + [Iterator Pattern](#Iterator-Pattern)
        + [Strategy Pattern](#Strategy-Pattern)
        + [Memento Pattern](#Memento-Pattern)
        + [Mediator Pattern](#Mediator-Pattern)
        + [Command Pattern](#Command-Pattern)

# Javascript: Patterns

The academic definition is a general, reusable solution to a commonly occurring problem within a given context in software design.

Patterns are split into 3 categories:
1. **Creational** - create new things
2. **Structural** - structure your code
3. **Behavioral** - use for behaviours in code

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

## Structural Patterns
* Organization of your code
* Patterns explored: modules, mixins, facade, flyweight and decorator
* Also patterns that apply to applications at large like MVC, MVP and NVVM.

### Module Pattern
The idea behind using modules is to organize your code in pure functions. So if you have your code to debug, it is much easier to find where the error is. We often use modules too, with the key word import or export.

Example:
```javascript
const calc = () => {
    return 4 * 3
}

export default calc;
```
And now, you can import calc in another javascript file with:
```javascript
import calc from './calc';

const aNumber = calc();
```
The module pattern is used everywhere in our code. Especially if you use any frameworks.

### Mixins Pattern
Mixins are a great way to mix functions and instances of classes after they have been created. In other words you could use mixins to add interesting functions to the car class we created earlier.

Example:
```javascript
//after creating the above car classes, add the following
let carMixin = {
    revEngine() {
        console.log(`The ${this.engine} engine is doing Vroom Vroom!`);
        
    }
}

Object.assign(Car.prototype, carMixin);
const honda = autoManufacturer('car', 'honda');

honda.revEngine(); // The V8 engine is doing Vroom Vrrom!
```
So now we have this mixin or basically the function that we mixed with our class available to us and we can execute it whenever we want.

### Facade Pattern
It is basically the pattern of hiding complexity away by creating a facade for the complex code. When you're building your component in any framework, you code the complexity of this component into a module, or file, and then leverage a simple line to render this component into your code. This is what the facade pattern is.

Example:
```javascript
//refer to the module pattern example.
```
So whenever you're looking at code that is imported from another module, and then insert it into that specific file, this is basically facade pattern.

### Flyweight Pattern
The flyweight pattern is a method to minimize recreating the same items twice, and therefore minimize the memory impact in our systems. Whenever we create new items with our applications, we stack these items into memory. Your browsers uses the flyweight pattern to save images in memory so they don't load twice.
The flyweight pattern uses a similar approach to the singleton. So if we look at the code we've done with the singleton, it is similar.

You can refer to the example of singleton pattern.

So basically, we're preventing the creation of more items into the memory of our browsers, or wherever this application is actually running.

### Decorator Pattern
The decorator pattern is very similar to mixins, where we decorate code with classes or code that came from another area. There is actual syntax in the most recent versions of JavaScript and has been used for a while in TypeScript and is heavily used in Angular code. The purpose of a decorator pattern, like a mixin, is to to take, for example, a class and extended it with other code.

Example: https://www.typescriptlang.org/docs/handbook/decorators.html#decorators

### Model-View-Controller Pattern
This pattern basically defines how an application should be split, and often reflects how your modules are organized within three simple categories, models, views, and controllers. The model is where your data resides, where you define your schemas and the models for your data. The views is where you have your views, or in most cases, the pure HTML of you application, where the visuals are. And finally, the controllers are where you have your logic of your application, the functions that makes your application run.

Model = Data
View = Visuals (HTML)
Controller = Logic

### Model-View-Presenter Pattern
The Model-View-Presenter pattern, which is loosely based on MVC, and almost the same. In MVC, the views have access to both the models and controllers. Where MVP differs is the view doesn't have to access the model. It has to get it from the presenter and the presenter serves as the logic, and supplier of data. It is the major difference.

### Model-View-ViewModel Pattern
The model view view model pattern is similar than the other two we just explored, and is different only in implementation again. It is also sometimes referred to as MVVC, or model view view controller. But in both cases, it serves the same purpose. The first view is your view which doesn't have any data or logic. Then you have the second view, model, which holds the logic in a state of the data, and this view model connects to a model. 

## Behavioral Patterns
* Focussed on the communication between objects
* Similar to implementing better communication between us.
* Some examples will be shown and not implemented due to complexity.

### Observer Pattern
The Observer pattern is one where we maintain a list of objects based on events, and is typically done with updating data based on these events.

Example:
```javascript
class Car {
    constructor(gas) {
        this.gas = gas;
    }

    setGasLevel(val) {
        this.gas = val;
        this.notifyAll();
    }

    register(observer) {
        this.actions.push(observer);
    }

    unregister(observer) {
        this.actions.remove.filter(function(el) {
            return el !== observer;
        });
    }

    notifyAll() {
        return this.actions.forEach(function(el) {
            el.update(this);
        }.bind(this));
    }
}

class consumption {
    update(car) {
        car.gas = car.gas + 1;
    }
}
```
So basically this observer pattern is a way to publish information or objects or collections that we have access to, and then we can subscribe to it, or get that information from the observer, and then have access to all the information available for rooms or players or whatever is the data that you're working with.

### State Pattern
The state pattern is one where we hold the state of the application with all the data and properties needed and when it changes it updates a rendering of the application.

Example:
 If you were to use a chat application, where whenever a true statement turns the color of the fonts of your chat red because somebody is talking to you or typing something well that's a state of the application, and we need data to actually make that happen with the application, and this is how it works, so you have the state, which holds all of the information that you need and then the application reacts based on that, or get the data from the state. So this is what the state pattern is.

###  Chain of Responsibility
The Chain of Responsibility is a pattern to help solve common practical issues of having a request from a client and needing this request to pass through multiple functions or logic to get the result.

Example:
When we hit the Buy button, then the application needs to check if you're logged in, then needs to check if it has your address. If not, add an address. Then it needs to calculate the taxes, shipping, process payment, and finally process the order, and display success message.
So this is where the chain of responsibility comes into play and where we need to create a proper chain so these events occur in a linear way. What we end up with is a request going through an abstract handler which calls one function or handler after another until the chain is completed. When one handler is completed, we can go to the next one. If there are errors, the abstract handler can provide error information to the back end end client, and so on and so forth.

### Iterator Pattern
The iterator pattern is another method of iterating through list of items, whereas the chain of responsibility will use more of a handler type and go through a chain. The iterator is best used with a for loop and is perfect when you want to iterate through rays of objects.

Example:
```javascript
newsfeeds = [
    {
      type: 'top-headlines',
      query: 'sources=bbc-news'
    },
    {
      type: 'everything',
      query: 'domains=techcrunch.com&language=en'
    },
    {
      type: 'technology',
      query: 'domains=comicbookmovie.com&language=en'
    }
]

for (let feed of newsfeeds) {
    console.log(feed.type);
}
```

### Strategy Pattern
The strategy pattern is basically a way to encapsulate different algorithms or functions and then at runtime practically use the same code to run different scenarios.

Example:
```javascript
class Car {
    constructor(doors, engine, color) {
        this.doors = doors;
        this.engine = engine;
        this.color = color;
    }
}

class SUV extends Car {
    constructor(doors, engine, color) {
        super(doors, engine, color);
        this.wheels = 4;
    }
}


const civic = new Car(4, 'V6', 'grey');
const cx5 = new SUV(4, "V8", 'red');

console.log(civic);
console.log(cx5);
```
We're encapsulating code by creating a class, or it could be a function, or it could be anything. And then we're reusing that code multiple times to create new cars or new objects of these cars.

### Memento Pattern
 The memento pattern is basically providing temporary state of an object and restoration of that object from a conversion into a different format or whatnot. It is often used into serialization and deserialization of data

 Example:
 We serialize javascript object to a JSON object for streaming it through HTTP protocols and while receving the response, we might need to deserialize the JSON object back into a JavaScript object for consumption into our application. Well, this is basically the memento pattern in action, where the data never loses its accuracy, despite several conversions in between formats.

 ### Mediator Pattern
 The mediator pattern provides a set of objects which interact with each other, mostly by having a central authority dictating the terms in between objects.

 Example:
 ```javascript
 class TrafficTower {
    constructor() {
        this.airplanes = [];
    }

    requestPositions() {
        return this.airplanes.map(airplane => {
            return airplane.position;
        });
    }
}

class Airplane{
    constructor(position, trafficTower) {
        this.position = position;
        this.trafficTower = trafficTower;
        this.trafficTower.airplanes.push(this);
    }

    requestPositions() {
        return this.trafficTower.requestPositions();
    }
}
 ```

 The mediator pattern provides a set of objects which interact with each other, mostly by having a central authority dictating the terms in between objects.

### Command Pattern
The command pattern is one that encapsulates actions or operations as objects. So in other words, in this pattern you abstract the actual function or execution of the action from the action itself.