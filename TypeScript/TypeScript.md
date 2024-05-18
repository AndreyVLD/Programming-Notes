# TypeScript
JavaScript but with types

## Data Types:
- `number`: both floats and integers
  - Special values: `Infinity`, `-Infinity` and `Nan`
- 
## Functions
- `function` keyword for declaring functions.
- `export` keyword used for declaring public functions that can be accessed from outside the current file.
- `default` keyword is used for marking the default function used when importing a `.ts` file. Only **one** default function allowed per file.

### Optional parameter
-  Append `?` to function parameter type marks that parameter as optional. Meaning it does not have to be supplied to be able to call the function.

## f-strings
- To embed variables inside some string use `${var}`.
- For example: `"Cool ${title}"`

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