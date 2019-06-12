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
<p>We can see that it repeats itself very quickly. This is of course due to the small modulus we choose. Furthermore we can see that it does not cover all the values in the interval <span class="math inline">\(\left(0, M\right)\)</span>. If we now choose a starting value that is any number in the sequence above, we will obtain the same sequence again. So let’s choose a value that has not occured yet.</p>
<h3 id="m-9-a-2-c-0-x_0-3"><span class="math inline">\(M = 9\)</span>, <span class="math inline">\(A = 2\)</span>, <span class="math inline">\(C = 0\)</span>, <span class="math inline">\(X_{0} = 3\)</span></h3>
<p>These parameters generate the following sequence of numbers:</p>
<p><span class="math display">\[6, 3, 6, 3, 6, 3, 6, 3, 6, 3, 6, 3, 6, 3, 6, 3, 6, 3, 6, 3, \dots\]</span></p>
<p>This sequence is even less random, as it only takes on the values <span class="math inline">\(3\)</span> and <span class="math inline">\(6\)</span>. Now we have exhausted all values in <span class="math inline">\(\left(0, M\right)\)</span>.</p>
<h2 id="references">References</h2>
<ul>
<li>Donald E. Knuth. <em>The Art of Computer Programming, Volume 2: Seminumerical Algorithms</em>. Addison-Wesley, 1997.</li>
<li>Werner Schindler. <em>Functionality classes and evaluation methodology for deterministic random number generators</em>. <a href="">https://www.bsi.bund.de/SharedDocs/Downloads/DE/BSI/Zertifizierung/Interpretationen/AIS_20_Functionality_Classes_Evaluation_Methodology_DRNG_e.pdf</a>, 1999.</li>
</ul>
