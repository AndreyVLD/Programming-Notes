# JavaScript

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

`Number(x)` -> Converts x to a number. If the conversion fails we get a `NaN`.

`Boolean(x)`-> Converts x to a boolean. 
- Values that are intuitively “empty”, like `0`, an empty string, `null`, `undefined`, and `NaN`, become **false**.
- Other values become `true`.

Number converts **true into 1** and **false into 0**.

