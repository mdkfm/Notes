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

### Ln norm
Ln norm is a class of norm.
$$L_n = \sqrt[n]{x_1^n +  ... + x_n^n}$$

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

