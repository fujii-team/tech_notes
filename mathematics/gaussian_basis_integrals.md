# List of Gaussian Basis Integrals

## Basic integrals
$$
\int_{0}^{u} e^{-x^2}\mathrm{d}x = \frac{\sqrt{\pi}}{2}\mathrm{erf}(u)
$$

$$
\int_{0}^{u} e^{-\alpha x^2}\mathrm{d}x = \frac{\sqrt{\pi}}{2\sqrt{\alpha}}\mathrm{erf}(\sqrt{\alpha}u)
$$

## Gaussian basis integrals
### 1st order
$$
\int_{0}^{u} xe^{-\alpha x^2}\mathrm{d}x =
\frac{1}{2\alpha}\left[1-e^{-\alpha u^2} \right]
$$

$$
\int_{0}^{\infty} xe^{-\alpha x^2}\mathrm{d}x = \frac{1}{2\alpha}
$$
$$
\int_{\infty}^{\infty} xe^{-\alpha x^2}\mathrm{d}x = 0
$$

### 2nd order
$$
\int_{0}^{u} x^2e^{-\alpha x^2}\mathrm{d}x =
\frac{1}{2\alpha\sqrt{\alpha}}
 \left[
  \frac{\sqrt{\pi}}{2}\mathrm{erf}(\sqrt{\alpha}u)-\sqrt{\alpha}ue^{\alpha u^2}
 \right]
$$

$$
\int_{0}^{\infty} x^2e^{-\alpha x^2}\mathrm{d}x =
 \frac{\sqrt{\pi}}{4\alpha\sqrt{\alpha}}
$$
$$
\int_{-\infty}^{\infty} x^2e^{-\alpha x^2}\mathrm{d}x =
 \frac{\sqrt{\pi}}{2\alpha\sqrt{\alpha}}
$$

### 3rd order
$$
\int_{0}^{u} x^3e^{-\alpha x^2}\mathrm{d}x =
\frac{1}{2\alpha\sqrt{\alpha}}
 \left[
  1 - (1+\alpha u^2)e^{-\alpha u^2}
 \right]
$$

$$
\int_{0}^{\infty} x^3e^{-\alpha x^2}\mathrm{d}x =
 \frac{1}{2\alpha^2}
$$
$$
\int_{-\infty}^{\infty} x^3e^{-\alpha x^2}\mathrm{d}x = 0
$$
