- Javascript Hoisting refers to the process whereby the <strong>interpreter appears to move the declaration of functions, variables or classes to top of their scope</strong>, prior to the execution of code.

- <strong>Temporal Dead Zone</strong>: The zone between the variable is declared/hoisted and variable is actually assigned.

#### Example 1:

```js
function test() {
  console.log("Value of X is", x)
  var x
}

test()
```

<details>
<summary>Solution</summary>

```js
// undefined
```

</details>

---

#### Example 2:

```js
function test() {
  console.log("Value of X is", x)
  var x = 60
}

test()
```

<details>
<summary>Solution</summary>

```js
// undefined

// Reason: Only variable declartion is moved to top and by default value is undefined
```

</details>

---

#### Example 3:

```js
function test() {
  console.log("Value of X is", x)
  let x = 60
}

test()
```

<details>
<summary>Solution</summary>

```js
// ReferenceError: Cannot access 'x' before initialization

// Reason: This goes into a state called Temporal Dead Zone
```

</details>

---

#### Example 4:

```js
function test() {
  console.log("Value of X is", x);
  const x;
}

test();
```

<details>
<summary>Solution</summary>

```js
// SyntaxError: Missing initializer in const declaration

// Reason: We cannot declare a const variable without initializing it.
```

</details>

---

#### Example 5:

```js
function test() {
  console.log("Value of X is", x)
  const x = 10
}

test()
```

<details>
<summary>Solution</summary>

```js
// ReferenceError: Cannot access 'x' before initialization.

// Reason: Temporal Dead Zone (Default value is not initialized)
```

</details>

---

#### Example 6:

```js
function test() {
  var x = 10
  var x
  console.log("X is " + x)
}
test()
```

<details>
<summary>Solution</summary>

```js
// 10
// Reason: second line of var x point to the old var x value that is stored in the memory and it prints the old value instead of undefined.
```

</details>

---

#### Example 7:

```js
function varTest() {
  var x = 1
  {
    var x = 2
    console.log(x)
  }
  console.log(x)
}

varTest()
```

<details>
<summary>Solution</summary>

```js
// 2 2
// Reason:

- variable created with var instance will be created only once and redeclaring is allowed inside the block.

- There is only one instance of variable x and as the last variable declaration points to value 2. It will print 2 twice.
```

</details>

---

#### Example 8:

```js
function letTest() {
  let x = 1
  {
    let x = 2
    console.log(x)
  }
  console.log(x)
}

letTest()
```

<details>
<summary>Solution</summary>

```js
// 2 1
// Reason:

- variable created with let instance will have lexical scope/block scope.

- A separate execution context gets created for a block and let x=2 will be destroyed post the end of the block end tag

- The second console.log prints 1 because due to scope chain concept.

```

</details>

---

#### Example 9:

```js
function letTest() {
  let x = 1
  let x = 2
  console.log(x)
  console.log(x)
}

letTest()
```

<details>
<summary>Solution</summary>

```js
// SyntaxError: Identifier 'x' is already been declared.
// Reason:

- variables declared with let cannot be re-declared but can be re-assigned.

```

</details>

---

#### Example 10:

```js
function do_something() {
  console.log(bar)
  var bar = 111
  console.log(bar)
}
```

<details>
<summary>Solution</summary>

```js
// undefined
// 111

Reason:

- var declarations are moved to top for var keyword and the default value is undefined.

- After var is assigned with the value, var will print with that assigned value (ex: 111)

```

</details>

---

#### Example 11:

```js
var rate = 10
function getRate() {
  if (rate === undefined) {
    var rate = 6
    return rate
  } else {
    return 10
  }
}
console.log("Rate is", getRate())
```

<details>
<summary>Solution</summary>

```js
// 6

Reason:

- as var rate=6 is inside the if block, var declaration will be moved to top (before if conditon) as per Hoisting and it holds undefined value

- var declarations are moved to top for var keyword and the default value is undefined and it satisfies the if condition and returns 6.

- When the global scope and local scope variable has same naming convention (local scope variable will be given priority)

- Above is the reason why rate=10 value not being considered here.
```

</details>

---

#### Example 12:

```js
var rat = 10
function getRate() {
  if (rat === undefined) {
    var rate = 6
    return rate
  } else {
    return 10
  }
}
console.log("Rate is", getRate())
```

<details>
<summary>Solution</summary>

```js
// 10

Reason:

- rat holds the value of 10 and it satisfies the else condition and returns 10.
```

</details>

---

#### Example 13:

```js
{
  const func = () => console.log(letVar)
  let letVar = 3
  func()
}
```

<details>
<summary>Solution</summary>

```js
// 3

Reason: Before the func() was invoked, the letVar was initialized

```

</details>

---

Q1) Where the Temporal Dead Zone starts?

<details>
<summary>Solution</summary>

#### It starts at the top of the block

<img width="394" alt="image" src="https://user-images.githubusercontent.com/42731246/212748085-e28a14d2-b8ce-4a24-af26-7c8c1cacadc9.png">

</details>

---

Q2) Where is the actual Temporal Dead Zone?

<details>
<summary>Solution</summary>

### Just before the value is got initialized

<img width="395" alt="image" src="https://user-images.githubusercontent.com/42731246/212748585-5faa8c87-5424-4736-9c0f-bff966c33c14.png">

</details>

---

Q3) Where is the Temporal Dead Zone ends?

<details>
<summary>Solution</summary>

### It ends when the value is initialize

<img width="395" alt="image" src="https://user-images.githubusercontent.com/42731246/212748338-7044604d-f876-4106-8732-c128854f5429.png">

</details>

---

#### Example 14:

```js
{
  func()
  const func = () => console.log(letVar)
  let letVar = 3
}
```

<details>
<summary>Solution</summary>

```js
// ReferenceError: Cannot access 'func' before initialization

Reason: function is declared with const keyword and also it is a arrow function whereas the arrow functions are not hoisted

```

</details>

---

#### Example 15:

```js
{
  const func = () => console.log(letVar)
  func()
  let letVar = 3
}
```

<details>
<summary>Solution</summary>

```js
// ReferenceError: Cannot access 'letVar' before initialization
```

</details>

---
