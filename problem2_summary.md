# Problem 2 Summary

## Core Result

For an SVM trained on `n` samples with `k` support vectors, the leave-one-out cross-validation error satisfies

```math
LOO(S) \leq \frac{k}{n}.
```

This is an upper bound, not generally an exact equality.

## Why This Works

In leave-one-out cross-validation, one training point is removed, the SVM is retrained, and the left-out point is tested.

If the removed point was **not** a support vector, then removing it does not change the SVM decision boundary. Therefore, that point will still be classified the same way. Only omitted points that are support vectors can potentially create a leave-one-out error.

Since there are only `k` support vectors among `n` training points, at most `k` of the `n` leave-one-out trials can fail, giving the bound `k/n`.

## Connection to Generalization Error

The expected leave-one-out error matches the expected test error of a classifier trained on `n` samples, so

```math
\mathbb{E}[\mathrm{err}(h_S)] = \mathbb{E}[LOO(S)] \leq \mathbb{E}\left[\frac{k}{n}\right].
```

This means fewer support vectors generally imply a tighter upper bound on generalization error.

## Leave-p-Out Generalization

For leave-`p`-out cross-validation, errors can only occur when the omitted subset contains at least one support vector. This gives the bound

```math
LPO_p(S) \leq 1 - \frac{\binom{n-k}{p}}{\binom{n}{p}}.
```

This is the fraction of size-`p` omitted subsets that contain at least one support vector.

### Examples

- Leave-1-out:

```math
LPO_1(S) \leq \frac{k}{n}
```

- Leave-2-out:

```math
LPO_2(S) \leq 1 - \frac{(n-k)(n-k-1)}{n(n-1)}
```

- Leave-3-out:

```math
LPO_3(S) \leq 1 - \frac{(n-k)(n-k-1)(n-k-2)}{n(n-1)(n-2)}
```

When `k << n`, these behave approximately like

```math
LPO_p(S) \approx \frac{pk}{n}.
```

## Practical Interpretation

- Small `k/n` suggests a tighter leave-one-out error bound.
- Larger `p` makes the bound looser.
- At `p = n`, the bound becomes uninformative.
