# TypeScript
JavaScript but with types

## Data Types:
- `number`: both floats and integers.
  - Special values: `Infinity`, `-Infinity` and `Nan`.
- `BigInt`: to store values larger than 64 bits.
  - To create a BigInt you need to append `n` to the number.
  - Example: `const bigInt = 1234567890123456789012345678901234567890n;`
- `string`: can be surrounded by both `"` and `'` or backticks.
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
## Functions
- `function` keyword for declaring functions.
- `export` keyword used for declaring public functions that can be accessed from outside the current file.
- `default` keyword is used for marking the default function used when importing a `.ts` file. Only **one** default function allowed per file.

### Optional parameter
-  Append `?` to function parameter type marks that parameter as optional. Meaning it does not have to be supplied to be able to call the function.

## f-strings
- To embed variables inside some string use `${var}`.
- For example: `'Cool ${title}'` but you need to use backticks: `.

## Displaying uploaded Data
- To display data that the user submitted through a form use: `URL.createObjectURL`. This will create a local URL for the File or Image and you can use that in the `src`.
  
## Composite types
- To define the type of object we can use `type` or `interface` and pass that as generic type.
- Example: This is an object that contains 2 fields: `person` and `clothing` that are either a `File` or `null` type.
```TypeScript
type ImageFileState = {
  person: File | null;
  clothing: File | null;
}
```