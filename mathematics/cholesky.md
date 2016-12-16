# List of formulas related to Cholesky decomposition

## Definition
The Cholesky factor of positive-definite symmetric matrix $X$ is
$$
X = L L^\top
$$
where $L$ is a lower triangular matrix.

## Trace
### Theorem
The trace of $X$ is
$$
Tr(X) = \sum_{i,j}L_{i,j}^2
$$
### Proof
$$
Tr(X) = \sum_{i}X_{i,i} = \sum_{i}\left(\sum_{j}L_{i,j}L_{j,i}^\top\right)
= \sum_{i,j}L_{i,j}^2
$$

## Determinant
### Theorem
The determinant of $X$ is
$$
\mathrm{det}(X) = \prod_{i}L_{i,i}^2
$$
### Proof
$$
\mathrm{det}(X) = \mathrm{det}(L) \times \mathrm{det}(L^\top)
 = \prod_{i}L_{i,i} \times \prod_{i}L_{i,i} = \prod_{i}L_{i,i}^2
$$
