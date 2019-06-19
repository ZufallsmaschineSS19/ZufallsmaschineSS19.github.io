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

The binary number sequence of [example three](#m-251-a-33-c-0-x_0-1) would be
$$ 00100001, 01010101, 00101100, 11000101, 11100010, 10110011, 10000110, \dots $$

To perform the following tests we take all binary numbers and concatenate them into a long string. This string is then truncated to be exactly $20000$ bits long. This binary string is denoted $b$, individual bits are denoted $b_{i}$ (for the $i$th bit).
$$ b = 00100001010101010010110011000101111000101011001110000110\dots $$

There are a total of five statistical tests recommended:

### Monobit Test

We sum up all bits in the string $b$.

$$ X_{b} = \sum_{i=1}^{i=20000} b_{i}\mathrm{.}$$

To pass the monobit test the result $X_{b}$ has to fulfill $9654 < X_{b} < 10346$. In words: the sequence is binary, made up of ones and zeros. Either appearance is equally probable (exactly $0.5$). Therefore we expect the roughly the same number of ones as we have zeros.

### Poker Test

We divide the binary sequence into segments of four bits each,
$$ 0010, 0001, 0101, 0101, 0010, 1100, 1100, 0101, 1110, 0010, 1011, \dots $$
We can turn each segment into a four bit number between $0$ to $15$. There are exactly $16$ different numbers. We now count the occurrence of each of these numbers, denoted $s_{i}$ with $i \in [0, 15]$. With this we calculate the sum
$$X_{s} = \sum_{i=0}^{i=15} s_{i}^{2} - 5000\mathrm{.}$$

To pass the poker test we expect $1.03 < X_{s} < 57.4$ for the result of the sum. This is in essence a $\chi^{2}$-test with 15 degrees of freedom.

### Runs Test

We look at the binary sequence and count sequences of ones and zeros. In the sequence
$$ 1, 0, 0, 1, 1, 1, 0, 1 $$
we have three sequences of length $1$ (the first $1$ and the $0$ and the $1$ at the end), one sequence of length $2$ ($0, 0$) and one sequence of length $3$ ($1, 1, 1$). The occurrences of each length has to follow a distribution if the sequence is truly random. For a sequence of length $20000$ this distribution is as follows.

| Sequence length | Occurrence interval |
| --- | ---: |
| 1 | 2267-2733 |
| 2 | 1079-1421 |
| 3 | 502-748 | 
| 4 | 233-402 |
| 5 | 90-223 |
| 6 and more | 90-233 |

### Long Runs Test

The Long Runs Test is essentially the same as the runs test. In this we just see if there are sequences of length $34$ or longer in the binary sequence. If there are the test has failed.

### Autocorrelation Test

The Autocorrelation Test tests sub sequences of the original binary sequence and looks how much they depend on each other (or how "similar" they are). Let's take the sequence
$$ b = 0, 0, 1, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 1, 0, 1, 0, 0, 1, 0, 1, 1, 0, 0, \dots $$
and create from it two sub sequences of length $10$. We let $b_{i}$ be the sub sequence of length $10$ that was created by removing the _first_ $i$ bits from the sequence $b$ and then removing everything that makes $b_{i}$ longer than length $10$.
$$b_{0} = 0, 0, 1, 0, 0, 0, 0, 1, 0, 1$$
$$b_{1} = 0, 1, 0, 0, 0, 0, 1, 0, 1, 0$$
The next step is to perform a bitwise XOR operation on the two sequences,
$$b_{0 \oplus 1} = b_{0} \oplus b_{1} = 1, 0, 0, 1, 1, 1, 0, 0, 0, 0$$
XOR is a logic operation with the following logic table
$$0 \oplus 0 = 0\mathrm{,} \quad 0 \oplus 1 = 1\mathrm{,} \quad 1 \oplus 0 = 1\mathrm{,} \quad 1 \oplus 1 = 0$$


## References

 * <a name="knuth">[1]</a> Donald E. Knuth. _The Art of Computer Programming, Volume 2: Seminumerical Algorithms_. Addison-Wesley, 1997.
 * <a name="schindler">[2]</a> Werner Schindler. _Functionality classes and evaluation methodology for deterministic random number generators_. [https://www.bsi.bund.de/SharedDocs/Downloads/DE/BSI/Zertifizierung/Interpretationen/AIS_20_Functionality_Classes_Evaluation_Methodology_DRNG_e.pdf](https://www.bsi.bund.de/SharedDocs/Downloads/DE/BSI/Zertifizierung/Interpretationen/AIS_20_Functionality_Classes_Evaluation_Methodology_DRNG_e.pdf), 1999.
 * <a name="plock">[3]</a> Matthias Plock. _lcg\_tests. A small analysis suite for linear congruential generators for a university seminar._ [https://github.com/Klump3n/lcg_tests](https://github.com/Klump3n/lcg_tests), 2019.
