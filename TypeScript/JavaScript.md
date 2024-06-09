# JavaScript
## Variable declaration:
- `let` - (classic variable, mutable)
- `const` - (constant, can’t be changed)
- `var` - (old-style)

## Data Types:
- `number`: both floats and integers.
  - Special values: `Infinity`, `-Infinity` and `Nan`.
- `BigInt`: to store values larger than 64 bits.
  - To create a BigInt you need to append `n` to the number.
  - Example: `const bigInt = 1234567890123456789012345678901234567890n;`
- `string`: can be surrounded by both `"` and `'` or backticks: `.
- `boolean`
- `null`: reference to a non-existent object.
- `undefined`: value is not assigned yet.
  ```javascript
    let age;
    alert(age); // shows "undefined"
  ```
- `symbol`: creates unique identifiers for objects.
- `object`: reference to an object or instance of a class.

### `typeof`operator
Returns the type of the operand: `typeof 0 // "number"`

## Interaction: alert, prompt, confirm
### Alert
- It shows a message and waits for the user to press “OK”.
- Example: `alert("Hello");`

### Prompt
- It shows a modal window with a text message, an input field for the visitor, and the buttons OK/Cancel.
- Example: `prompt(title, [defaultValue]);`

### Confirm
- The function `confirm` shows a modal window with a `question` and two buttons: OK and Cancel.
- Example: `confirm(question);`

## Type Conversion
Functions and operators automatically convert to the right type.
 - Mathematical operations automatically convert to `number`.

`String(x)` -> Converts x to a string.

`Number(x)` -> Converts x to a number. If the conversion fails we get a `NaN`. Number converts **true into 1** and **false into 0**.

`Boolean(x)`-> Converts x to a boolean. 
- Values that are intuitively “empty”, like `0`, an empty string, `null`, `undefined`, and `NaN`, become **false**.
- Other values become `true`.



## Operators
JS supports all basic operators plus `**` used for exponentiation.

### Exponentiation
The exponentiation operator `a ** b` raises `a` to the power of `b`.
  - b can also be smaller than 1 to have roots.

### String concatenation with `+`
If the binary + is applied to strings, it merges (concatenates) them:
```javascript
let s = "my" + "string";
alert(s); // mystring
```
Note that if any of the operands is a string, then the other one is converted to a string too.
```javascript
alert( '1' + 2 ); // "12"
alert( 2 + '1' ); // "21"
```
### Numeric conversion, unary +
Unary `+` converts the operand to number.
It does the same, think as `Number(...)` but shorter.

### Assignment = returns a value
The assigment operator return the value on the right.

`b = (a = 1) + 1` : here b has value 2.

Assignments can be changed:
```javascript
let a, b, c;

a = b = c = 2 + 2;

alert( a ); // 4
alert( b ); // 4
alert( c ); // 4
```

## Comparison

### String comparison
Strings are compared lexicographically with the usual operators: `<`, `>`, `==`.
It uses the unicode (ASCII) coding for comparison.

### Different types comparison
When comparing different types Javascript converts them to `number`.

Examples:
```javascript
alert( '2' > 1 ); // true, string '2' becomes a number 2
alert( '01' == 1 ); // true, string '01' becomes a number 1
```
```javascript
alert( true == 1 ); // true
alert( false == 0 ); // true
```

### Strict equality
A regular equality check `==` has a problem. It cannot differentiate `0` from `false`.

**A strict equality operator `===` checks the equality without type conversion.**

If `a` and `b` are of different types, then `a === b` immediately returns `false` without an attempt to convert them.

### Null and undefined
The values `null` and `undefined` equal `==` each other and do not equal any other value/

## Conditionals
### Conditional operator: ?
The syntax is: `let result = condition ? value1 : value2;`.

## Logical Operators

### || (OR)
It returns the first `truthy` value or the last value if no `truthy` values are found. It returns the original value of the operand.

### && (AND)
It returns the first `falsy` value or the last value if no `falsy` values are found. It returns the original value of the operand.

### ?? (Nullish coalescing)
The result of `a ?? b` is:

- if `a` is defined, then `a`,
- if `a` isn’t defined, then `b`

`??` returns the first argument if it’s not `null/undefined`. Otherwise, the second one.

The important difference between `OR` and `??` is that:

- `||` returns the first **truthy** value.
- `??` returns the first **defined** value.

## Switch
Case uses **strict equality**.

Syntax example for switch statement:
```javascript
switch(x) {
  case 'value1':  // if (x === 'value1')
    ...
    break;

  case 'value2':  // if (x === 'value2')
    ...
    break;

  default:
    ...
    break;
}
```
## Functions
To define a functions use the `function` keyword.

If a function parameter is not passed it will be automatically assigned as `undefined`.

If a function does not return a value, it returns `undefined`.

### Default value parameters
You can assign a default value to some parameters:
```javascript
function showMessage(from, text = "no text given") {
  alert( from + ": " + text );
}
``` 
Here text has the default value. If it is passed as an argument this default value will be overridden.

### Argument passing
Values passed to a function as parameters are **copied** to its local variables.

### Function expression
A function can be passed around as a normal value.

To write anonymous functions we can use **Function Expressions** like this:
```javascript
let sayHi = function() {
  alert( "Hello" );
};
```
### Function expression vs Function declaration
**Function Declaration** is only visible inside the code block in which it resides.

#### Scope
- **A Function Expression is created when the execution reaches it and is usable only from that moment.**
- **A Function Declaration can be called earlier than it is defined.**

### Arrow functions
Another way to declare functions is with the arrow notation. These are anonymous functions which can be assigned to variables.

Examples:

```javascript
let func = (arg1, arg2, ..., argN) => expression;
```
or with braces
```javascript
let func = (arg1, arg2, ..., argN) => {
  return expression;
};
```

