---
title: "Automatic differentiation"
weight: 10
description: "Planned for wave 2: forward and reverse automatic differentiation with Jacobian and Hessian helpers."
---

<!-- From go-scikit/roadmap PLAN.md and its bib/ files: the text is the plan's, summarised, with links to the references. Change it there first. -->

**Status: planned, wave 2; repository not created yet, `ad` is the name proposed in the roadmap bibliography.**

Forward and reverse automatic differentiation for Go (PLAN.md item 8, wave 2, size M). The organisation is to hold one library, proposed as `ad`.

No code exists yet: nothing on this page is released, measured or tested. It
says what the library is planned to provide and how it will be checked. The wave
and the order are in [PLAN.md](https://github.com/go-scikit/roadmap/blob/main/PLAN.md); the state of each item in
[STATUS.md](https://github.com/go-scikit/roadmap/blob/main/STATUS.md).

## What it will provide

| | |
|---|---|
| Forward mode | dual and hyper-dual types with explicit methods (`Add`, `Mul`) |
| Reverse mode | a tape (Wengert list) built by calling tape methods, one sweep per gradient |
| Jacobians and Hessians | helpers, including forward-over-reverse Hessian-vector products |
| Solver glue | gradients for `go-numerics/optimize` and an AD-built Jacobian for `integrate`'s `JacFunc` |

## References

The references the work starts from (bibliography first):

- Griewank and Walther, *Evaluating Derivatives*, 2nd ed., SIAM 2008, doi:10.1137/1.9780898717761
- [Baydin, Pearlmutter, Radul and Siskind, Automatic differentiation in machine learning: a survey, JMLR 18(153), 2018](https://jmlr.org/papers/v18/17-468.html)
- [The Go language specification (no operator overloading; type parameters)](https://go.dev/ref/spec)
- [Tapenade, source transformation](https://tapenade.gitlabpages.inria.fr/tapenade/distrib/LICENSE.html)

## Reference implementations

| Implementation | Licence and use |
|---|---|
| itsubaki/autograd (Go) | MIT; a reference for tape AD |
| gorgonia (Go) | Apache-2.0; ideas for graph-based AD on tensors |
| pointlander/gradient (Go) | BSD-3-Clause; a reference |
| pbenner/autodiff (Go) | GPL-3.0: read-only, the licence blocks reuse |
| Tapenade, Enzyme, JAX | MIT, Apache-2.0 with LLVM exception, Apache-2.0: design references and derivative oracles |

## How it will be validated

Reference tools are run as oracles, driven from Go by exec with JSON on a pipe;
the unit suite must pass with no oracle installed.

| Oracle | How |
|---|---|
| JAX | `uv run --with jax`; Jacobians and Hessians as reference values |
| Finite differences | `optimize.CheckGrad` and `ApproxFprime` in go-numerics |
| Analytic derivatives | closed forms for the test functions |

What "correct" means:

| Area | Criterion |
|---|---|
| Forward and reverse vs analytic | exact to rounding; maximum relative error and ULPs reported |
| Against finite differences | agreement to O(h) |

## Risks and open questions

- Go has no operator overloading (language specification), so AD is one of: dual-number types with explicit methods, a tape built by method calls, source transformation with `go/parser`, `go/ast` and `go/types`, or generics over an interface of operations. The design is not fixed.
- Retrofitting an existing `func([]float64) float64` objective is only possible by rewriting a restricted subset of Go with `go/ast`.
- go-symbolic's code generation is to emit gradient code that matches this tape (the reverse-mode sharing of Griewank and Walther).
