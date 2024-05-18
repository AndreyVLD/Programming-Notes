# C#
## Functions
### Optional parameters
Syntax for **optional params**: `paramType param = value`.
If the parameter is omitted in the call the default value will be used.
```C
static void YourMethod(string message, string punctuation = ".")
{
    ...body...
}
```
### Positional arguments and named arguments

Syntax for **named arguments** call: `argumetName : value`
- `YourMethodName(d: 4, b: 1, a: 2);`

Positional arguments (usual arguments) come **before** the named arguments.
Useful when having lots of optional arguments.

### `out` keyword
The `out` keyword is used to pass variables by reference. The mutation inside the function to that variable will persist after the call. `out` is prefixed both in signature and call. 
- `public static bool TryParse (string s, out int result);`    - >    method signature
- `bool success = Int32.TryParse("10602", out int number);`    ->     method call

### Lambda
C# Supports higher oreder functions and anonymous functions with **lambdas**.
Lambdas are creating with `=>`: `bool isEven(int num) =>num % 2 == 0;`.

They can be passed anonymously to higher order functions.

Lambda Shortucts:
	- We can remove the parameter type if it can be inferred.
	- We can remove the parentheses if there is one parameter.
### `foreach`
Syntax `foreach`: `foreach(type varName in collection)`

## Classes
Very similar to Java classes so we skip the basics.

### Properties
- Classes properties are used to define constraints for a given field.
- Properties are defined as common fields but with capital letter by convention. 
- Properties have 2 methods: `get` and `set`.
- Example:
```C#
public class TimePeriod
{
    private double _seconds;

    public double Hours
    {
        get { return _seconds / 3600; }
        set
        {
            if (value < 0 || value > 24)
                throw new ArgumentOutOfRangeException(nameof(value),
                      "The valid range is between 0 and 24.");

            _seconds = value * 3600;
        }
    }
}
```
- Usage:
  - If we call `object.Hours` we execute the `get`.
  - If we mutate the property Hours: `object.Hours = num` the `set` is called with `value` variable being equal to `num`.

- Automatically implement properties. This properties only return and set values:

```C#
public class SaleItem
{
    public string Name
    { get; set; }

    public decimal Price
    { get; set; }
}
```
### Inheritance
- Inheritance is done with the following syntax: `ChidClass : Parent`
- To access the super class you use `base`. To access the super class constructor you use `base()`.
- The super class constructor must be called before the child class constructor. Thefore we have the following example:
- Constructors have the same name as the classname and need to be `public` with no return type.
```C#
public InterestEarningAccount(string name, decimal initialBalance) : base(name, initialBalance)
{

}
```
Here  `public InterestEarningAccount` is the constructor of the child class.

#### Virtual vs Abstract
- Is used to define functions that can be overriden by the child.
- For **abstract** the functions **MUST** be overriden but for **virtual** you can override or not.
- `public virtual/abstract void PerformMonthEndTransactions() { }`

### Override
- Used to declare a function that overrides one of the parrent functions.
- `public override void PerformMonthEndTransactions() { }`

