# math-as-code

This is a reference to ease developers into mathematical notation using C#, this project is based on [Math-As-Code](https://github.com/Experience-Monks/math-as-code)

# contents

- [Variable naming conventions](#variable-name-conventions)
- [Equality, equivalence and similarity $=$ $≈$ $≠$ $:=$](#equals-symbols)
- [square root and complex numbers $√$ $i$](#square-root-and-complex-numbers)
- [dot & cross $·$ $×$ $∘$](#dot--cross)
  - [scalar multiplication](#scalar-multiplication)
  - [vector multiplication](#vector-multiplication)
  - [dot product](#dot-product)
  - [cross product](#cross-product)
- [sigma `Σ`](#sigma) - *summation*
- [capital Pi `Π`](#capital-pi) - *products of sequences*
- [pipes `||`](#pipes)
  - [absolute value](#absolute-value)
  - [Euclidean norm](#euclidean-norm)
  - [determinant](#determinant)
- [hat **`â`**](#hat) - *unit vector*
- ["element of" `∈` `∉`](#element)
- [common number sets `ℝ` `ℤ` `ℚ` `ℕ`](#common-number-sets)
- [function `ƒ`](#function)
  - [piecewise function](#piecewise-function)
  - [common functions](#common-functions)
  - [function notation `↦` `→`](#function-notation)
- [prime `′`](#prime)
- [floor & ceiling `⌊` `⌉`](#floor--ceiling)
- [arrows](#arrows)
  - [material implication `⇒` `→`](#material-implication)
  - [equality `<` `≥` `≫`](#equality)
  - [conjunction & disjunction `∧` `∨`](#conjunction--disjunction)
- [logical negation `¬` `~` `!`](#logical-negation)
- [intervals](#intervals)
- [more...](#more)

## Variable naming conventions

There are a variety of naming conventions depending on the context and field of study, and they are not always consistent. However, in some of the literature you may find variable names to follow a pattern like so:

- *s* - italic lowercase letters for scalars (e.g. a number)
- **x** - bold lowercase letters for vectors (e.g. a 2D point)
- **A** - bold uppercase letters for matrices (e.g. a 3D transformation)
- *θ* - italic lowercase Greek letters for constants and special variables (e.g. [polar angle *θ*, *theta*](https://en.wikipedia.org/wiki/Spherical_coordinate_system))

This will also be the format of this guide.

## Equality, equivalence and similarity

There are a number of symbols resembling the equals sign `=`. Here are a few common examples:

- $=$ is for equality (values are the same, e.g. $x = 2$)
- $≠$ is for inequality (value are not the same, e.g. $x ≠ 3$)
- $≈$ is for approximately equal to (e.g. $π ≈ 3.14159$)
- $:=$, $=:$, $≝$ are for definition (A is defined as B, e.g. $ x:=2kj $)

The corresponding translation in C# of those symbols is the following:

```csharp
// equality
x == 2;

// inequality
x != 3;

// approximately equal
ApproximatelyEqual(Math.PI, 3.14159d, 1e-5d);

public static bool ApproximatelyEqual(double a, double b, double epsilon) => System.Math.Abs(a - b) < epsilon ;

// definition of variable and expression
var x = (int k, int j) => 2 * k * j;
```

## Arithmetic
### Basic Operations
- $+$ is for addition (e.g. $ 2 + 2$)
- $-$ is for substraction (e.g. $2 - 3$)
- $×$, $·$ is for multiplication (e.g. $2 × 3$)
- $/$, $÷$ is for division (e.g. $2 / 3$)

```csharp
// addition
2 + 2;

// substraction
2 - 3;

// multiplication
2 * 3;

// division
2 / 3;
```

#### Sigma
The Capital Sigma symbol can be used to represent the sum of related numbers, the notation is the following:
${\displaystyle \sum _{i\mathop {=} m}^{n}a_{i}}$

Where:
- $i$ is the index of the summation, it is incremented by one for each successive term
- $a_{i}$ is an indexed variable representingeach term of the sum
- $m$ is the lower bound of summation
- $n$ is the upper bound of summation


Here is an example, where we want to get the summation of squares:
${\displaystyle \sum _{k=1}^{5}k^{2}}$

It can be understood as:
$1^{2}+2^{2}+3^{2}+4^{2}+5^{2}$

And in C# we can represent it like this:
```csharp
var sum = 0.0d;
for (var i = 1; i <= 5; i++)
{
  sum += Math.Pow(i, 2);
}
// sum value is 55.0
```

The sigma notation can be nested. We should evaluate the right-most sigma first by default. The order can be altered using parentheses.
${\displaystyle \sum _{i\mathop {=} 1}^{2} \sum _{j\mathop {=} 4}^{6}(3ij)}$

We can implement it in C# in the following way:
```csharp
var sum = 0;
for (var i = 1; i <= 2; i++)
{
  for (var j = 4; j <= 6; j++)
  {
    sum += (3 * i * j);
  }
}
// sum value is 135
```


# WIP Below
### Exponentiation and Square root
Exponentiation is an operation involving two numbers, the base and the exponent that can be in the following form:
$2 ^ 3$

A square root operation is of the form:

$\sqrt{9} = 3$

In C# we can use the method `Pow` for exponentiation and `Sqrt` for square root: 

```csharp
//Exponentiation
var x = 2;
var y = 3;
System.Math.Pow(x, y) == 8;

//Square root
var x = 9;
System.Math.Sqrt(x) == 3;
```

## Scalar Operations

Scalar
The dot $·$ and cross $×$ symbols have different uses depending on context.

They might seem obvious, but it's important to understand the subtle differences before we continue into other sections.

#### Scalar multiplication

Both symbols can represent simple multiplication of scalars. The following are equivalent:
$5 \cdot 4 = 5 \times 4 $


In programming languages we tend to use asterisk for multiplication:

```csharp
var result = 5 * 4
```

Often, the multiplication sign is only used to avoid ambiguity (e.g. between two numbers). In the following example, we can see that it was omitted entirely:

$3kj$

If these variables represent scalars, the code would be:

```csharp
var result = 3 * k * j
```

#### Vector multiplication

To denote multiplication of one vector with a scalar, or element-wise multiplication of a vector with another vector, we typically do not use the dot $·$ or cross $×$ symbols. These have different meanings in linear algebra, discussed shortly.

Let's take our earlier example but apply it to vectors. For element-wise vector multiplication, you might see an open dot $∘$ to represent the [Hadamard product](https://en.wikipedia.org/wiki/Hadamard_product_%28matrices%29).<sup>[2]</sup>

$3\mathbf{k}\circ\mathbf{j}$

In other instances, the author might explicitly define a different notation, such as a circled dot $⊙$ or a filled circle $●$.<sup>[3]</sup>

Here is how it would look in code, using arrays `[x, y]` to represent the 2D vectors.

```js
var s = 3
var k = [ 1, 2 ]
var j = [ 2, 3 ]

var tmp = multiply(k, j)
var result = multiplyScalar(tmp, s)
//=> [ 6, 18 ]
```

Our `multiply` and `multiplyScalar` functions look like this:

```js
function multiply(a, b) {
  return [ a[0] * b[0], a[1] * b[1] ]
}

function multiplyScalar(a, scalar) {
  return [ a[0] * scalar, a[1] * scalar ]
}
```

Similarly, matrix multiplication typically does not use the dot `·` or cross symbol `×`. Matrix multiplication will be covered in a later section.

## Complex Numbers
Complex numbers are expressions of the form $a + ib$, where $a$ is the real part and $b$ is the imaginary part. The imaginary number $i$ is defined as:

$i=\sqrt{-1}$

In C#, we can use the APIs under the namespace `System.Numerics.Complex`:

```csharp

var a = new Complex(3, -1); //=> { re: 3, im: -1 }
var b = new Complex(0, 1); //=> { re: 0, im: 1 }
var z = a * b; //=> '1 + 3i'

```
More information about the API for complex numbers can be found [here](https://learn.microsoft.com/en-us/dotnet/fundamentals/runtime-libraries/system-numerics-complex).
