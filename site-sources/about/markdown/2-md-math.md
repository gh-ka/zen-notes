---
title: Markdown - Math
author: gh-ka
description: 
icon: 
status: 
# template: 
hide: 
tags:
    - 
cdate: 2026-06-28-Sun 13:20
mdate:
    - 2026-06-28-Sun 13:20
---

# Markdown - Math

contents:

[TOC]

---

## Zensical support

Zensical supports both MathJax and KaTeX, see [docs](https://zensical.org/docs/authoring/math)

### Usage

### Use block syntax

Blocks must be enclosed in `$$...$$` or `\[...\]` on separate lines:

block syntax

```tex
$$
\cos x=\sum_{k=0}^{\infty}\frac{(-1)^k}{(2k)!}x^{2k}
$$
```

$$
\cos x=\sum_{k=0}^{\infty}\frac{(-1)^k}{(2k)!}x^{2k}
$$

### Use inline block syntax

Inline blocks must be enclosed in `$...$` or `\(...\)`:

inline syntax

```tex
The homomorphism $f$ is injective if and only if its kernel is only the
singleton set $e_G$, because otherwise $\exists a,b\in G$ with $a\neq b$ such
that $f(a)=f(b)$.
```

The homomorphism $f$ is injective if and only if its kernel is only the
singleton set $e_G$, because otherwise $\exists a,b\in G$ with $a\neq b$ such
that $f(a)=f(b)$.

## Simple Formulas

**Inline** formulas are wrapped by single dollar sign (`$`), e.g., \$x^2\$ renders as $x^2$

---

**Blocks** begin and end with double dollar sign (`$$`), e.g.:

```tex
$$
a^2 + b^2 = c^2
$$
```

renders as:

\[
a^2 + b^2 = c^2
\]

---

**Matrices** work with `{pmatrix}`, e.g.: 

```tex
$$
\begin{pmatrix}
a & b \cr
c & d
\end{pmatrix}
+
\begin{pmatrix}
e & f \cr
g & h
\end{pmatrix}
$$
```

renders as:

$$
\begin{pmatrix}
a & b \cr
c & d
\end{pmatrix}
+
\begin{pmatrix}
e & f \cr
g & h
\end{pmatrix}
$$
---

If-cases work with `{dcases}`:

```tex
$$
\begin{dcases}
   a &\text{if } b \cr
   c &\text{if } d
\end{dcases}
$$
```

renders:
$$
\begin{dcases}
   a &\text{if } b \cr
   c &\text{if } d
\end{dcases}
$$
---

Summation:

```tex
$$
\displaystyle\sum_{k=3}^5 k^2=3^2 + 4^2 + 5^2 =50
$$
```

rednders as:

$$
\displaystyle\sum_{k=3}^5 k^2=3^2 + 4^2 + 5^2 =50
$$

---


## Cheat Sheet

### Arithmetic

| Notation | Example | Inline | Code Block |
| --- | --- | --- | --- |
| Addition | a+ba+ba+b | `$a+b$` | `$$` `a+b` `$$` |
| Subtraction | a−ba-ba−b | `$a-b$` | `$$` `a-b` `$$` |
| Various Forms of Multiplication | a×ba \\times ba×b a∗ba \\ast ba∗b a⋅ba \\cdot ba⋅b | `$a \times b$` `$a \ast b$` `$a \cdot b$` | `$$` `a \cdot b` `$$` |
| Various Forms of Division | a ⁣:ba \\colon ba:b a/ba / ba/b a÷ba \\div ba÷b ab\\frac{a}{b}ba​ | `$a \colon b$` `$a / b$` `$a \div b$` `$\frac{a}{b}$` | `$$` `a \div b` `$$` |
| Remainder / Modulo | 5mod 2=15 \\mod 2 = 15mod2=1 | `$5\mod 2=1$` | `$$` `5\mod 2=1` `$$` |
| Negative Value | −a-a−a | `$-a$` | `$$` `-a` `$$` |
| Plus or Minus, Minus or Plus | ±a\\pm a±a ∓a\\mp a∓a | `$\pm a$` `$\mp a$` | `$$` `\pm a` `$$` |
| Squared, Cubed, nth-Power | a2a^2a2 a3a^3a3 ana^nan | `$a^2$` `$a^3$` `$a^n$` | `$$` `a^3` `$$` |
| Square Root, Cube Root, nth-Root | a\\sqrt{a}a​ a3\\sqrt\[3\]{a}3a​ an\\sqrt\[n\]{a}na​ | `$\sqrt{a}$` `$\sqrt[3]{a}$` `$\sqrt[n]{a}$` | `$$` `\sqrt[3]{a}` `$$` |

### Equality

| Notation | Example | Inline | Code Block |
| --- | --- | --- | --- |
| Equals | 3=1+23=1+23=1+2 | `$3=1+2$` | `$$` `3=1+2` `$$` |
| Not Equals | 3≠43 \\neq 43=4 | `$3\neq4$` | `$$` `3\neq4` `$$` |
| Identical / Equivalent To | a≡ba \\equiv ba≡b | `$a \equiv b$` | `$$` `a \equiv b` `$$` |
| Proportional To | a∝ba \\propto ba∝b | `$a \propto b$` | `$$` `a \propto b` `$$` |
| Approximately Equal To | sin⁡(0.01)≈0.01\\sin(0.01) \\approx 0.01sin(0.01)≈0.01 | `$\sin(0.01) \approx 0.01$` | `$$` `\sin(0.01) \approx 0.01` `$$` |

### Comparison

| Notation | Example | Inline | Code Block |
| --- | --- | --- | --- |
| a Less Than b a Greater Than b | a<ba < ba<b a>ba > ba>b | `$a<b$` `$a>b$` | `$$` `a<b` `$$` |
| a Less Than or Equal To b a Greater Than or Equal To b | a≤ba \\leq ba≤b a≥ba \\geq ba≥b | `$a \leq b$` `$a \geq b$` | `$$` `a \leq b` `$$` |
| a Much Smaller Than b a Much Larger Than b | a≪ba \\ll ba≪b a≫ba \\gg ba≫b | `$a \ll b$` `$a \gg b$` | `$$` `a \ll b` `$$` |

### Algebra

| Notation | Example | Inline | Code Block |
| --- | --- | --- | --- |
| Factorial | 5!=5×4×3×2×15 ! = 5 \\times 4 \\times 3 \\times 2 \\times 15!=5×4×3×2×1 | `$5!=5 \times 4 \times 3 \times 2 \times 1$` | `$$` `5!=5 \times 4 \times 3 \times 2 \times 1` `$$` |
| Absolute Value | ∣−5∣=5\| -5 \| = 5∣−5∣=5 | `$\|-5\|=5$` | `$$` `\|-5\|=5` `$$` |
| Function Of | f(x)=2x2f(x) = 2x^2f(x)=2x2 | `$f(x)=2x^2$` | `$$` `f(x)=2x^2` `$$` |
| Change or Difference | Δx=x1−x0\\Delta x = x\_1 - x\_0Δx=x1​−x0​ | `$\Delta x = x_1 - x_0$` | `$$` `\Delta x = x_1 - x_0` `$$` |
| Pi | π=3.14159…\\pi = 3.14159…π=3.14159… | `$\pi = 3.14159...$` | `$$` `\pi` `$$` |
| Euler’s Constant | e=2.71828…e = 2.71828…e=2.71828… | `$e = 2.71828...$` | `$$` `e = 2.71828...` `$$` |
| Sum | ∑k=35k2=32+42+52=50\\displaystyle\\sum\_{k=3}^5 k^2 = 3^2 + 4^2 + 5^2 = 50k=3∑5​k2=32+42+52=50 | `$\displaystyle\sum_{k=3}^5 k^2=3^2 + 4^2 + 5^2 =50$` | `$$` `\displaystyle\sum_{k=3}^5 k^2=3^2 + 4^2 + 5^2 =50` `$$` |
| Series Product | ∏x=24x2=22×32×42=576\\displaystyle\\prod\_{x=2}^4 x^2 = 2^2 \\times 3^2 \\times 4^2 = 576x=2∏4​x2=22×32×42=576 | `$\displaystyle\prod_{x=2}^4 x^2 = 2^2 \times 3^2 \times 4^2 = 576$` | `$$` `\displaystyle\sum_{k=2}^4 k^2=2^2 \times 3^2 \times 4^2 = 576` `$$` |
| Brackets & Parentheses | \[…\]\[\\ldots\]\[…\] (…)(\\ldots)(…) | `$[\ldots] (\ldots)$` | `$$` `[\ldots] (\ldots)` `$$` |

### Angles

| Notation | Example | Inline | Code Block |
| --- | --- | --- | --- |
| Angle | ∠\\angle∠ | `$\angle$` | `$$` `\angle` `$$` |
| Degree, Arc Min, Arc Sec | 30°45′30′′30\\degree45\\rq30\\rq\\rq30°45′30′′ | `$30\degree45\rq30\rq\rq$` | `$$` `30\degree45\rq30\rq\rq` `$$` |
| Radians | 360°=2πrad360\\degree = 2\\pi rad360°=2πrad | `$360\degree = 2\pi rad$` | `$$` `360\degree = 2\pi rad` `$$` |

### Probability & Statistics

| Notation | Example | Inline | Code Block |
| --- | --- | --- | --- |
| Probability of Event A | P(A)P(A)P(A) or Pr⁡(A)\\Pr(A)Pr(A) | `$P(A)$ or $\Pr(A)$` | `$$` `P(A)` `$$` |
| Intersection Prob. of A & B | P(A∩B)P(A \\cap B)P(A∩B) | `$P(A \cap B)$` | `$$` `P(A \ca pB)` `$$` |
| Union Prob. of A or B | P(A∪B)P(A \\cup B)P(A∪B) | `$P(A \cup B)$` | `$$` `P(A \cup B)` `$$` |
| Conditional Prob. of A Given B | P(A∣B)P(A \| B)P(A∣B) | `$P(A\|B)$` | `$$` `P(A\|B)` `$$` |
| Median | x~\\tilde{x}x~ | `$\tilde{x}$` | `$$` `\tilde{x}` `$$` |
| Population Mean | μ,x‾,⟨x⟩\\mu , \\overline{x} , \\langle x \\rangleμ,x,⟨x⟩ | `$\mu , \overline{x} , \langle x \rangle$` | `$$` `\mu , \overline{x} , \langle x \rangle` `$$` |
| Standard Deviation | σ\\sigmaσ | `$\sigma$` | `$$` `\sigma` `$$` |
| Varience | σ2\\sigma^2σ2 | `$\sigma^2$` | `$$` `\sigma^2` `$$` |

### Linear Algebra

#### Linear Algebra: Vectors

| Notation | Example | Inline | Code Block |
| --- | --- | --- | --- |
| Vectors | vv‾v⃗\\mathbf{v} \\overline{v} \\vec{v}vvv | `$\mathbf{v}\overline{v}\vec{v}$` | `$$` `\mathbf{v} \overline{v} \vec{v}` `$$` |
| Row Vector | v=(123)v = \\begin{pmatrix} 1 & 2 & 3 \\end{pmatrix}v=(1​2​3​) | `$v=\begin{pmatrix}1&2&3\end{pmatrix}$` | `$$` `v = \begin{pmatrix}` `1 & 2 & 3` `\end{pmatrix}` `$$` |
| Column Vector | w=(456)w = \\begin{pmatrix} 4 \\cr 5 \\cr 6 \\cr \\end{pmatrix}w=⎝⎛​456​⎠⎞​ | `$w=\begin{pmatrix}4\cr5\cr6\cr\end{pmatrix}$` | `$$` `w=\begin{pmatrix}` `4 \cr` `5 \cr` `6 \cr` `\end{pmatrix}` `$$` |
| Dot Product | v⋅w\\mathbf{v} \\cdot \\mathbf{w}v⋅w (v,w)(v,w)(v,w) <v∣w>\\left< v\|w \\right>⟨v∣w⟩ | `$\mathbf{v} \cdot \mathbf{w}$<br>$(v,w)$<br>$\left<v \| w\right>$` | `$$` `\mathbf{v}\cdot\mathbf{w}` `(v,w)` `\left<v\|w \right>` `$$` |
| Cross Product | v×wv \\times wv×w | `$v \times w$` | `$$` `v \times w` `$$` |
| Length of v | ∣v∣\|v\|∣v∣ | `$\|v\|$` | `$$` `\|v\|` `$$` |
| Norm of v | ∣∣v∣∣\|\|v\|\|∣∣v∣∣ | `$\|\|v\|\|$` | `$$` `\|\|v\|\|` `$$` |

#### Linear Algebra: Matrices

| Notation | Example | Inline | Code Block |
| --- | --- | --- | --- |
| Matrix, 2 By 3 | A=\[123456\]A=\\begin{bmatrix} 1 & 2 & 3 \\cr 4 & 5 & 6 \\end{bmatrix}A=\[14​25​36​\] | `$A=\begin{bmatrix}1&2&3\cr4&5&6\end{bmatrix}$` | `$$` `A=` `\begin{bmatrix}` `1 & 2 & 3 \cr` `4 & 5 & 6` `\end{bmatrix}` `$$` |
| Product | A⋅BA \\cdot BA⋅B | `$A \cdot B$` | `$$` `A \cdot B` `$$` |
| Hadamard Product | A∘BA \\circ BA∘B | `$A \circ B$` | `$$` `A \circ B` `$$` |
| Kronecker Product | A⊗BA \\otimes BA⊗B | `$A \otimes B$` | `$$` `A \otimes B` `$$` |
| Transposed Matrix | ATA^TAT | `$A^T$` | `$$` `A^T` `$$` |
| Hermitian Matrix or Conjugate Transpose | A†A^\\dagA† A∗A^\\astA∗ | `$A^\dag$` `$A^\ast$` | `$$` `A^\dag` `A^\ast` `$$` |
| Inverse Matrix | A−1A^{-1}A−1 | `$A^{-1}$` | `$$` `A^{-1}` `$$` |
| Determinant | ∣A∣\|A\|∣A∣ | `$\|A\|$` | `$$` `\|A\|` `$$` |
| Norm | ∣∣A∣∣\|\|A\|\|∣∣A∣∣ | `$\|\|A\|\|$` | `$$` `\|\|A\|\|` `$$` |

### Calculus

| Notation | Example | Inline | Code Block |
| --- | --- | --- | --- |
| Example Function: y=x24y = \\frac{x^2}{4}y=4x2​ | y=x24y = \\frac{x^2}{4}y=4x2​ | `$y = \frac{x^2}{4}$` | `$$` `y = \frac{x^2}{4}` `$$` |
| Integration (Limits: 1 to 4) | A=∫14x2xdxA = \\int\_1^4 \\frac{x^2}{x} dxA=∫14​xx2​dx | `$A = \int_1^4 \frac{x^2}{x} dx$` | `$$` `A = \int_1^4 \frac{x^2}{x} dx` `$$` |
| Differentiation |  |  |  |
| First Derivative With Respect To xxx | dfdx\\frac{df}{dx}dxdf​ | `$\frac{df}{dx}$` | `$$` `\frac{df}{dx}` `$$` |
| Partial Derivative With Respect To xxx | ∂f∂x\\frac{\\partial f}{\\partial x}∂x∂f​ | `$\frac{\partial f}{\partial x}$` | `$$` `\frac{\partial f}{\partial x}` `$$` |
| First and Second Derivative of Function | f′f\\rqf′ f′′f\\rq\\rqf′′ | `$f\rq$` `$f\rq\rq$` | `$$` `f\rq` `f\rq\rq` `$$` |
| First and Second Derivative With Respect To Time | f˙\\dot ff˙​ f¨\\ddot ff¨​ | `$\dot f$` `$\ddot f$` | `$$` `\dot f` `\ddot f` `$$` |

### Complex Numbers

| Notation | Example | Inline | Block |
| --- | --- | --- | --- |
| Imaginary Unit iii | z=3+2iz=3+2iz=3+2i | `$z=3+2i$` | `$$` `z=3+2i` `$$` |
| Real Part Of Complex Number | ℜ(z)=3\\Re(z)=3ℜ(z)=3 Re⁡(z)=3\\operatorname{Re}(z)=3Re(z)=3 | `$\Re(z)=3$` `$\operatorname{Re}(z)=3$` | `$$` `\Re(z)=3` `\operatorname{Re}(z)=3` `$$` |
| Imaginary Part Of Complex Number | ℑ(z)=2\\Im(z)=2ℑ(z)=2 Im⁡(z)=2\\operatorname{Im}(z)=2Im(z)=2 | `$\Im(z)=2$` `$\operatorname{Im}(z)=2$` | `$$` `\Im(z)=2` `\operatorname{Im}(z)=2` `$$` |
| Complex Conjugate | zˉ=z∗=3−2i\\bar{z}=z^\*=3-2izˉ=z∗=3−2i | `$\bar{z}=z^*=3-2i$` | `$$` `\bar{z}=z^*=3-2i` `$$` |

### Greek Alphabet

| Letter | Lower | Inline | Upper | Inline |
| --- | --- | --- | --- | --- |
| Alpha | α\\alphaα | `$\alpha$` | A\\AlphaA | `$\Alpha$` |
| Beta | β\\betaβ | `$\beta$` | B\\BetaB | `$\Beta$` |
| Gamma | γ\\gammaγ | `$\gamma$` | Γ\\GammaΓ | `$\Gamma$` |
| Delta | δ\\deltaδ | `$\delta$` | Δ\\DeltaΔ | `$\Delta$` |
| Epsilon | ϵ\\epsilonϵ | `$\epsilon$` | E\\EpsilonE | `$\Epsilon$` |
| Zeta | ζ\\zetaζ | `$\zeta$` | Z\\ZetaZ | `$\Zeta$` |
| Eta | η\\etaη | `$\eta$` | H\\EtaH | `$\Eta$` |
| Theta | θ\\thetaθ | `$\theta$` | Θ\\ThetaΘ | `$\Theta$` |
| Iota | ι\\iotaι | `$\iota$` | I\\IotaI | `$\Iota$` |
| Kappa | κ\\kappaκ | `$\kappa$` | K\\KappaK | `$\Kappa$` |
| Lambda | λ\\lambdaλ | `$\lambda$` | Λ\\LambdaΛ | `$\Lambda$` |
| Mu | μ\\muμ | `$\mu$` | M\\MuM | `$\Mu$` |
| Nu | ν\\nuν | `$\nu$` | N\\NuN | `$\Nu$` |
| Xi | ξ\\xiξ | `$\xi$` | Ξ\\XiΞ | `$\Xi$` |
| Omicron | ο\\omicronο | `$\omicron$` | O\\OmicronO | `$\Omicron$` |
| Pi | π\\piπ | `$\pi$` | Π\\PiΠ | `$\Pi$` |
| Rho | ρ\\rhoρ | `$\rho$` | P\\RhoP | `$\Rho$` |
| Sigma | σ\\sigmaσ | `$\sigma$` | Σ\\SigmaΣ | `$\Sigma$` |
| Tau | τ\\tauτ | `$\tau$` | T\\TauT | `$\Tau$` |
| Upsilon | υ\\upsilonυ | `$\upsilon$` | Υ\\UpsilonΥ | `$\Upsilon$` |
| Phi | ϕ\\phiϕ | `$\phi$` | Φ\\PhiΦ | `$\Phi$` |
| Chi | χ\\chiχ | `$\chi$` | X\\ChiX | `$\Chi$` |
| Psi | ψ\\psiψ | `$\psi$` | Ψ\\PsiΨ | `$\Psi$` |
| Omega | ω\\omegaω | `$\omega$` | Ω\\OmegaΩ | `$\Omega$` |

## Refs

- [KaTeX](https://katex.org/) - supported by vscode
- https://www.upyesp.org/posts/makrdown-vscode-math-notation/

