# MicroPoroChemoMechanics

<p align="center">
  <img src="https://github.com/MicroPoroChemoMechanics/.github/blob/main/profile/logo.svg?raw=true" width="160" alt="MicroPoroChemoMechanics logo"/>
</p>

_Julia ecosystem for the coupled micro-chemo-mechanics of porous reactive media_

_Computational chemistry · Mean-field homogenization · Adaptive cubature · Structured tensors · Reactive transport · Poromechanics_

---

**MicroPoroChemoMechanics** is a family of Julia packages for the
multiscale modelling of porous reactive materials — from molecular-level
thermodynamic equilibrium to macroscopic poromechanical response.
Every package is `ForwardDiff`-compatible, dimensionally aware via
`DynamicQuantities` where relevant, and designed to compose cleanly
with the [SciML](https://sciml.ai/) ecosystem (`Optimization`,
`OrdinaryDiffEq`, `NonlinearSolve`, `Integrals`, …).

The packages `TensND.jl`, `DECUHR.jl`, `OptimaSolver.jl`, `ChemistryLab.jl`
and `MeanFieldHomogenization.jl` are registered in Julia's **General registry**
and install with `Pkg.add`. `PoroMechanics.jl`, the most recent addition, is not
registered yet and installs from its repository URL.

---

## Packages

### [ChemistryLab.jl](https://github.com/MicroPoroChemoMechanics/ChemistryLab.jl) — Computational chemistry toolkit

[![Docs stable](https://img.shields.io/badge/docs-stable-blue.svg)](https://MicroPoroChemoMechanics.github.io/ChemistryLab.jl/stable/)
[![Docs dev](https://img.shields.io/badge/docs-dev-blue.svg)](https://MicroPoroChemoMechanics.github.io/ChemistryLab.jl/dev/)
[![DOI](https://img.shields.io/badge/DOI-10.5281%2Fzenodo.17756074-blue)](https://doi.org/10.5281/zenodo.17756074)

Formula parsing, species and reaction handling, stoichiometric matrix
construction, thermodynamic equilibrium via Gibbs free energy
minimisation, dilute-solution / Debye-Hückel / Davies activity models,
ideal and Redlich-Kister solid solutions, kinetics (Parrot–Killoh and
transition-state theory), and interoperability with **ThermoFun JSON**
and **PHREEQC** databases. Initially focused on cement chemistry but
applicable more broadly.

| Feature | Details |
|---|---|
| **Equilibrium** | Gibbs minimisation under mass-balance constraints |
| **Activity models** | Dilute solution; HKF aqueous solutes |
| **Solid solutions** | Ideal mix, Redlich-Kister (cement-data-18 calibrated) |
| **Kinetics** | TST, Parrot–Killoh for cement clinkers; coupled to OrdinaryDiffEq |
| **Calorimetry** | Isothermal and semi-adiabatic models with variable Cp |
| **AD** | ForwardDiff-compatible across the full pipeline |

---

### [TensND.jl](https://github.com/MicroPoroChemoMechanics/TensND.jl) — Structured tensor types

[![Docs stable](https://img.shields.io/badge/docs-stable-blue.svg)](https://MicroPoroChemoMechanics.github.io/TensND.jl/stable/)
[![Docs dev](https://img.shields.io/badge/docs-dev-blue.svg)](https://MicroPoroChemoMechanics.github.io/TensND.jl/dev/)
[![DOI](https://img.shields.io/badge/DOI-10.5281%2Fzenodo.17985768-blue)](https://doi.org/10.5281/zenodo.17985768)

Structured tensor types (`TensISO`, `TensWalpole`, `TensOrtho`, `TensTI`,
…) with base-1 indexing and symmetry-aware storage. Tensor calculations
of any order and dimension in arbitrary coordinate systems, symbolic
(`SymPy`, `Symbolics`) and numerical. Shared tensor-algebra backbone
across the MicroPoroChemoMechanics stack.

| Feature | Details |
|---|---|
| **Tensors** | `TensISO`, `TensWalpole`, `TensTI`, `TensOrtho`, generic `Tens` — symmetry-aware storage with closed-form products and inverses |
| **Bases** | Canonical, rotated, orthogonal, general (non-orthogonal, symbolic) |
| **Coord. systems** | Cartesian, polar, cylindrical, spherical, spheroidal, user-defined |
| **Differential ops** | `GRAD`, `SYMGRAD`, `DIV`, `LAPLACE`, `HESS` via Christoffel symbols, symbolic or by AD |
| **Symmetry projection** | Closest ISO / TI / ORTHO tensor, orientation given or optimized |
| **Submanifolds** | Embedded hypersurfaces with fundamental forms, connection and curvatures |
| **AD** | ForwardDiff-compatible end-to-end |

---

### [MeanFieldHomogenization.jl](https://github.com/MicroPoroChemoMechanics/MeanFieldHomogenization.jl) — Mean-field homogenization

[![Docs stable](https://img.shields.io/badge/docs-stable-blue.svg)](https://MicroPoroChemoMechanics.github.io/MeanFieldHomogenization.jl/stable/)
[![Docs dev](https://img.shields.io/badge/docs-dev-blue.svg)](https://MicroPoroChemoMechanics.github.io/MeanFieldHomogenization.jl/dev/)
[![DOI](https://img.shields.io/badge/DOI-10.5281%2Fzenodo.21884243-blue)](https://doi.org/10.5281/zenodo.21884243)

Effective properties of heterogeneous materials by mean-field homogenization.
Hill polarization tensors for ellipsoidal inclusions and infinite cylinders
(2-D and 3-D, isotropic to fully anisotropic matrices), crack-opening
displacement and compliance tensors with stress/displacement intensity factors
for flat cracks, second-order Hill tensors for transport, composite `n`-layer
spheres and confocal spheroids with imperfect interfaces, periodic laminates,
and ageing linear viscoelasticity — all behind a common abstraction hierarchy
and a single dispatch mechanism. Beyond the one-site picture: **N-body schemes**
on assemblies that carry positions, inclusions solved by **finite elements** or
by a trained **neural surrogate**, and homogenization exposed as a
**constitutive law** to a structural FE code. Generic over the scalar type:
`Float64`, `BigFloat`, `ForwardDiff.Dual` and symbolic (`SymPy`, `Symbolics`)
throughout.

| Feature | Details |
|---|---|
| **Hill / Eshelby** | Ellipsoids, spheroids, spheres, infinite cylinders, 2-D plane strain; closed forms for isotropic and coaxial transversely isotropic matrices |
| **Anisotropy** | Masson residue reduction and DECUHR adaptive cubature for arbitrary anisotropy; **closed form for any anisotropy** in transport (order-2) |
| **Cracks** | COD tensor, compliance contribution, dilute correction via Budiansky density, SIF/DIF and mode decomposition; spring-like interfaces |
| **Composite inclusions** | `n`-layer spheres (Hervé–Zaoui) and confocal spheroids; Kapitza and surface-conductive imperfect interfaces; equivalent-particle conductivity |
| **Schemes** | Voigt/Reuss and Hashin–Shtrikman bounds, dilute, Mori–Tanaka, self-consistent, Ponte Castañeda–Willis, Maxwell, differential with loading paths; exact laminates |
| **N-body** | Two-inclusion interaction tensor; cluster model (Molinari & El Mouden) and equivalent inclusion method (Brisard, Dormieux & Sab) on particle assemblies, with rigorous bounds |
| **Open morphologies** | User-defined inclusion contract; Eshelby problem solved by Ferrite / Gridap finite elements, or by a differentiable trained surrogate |
| **Poromechanics & FE coupling** | Biot tensor and skeleton modulus; a microstructure as a Gauss-point material law returning stress, consistent tangent and an aperture-driven permeability |
| **Viscoelasticity** | Ageing linear viscoelasticity via Volterra operators, with structured iso/TI/ortho kernel storage |
| **AD & symbolics** | ForwardDiff-compatible end-to-end; sensitivities through self-consistent fixed points by implicit differentiation |
| **Tooling** | MFH Studio, a local browser interface that writes and runs the model script for you |

---

### [PoroMechanics.jl](https://github.com/MicroPoroChemoMechanics/PoroMechanics.jl) — Reactive transport and poromechanics

[![Docs dev](https://img.shields.io/badge/docs-dev-blue.svg)](https://MicroPoroChemoMechanics.github.io/PoroMechanics.jl/dev/)

Simulation of coupled phenomena in porous media at the macroscopic scale —
unsaturated flow, solute and multi-ionic reactive transport, cement chemistry
and poromechanics — on two numerical backends: **finite volumes**
([VoronoiFVM.jl](https://github.com/j-fu/VoronoiFVM.jl)) for transport,
**finite elements** ([Ferrite.jl](https://github.com/Ferrite-FEM/Ferrite.jl))
for coupled mechanics. A physics model is a plain Julia struct holding its
material parameters; multiple dispatch on that struct selects the constitutive
behaviour, so a model file stays a description of its own equations and knows
nothing about time stepping or assembly. Jacobians are never written by hand:
the finite-volume callbacks are differentiated with `ForwardDiff`.

This is the package announced earlier as the reactive-transport/poromechanics
layer of the stack: thermodynamic equilibrium is delegated to
`ChemistryLab.jl` (and through it `OptimaSolver.jl`). The chemistry still
hosted in `PoroMechanics.jl` — surface complexation on C-S-H, dissolution and
precipitation kinetics — is being migrated upstream to `ChemistryLab.jl`,
leaving this package to describe transport and mechanics.

| Feature | Details |
|---|---|
| **Unsaturated flow** | Richards' equation with Van Genuchten retention and Mualem relative permeability; transient Darcy flow |
| **Solute transport** | Fick diffusion; Nernst–Planck multi-ionic transport closed by an electroneutrality constraint; Oh–Jang tortuosity for effective diffusivity |
| **Non-isothermal drying** | Liquid water, dry air and heat coupled through a modified Kelvin equation and an entropy balance, with latent-heat transport by vapour |
| **Poromechanics** | Biot poroelasticity on unstructured meshes, assembled once and reused across time steps |
| **Reactive transport** | Operator splitting (SNIA) with cemdata18 equilibrium via `ChemistryLab.jl`; Friedel's salt binding; surface complexation on C-S-H |
| **Model interface** | `storage!` / `flux!` / `bcondition!` / `reaction!` for finite volumes, `element_matrices!` / `facet_load!` for finite elements |
| **AD** | ForwardDiff-differentiated callbacks; no hand-written Jacobians, Newton loop and adaptive time stepping owned by the solver |
| **Examples** | One worked problem per physics, each with its equations, material data and reference solution |

---

## Backend dependencies

Lower-level libraries used internally by the main packages above. They
are designed to be reusable in their own right and can be installed and
cited standalone from the General registry.

### [OptimaSolver.jl](https://github.com/MicroPoroChemoMechanics/OptimaSolver.jl) — Primal-dual interior-point solver

[![Docs stable](https://img.shields.io/badge/docs-stable-blue.svg)](https://MicroPoroChemoMechanics.github.io/OptimaSolver.jl/stable/)
[![Docs dev](https://img.shields.io/badge/docs-dev-blue.svg)](https://MicroPoroChemoMechanics.github.io/OptimaSolver.jl/dev/)

Julia-native primal-dual interior-point solver for Gibbs-energy
minimisation under linear equality and bound constraints. Used by
`ChemistryLab.jl` as the default equilibrium solver. Schur-complement
Newton steps exploit the diagonal Hessian structure; filter-based line
search (Wächter & Biegler 2006); implicit differentiation provides
post-solve sensitivities (`∂n*/∂b`, `∂n*/∂(μ⁰/RT)`); warm-start support.
Julia port of the Optima C++ library by Allan Leal (ETH Zürich).

| Feature | Details |
|---|---|
| **Method** | Primal-dual interior-point with filter line search |
| **Newton step** | Schur-complement reduction (`m×m` instead of `(ns+m)×(ns+m)`) |
| **Sensitivities** | Implicit differentiation, ForwardDiff-compatible |
| **Warm start** | Persistent cache between solves |
| **SciML** | `OptimaOptimizer <: AbstractOptimizer` |

---

### [DECUHR.jl](https://github.com/MicroPoroChemoMechanics/DECUHR.jl) — Adaptive cubature for vertex singularities

[![Docs stable](https://img.shields.io/badge/docs-stable-blue.svg)](https://MicroPoroChemoMechanics.github.io/DECUHR.jl/stable/)
[![Docs dev](https://img.shields.io/badge/docs-dev-blue.svg)](https://MicroPoroChemoMechanics.github.io/DECUHR.jl/dev/)

Pure-Julia port of the DECUHR algorithm (Espelid & Genz, 1994) for
automatic adaptive integration of functions with **vertex
singularities** over hyper-rectangular regions. Used by
`MeanFieldHomogenization.jl` as the adaptive-cubature backend for the anisotropic
Hill and crack kernels. Exposed as a pluggable algorithm for the SciML
[Integrals.jl](https://docs.sciml.ai/Integrals/stable/) solver stack.

| Feature | Details |
|---|---|
| **Dimensions** | 2-D and 3-D integration on hyper-rectangles |
| **Singularities** | Vertex singularities with user or auto-estimated `α`; logarithmic weights |
| **Integrands** | Vector-valued; retcode compatible with Integrals.jl |
| **Extrapolation** | Richardson extrapolation on sub-region averages |

---

## Dependency graph

```
ChemistryLab.jl
  └── OptimaSolver.jl       (weakdep — equilibrium solver backend)

MeanFieldHomogenization.jl
  ├── DECUHR.jl             (adaptive cubature backend)
  └── TensND.jl             (structured tensors)

PoroMechanics.jl
  ├── ChemistryLab.jl       (equilibrium + kinetics)
  │     └── OptimaSolver.jl
  ├── VoronoiFVM.jl         (finite volumes — transport)
  └── Ferrite.jl            (finite elements — coupled mechanics)
```

Coupling `PoroMechanics.jl` to the effective properties predicted by
`MeanFieldHomogenization.jl` is the next step of the roadmap.

`TensND.jl`, `DECUHR.jl` and `OptimaSolver.jl` are standalone and can be
used outside the MPCM context.

---

## Status

| Package           | Role     | Visibility | Registered (General) | Documentation |
|-------------------|----------|------------|----------------------|---------------|
| `ChemistryLab.jl` | main     | Public     | Yes                  | [docs](https://MicroPoroChemoMechanics.github.io/ChemistryLab.jl) |
| `TensND.jl`       | main     | Public     | Yes                  | [docs](https://MicroPoroChemoMechanics.github.io/TensND.jl) |
| `MeanFieldHomogenization.jl` | main | Public | Yes | [docs](https://MicroPoroChemoMechanics.github.io/MeanFieldHomogenization.jl) |
| `PoroMechanics.jl`| main     | Public     | Not yet              | [docs](https://MicroPoroChemoMechanics.github.io/PoroMechanics.jl/dev/) |
| `OptimaSolver.jl` | backend  | Public     | Yes                  | [docs](https://MicroPoroChemoMechanics.github.io/OptimaSolver.jl) |
| `DECUHR.jl`       | backend  | Public     | Yes                  | [docs](https://MicroPoroChemoMechanics.github.io/DECUHR.jl) |

---

## Quick start

```julia
using Pkg
Pkg.add(["ChemistryLab", "OptimaSolver", "DECUHR", "TensND",
         "MeanFieldHomogenization"])

# PoroMechanics.jl is not registered yet
Pkg.add(url = "https://github.com/MicroPoroChemoMechanics/PoroMechanics.jl")

# Compute a thermodynamic equilibrium (Portlandite dissolution)
using ChemistryLab, OptimaSolver
# … see ChemistryLab.jl documentation for full examples

# Compute a Hill polarisation tensor for a sphere in an isotropic matrix
using MeanFieldHomogenization, TensND
C₀ = iso_stiffness_E_nu(210e3, 0.3)
P  = hill_tensor(Ellipsoid(1.0), C₀)

# Solve a transport or poromechanics problem on a mesh
using PoroMechanics
# … see PoroMechanics.jl documentation and its `examples/` directory
```

The organisation also hosts
[**MPCM-Registry**](https://github.com/MicroPoroChemoMechanics/MPCM-Registry),
a Julia registry used to distribute development versions of the packages ahead
of their General-registry releases:

```julia
Pkg.Registry.add(RegistrySpec(url = "https://github.com/MicroPoroChemoMechanics/MPCM-Registry"))
```

---

## Authors & Institution

Developed by [**Jean-François Barthélémy**](https://github.com/jfbarthelemy)
and [**Anthony Soive**](https://github.com/anthonysoive), both researchers at
[Cerema](https://www.cerema.fr/en) in the research unit
[UMR MCD](https://mcd.univ-gustave-eiffel.fr/). See each package's
`CITATION.cff` for per-package authorship and contributors.

## Credits and acknowledgements

Parts of this codebase were developed with the assistance of
Anthropic's *Claude Code*, under the authors' review and validation.

## License

See the `LICENSE` file of each repository.

**Main packages:**

- [ChemistryLab.jl](https://github.com/MicroPoroChemoMechanics/ChemistryLab.jl/blob/main/LICENSE) — LGPL-2.1-or-later
- [TensND.jl](https://github.com/MicroPoroChemoMechanics/TensND.jl/blob/main/LICENSE) — MIT
- [MeanFieldHomogenization.jl](https://github.com/MicroPoroChemoMechanics/MeanFieldHomogenization.jl/blob/main/LICENSE) — MIT
- [PoroMechanics.jl](https://github.com/MicroPoroChemoMechanics/PoroMechanics.jl/blob/main/LICENSE) — MIT

**Backend dependencies:**

- [OptimaSolver.jl](https://github.com/MicroPoroChemoMechanics/OptimaSolver.jl/blob/main/LICENSE) — LGPL-2.1-or-later
- [DECUHR.jl](https://github.com/MicroPoroChemoMechanics/DECUHR.jl/blob/main/LICENSE) — MIT (Julia port; the upstream Fortran routines of Espelid & Genz carry their own copyright — see `NOTICE`)
