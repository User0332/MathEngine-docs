# MathEngine.Algebra

The `MathEngine.Algebra` library contains the basic necessities required to perform algebraic computation, including polynomial representations and the ability to solve select classes of polynomials.

Below are some code examples for the Algebra library and a list of the main types contained within the library.

## Examples

### Solving a Quadratic

```cs
using MathEngine.Algebra;
using MathEngine.Algebra.Equations;
using MathEngine.Algebra.Expressions.Polynomial;
using MathEngine.Algebra.Solver;

var x = Variable.X;

var expr = PolynomialExpression.From(
	(x^2) + 2*x + 1 + (-4*x)
);

PolynomialEquation eq = new(expr, PolynomialExpression.ZeroExpr());

var solns = eq.Solve(PolynomialSolvingStrategy.ViaFormula).Select(soln => soln.Simplify()).Distinct(); // .Distinct() ensures double-roots are ignored

foreach (var soln in solns)
{
	Console.WriteLine(soln); // should output 1, the only root/x-intercept to the function x^2 - 2x + 1
}
```