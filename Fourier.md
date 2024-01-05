# Fourier Transform


## Dirac Delta Function

The Dirac Delta Function, denoted as $\delta(x)$, is a mathematical function having the following properties:

1. **Zero Everywhere Except at Zero:**
   The Dirac Delta Function $\delta(x)$ is defined as:
   $$
   \delta(x) = \begin{cases} 
   \infty & \text{for } x = 0 \\
   0 & \text{for } x \neq 0
   \end{cases}
   $$
   with the additional property that its integral over the entire real line is 1.

2. **Integral over the Real Line:**
   The integral of $\delta(x)$ over the real line is 1:
   $$
   \int_{-\infty}^{\infty} \delta(x) \, dx = 1
   $$

> **Sifting Property:**
>
>   For a function $f : \mathbb{R} \to \mathbb{R}$ that is continuous (at least on a):
>   $$f(a) = \int_{-\infty}^{\infty} f(x) \delta(x - a) \, dx$$
>
>This property allows the function to 'pick out' the value of another function at a particular point through integration.
>
> **Proof :**
>
>Because $\delta = 0$ everywhere except on $a$:
>
>$$
>\begin{align*}
>\int_{-\infty}^{\infty} f(x) \delta(x - a) \, dx &= \int_{-\infty}^{\infty} f(a) \delta(x - a) \, dx\\
>&= f(a) \int_{-\infty}^{\infty} \delta(x - a) \, dx\\
>&= f(a)
>\end{align*}
>$$



Several mathematical functions exhibit properties similar to the Dirac Delta function. These include:

1. **Normal Distribution Function in the Limit:**
   A normalized Gaussian function becomes similar to the Dirac Delta function as its variance approaches zero. This is represented as:
   $$\lim_{\sigma \to 0} \frac{1}{\sigma\sqrt{2\pi}} e^{-\frac{x^2}{2\sigma^2}} = \delta(x).$$

2. **Sinc Function:**
   The sinc function, particularly when normalized, also approximates the Dirac Delta function as its width goes to infinity:
   $$\lim_{a \to \infty} \frac{\sin(ax)}{\pi x} = \delta(x).$$

3. **Rectangular Pulse Function:**
   A rectangular pulse function (or boxcar function) narrows down to the Dirac Delta function as its width becomes infinitesimally small:
   $$\lim_{a \to 0} \frac{1}{a} \text{rect}\left(\frac{x}{a}\right) = \delta(x),$$
   where $\text{rect}(x)$ is the rectangular function, which is 1 for $|x| \leq \frac{1}{2}$ and 0 otherwise.

These functions serve as practical approximations of the Dirac Delta function in various fields, particularly in signal processing and physics.


## Fourier Transform

The **Fourier Transform** of a function $f(t)$ is given by the equation:
$$
F(\omega) = \int_{-\infty}^{\infty} f(t) e^{-i\omega t} dt
$$
This equation transforms $f(t)$, a function of time, into $F(\omega)$, a function of frequency. It essentially multiplies $f(t)$ by a complex exponential that oscillates at frequency $\omega$, and integrates over all time. This process decomposes the function into its frequency components.

The **Inverse Fourier Transform** allows us to reconstruct $f(t)$ from $F(\omega)$ and is given by:
$$
f(t) = \frac{1}{2\pi} \int_{-\infty}^{\infty} F(\omega) e^{i\omega t} d\omega
$$
This equation does the reverse of the Fourier Transform - it takes the frequency-domain function $F(\omega)$ and reconstructs the original time-domain function $f(t)$ by integrating over all frequencies.

## Proof of Consistency between Fourier Transform and its Inverse

**Fourier Transform** of a function $f(t)$ is given by:
$$
    F(\omega) = \int_{-\infty}^{\infty} f(t) e^{-i\omega t} dt
$$

**Inverse Fourier Transform** is defined as:
$$
    f(t) = \frac{1}{2\pi} \int_{-\infty}^{\infty} F(\omega) e^{i\omega t} d\omega
$$

Applying the Inverse Fourier Transform to $F(\omega)$, we get:
$$
\begin{align*}
    f(t) &= \frac{1}{2\pi} \int_{-\infty}^{\infty} F(\omega) e^{i\omega t} d\omega \\
    &= \frac{1}{2\pi} \int_{-\infty}^{\infty} \left( \int_{-\infty}^{\infty} f(\tau) e^{-i\omega \tau} d\tau \right) e^{i\omega t} d\omega \\
    &= \frac{1}{2\pi} \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} f(\tau) e^{-i\omega \tau} e^{i\omega t} d\tau d\omega \\
    &=  \int_{-\infty}^{\infty} f(\tau) \left( \frac{1}{2\pi} \int_{-\infty}^{\infty} e^{i\omega (t - \tau)} d\omega \right) d\tau
\end{align*}
$$


Using the property of the Dirac delta function $\delta(t - \tau)$:
$$
    \delta(t - \tau) = \frac{1}{2\pi} \int_{-\infty}^{\infty} e^{i\omega (t - \tau)} d\omega
$$

Substituting this back into the reconstructed function:
$$
    f(t) = \int_{-\infty}^{\infty} f(\tau) \delta(t - \tau) d\tau \\
    = f(t)
$$

This proves that applying the Fourier Transform followed by the Inverse Fourier Transform to a function $f(t)$ returns the original function $f(t)$. The process is consistent and validates the mathematical formulation of both the Fourier Transform and its inverse.


## $\delta(t-\tau)\frac{1}{2\pi} \int_{-\infty}^{\infty} e^{i(x-\tau)} \, dx$

Let shows that $\frac{1}{2\pi} \int_{-\infty}^{\infty} e^{i(x-\tau)} \, dx$ can be considered equivalent to $\delta(t-\tau)$:

1. **When $t = \tau$:**
   $$\frac{1}{2\pi} \int_{-\infty}^{\infty} 1 \, dt = \infty$$

2. **When $ t \neq \tau $:**
   Starting with the integral:
   $$
   \begin{align*}
       \frac{1}{2\pi} \int_{-\infty}^{\infty} e^{i(t - \tau)} dt &= \frac{1}{2\pi} \left( \underbrace{\int_{-\infty}^{\infty} \cos(t - \tau) dt}_{0} + i \underbrace{ \int_{-\infty}^{\infty} \sin(t - \tau) dt}_{0} \right) \\
       &= 0
   \end{align*}
   $$
   Since the integral of $\cos(x - \tau)$ over an infinite interval is zero for $ t \neq \tau $.


The integral $\frac{1}{2\pi} \int_{-\infty}^{\infty} e^{i(x-\tau)} \, dx$ can also be viewed as the Fourier transform of a constant function. Since the Fourier transform of a constant function (except at the origin) is zero, this integral also evaluates to zero. This perspective simplifies the understanding of the integral's behavior and its connection to the Fourier transform
