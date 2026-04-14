[中文](./Math.zh.md) | **English**

# Math & LaTeX

Gleaner renders math formulas using [MathJax](https://www.mathjax.org/), matching Obsidian's behavior. Both inline and block formulas are supported.

## Inline Formulas

Wrap inline math with single dollar signs: `$...$`

Einstein's famous equation $E = mc^2$ changed physics forever. The quadratic formula $x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$ solves any quadratic equation.

## Block Formulas

Wrap display math with double dollar signs: `$$...$$`

The Gaussian integral:

$$\int_{-\infty}^{\infty} e^{-x^2} \, dx = \sqrt{\pi}$$

Euler's identity:

$$e^{i\pi} + 1 = 0$$

## Common Examples

### Fractions and Roots

$$\frac{n!}{k!(n-k)!} = \binom{n}{k}$$

### Summation and Products

$$\sum_{i=1}^{n} i = \frac{n(n+1)}{2}$$

$$\prod_{i=1}^{n} i = n!$$

### Matrices

$$\begin{pmatrix} a & b \\ c & d \end{pmatrix} \begin{pmatrix} x \\ y \end{pmatrix} = \begin{pmatrix} ax + by \\ cx + dy \end{pmatrix}$$

### Greek Letters

Inline Greek letters work naturally: $\alpha$, $\beta$, $\gamma$, $\delta$, $\epsilon$, $\theta$, $\lambda$, $\pi$, $\sigma$, $\omega$.

### Calculus

$$\frac{d}{dx}\left[\int_0^x f(t)\,dt\right] = f(x)$$

### Extra-Long Formula

$$\mathcal{L}_{\text{total}} = \underbrace{-\frac{1}{4}F_{\mu\nu}F^{\mu\nu}}_{\text{gauge}} + \underbrace{\bar{\psi}(i\gamma^\mu D_\mu - m)\psi}_{\text{fermion}} + \underbrace{(D_\mu\phi)^\dagger(D^\mu\phi) - V(\phi)}_{\text{scalar}} + \underbrace{\lambda_y \bar{\psi}_L \phi \psi_R + \text{h.c.}}_{\text{Yukawa}} + \underbrace{\theta\frac{g^2}{32\pi^2}F_{\mu\nu}\tilde{F}^{\mu\nu}}_{\text{topological}} + \underbrace{\frac{1}{16\pi G}\int d^4x\sqrt{-g}\,R}_{\text{gravity}}$$

## Code Blocks Are Not Affected

The dollar sign `$` in code blocks and inline code is left as-is:

```python
price = 9.99
print(f"Total: ${price}")
```

Inline code: `$HOME` and `$PATH` are shell variables, not formulas.

## Error Handling

When a formula contains invalid LaTeX, Gleaner falls back to displaying the raw text with an error message:

$$\invalidcommand{this will show an error}$$

## Wikilinks in Formulas

Formulas can appear alongside [[Wikilink Syntax|wikilinks]] — the `$` and `[[` delimiters do not interfere with each other.
