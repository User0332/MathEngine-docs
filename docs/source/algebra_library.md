# MathEngine.Algebra

The `MathEngine.Algebra` library contains the basic necessities required to perform algebraic computation, including expression & equation abstractions, polynomial representations, and the ability to solve select classes of polynomials.

Below are some code examples for the Algebra library and a list of the main types contained within the library.

## Examples

### Analyzing a Polynomial Expression

```cs
using MathEngine.Algebra;
using MathEngine.Algebra.Expressions.Polynomial;

var x = Variable.X;

var expr = PolynomialExpression.From(
	(x^2) + 2*x + 1 + (-4*x)
);

NormalizedPolynomialExpression normalized = expr.Normalize();

foreach (var term in normalized.NormalizedTerms)
{
	Console.WriteLine($"Degree of Term: {NormalizedPolynomialExpression.DegreeOfNormalizedTerm(term)}");
	Console.WriteLine($"Coefficient of Term: {NormalizedPolynomialExpression.CoefficientOfNormalizedTerm(term)}");
}
```

### Solving a Polynomial Equation


```cs
using MathEngine.Algebra;
using MathEngine.Algebra.Solver.Polynomial;

var x = Variable.X;

var eq = ((x^2)+5*x+6).SetEqualTo(2*x+8).ToPolynomial();

var solns = eq.Solve(strategy: PolynomialSolvingStrategy.UseFormula).Select(soln => soln.Simplify()).Distinct();

foreach (var soln in solns)
{
	Console.WriteLine(soln.LaTeX());
}
```

### Simplifying an Expression

```cs
using MathEngine.Algebra;
using MathEngine.Algebra.Expressions.Simplification;

var x = Variable.X;

var expr = (x^2) + 2*x + 1 + (-4*x)/2 - 3;

Console.WriteLine(expr);
Console.WriteLine(expr.Simplify(SimplificationStrategy.Default)); /* SimplificationStrategy.Default is the default/implicit parameter value, so it does not need to be passed. If you choose not to use SimplificationStrategy, you do not need to use the namespace MathEngine.Algebra.Expressions.Simplification either */
```

### Substituting in for a Variable

```cs
using MathEngine.Algebra;
using MathEngine.Algebra.Expressions;

Variable h = new('h');

Expression expr = (h^4)+2*h+3;

Console.WriteLine(expr.Substitute(h, Expression.OneHalf).Simplify());
Console.WriteLine(expr.Substitute(Variable.T, Expression.OneHalf).Simplify()); /* does nothing because the variable 't' is not in the expression */
```

## Main Types

### Namespace `MathEngine.Algebra.Expressions`

#### `Expression`

The abstract base class for all mathematical expressions. Implements `IEquatable<Expression>`.

##### *<code>[ValueExpression](./algebra_library.md#ValueExpression) Expression.One</code>*

Represents the integral value `1`.

##### *<code>[ValueExpression](./algebra_library.md#ValueExpression) Expression.Zero</code>*

Represents the integral value `0`.

##### *<code>[ValueExpression](./algebra_library.md#ValueExpression) Expression.NegativeOne</code>*

Represents the integral value `-1`.

##### *<code>[ValueExpression](./algebra_library.md#ValueExpression) Expression.OneHalf</code>*

Represents the rational value `1/2`.

##### *<code>[ValueExpression](./algebra_library.md#ValueExpression) Expression.PI</code>*

Represents the transcendental value `π`.

##### *<code>[ValueExpression](./algebra_library.md#ValueExpression) Expression.E</code>*

Represents the transcendental value `e`.

##### *<code>[Expression](./algebra_library.md#Expression) Expression.Undefined</code>*

Represents an undefined expression.

##### *`string ToString()`*

Returns the string representation of this expression, grouped in order of **mathematical** precendence.

##### *`string LaTeX()`*

Returns the LaTeX markup that represents this expression.

##### *`string Repr()`*

Returns a string representation of this expression in a heirarchical view.

##### *<code>[Expression](./algebra_library.m#Expression) Simplify([SimplificationStrategy](./algebra_library.md#SimplificationStrategy) strat = SimplificationStrategy.Default)</code>*

Simplifies this expression using the requested *[`SimplificationStrategy`]()*. See *[`SimplificationStrategy`]()* for more details on what each strategy accomplishes.

#### *<code>[PowerExpression](./algebra_library.md#PowerExpression) Square()</code>*

Returns the square of this expression (this expression raised to the power of two).

#### *<code>[PowerExpression](./algebra_library.md#PowerExpression) Sqrt()</code>*

Returns the square root of this expression.

#### *<code>[PowerExpression](./algebra_library.md#PowerExpression) Cube()</code>*

Returns the cube of this expression (this expression raised to the power of three).

#### *<code>[PowerExpression](./algebra_library.md#PowerExpression) Cbrt()</code>*

Returns the cube root of this expression.

#### *<code>[PolynomialExpression](./algebra_library.md#PolynomialExpression) ToPolynomial()</code>*

Attempts to convert this expression to a *[`PolynomialExpression`](./algebra_library.md#polynomialexpression)*. May throw an *`ArgumentException`* on failure (if the expression could not be interpreted as a polynomial).

#### `ValueExpression`