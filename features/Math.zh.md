[English](./Math.md) | **中文**

# 数学公式与 LaTeX

Gleaner 使用 [MathJax](https://www.mathjax.org/) 渲染数学公式，与 Obsidian 行为一致。支持行内公式和块级公式。

## 行内公式

用单个美元符号包裹行内公式：`$...$`

爱因斯坦的著名方程 $E = mc^2$ 改变了物理学。一元二次方程的求根公式 $x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$ 可以解任意二次方程。

## 块级公式

用双美元符号包裹独立公式：`$$...$$`

高斯积分：

$$\int_{-\infty}^{\infty} e^{-x^2} \, dx = \sqrt{\pi}$$

欧拉恒等式：

$$e^{i\pi} + 1 = 0$$

## 常见示例

### 分数与根号

$$\frac{n!}{k!(n-k)!} = \binom{n}{k}$$

### 求和与连乘

$$\sum_{i=1}^{n} i = \frac{n(n+1)}{2}$$

$$\prod_{i=1}^{n} i = n!$$

### 矩阵

$$\begin{pmatrix} a & b \\ c & d \end{pmatrix} \begin{pmatrix} x \\ y \end{pmatrix} = \begin{pmatrix} ax + by \\ cx + dy \end{pmatrix}$$

### 希腊字母

行内希腊字母自然呈现：$\alpha$、$\beta$、$\gamma$、$\delta$、$\epsilon$、$\theta$、$\lambda$、$\pi$、$\sigma$、$\omega$。

### 微积分

$$\frac{d}{dx}\left[\int_0^x f(t)\,dt\right] = f(x)$$

### 超长公式

$$\mathcal{L}_{\text{total}} = \underbrace{-\frac{1}{4}F_{\mu\nu}F^{\mu\nu}}_{\text{gauge}} + \underbrace{\bar{\psi}(i\gamma^\mu D_\mu - m)\psi}_{\text{fermion}} + \underbrace{(D_\mu\phi)^\dagger(D^\mu\phi) - V(\phi)}_{\text{scalar}} + \underbrace{\lambda_y \bar{\psi}_L \phi \psi_R + \text{h.c.}}_{\text{Yukawa}} + \underbrace{\theta\frac{g^2}{32\pi^2}F_{\mu\nu}\tilde{F}^{\mu\nu}}_{\text{topological}} + \underbrace{\frac{1}{16\pi G}\int d^4x\sqrt{-g}\,R}_{\text{gravity}}$$

## 代码块不受影响

代码块和行内代码中的美元符号 `$` 保持原样：

```python
price = 9.99
print(f"Total: ${price}")
```

行内代码：`$HOME` 和 `$PATH` 是 shell 变量，不是公式。

## 错误处理

当公式包含无效的 LaTeX 时，Gleaner 会回退显示原始文本并提示错误：

$$\invalidcommand{这里会显示错误}$$

## 公式与 Wikilinks

公式可以与 [[Wikilink Syntax|双向链接]] 共存——`$` 和 `[[` 定界符互不干扰。
