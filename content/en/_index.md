---
title: "go-autodiff documentation"
linkTitle: "Home"
type: docs
cascade:
  type: docs
description: "Automatic differentiation in pure Go. Planned, wave 2 of the go-scikit roadmap."
---

**go-autodiff is the planned home of automatic differentiation for go-scikit**: forward and reverse modes, with Jacobian and Hessian helpers that feed `go-numerics/optimize` gradients and the `JacFunc` of `go-numerics/integrate`, both of which take user-supplied derivatives or finite differences today. It is in **wave 2** (PLAN.md item 8).

**Status: planned (wave 2).** The organisation has no library and no
release tag. These pages state the scope, the plan and the references each
library will be validated against. The plan itself is
[PLAN.md](https://github.com/go-scikit/roadmap/blob/main/PLAN.md) of [go-scikit/roadmap](https://github.com/go-scikit/roadmap),
and the state of each item is in [STATUS.md](https://github.com/go-scikit/roadmap/blob/main/STATUS.md).

## Plan

In PLAN.md, wave 2:

- item 8 (wave 2): forward (dual) and reverse (tape) modes, Jacobians and Hessians for optimize and integrate; size M.

It builds on go-ndarray; it feeds go-numerics/optimize and go-numerics/integrate, and later the neural networks of go-mlkit.

## The libraries

| Library | Status | What it will provide |
| --- | --- | --- |
| [Automatic differentiation]({{< relref "ad" >}}) | planned (wave 2) | Planned for wave 2: forward and reverse automatic differentiation with Jacobian and Hessian helpers. |

Every library of the go-scikit family is pure Go (`CGO_ENABLED=0`), validated
against the tool that is the reference of its domain, run as an oracle from Go,
and measured against it on one core. None of that is claimed here yet: there is
nothing to measure.

## What each library's pages hold

| Library | Pages |
| --- | --- |
| Automatic differentiation | [overview]({{< relref "ad" >}}) |

