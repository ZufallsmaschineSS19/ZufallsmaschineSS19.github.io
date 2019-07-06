<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
<h1 id="linear-congruential-generators">Linear Congruential Generators</h1>
<p>Linear Congruential Generators (or LCGs in short) are algorithms that can be used to generate pseudo random numbers. To generate a random number with an LCG we need three discrete parameters and a starting value. The parameters are</p>
<ul>
<li>the <em>modulus</em> <span class="math inline">\(M\)</span>, with <span class="math inline">\(0 &lt; M\)</span>,</li>
<li>the <em>multiplier</em> <span class="math inline">\(A\)</span>, with <span class="math inline">\(0 &lt; A &lt; M\)</span> and</li>
<li>the <em>increment</em> <span class="math inline">\(C\)</span>, with <span class="math inline">\(0 \leq C &lt; M\)</span>.</li>
</ul>
<p>The starting value is usually denoted as <span class="math inline">\(X_{0}\)</span> with <span class="math inline">\(0 \leq X_{0} &lt; M\)</span>.</p>
<p>To now generate a new random number from a starting point <span class="math inline">\(X_{n}\)</span> (for the sake of generality we set <span class="math inline">\(n = 0\)</span>), we simply calculate</p>
<p><span class="math display">\[X_{n+1} = A * X_{n} + C \mod M \mathrm{.}\]</span></p>
<p>Since all values are discrete the result of the linear transformation <span class="math inline">\(R = A * X_{n} + C\)</span> is again a discrete number. Through the modulo operation <span class="math inline">\(X_{n+1} = R \mod M\)</span> we assert <span class="math inline">\(0 \leq X_{n+1} &lt; M\)</span>.</p>
<h2 id="a-few-examples">A few examples</h2>
<p>To get a feeling for this formula we choose a couple of parameters and see what we get for the output.</p>
<h3 id="m-9-a-2-c-0-x_0-1"><span class="math inline">\(M = 9\)</span>, <span class="math inline">\(A = 2\)</span>, <span class="math inline">\(C = 0\)</span>, <span class="math inline">\(X_{0} = 1\)</span></h3>
<p>These parameters generate the following sequence of numbers:</p>
<p><span class="math display">\[ 2, 4, 8, 7, 5, 1, 2, 4, 8, 7, 5, 1, 2, 4, 8, 7, 5, 1, 2, 4, \dots \]</span></p>
<p>We can see that it repeats itself very quickly. This is of course due to the small modulus we choose. Furthermore we can see that it does not cover all the values in the interval <span class="math inline">\(\left(0, M\right)\)</span>. If we now choose a starting value that is any number in the sequence above, we will obtain the same sequence again. So let’s choose a value that has not occurred yet.</p>
<h3 id="m-9-a-2-c-0-x_0-3"><span class="math inline">\(M = 9\)</span>, <span class="math inline">\(A = 2\)</span>, <span class="math inline">\(C = 0\)</span>, <span class="math inline">\(X_{0} = 3\)</span></h3>
<p>These parameters generate the following sequence of numbers:</p>
<p><span class="math display">\[6, 3, 6, 3, 6, 3, 6, 3, 6, 3, 6, 3, 6, 3, 6, 3, 6, 3, 6, 3, \dots\]</span></p>
<p>This sequence is even less random, as it only takes on the values <span class="math inline">\(3\)</span> and <span class="math inline">\(6\)</span>. Now we have exhausted all values in <span class="math inline">\(\left(0, M\right)\)</span>.</p>
<p>We can already tell that to obtain truly randomly <em>looking</em> numbers, we need to pick a larger modulus.</p>
<h3 id="m-251-a-33-c-0-x_0-1"><span class="math inline">\(M = 251\)</span>, <span class="math inline">\(A = 33\)</span>, <span class="math inline">\(C = 0\)</span>, <span class="math inline">\(X_{0} = 1\)</span></h3>
<p>We obtain</p>
<p><span class="math display">\[33, 85, 44, 197, 226, 179, 134, 155, 95, 123, 43, 164, 141, 135, 188, 180, 167, 240, 139, 69, \dots\]</span></p>
<p>This appears to be a much better sequence. At first glance we can not spot repeating values and we are also unable to predict a successor to some value. The only obvious shortcoming is the small modulus. A modulus of <span class="math inline">\(M = 251\)</span> causes the values to only be in the range <span class="math inline">\(\left( 0, M\right)\)</span>. After <span class="math inline">\(250\)</span> numbers the values will definitely start repeating.</p>
<h2 id="testing-for-randomness">Testing for randomness</h2>
<p>Our third example already makes it hard to tell if these numbers are <em>good</em> pseudo random numbers. But what makes a sequence of pseudo random numbers <em>good</em>? The German Bundesamt für Sicherheit in der Informationstechnik (BSI) recommends a series of statistical tests [<a href="#schindler">2</a>]. These tests look at the binary sequence of the random numbers.</p>
<p>The binary number sequence of <a href="#m-251-a-33-c-0-x_0-1">example three</a> would be <span class="math display">\[ 00100001, 01010101, 00101100, 11000101, 11100010, 10110011, 10000110, \dots \]</span></p>
<p>To perform the following tests we take all binary numbers and concatenate them into a long string. This string is then truncated to be exactly <span class="math inline">\(20000\)</span> bits long. This binary string is denoted <span class="math inline">\(b\)</span>, individual bits are denoted <span class="math inline">\(b_{i}\)</span> (for the <span class="math inline">\(i\)</span>th bit). <span class="math display">\[ b = 00100001010101010010110011000101111000101011001110000110\dots \]</span></p>
<p>There are a total of five statistical tests recommended:</p>
<h3 id="monobit-test">Monobit Test</h3>
<p>We sum up all bits in the string <span class="math inline">\(b\)</span>.</p>
<p><span class="math display">\[ X_{b} = \sum_{i=1}^{i=20000} b_{i}\mathrm{.}\]</span></p>
<p>To pass the monobit test the result <span class="math inline">\(X_{b}\)</span> has to fulfill <span class="math inline">\(9654 &lt; X_{b} &lt; 10346\)</span>. In words: the sequence is binary, made up of ones and zeros. Either appearance is equally probable (exactly <span class="math inline">\(0.5\)</span>). Therefore we expect the roughly the same number of ones as we have zeros.</p>
<h3 id="poker-test">Poker Test</h3>
<p>We divide the binary sequence into segments of four bits each, <span class="math display">\[ 0010, 0001, 0101, 0101, 0010, 1100, 1100, 0101, 1110, 0010, 1011, \dots \]</span> We can turn each segment into a four bit number between <span class="math inline">\(0\)</span> to <span class="math inline">\(15\)</span>. There are exactly <span class="math inline">\(16\)</span> different numbers. We now count the occurrence of each of these numbers, denoted <span class="math inline">\(s_{i}\)</span> with <span class="math inline">\(i \in [0, 15]\)</span>. With this we calculate the sum <span class="math display">\[X_{s} = \sum_{i=0}^{i=15} s_{i}^{2} - 5000\mathrm{.}\]</span></p>
<p>To pass the poker test we expect <span class="math inline">\(1.03 &lt; X_{s} &lt; 57.4\)</span> for the result of the sum. This is in essence a <span class="math inline">\(\chi^{2}\)</span>-test with 15 degrees of freedom.</p>
<h3 id="runs-test">Runs Test</h3>
<p>We look at the binary sequence and count sequences of ones and zeros. In the sequence <span class="math display">\[ 1, 0, 0, 1, 1, 1, 0, 1 \]</span> we have three sequences of length <span class="math inline">\(1\)</span> (the first <span class="math inline">\(1\)</span> and the <span class="math inline">\(0\)</span> and the <span class="math inline">\(1\)</span> at the end), one sequence of length <span class="math inline">\(2\)</span> (<span class="math inline">\(0, 0\)</span>) and one sequence of length <span class="math inline">\(3\)</span> (<span class="math inline">\(1, 1, 1\)</span>). The occurrences of each length has to follow a distribution if the sequence is truly random. For a sequence of length <span class="math inline">\(20000\)</span> this distribution is as follows.</p>
<table>
<thead>
<tr class="header">
<th>Sequence length</th>
<th style="text-align: right;">Occurrence interval</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>1</td>
<td style="text-align: right;">2267-2733</td>
</tr>
<tr class="even">
<td>2</td>
<td style="text-align: right;">1079-1421</td>
</tr>
<tr class="odd">
<td>3</td>
<td style="text-align: right;">502-748</td>
</tr>
<tr class="even">
<td>4</td>
<td style="text-align: right;">233-402</td>
</tr>
<tr class="odd">
<td>5</td>
<td style="text-align: right;">90-223</td>
</tr>
<tr class="even">
<td>6 and more</td>
<td style="text-align: right;">90-233</td>
</tr>
</tbody>
</table>
<h3 id="long-runs-test">Long Runs Test</h3>
<p>The Long Runs Test is essentially the same as the runs test. In this we just see if there are sequences of length <span class="math inline">\(34\)</span> or longer in the binary sequence. If there are the test has failed.</p>
<h3 id="autocorrelation-test">Autocorrelation Test</h3>
<p>The Autocorrelation Test tests sub sequences of the original binary sequence and looks how much they depend on each other (or how “similar” they are).</p>
<h4 id="an-explanation">An explanation</h4>
<p>Let’s take the sequence <span class="math display">\[ b = 0, 0, 1, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 1, 0, 1, 0, 0, 1, 0, 1, 1, 0, 0, \dots \]</span> and create from it two sub sequences of length <span class="math inline">\(10\)</span>. We let <span class="math inline">\(s_{i}\)</span> be the sub sequence of length <span class="math inline">\(10\)</span> that was created by removing the <em>first</em> <span class="math inline">\(i\)</span> bits from the sequence <span class="math inline">\(b\)</span> and then removing everything that makes <span class="math inline">\(s_{i}\)</span> longer than length <span class="math inline">\(10\)</span>. <span class="math display">\[s_{0} = 0, 0, 1, 0, 0, 0, 0, 1, 0, 1\]</span> <span class="math display">\[s_{1} = 0, 1, 0, 0, 0, 0, 1, 0, 1, 0\]</span> The next step is to perform a bitwise XOR operation on the two sequences, <span class="math display">\[s_{0 \oplus 1} = s_{0} \oplus s_{1} = 0, 1, 1, 0, 0, 0, 1, 1, 1, 1\]</span> XOR is a logic operation with the following logic table <span class="math display">\[0 \oplus 0 = 0\mathrm{,} \quad 0 \oplus 1 = 1\mathrm{,} \quad 1 \oplus 0 = 1\mathrm{,} \quad 1 \oplus 1 = 0\]</span> Then the sum of <span class="math inline">\(b_{0 \oplus 1}\)</span> is calculated. For a totally uncorrelated original binary sequence we expect a value of roughly <span class="math inline">\(5\)</span> (half the length of the sub sequences).</p>
<h4 id="the-actual-test">The actual test</h4>
<p>For the actual test the sequences are <span class="math inline">\(5000\)</span> bits long. We take bits <span class="math inline">\(b_{i}\)</span> from the original sequence <span class="math inline">\(b\)</span> and calculate for <span class="math inline">\(n \in [1, 5000]\)</span> <span class="math display">\[X_{n} = \sum_{j=1}^{j=5000} b_{j} \oplus b_{j+n}\]</span> The test has passed when <span class="math inline">\(2326 &lt; X_{n} &lt; 2674\)</span> for each <span class="math inline">\(n\)</span>. To avoid confusion it should be noted that the test is only performed on the first <span class="math inline">\(10000\)</span> bits of the original sequence.</p>
<h4 id="example-plots">Example plots</h4>
<figure>
<img src="short_ac.png" alt="Parameters chosen from example three. The modulus of the LCG was choosen to be very small. The result is strong autocorrelation, the sequence repeats after roughly 2000 bits (plot goes to 0)." /><figcaption>Parameters chosen from <a href="#m-251-a-33-c-0-x_0-1">example three</a>. The modulus of the LCG was choosen to be very small. The result is strong autocorrelation, the sequence repeats after roughly 2000 bits (plot goes to 0).</figcaption>
</figure>
<figure>
<img src="truly_random.png" alt="Autocorrelation of truly random numbers (in this case generated by a quantum random number generator)." /><figcaption>Autocorrelation of truly random numbers (in this case generated by a quantum random number generator).</figcaption>
</figure>
<p>In the first image we can see the autocorrelation values of a binary sequence from an LCG where the modulus was choosen to be too small. The result is a strong autocorrelation. The second image shows the autocorrelation for a binary sequence that was generated by a quantum mechanical random number generator. Because of the quantum nature these numbers are truly random. This can also be seen in the autocorrelation plot.</p>
<h2 id="pitfalls-of-lcgs-the-spectral-test">Pitfalls of LCGs – The Spectral Test</h2>
<p>Statistical tests are a good way of assessing some basic distribution properties of (pseudo random) binary sequences. In the case of pseudo random binary sequences generated from LCGs however, they don’t necessarily tell the whole story. Let’s generate a random number sequence <span class="math inline">\(X_{n}\)</span> (the parameters for the LCG are <span class="math inline">\(X_{0} = 1\)</span>, <span class="math inline">\(A = 33\)</span>, <span class="math inline">\(C = 0\)</span> and <span class="math inline">\(M = 251232131\)</span>; for these parameters all statistical tests pass) and look at the random number sequence <span class="math inline">\(X_{n}\)</span> plotted against the random number sequence <span class="math inline">\(X_{n+1}\)</span> (the same sequence, just shifted to the right by one number).</p>
<p><img src="spectral_v2_fail.png" /></p>
<p>What do we see? Even though the statistical tests all pass, we see that the random numbers seem to fall onto a set of lines. We can find similar pictures in higher dimensions. For three dimensions we would have to plot <span class="math inline">\(X_{n}\)</span> versus <span class="math inline">\(X_{n+1}\)</span> versus <span class="math inline">\(X_{n+2}\)</span>. The random numbers would then fall on planes (or hyperplanes in four or more dimensions).</p>
<p>These lines are determined by our choice of parameters for the LCG. Since the increment <span class="math inline">\(C\)</span> only shifts the random numbers it only affects the positions of the lines, not the distance or the angle. The distance and angle of the lines is determined by the multiplier <span class="math inline">\(A\)</span> and the modulus <span class="math inline">\(M\)</span>.</p>
<p>The closer the lines are to each other, the higher quality the random numbers are. This is because a sequence of random numbers will fill the space (the squared interval <span class="math inline">\((0, M) \times (0, M)\)</span> in two dimensions). This is what the Spectral Test does: it finds the distance between adjacent lines (or (hyper-)planes).</p>
<p>For a detailed explanation please refer to the excellent (although technical) chapter on the Spectral Test in <a href="#knuth">Knuths book [1] (pp. 89)</a>.</p>
<h2 id="performing-the-tests">Performing the tests</h2>
<p>To perform the tests that were introduced we can use the Python program downloadable <a href="https://github.com/Klump3n/lcg_tests">here</a> <a href="#plock">[3]</a>. We pick a couple of “famous” LCG parameters and perform tests in a range around them.</p>
<h3 id="randu">RANDU</h3>
<p>A very famous and bad example is the LCG implementation <code>RANDU</code> by IBM, that has been used since the 1960s <a href="#knuth">[1]</a>. The faults were discovered by 1963 but <code>RANDU</code> has been noted to have been in use up until 1999. <code>RANDU</code> is the reason that results from simulations from that era should always be taken with a grain of salt.</p>
<p>The parameters for <code>RANDU</code> are <span class="math display">\[A = 65539\mathrm{,} \quad C = 0\mathrm{,} \quad M = 2^{31}-1\mathrm{.}\]</span></p>
<p>First we look at the statistical tests. Yellow colors indicate that all tests have passed. For the proposed parameter all statistical tests have passed. We notice a reduction in passed tests for LCGs that have <span class="math inline">\(A = 65536 = 2^{16}\)</span>. In general tests with even parameters <span class="math inline">\(A\)</span> and <span class="math inline">\(M\)</span> seem to fail more often. <img src="results_x0_1_a_65529_65549_c_0_0_m_2147483637_2147483657_statistical_c_is_0.png" alt="Results for the statistical tests for RANDU in an interval of A = 65539 \pm 10 and M = (2^{31} - 1) \pm 10." /></p>
<p>The Spectral Test is performed for the dimensions <span class="math inline">\(2\)</span> to <span class="math inline">\(5\)</span>. These are still computationally easy. We note that for the chosen interval no parameter combination has passed the tests for every dimension <span class="math inline">\(2\)</span>, <span class="math inline">\(3\)</span>, <span class="math inline">\(4\)</span> and <span class="math inline">\(5\)</span>. On the top right corner we spot two combinations that passed <span class="math inline">\(3\)</span> out of <span class="math inline">\(4\)</span> tests. <img src="results_x0_1_a_65529_65549_c_0_0_m_2147483637_2147483657_spectral_c_is_0.png" alt="Results for the Spectral Test for RANDU in an interval of A = 65539 \pm 10 and M = (2^{31} - 1) \pm 10." /></p>
<p>Ideally the chosen parameters pass the statistical tests as well as the spectral test. For <code>RANDU</code> and the chosen interval around the proposed paramter combination, no combination passed all the statistical tests and the Spectral test for more than <span class="math inline">\(2\)</span> dimensions. <img src="results_x0_1_a_65529_65549_c_0_0_m_2147483637_2147483657_spectral_if_statistical_c_is_0.png" alt="Results for the Spectral Test in places where ALL statistical tests passed for RANDU in an interval of A = 65539 \pm 10 and M = (2^{31} - 1) \pm 10." /></p>
<p>The conclusion is that <code>RANDU</code> is a very bad LCG and should not be used.</p>
<h3 id="c-lcg-implementations">C++ LCG implementations</h3>
<p>A more recent example is the LCG implementation found in the C++ standard <a href="#cpp">[4]</a>. There exist two different parameter choices, <code>minstd_rand0</code> and <code>minstd_rand</code>.</p>
<h4 id="minstd_rand0">minstd_rand0</h4>
<p>The parameters for <code>minstd_rand0</code> are <span class="math display">\[A = 16807\mathrm{,} \quad C = 0\mathrm{,} \quad M = 2^{31} - 1\mathrm{.}\]</span></p>
<figure>
<img src="results_x0_1_a_16797_16817_c_0_0_m_2147483637_2147483657_statistical_c_is_0.png" alt="Results for the statistical tests for minstd_rand0 in an interval of A = 16807 \pm 10 and M = (2^{31} - 1) \pm 10." /><figcaption>Results for the statistical tests for <code>minstd_rand0</code> in an interval of <span class="math inline">\(A = 16807 \pm 10\)</span> and <span class="math inline">\(M = (2^{31} - 1) \pm 10\)</span>.</figcaption>
</figure>
<figure>
<img src="results_x0_1_a_16797_16817_c_0_0_m_2147483637_2147483657_spectral_c_is_0.png" alt="Results for the Spectral Test for minstd_rand0 in an interval of A = 16807 \pm 10 and M = (2^{31} - 1) \pm 10." /><figcaption>Results for the Spectral Test for <code>minstd_rand0</code> in an interval of <span class="math inline">\(A = 16807 \pm 10\)</span> and <span class="math inline">\(M = (2^{31} - 1) \pm 10\)</span>.</figcaption>
</figure>
<figure>
<img src="results_x0_1_a_16797_16817_c_0_0_m_2147483637_2147483657_spectral_if_statistical_c_is_0.png" alt="Results for the Spectral Test in places where ALL statistical tests passed for minstd_rand0 in an interval of A = 16807 \pm 10 and M = (2^{31} - 1) \pm 10." /><figcaption>Results for the Spectral Test in places where <em>ALL</em> statistical tests passed for <code>minstd_rand0</code> in an interval of <span class="math inline">\(A = 16807 \pm 10\)</span> and <span class="math inline">\(M = (2^{31} - 1) \pm 10\)</span>.</figcaption>
</figure>
<h4 id="minstd_rand">minstd_rand</h4>
<p>The parameters for <code>minstd_rand</code> are <span class="math display">\[A = 48271\mathrm{,} \quad C = 0\mathrm{,} \quad M = 2^{31} - 1\mathrm{.}\]</span></p>
<figure>
<img src="results_x0_1_a_48261_48281_c_0_0_m_2147483637_2147483657_statistical_c_is_0.png" alt="Results for the statistical tests for minstd_rand0 in an interval of A = 48271 \pm 10 and M = (2^{31} - 1) \pm 10." /><figcaption>Results for the statistical tests for <code>minstd_rand0</code> in an interval of <span class="math inline">\(A = 48271 \pm 10\)</span> and <span class="math inline">\(M = (2^{31} - 1) \pm 10\)</span>.</figcaption>
</figure>
<figure>
<img src="results_x0_1_a_48261_48281_c_0_0_m_2147483637_2147483657_spectral_c_is_0.png" alt="Results for the Spectral Test for minstd_rand0 in an interval of A = 48271 \pm 10 and M = (2^{31} - 1) \pm 10." /><figcaption>Results for the Spectral Test for <code>minstd_rand0</code> in an interval of <span class="math inline">\(A = 48271 \pm 10\)</span> and <span class="math inline">\(M = (2^{31} - 1) \pm 10\)</span>.</figcaption>
</figure>
<figure>
<img src="results_x0_1_a_48261_48281_c_0_0_m_2147483637_2147483657_spectral_if_statistical_c_is_0.png" alt="Results for the Spectral Test in places where ALL statistical tests passed for minstd_rand0 in an interval of A = 48271 \pm 10 and M = (2^{31} - 1) \pm 10." /><figcaption>Results for the Spectral Test in places where <em>ALL</em> statistical tests passed for <code>minstd_rand0</code> in an interval of <span class="math inline">\(A = 48271 \pm 10\)</span> and <span class="math inline">\(M = (2^{31} - 1) \pm 10\)</span>.</figcaption>
</figure>
<h1 id="references">References</h1>
<ul>
<li><a name="knuth">[1]</a> Donald E. Knuth. <em>The Art of Computer Programming, Volume 2: Seminumerical Algorithms</em>. Addison-Wesley, 1997.</li>
<li><a name="schindler">[2]</a> Werner Schindler. <em>Functionality classes and evaluation methodology for deterministic random number generators</em>. <a href="https://www.bsi.bund.de/SharedDocs/Downloads/DE/BSI/Zertifizierung/Interpretationen/AIS_20_Functionality_Classes_Evaluation_Methodology_DRNG_e.pdf" class="uri">https://www.bsi.bund.de/SharedDocs/Downloads/DE/BSI/Zertifizierung/Interpretationen/AIS_20_Functionality_Classes_Evaluation_Methodology_DRNG_e.pdf</a>, 1999.</li>
<li><a name="plock">[3]</a> Matthias Plock. <em>lcg_tests. A small analysis suite for linear congruential generators for a university seminar.</em> <a href="https://github.com/Klump3n/lcg_tests" class="uri">https://github.com/Klump3n/lcg_tests</a>, 2019.</li>
<li><a name="cpp">[4]</a> CPP Reference. <em>std::linear_congruential_engine</em> <a href="https://en.cppreference.com/w/cpp/numeric/random/linear_congruential_engine" class="uri">https://en.cppreference.com/w/cpp/numeric/random/linear_congruential_engine</a>, looked up July 6, 2019.</li>
</ul>
