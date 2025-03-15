# JavaScript Refresher

React is obviously very heavy on JavaScript, but a lot of is also CSS and (kind of) HTML. This goes over the bare minimum amount of JavaScript you'll need to understand, or at least recognize, to write some basic, stateless components.

## Arrow Functions

There a handful of ways to write functions in JavaScript, but React tends to use the `arrow function`. A traditional JavaScript function looks something like:

```js
function sayHello() {
    console.log("Hello world")
}

sayHello();
// Hello World
```

This same function in React would instead be:

```js
const sayHello = () => console.log("Hello world");

sayHello();
// Hello world
```

Here, we're declaring ***sayHello*** as a variable, equalling it to `()`, which is how we designate something as a function, then using a fat arrow, `=>`, to declare what the function should do. There is a difference in execution between a regular function and an arrow function, but it's harder to explain than it is to just get used to using the arrow function.

The ***sayHello*** function also include three important aspects of functions: parameters / arguments, functions calling other functions, and dot notation.

## Parameters / Arguments

Functions are like mini-factories that (almost) always create something new when they're executed. Parameters, sometimes called arguments, are things that you can put into a function before it's executed to influence the output.

```js
const multiplyNumbers = (x, y) => x * y;

multiplyNumbers(8, 3);
// 24

multiplyNumbers(6, -9);
// -54
```

The function takes in two values, the first one that we call "x" and the second one we call "y", and those two values are multiplied.

## Functions Inside Functions

You may have noticed in ***sayHello***, that console.log() is itself a function, and that it's taking in the "Hello world" string as a parameter. This will be important down the line, as components themselves are functions, and there are several functions you can put inside components to help build them better.

## Objects and Arrays

The two most common list elements in JavaScript are `arrays` and `objects`.

### Arrays

An array is a simple collection of items, stored in brackets and separated by commas.

```js
const numbers = [1, 2, 3, 4, 5];
```

Arrays are `zero-indexed`, in that each element is numbered depending on their order in the array, and that the first number isn't 1, but 0. You can access the index of an array with `array[index]`:

```js
const numbers = [1, 2, 3, 4, 5];

numbers[0];
// 1

numbers[1];
// 2

numbers[3];
// 4
```

### Objects

An `object` is like an array, but instead of default numeric indexes, the items are indexed in `key/value pairs`:

```js
const exampleObject = {
    key: "value"
}
```

A key's value can also be a function, and those functions are called `methods`.

### Dot Notation

You can access the items from an object in the same way you can arrays:

```js
exampleObject[key];
// "value";
```

But the easier, and more standard way of accessing the item is with `dot notation`.

```js
exampleObject.key;
// "value"
```

Every item in JavaScript is technically an object, you'll see dot notation everywhere - such as *console.log()* - which is console executing its log method.

### Map

Because every item in JavaScript is an object, this means that even arrays are objects. There's a standard, master array called `Array` that has several prototype methods. You don't need to know exactly how it works, just know that because of this, every array that you make has a handful of built-in methods you can use. The most important one to React is the `map()` method.

Let's resuse the ***multiplyNumbers*** function from earlier and our ***numbers*** array.

```js
const multiplyNumbers = (x, y) => x * y;

const numbers = [1, 2, 3, 4, 5];
```

The ***map()*** method uses an existing array to create a new one. It does this by executing a specified function on the first item of the original array, then putting that value as the first item of the new array. Then it executes the same function on the second item of the original array, and puts that result as the second item of the new array, and so on until it's gone through all of the original items.

So if we want to multiply every number in ***numbers*** by 4:

```js
const quadruple = (nums) => nums.map(x => multiplyNumbers(x, 4));

quadruple(numbers);
// [4, 8, 12, 16, 20]
```

An important feature of the map method is that it lets you access the indexes of each item as well. You'll often see it named "id", "i", "idx", "index", or something similar. Just note that if you want to use more than one variable in your map fuction, you need to wrap them both in parantheses first

```js
const indexArray = [
    "This string is index #", "This string is index #", "This string is index #"
]

const wrongFormat = indexArray.map(x, i => x + i);
// Uncaught ReferenceError: x is not defined

const correctFormat = indexArray.map((x, i) => x + i);
// ['This is index #0', 'This is index #1', 'This is index #2']
```

## Destructuring

This looks complicated at first, but it's actually really simple and very convenient. It works with both objects and arrays, but they're handled slightly differently.

### Array Destructuring

Say we wanted to take all the numbers out of ***numbers*** and make them each a variable. Initially, we'd have to do it one at a time:

```js
const numbers = [1, 2, 3, 4, 5];

const one = numbers[0];
const two = numbers[1];
const three = numbers[2];
const four = numbers[3];
const five = numbers[4];
```

But what we can do instead is `destructure` the array multiple variables.

```js
const [one, two, three, four, five] = numbers;

one;
// 1

two;
// 2

four;
// 4
```

Think of it sort of like algebra, if you write ***numbers*** out as its actual value instead of the variable name, it looks like:

```js
[one, two, three, four, five] = [1, 2, 3, 4, 5]
```

If these two arrays are the same values, then the first index of the array on the left should equal the first index of the array on the right, and same with the second, third, etc.

Because you're creating a completely new variable, you can name it whatever you want, but be careful or you'll have very confusing variable names:

```js
const numbers = [1, 2, 3];

const [four, seven, blue] = numbers;

four;
// 1

seven;
// 2

blue;
// 3
```

### Object Destructuring

Destructuring objects is a lot more straightforward, but less flexible. Unlike array destructuring where you choose your own variable names, destructuring an object is extracting a key from your object, and making that key a standalone variable. For example, the ***console.log()*** method we've been using can be destructured:

```js
const { log } = console;

log("Hello world");
// 'Hello world'
```

This is incredibly common in React, as we'll be pulling from several libraries, and libraries are typically stored as objects:

```js
import { Link } from "react-router-dom"
```

We'll go over exactly what the above code means later on, but you can see it's extracting the `Link` key from the React router dom object, and allowing you to use it as a standalone variable.

## Template Literals

Strings can run into some issues in JavaScript, as they can be designated with double quotes, or single quotes.

```js
const doubleQuote = "This is a valid string";

const singleQuote = 'This is also a valid string';
```

However, we can run into issues when the strings themselves include quotes in them:

```js
const badString = "And then he said "This breaks the string format.";
```
```js
const alsoBadString = 'You can't write strings like this.';
```

But if you use the backticks just below the esc key, everything you put inside the ticks will be converted to a string.

```js
const goodString = `My professor told me, "There's no easier way to write JavaScirpt strings.";
```

You can technically use escape characters within strings with regular quotes, but there's absolutely no downside to using the backticks, so it's best to go with them.

However, the real benefit of template literals is that you can execute JavaScript inside of strings, dynamically creating values:

```js
const person = {
    name: "Mark",
    age: 30,
    job: "programmer"
}

const { name, age, job } = person;

const greeting = `Hello, my name is ${name}, and I'm a ${age} year old ${job}.`;

greeting;
// 'Hello, my name is Mark, and I'm a 30 year old programmer.'
```

In addition to variables, you can also perform actual JavaScript functions inside the `${}` breakaway:

```js
const dynamicAdd = `2 + 2 = ${2 + 2}`;

dynamicAdd;
// '2 + 2 = 4'

const dynamicMultiply = `4 * 3 = ${multiplyNumbers(4, 3)}`;

dynamicMultiply;
// '4 * 3 = 12'
```

## Ternary Operator

JavaScript `if-else` conditions are relatively straightfoward:

```js
if (condition === true) {
    excuteFunction();
} else { // condition === false
    executeDifferentFunction();   
}
```

For the `if` block, you want to set up a JavaScript statement that is either true (or *truthy*) or false (or *falsey*, more on those later), and if it's true, execute the function you have in mind. If the initial condition isn't true, you have a backup behavior you want to execute in its place.

```js
const isEven = (number) => {
    if (number % 2 === 0) { // modulo operator, divides the number by 2 and returns the remainder
        return `${number} is even`;
        
    } else {
        return `${number} is odd`;
    }
}
```

In modern JavaScript, especially React, this is abbreviated with a `ternary operator`.

```js
const isEven = (number) => number % 2 === 0 ? `${number} is even` : `${number} is odd`;
```

This looks confusing, but ultimately it breaks down into:

```js
conditon ? trueCondition : falseCondition
```

The question mark indicates the end of the true/false condition, and the colon splits the two possible outcomes. If the condition is true, it executes the first function on the left of the colon, if it's false, the function on the right.

### Truthy / Falsey

Both `true` and `false` are booleans, which is a data type in JavaScript, but we can use conditionals to for statements that don't cleanly translate into exactly true or exactly false. For example, every string, except for an empty string, will successfully pass a "true" condition.

```js
"" ? true : false;
// false

"a" ? true : false;
// true
```

A string isn't "true" in the literal sense, a boolean is a data type and a string is a completely data type, but because there's some kind of content, JavaScript conditionals treat strings the same way they treat **true**. Values like this that act as **true** without literally being **true** are called "truthy", and "falsey" works the same with **false**. 

This is used a lot in React, because components create different values based on the state of your app. For example, if your app supports users logging in:

```jsx
const LandingPage = ({ user }) => {
    return (
        {
            user
            ? <h1> Welcome Back {user.name} </h1>
            : <h1> Please Log In or Sign Up </h1>
        }
    )
}
```

You can have logic in your app to create a "user" object upon someone logging in or signing up, and have the LandingPage component display either way. The absence of a value is treated the same as a **false** value, so if the user is logged in, the landing page has a "user" object and displays its "name" key, but if there is no user, if defaults to the generic message.
