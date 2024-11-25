# Part I: A Haskell Primer for Physicists

## Chapter 1: Calculating with Haskell

### **A Kinematics Problem**
A car is accelerating at 0.4 m/s^2 at time t = 0. The car is stationary. How much time will it take to travel 2 meters?

Constant acceleration with position-time equation
x(t) = 1/2a_0t^2 + v(0)t + x()

We use Haskell as our calculator and since we need x(t) = 2 (it's position at 2m).

To enter the Glasgow Haskell Compiler we type ghci into the terminal and press <Enter>
```haskell
ghci> sqrt (2 * 2 / 0.4)
3.1622776601683795
```

The purpose of above is to show Haskell as a calculator

### **Numeric Functions**

Haskell provides many functions you would expect on a calculator. Some common numeric functions:

| Function  | Description   |
| :-------: | :-----------: |
| exp       | exp x = e^x   |
| sqrt      | Square root   |
| abs       | Absolute value |
| log       | Natural logarithm (log base e) |
| sin       | Argument in radians |
| cos       | Argument in radians |
| tan       | Argument in radians |
| asin      | Arcsine (inverse sine) |
| acos      | Arccosine (inverse cosine) |
| atan      | Arctangent (inverse tangent) |
| sinh      | sinh x = (e^x - e^-x) / 2 (hyperbolic sine) |
| cosh      | cosh x = (e^x + e^-x) / 2 (hyperbolic cosine) |
| tanh      | tanh x = sinh(x) / cosh(x) (hyperbolic tangent) |
| asinh     | Hyperbolic Arcsine (inverse hyperbolic sine) |
| acosh     | Hyperbolic Arccosine (inverse hyperbolic cosine) |
| atanh     | Hyperbolic Arctangent (inverse hyperbolic tangent) |

Examples:
```haskell
ghci> log(2)
0.6931471805599453
Prelude> log 2
0.6931471805599453
```
This is a natural log of 2. Haskell doesn't need parentheses because of **functional applications** within the language. This means that the juxtaposition of 2 expressions is taken that the first expression is a function and the second is an argument of that function (like f of x, i.e. f(x)).

Haskell also provides common constants like pi
```haskell
ghci> pi
3.141592653589793
```

Make sure to use parenthesis because of the function application in Haskell. For instance, cos(pi/2) should = 0:
```haskell
ghci> cos pi / 2
-0.5
ghci> cos (pi / 2)
6.123233995736766e-17
ghci> (cos pi) / 2
-0.5
```
You see what's happening here? It's the order of operations. The 6.123233995736766e-17 is as close to 0 as the computer can get when making approximations.

### **Operators**

There are many binary operators -- acting on 2 inputs/arguments -- that produce a result.
- **prefix operator** - Operator placed __before__ it's arguments.
- **postfix operator** - Operator placed __after__ it's arguments.
- **infix operator** - Operator placed __between__ it's arguments.

**Common Operators**
| Operation             | Operator(s) | Precedence | Associativity |
| :-------:             | :---------: | :--------: | :-----------: |
| Composition           |     .     |       9       | Right     |
| Exponentiation        | ^, ^^, ** |       8       | Right     |
| Multiplication/Division| *, /     |       7       | Left      |
| Addition/Subtraction  | +, -      |       6       | Left      |
| List Operators        | :, ++     |       5       | Right     |
| Equality/Inequality   | ==, /=    |       4       |           |
| Comparison            | <, >, <=, >= |    3       |           |
| Logical AND           | &&        |       2       | Right     |
| Logical OR            | &#124;&#124;|     1       | Right     |
| Application           | $         |       0       | Right     |

- Note:
    - The caret operator (^) can only handle non-negative integer exponents.
    - The double caret (^^) can handle any integer exponent.
    - The ** operator can handle any real exponent.
        - It probably makes the most sense to use the ** operator for now.

#### Precedence and Associativity
These are basically the order of operations in Haskell. Right associativity means to apply the rule to the right-most in the operator sequence first. For example, 2 ** 3 ** 2 let's Haskell know that the ** operator takes the last 2 in the sequence and applies it to the 3, making the new sequence 2 ** 9, which equates to 512. A better way to see what's happening here is to use parentheses: 2 ** ( 3 ** 2 ). The right-most operation is completed first!

This differs from left associativity. Consider 8 - 3 - 2. Now that you know what the associativity means, it doesn't take a genius to figure out that this means: (8 - 3) - 2 = 3. The left-most operation is completed first. This would yield in a wrong result if the rightmost operation was completed first 8 - (3 - 2) = 7.

Precedence simply means, do 9 before 8, 8 before 7, etc etc. Precedence and associativity together these are the order of operations in Haskell.

#### The Application Operator
Operator $ serves as a one-symbol parentheses because it basically means, do this last! Take our `cos pi / 2` example from before.
```haskell
ghci> cos pi / 2 -- cos pi has higher precedence, so we get a different result than expected
-0.5
ghci> cos ( pi / 2 ) -- order is right here because we specify the correct way using parentheses
6.123233995736766e-17
ghci> cos $ pi / 2 -- cos pi now has a precedence of 0 (done last), so pi / 2 is done first
6.123233995736766e-17
```

Note: Because $ has right associativity,the function application operator is frequently used in Haskell to make nested applications ( h $ g $ f x ) easier to read.
- h $ g $ f x - h(g(f(x))) - h of g of f of x. Which is easiest to read?

### Functions with 2 Arguments
The only thing to note now is the `logBase` and `atan2` take in 2 arguments. For a deeper dive see below.

Example:
| Function | Example |
|----------|---------|
logBase | logBase 10 100 = 2
atan2 | atan2 1 0 = pi/2

```haskell
ghci> logBase 10 100
2.0
ghci> atan2 1 0
1.5707963267948966
```

- **logBase** - first argument is the base, second is the number we take the log of.
- **atan2** - Remember that there's a circle here, with angles, and 4 quadrants. tan = sin / cos.

| Quadrant | Angle | sin | cos | tan |
| -------- | ----- | --- | --- | --- |
I | 0 < a < pi/2 | + | + | +
II | pi/2 < a < pi | + | - | -
III | pi < a < 3pi/2 | - | - | +
IV | 3pi/2 < a < 2pi | - | + | -

If tan is positive, we can say it's from the 1st or 3rd quadrant vs. negative being 2nd or 4th. So by convention, atan returns an angle from the first/fourth quadrants. In order to get back all the info resulted in the division of sin/cos, we need to look at the values separately. __Walks in `atan2`__, "Somebody say they need 4 quadrants?" in the thickest southern accent you can imagine. `atan2` takes sin and cos and resolves all 4 quadrants by adding pi to the result of `atan` whenever cos is negative.

The atan2(y, x) takes y && x as arguments to project a vector with length v and angle a on the y and x axis.
- y = v * sin(a)
- x = v * cos(a)

which gives the relation
- y/x = tan(a)

Basically `atan(y/x)` holds back info and assumes input from quadrants I or IV, while in contrast `atan2(y,x)` gets all the data and thus can resolve the correct angle.

### Numbers in Haskell
- The minus sign is a unary operator and a binary operator. Since Haskell syntax depends heavily on the consistency of operators, you must specify negation within parentheses.
- Decimal numbers must have a number before and after the decimal point i.e., 0.9 or 1.0, not .9 or 1. (respectively).
- Haskell uses scientific notation with 3.00 x 10^8 being `3.00e8` in Haskell. Very large numbers will be converted to this notation. 8**8 evaluates to 1.6777216e7.

### Approximate Calculations
When the computer approximates, it needs to convert the binary to decimal. Any division by an odd number results in a repeating number in binary.

- 1/ 3 in binary is 0.010101010101010101010101....
- 1/5 in binary is  0.001100110011001100110011....

Example of this approximation:
```haskell
ghci> sqrt 5 ^ 2
5.000000000000001
```
Note: Never do equality checking of numbers when either number has been approximated.

### Errors
- You get a **precedence parsing error** when you multiply 5 by -1
```haskell
ghci> 5 * -1

<interactive>:22:1: error:
    Precedence parsing error
        cannot mix ‘*’ [infixl 7] and prefix `-' [infixl 6] in the same infix expression
```
This is due to not enclosing -1 in parentheses. The Haskell compiler doesn't know how to combine the * and - operators.

- You get a **No instance for Show error** when the Haskell compiler tries to output the value of an inbuilt function.
```haskell
ghci> sqrt

<interactive>:24:1: error:
    • No instance for (Show (Double -> Double))
        arising from a use of ‘print’
        (maybe you haven't applied a function to enough arguments?)
    • In a stmt of an interactive GHCi command: print it
```
The GHCi is saying it doesn't know how to display the value of `sqrt`.

### Help and Quitting
- Type `:help`, or `:h` for help.
- Type `:quit`, or `:q` to quit.
