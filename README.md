# Albanese Variety

The **Albanese variety** is an abelian variety canonically associated with a smooth projective variety, representing the target of the universal morphism to an abelian variety.

## Why It Matters

In algebraic geometry, the Albanese variety captures the first homology group of a variety. It's the algebraic analogue of the Jacobian of a curve and plays a central role in the classification of algebraic varieties and Hodge theory.

## How It Works

Constructed as the dual of the Picard variety, Alb(X) = Pic⁰(X)∨. For a curve, it coincides with the Jacobian. The implementation computes Albanese via integration of holomorphic 1-forms along cycle paths.

## Usage

```toml
[dependencies]
albanese-variety = "0.1.0"
```

```rust
use albanese_variety;

// See examples/ directory for detailed usage
```

## API

- `ComplexTorus` (lib.rs)
- `betti_number` (lib.rs)
- `albanese_dimension` (lib.rs)
- `AlbaneseMap` (lib.rs)

## Architecture

This crate is part of the **[SuperInstance](https://github.com/SuperInstance)** ecosystem — a conservation-law-based framework for fleet coordination, ternary computation, and distributed agent systems.

### Related Crates

- [`superinstance-core`](https://github.com/SuperInstance/superinstance-core) — Core conservation law (γ + η = C)
- [`superinstance-harness`](https://github.com/SuperInstance/superinstance-harness) — Build harness and self-improving loop
- [`fleet-coordinator`](https://github.com/SuperInstance/fleet-coordinator) — Fleet-level coordination

## References

- [SuperInstance Architecture](https://github.com/SuperInstance/SuperInstance/blob/main/ARCHITECTURE.md)
- [Conservation Law Paper](https://github.com/SuperInstance/SuperInstance/blob/main/docs/conservation-law.md)

## License

MIT
