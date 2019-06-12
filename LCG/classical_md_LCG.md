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

We can see that it repeats itself very quickly. This is of course due to the small modulus we choose. Furthermore we can see that it does not cover all the values in the interval $\left(0, M\right)$. If we now choose a starting value that is any number in the sequence above, we will obtain the same sequence again. So let's choose a value that has not occurred yet.

### $M = 9$, $A = 2$, $C = 0$, $X_{0} = 3$

These parameters generate the following sequence of numbers:

$$6, 3, 6, 3, 6, 3, 6, 3, 6, 3, 6, 3, 6, 3, 6, 3, 6, 3, 6, 3, \dots$$

This sequence is even less random, as it only takes on the values $3$ and $6$. Now we have exhausted all values in $\left(0, M\right)$.

We can already tell that to obtain truly randomly _looking_ numbers, we need to pick a larger modulus.

### $M = 251$, $A = 33$, $C = 0$, $X_{0} = 1$

We obtain

$$33, 85, 44, 197, 226, 179, 134, 155, 95, 123, 43, 164, 141, 135, 188, 180, 167, 240, 139, 69, \dots$$

This appears to be a much better sequence. At first glance we can not spot repeating values and we are also unable to predict a successor to some value. The only obvious shortcoming is the small modulus. A modulus of $M = 251$ causes the values to only be in the range $\left( 0, M\right)$. After $250$ numbers the values will definitely start repeating.

## Testing for randomness

Our third example already makes it hard to tell if these numbers are _good_ pseudo random numbers. But what makes a sequence of pseudo random numbers _good_? The German Bundesamt für Sicherheit in der Informationstechnik (BSI) recommends a series of statistical tests [[2](#schindler)]. These tests look at the binary sequence of the random numbers.

The binary sequence of [example three](#m-251-a-33-c-0-x_0-1) would be
$$ 00100001, 01010101, 00101100, 11000101, 11100010, 101100111, 00001101, \dots $$

To perform the following tests we take all binary numbers and concatenate them into a long string. This string is then truncated to be exactly $20000$ bits long. This binary string is denoted $b$, individual bits are denoted $b_{i}$ (for the $i$th bit).

There are a total of five statistical tests recommended:

### Monobit Test

We sum up all bits in this binary string. The result has to conform to a distribution.

### Poker Test

### Runs Test

### Long Runs Test

### Autocorrelation Test

## References

 * <a name="knuth">[1]</a> Donald E. Knuth. _The Art of Computer Programming, Volume 2: Seminumerical Algorithms_. Addison-Wesley, 1997.
 * <a name="schindler">[2]</a> Werner Schindler. _Functionality classes and evaluation methodology for deterministic random number generators_. [https://www.bsi.bund.de/SharedDocs/Downloads/DE/BSI/Zertifizierung/Interpretationen/AIS_20_Functionality_Classes_Evaluation_Methodology_DRNG_e.pdf](https://www.bsi.bund.de/SharedDocs/Downloads/DE/BSI/Zertifizierung/Interpretationen/AIS_20_Functionality_Classes_Evaluation_Methodology_DRNG_e.pdf), 1999.
 * <a name="plock">[3]</a> Matthias Plock. _lcg\_tests. A small analysis suite for linear congruential generators for a university seminar._ [https://github.com/Klump3n/lcg_tests](https://github.com/Klump3n/lcg_tests), 2019.
