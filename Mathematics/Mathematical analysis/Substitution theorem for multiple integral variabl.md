[toc]

## Substitution theorem for multiple integral variables
Let $\Omega$ is a open set in $R^m$
$$\varphi:  \Omega \rightarrow R^m$$
is a continuous differentiable mapping, $E \subset \Omega$ is a closed Jordan measurable set. If
1. $\det D\varphi(t) \neq 0, \forall t \in int E$
2. $\varphi$ is injective in $int E$

Then, $\varphi(E)$ is a closed Jordan measurable set too, and for $\forall f(x)$ that is contimuous in $\varphi(E)$:
$$ \int_{\varphi(E)}f(x)dx = \int_{E}f(\varphi(t))|\det D\varphi(t)|dt $$

## Prove
We could prove this theorem by following clue.

Lemma 1, we prove that $\varphi$ is a finite mapping, it means
$$ |\varphi(x) - \varphi(y)| \leqslant \lambda|x - y|, \forall x, y \in K$$
$K \subset \Omega$ is a compact set.

According to lemma 1, we have lemma 2.
Lemma 2, any closed Jordan measurable set could be fitted using simple graphics.
A simple graphic is a union set of finite closed block that has not public interior point each other.
It means
$$v(E - S) \le \varepsilon,\\
v(\varphi(E) - \varphi(S)) \le \varepsilon,\\
S=S_{\varepsilon} \subset intE$$

Accoding to lemma 2, we have lemma 3
If for all closed bolck $\Pi \subset intE$, we have 
$$ \int_{\varphi(\Pi)}f(x)dx = \int_{\Pi}f(\varphi(t))|\det D\varphi(t)|dt $$
then the theorem holds.

Lemma 4, for simple mapping, the theorem obviouly holds.
A simple mapping is a transformation that changes only one variable.
$$
\begin{aligned}
\varphi :
\begin{cases}
    x^i = t^i (i \neq h), \\
    x^h = \varphi^{h}(t^1, ..., t^m).
\end{cases}
\end{aligned}
$$

According to lemma 4, we have
Lemma 5, if $\det D\varphi(\tau) \neq 0$, $\exists \delta,  \forall E \subset U_{\rho}(\tau, \delta)$, the theorem holds.
In the neighborhood $U_{\rho}(\tau, \delta)$, we could divide any complex mapping to a series of simple mapping.

At last, we could use a finite set $U$ of sets to cover $E$
$$U_{\rho}(\tau_1, \frac{\delta_1}{2}), ..., U_{\rho}(\tau_p, \frac{\delta_p}{2})$$
then we could divide any closed block in E to a set of smaller colsed bolcks that covered with $U$
$$ \Pi_1, ..., \Pi_r,\\
l(\Pi_k) < \mu = min\{\frac{\delta_1}{2}, ..., \frac{\delta_p}{2}\}$$
Then, any $\Pi_k$ intersects with a $U_{\rho}(\tau_h, \frac{\delta_h}{2})$, so $\Pi_k \subset U_{\rho}(\tau_h, \delta_h)$.
According lemma 3, 4, 5, we have proven the theorem.


## Application
Then we could do some usual substitution.
According the substituantion theorem,
$$ |\frac{\partial(y^1, ..., y^n)}{\partial(x^1, ..., x^n)}|dx^1...dx^n = |\frac{\partial(y^1, ..., y^n)}{\partial(x^1, ..., x^n)}|\Delta x^1...\Delta x^n$$
we call this as area element in curved coordinates.

### Polar coordinate transformation
We uausaly use the polar coordinate transformation in two dimensions.
$$
\begin{aligned}
\varphi :
\begin{cases}
    x = r\cos \theta, \\
    y = r\sin \theta
\end{cases}
\end{aligned}
$$
The area element area
$$ |\frac{\partial(x, y)}{\partial(r, \theta)}|drd\theta = rdrd\theta$$
Expandably, we could add two coefficiants a and b at front.
$$
\begin{aligned}
\varphi :
\begin{cases}
    x = ar\cos \theta, \\
    y = br\sin \theta
\end{cases}
\end{aligned}
$$
The area element area multipled with a and b, 
$$abrdrd\theta$$

### Cylindrical coordinate transformation
Cylindrical coordinate transformation is the linear expandment of polar in 3 dimentions space.
$$
\begin{aligned}
\varphi :
	\begin{cases}
    x = r\cos \theta, \\
    y = r\sin \theta, \\
	z = z.
	\end{cases}
\end{aligned}
$$
Obviously, area element is 
$$rdrd\theta$$

### Spherical coordinate transformation and n dimentions expanding
Normaly, we use spherical coordinate transformation to calculate integrands on a 3D balls.
$$
\begin{aligned}
\varphi :
	\begin{cases}
    x = r\cos \theta \cos \varphi, \\
    y = r\sin \theta \cos \varphi, \\
	z = r\sin \varphi.
	\end{cases}
\end{aligned}
$$
assume that $\theta \in [0, 2\pi]$, $\varphi \in [-\frac{\pi}{2}, \frac{\pi}{2}]$.
$$ |\frac{\partial(x, y, z)}{\partial(r, \theta, \varphi)}|drd\theta d\varphi = r^2\cos \varphi drd\theta d\varphi$$

Then, we could extend it to n dimensions.
$$
\begin{aligned}
\varphi :
	\begin{cases}
    x_1 = r\cos \theta_1 \cos \theta_2 ... \cos \theta_{n-2} \cos \theta_{n-1}, \\
    x_2 = r\sin \theta_1 \cos \theta_2 ... \cos \theta_{n-2} \cos \theta_{n-1}, \\
	x_3 = r\sin \theta_2 ... \cos \theta_{n-2} \cos \theta_{n-1}, \\
	........................................... \\
	x_{n-1} = r\sin \theta_{n-2} \cos \theta{n-1}, \\
	x_n = r\sin \theta_{n-1}.
	\end{cases}
\end{aligned}
$$
it transforms a closed cuboid
$$
\begin{aligned}
	\begin{cases}
	0 \leqslant r \leqslant a, 0 \leqslant \theta_1 \leqslant 2\pi, \\
	-\frac{\pi}{2} \leqslant \theta_{2}, ..., \theta_{n-1} \leqslant \frac{\pi}{2}. 
	\end{cases}
\end{aligned}
$$
to a cloased ball
$$ x_1^2 + ... + x_n^2 \leqslant a^2$$
We could use recursion to calculate the area element
$$ J_n = r\cos^{n-2}\theta_{n-1}J_{n-1} \\
J_2 = r\\
J_n = r^{n-1}\cos^{n-2}\theta{n-1}\cos^{n-3}\theta{n-2}...\cos \theta_2$$

