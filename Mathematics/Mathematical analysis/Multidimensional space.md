[toc]

# Multidimensional space
Definition: m real numbers arranged in sequence
$$(x_1, ..., x_m)$$
is called as a m-ary ordered real array. Consisted of all possible m-ary ordered real array, a set 
$$\mathbb{R}^m=\{(x_1, ..., x_m)|x_1, ..., x_m \in \mathbb{R}\}$$
is called as m dimentional space.
Every m-ary ordered real array is a point in m dimentional space.

# Algebraic and distance structures
 ## Algebraic structure
 We use superscript to order different coordinates of a point.
 $$x = (x^1, ..., x^m)$$
 We use same method to denote a vector.
 Addition and number multiplication:
 $$u + v = (u^1 + v^1, ..., u^m + v ^m), \\
 \lambda u = (\lambda u^1, ..., \lambda u^m)$$
 A $\mathbb{R}^m$ space with addition and number multiplication is called as a real linear space (real vector space).
 
 ## Distance structure
 ### Norm
 Any function N defined in $\mathbb{R}^m$, meets
 $(N_1)$ $N(x) \geqslant 0, \forall x \in \mathbb{R}^m; and$
 $$ N(x) = 0 \Leftrightarrow x = 0$$
 $(N_2)$ $N(\lambda x) = |\lambda|N(x), \forall x \in \mathbb{R}^m, \lambda \in \mathbb{R}$
 $(N_3)$ $N(x + y) \leqslant N(x) + N(y), \forall x, y \in \mathbb{R}^m$
 We call the function N a norm.
 
 Assume N is a norm in $\mathbb{R}^m$, then N determines a kind of distance
 $$  \lVert x - y\rVert =d_{N}(x, y) = N(x - y)$$
 According the distance, we could define the astringency of point range and the continuity of m-ary function. These are called as the astringency and continuity according norm N.
 
For real space $\mathbb{R}^m$, the astringency and continuity according any norm are equivalent.

#### The equivalence of norm
Definition:
Assume that $M$ and $N$ are two norms in $\mathbb{R}^m$.
If there are positive real num $a, A$, such that
$$aM(x) \leqslant N(x) \leqslant AM(x), \forall x \in \mathbb{R}^m$$
It means that $M$ is equivalent to $N$.

Theorem 1:
The astringency and continuity according equivalent norms are equivalent.

Theorem 2:
Any norms in $\mathbb{R}^m$ is equivalent.

#### Ln norm
$Ln$ norm is a class of norm.
$$L_n = \sqrt[n]{x_1^n +  ... + x_n^n}, n = 2, 3, ...$$
Specially, for $n = 1$
$$L_1 = \vert x_1 \vert + ... + \vert x_n \vert$$

### Distance space

## Converged point sequence
$$(\forall \varepsilon > 0)(\exists N \in \mathbb{N})(\forall n > N)(d(x_n, a) < \varepsilon)$$
it means
$$\lim x_n = a$$

### Cauchy point sequence
Definition: Assume that $\{x_n\}$ is a sequence in $\mathbb{R}^m$.
$$(\forall \varepsilon > 0)(\exists N \in \mathbb{N})(\forall n > N)(\forall p \in \mathbb{N})(\lVert x_{n+p}, x_n \rVert) < \varepsilon)$$
then we call $\{x_n\}$ a Cauchy point sequence.

Cauchy convergence principle:
Assume that $\{x_n\}$ is point sequence in $\mathbb{R}^m$, the necessary and sufficient condition of $\{x_n\}$ converging is that it is a Cauchy point sequence.

# Limit and continuity of multivariate function
Deleted neighborhood:
For all $a \in \mathbb{R}^m$, and $\eta \in \mathbb{R}, \eta >0$, 
$$\check{U}(a, \eta) = \{x \in \mathbb{R}^m | 0 < \lVert x - a\rVert \}$$
is called as a deleted neighborhood of point $a$.

Accumulation point:
Assume that $D \subset \mathbb{R}^m, a \in \mathbb{R}^m$. 
If any deleted neighborhood of point $a$ includes at least one point in $D$, then $a$ is a accumulation point of $D$.

## The limitation of multivariate function
Assume that $D \subset \mathbb{R}^m$, $a$ is a accumulation point of $D$, m-ary function $f$ is defined on $\check{U}(a, \eta) \cap D$.

### Sequential definition
If for all point sequences $\{x_n\}$ that converge to $a$ on $\check{U}(a, \eta) \cap D$, all corresponding sequence of function values $\{f(x_n)\}$ converge to the same real num $A$, we say that
when $x$ converges to $a$ along the set $D$, the function $f(x)$ converges to $A$, denoted as 
$$
\lim_{
\begin{subarray}{l}
   x \rightarrow a \\
   D
\end{subarray}} f(x) = A
$$
simply
$$\lim_{x\rightarrow a} f(x) = A$$

### $\varepsilon-\delta$ definition
If for all $\varepsilon > 0$, exists $\delta > 0$, such that only if
$$x \in D, \lVert x - a \rVert < \delta$$
then 
$$\vert f(x) - A \vert < \varepsilon$$
We have that
$$
\lim_{
\begin{subarray}{l}
   x \rightarrow a \\
   D
\end{subarray}} f(x) = A
$$

These two definition are eqvaluent of course.

## The continuity of multivariate function
Assume that $D \subset \mathbb{R}^m$, $a$ is a accumulation point of $D$, m-ary function $f$ is defined on $\check{U}(a, \eta) \cap D$.
### Continuity
If
$$
\lim_{
\begin{subarray}{l}
   x \rightarrow a \\
   D
\end{subarray}} f(x) = A
$$
the function $f$ is continuous at point $a$ allong the set $D$.
Simply, the function $f$ is continuous at point $a$.

Outlier:
If point $a \in D$, but $a$ is not a accumulation point, i.e.
$$\exists U(a, \eta) \cap D = a$$
we call $a$ a outlier.
Obivously, the function is must continuous at the outlier $a$ along the set $D$.

### Uniform continuity
$\forall x_1, x_2 \in D, \forall \varepsilon > 0, \exists \delta > 0$, only if
$$ \Vert x_1 - x_2 \Vert < \delta$$
then
$$\Vert f(x_1) - f(x_2) \Vert < \varepsilon$$
it means that function $f$ is uniform continuous on $D$.

# Continuous function on bounded closed set
Assume that $E \subset \mathbb{R}^m$, 
if $\exists L \in R$, such that
$$\Vert x \Vert \leqslant L, \forall x \in E$$
the set $E$ is a bounded set in $\mathbb{R}^m$;
if for any converged point sequence $\{x_n\} \in E$, its limitation
$$\lim x_n \in E$$
the set $E$ is a closed set.

## The Extended Bohr Charno - Weierstrass Theorem
Theorem 1:
Assume that $\{x_n\}$ is a bounded sequence in $\mathbb{R}^m$, we have that $\{x_n\}$ has at least one converged subsequence.

Theorem 2:
Assume that $K$ is a bounded closed set in $\mathbb{R}^m$, if the function $f$ is continuous on $K$, we have that $f$ is bounded on $K$.

Theroem 3:
Assume that $K$ is a bounded closed set in $\mathbb{R}^m$, if the function $f$ is continuous on $K$, we have that $f$ could reach its max and min value at a certain point in $K$
$$f(x_{max}) = \sup_{x \in K} f(x) \\
f(x_{min}) = \inf_{x \in K} f(x)$$

Theorem 4:
Assume that $K$ is a bounded closed set in $\mathbb{R}^m$, if the function $f$ is continuous on $K$, we have that $f$ is also uniform continuous on $K$.

