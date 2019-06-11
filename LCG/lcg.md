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
<p><span class="math display">\[X_{n+1} = A * X_{n} + C \mod M\]</span>.</p>
<p>Since all values are discrete the result of the linear transformation <span class="math inline">\(R = A * X_{n} + C\)</span> is again a discrete number. Through the modulo operation <span class="math inline">\(X_{n+1} = R \mod M\)</span> we assert <span class="math inline">\(0 \leq X_{n+1} &lt; M\)</span>.</p>
<h2 id="a-few-examples">A few examples</h2>
<p>To get a feeling for this formula we choose the parameters and see what we receive.</p>
