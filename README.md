# Albanese Variety

**Albanese Variety** is a Rust library implementing computational primitives for the Albanese variety — the abelian variety canonically associated to a smooth projective algebraic variety, serving as the universal receiver of regular 1-forms.

## Why It Matters

The Albanese variety is a fundamental construction in algebraic geometry, providing a bridge between the topology of a variety and the theory of abelian varieties. For a smooth projective variety X of dimension n over ℂ, the Albanese variety Alb(X) is an abelian variety of dimension g = h^{1,0}(X) (the genus), equipped with a canonical morphism alb: X → Alb(X) that is universal among morphisms from X to abelian varieties. This universality makes it indispensable in the classification of algebraic varieties, the study of periods and Hodge structures, and arithmetic geometry. The dual relationship between Alb(X) and the Picard variety Pic⁰(X) is a cornerstone of Hodge theory.

## How It Works

**Complex Torus Structure:**
The Albanese variety is constructed as a quotient:

```
Alb(X) = H⁰(X, Ω¹)* / H₁(X, ℤ)
```

Where H⁰(X, Ω¹)* is the dual of the space of holomorphic 1-forms (dimension g), and H₁(X, ℤ) is the first homology group (a lattice of rank 2g). The result is a complex torus ℂ^g / Λ with a Riemann form making it an abelian variety.

**Period Matrix:**
The lattice Λ is encoded as a g × 2g period matrix Π, where the first g columns are a basis for H⁰(X, Ω¹) evaluated on a symplectic basis of H₁, and the second g columns are their imaginary counterparts. The implementation stores this as a row-major `Vec<Vec<f64>>`.

**Betti Number:**
The first Betti number b₁ = 2g directly determines the torus dimension:

```
b₁(X) = rank H₁(X, ℤ) = 2g
```

**Albanese Map:**
Given a base point p₀ ∈ X, the Albanese map sends p ∈ X to the class of the path integral:

```
alb(p) = [∫_{p₀}^{p} ω₁, ∫_{p₀}^{p} ω₂, ..., ∫_{p₀}^{p} ωg] ∈ ℂ^g / Λ
```

The implementation uses a simplified identity map for the placeholder, with the base point set to the origin.

**Key properties:**
- dim Alb(X) = h^{1,0}(X) = genus g
- Alb(X) is dual to Pic⁰(X) (Picard variety)
- The Albanese map is universal for morphisms to abelian varieties

## Quick Start

```rust
fn main() {
    let torus = ComplexTorus::new(2);
    assert_eq!(torus.dimension, 2);
    assert_eq!(torus.period_matrix.len(), 2);

    assert_eq!(betti_number(3), 6);

    let map = AlbaneseMap::new(2);
    let result = map.map(&[1.0, 2.0, 3.0]);
    assert_eq!(result.len(), 2);
}
```

## API

| Type/Function | Description |
|---------------|-------------|
| `ComplexTorus` | ℂ^g / Λ with period matrix |
| `ComplexTorus::new` | Identity period matrix |
| `betti_number` | `genus → 2 × genus` |
| `albanese_dimension` | `genus → genus` (h^{1,0}) |
| `AlbaneseMap` | Canonical map X → Alb(X) |
| `AlbaneseMap::map` | Project point to Albanese torus |

## Architecture Notes

The Albanese variety provides the **geometric invariant theory** foundation for certain SuperInstance fleet topology computations. Within γ + η = C, the period matrix structure informs how conservation-law observations on high-dimensional variety spaces (γ-layer sensor configurations) map to lower-dimensional abelian invariants (η-layer compressed representations).

See [ARCHITECTURE.md](https://github.com/SuperInstance/SuperInstance/blob/main/ARCHITECTURE.md).

The Albanese variety is constructed via integration of holomorphic 1-forms along 1-cycles. For a curve of genus g, the resulting complex torus ℂ^g / Λ has dimension g. The period matrix Π must satisfy the Riemann bilinear relations for the torus to be an abelian variety (i.e., possess a positive-definite Riemann form). This integrality constraint on the period matrix is the computational bottleneck in explicit Albanese computations for varieties of genus > 3.

**Dual relationship:** The Albanese variety is dual (in the sense of abelian variety duality) to the Picard variety Pic⁰(X), parameterizing divisor classes algebraically equivalent to zero. This Alb(X) ↔ Pic⁰(X) duality is a special case of the more general Fourier-Mukai duality on derived categories.

## References

1. Birkenhake, C. & Lange, H. (2004). *Complex Abelian Varieties*. 2nd ed. Springer. Chapter 11: Albanese and Picard Variety.
2. Griffiths, P. & Harris, J. (1978). *Principles of Algebraic Geometry*. Wiley. Chapter 2: Riemann Surfaces and Period Matrices.

## License

MIT
