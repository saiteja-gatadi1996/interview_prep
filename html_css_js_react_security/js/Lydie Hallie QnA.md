## Below all are from Lydie Hallie Interview Questions Website

##### Hoisting:

For the variable with the var keyword the memory space is set up during the creation phase with the default value of undefined (until we actually get to the line where we define the variable it holds the undefined value)

Variables with the (let and const) are hoisted, but unlike var, don't get initialized. They are not accessible before the line we declare (initialize) them. This is called the "temporal dead zone". When we try to access the variables before they are declared, JavaScript throws a ReferenceError.

---

##### JS Engine Execution

Because of the event queue in JavaScript, the setTimeout callback function is called after the loop has been executed. If the variable i was declared using the var keyword, this value is global. During the loop, we incremented the value of i by 1 each time, using the unary operator ++. By the time the setTimeout callback function was invoked, i was equal to the number which we provide (ex: 3)

In the second loop, the variable i was declared using the let keyword: variables declared with the let (and const) keyword are block-scoped (a block is anything between { }). During each iteration, i will have a new value, and each value is scoped inside the loop.

---

##### this keyword

With arrow functions, this keyword refers to its current surrounding scope (window for example), unlike regular functions! .

---

##### Object Keys

In JavaScript, all object keys are strings (unless it's a Symbol). Even though we might not type them as strings, they are always converted into strings under the hood.

###### When we use bracket notation, first it evaluates the expression inside the bracket for example like below

mouse[bird.size]: First it evaluates bird.size

However, with dot notation, this doesn't happen. (ex: mouse.bird.size)

##### Object References

In JavaScript, all objects interact by reference when setting them equal to each other. (When you change one object, you change all of them)

![image](https://user-images.githubusercontent.com/42731246/181526317-6efcb118-418a-4984-a7fc-64da4edc64d9.png)

Ex:

```js
let c = { greeting: 'Hey!' }
let d

d = c //setting them equal to each other
c.greeting = 'Hello'
console.log(d.greeting)
```

---

##### new Number()

new Number() is a built-in function constructor. Although it looks like a number, it's not really a number: it has a bunch of extra features and is an object.

When we use the == operator (number with new Number()), it only checks whether it has the same value, so it returns true.

However, when we use the === operator, both value and type should be the same (number with new Number()).

###### new Number() is not a number, it's an object.

Ex:

```js
let a = 3
let b = new Number(3)
let c = 3

console.log(a == b)
console.log(a === b)
console.log(b === c)
```

---

##### static methods

Static methods are designed to live only on the constructor in which they are created, and cannot be passed down to any children or called upon class instances.

---

##### Functions are Objects

In JavaScript, because functions are objects! (Everything besides primitive types are objects). A function is a special type of object.

---

##### new Keyword

i) When using new, (this keyword) refers to the new empty object we create.
ii) If we don't add new, (this keyword) refers to the global object!

---

##### 3 phases of event propagation?

i) Capturing phase : The event goes through the ancestor elements down to the target element

ii) Target Phase: The event itself

iii) Bubbling Phase: The event goes from the target element to the ancestor element

###### Capturing > Target > Bubbling

![image](https://user-images.githubusercontent.com/42731246/181568084-138ffa36-93fb-4a16-bf3f-e85bef599c4a.png)

---

##### Does all Objects have Prototypes ?

###### All objects have prototypes, except for the base object.

###### The base object is the object created by the user, or an object that is created using the new keyword.

The base object has access to some methods and properties, such as .toString. This is the reason why you can use built-in JavaScript methods! All of such methods are available on the prototype. Although JavaScript can't find it directly on your object, it goes down the prototype chain and finds it there, which makes it accessible for you.
