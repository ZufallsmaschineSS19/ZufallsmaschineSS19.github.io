<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

# Linear Congruential Generators

Linear Congruential Generators (or LCGs in short) are algorithms that can be used to generate pseudo random numbers. To generate a random number with an LCG we need three discrete parameters and a starting value. The parameters are

 * the _modulus_ $M$, with $0 < M$,
 * the _multiplier_ $A$, with $0 < A < M$ and
 * the _increment_ $C$, with $0 \leq C < M$.

The starting value is usually denoted as $X_{0}$ with $0 \leq X_{0} < M$.

To now generate a new random number from a starting point $X_{n}$ (for the sake of generality we set $n = 0$), we simply calculate

$$X_{n+1} = A * X_{n} + C \mod M \mathrm{.}$$

Since all values are discrete the result of the linear transformation $R = A * X_{n} + C$ is again a discrete number. Through the modulo operation $X_{n+1} = R \mod M$ we assert $0 \leq X_{n+1} < M$.

## A few examples

To get a feeling for this formula we choose a couple of parameters and see what we get for the output.

### $M = 9$, $A = 2$, $C = 0$, $X_{0} = 1$

These parameters generate the following sequence of numbers:

$$ 2, 4, 8, 7, 5, 1, 2, 4, 8, 7, 5, 1, 2, 4, 8, 7, 5, 1, 2, 4, \dots $$

We can see that it repeats itself very quickly. This is of course due to the small modulus we choose. Furthermore we can see that it does not cover all the values in the interval $\left(0, M\right)$. If we now choose a starting value that is any number in the sequence above, we will obtain the same sequence again. So let's choose a value that has not occured yet.

### $M = 9$, $A = 2$, $C = 0$, $X_{0} = 3$

These parameters generate the following sequence of numbers:

$$6, 3, 6, 3, 6, 3, 6, 3, 6, 3, 6, 3, 6, 3, 6, 3, 6, 3, 6, 3, \dots$$

This sequence is even less random, as it only takes on the values $3$ and $6$. Now we have exhausted all values in $\left(0, M\right)$.

## References

 * Donald E. Knuth. _The Art of Computer Programming, Volume 2: Seminumerical Algorithms_. Addison-Wesley, 1997.
 * Werner Schindler. _Functionality classes and evaluation methodology for deterministic random number generators_. [https://www.bsi.bund.de/SharedDocs/Downloads/DE/BSI/Zertifizierung/Interpretationen/AIS_20_Functionality_Classes_Evaluation_Methodology_DRNG_e.pdf](), 1999.
