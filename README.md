# Dependent Types in Arend

[![Language: Arend](https://img.shields.io/badge/language-Arend-6A5ACD)](https://arend-lang.github.io/)
[![Topic: Formal proofs](https://img.shields.io/badge/topic-formal_proofs-2E8B57)](#selected-solutions)
[![Project: Coursework](https://img.shields.io/badge/project-coursework-64748B)](#about)

Coursework on dependent types, functional programming, and formal proofs in **Arend**. This repository combines lecture examples with my homework solutions: from recursive functions and length-indexed vectors to monad laws, algorithm correctness, and properties of types.

## About

Arend is a theorem prover based on homotopy type theory. In this project, specifications are expressed as types and proofs are written as terms that the typechecker can check.

This is a fork of [ProgMiner/deptypes](https://github.com/ProgMiner/deptypes). The lecture material and exercise statements come from the upstream course; my contributions are the homework implementations and proof terms in `src/hw*.ard`.

## Selected solutions

| Area | Examples | Source |
| --- | --- | --- |
| Recursive functions | Factorial, remainder, GCD, and equality checks for concrete inputs | [hw01.ard](src/hw01.ard) |
| Equational reasoning | List concatenation associativity, reversal of concatenation, and reversal as an involution | [hw03.ard](src/hw03.ard) |
| Data structures with type-level constraints | List lookup requiring an index-bounds proof; length-indexed vectors; height-indexed binary trees | [hw04.ard](src/hw04.ard) |
| Functional abstractions | A monad class with laws, plus `Maybe` and state monad instances | [hw06.ard](src/hw06.ard) |
| Algorithm correctness | Filtering properties, insertion-sort specification, tail-recursive factorial equivalence, and balanced-parentheses recognition | [hw08.ard](src/hw08.ard) |
| Properties of types | Injectivity, propositions, sets, and decidable equality | [hw10.ard](src/hw10.ard) |

### Example: bounds as a proof obligation

The lookup function in [hw04.ard](src/hw04.ard) requires evidence that the index is within the list's bounds. Its signature is:

```arend
\func lookup {A : \Type} (xs : List A) (n : Nat)
  (proof : T (n < length xs)) : A
```

The extra argument makes the precondition explicit in the type. The implementation handles the empty-list case through the impossibility of constructing the required proof.

### Example: concrete equality checks

[hw01.ard](src/hw01.ard) includes declarations such as:

```arend
\func gcdTest4 : gcd 4 6 = 2 => idp
\func gcdTest2 : gcd 0 3 = 3 => idp
```

These declarations illustrate the approach used throughout the exercises: an expected result is an equality type, and `idp` establishes it when both sides reduce to the same value.

## Getting started

### Requirements

- Git.
- Arend and its standard library, **`arend-lib`**.
- A JDK compatible with your Arend release. The current [installation guide](https://arend-lang.github.io/documentation/getting-started/download) requires JDK 17 or newer.

The repository does not pin an Arend or `arend-lib` version. Older course examples may need adjustments when used with a newer release.

### Clone the repository

```bash
git clone https://github.com/bozhnyukAlex/deptypes.git
cd deptypes
```

### IntelliJ IDEA

1. Install the **Arend** plugin using the [official instructions](https://arend-lang.github.io/documentation/getting-started/download).
2. Open the cloned project in IntelliJ IDEA.
3. Check that the Arend module uses `src` as its source directory and includes `arend-lib` as a dependency. These settings are declared in [arend.yaml](arend.yaml).
4. Open an `.ard` file to inspect definitions, typechecking messages, and remaining proof goals. Start with `hw01.ard`, `hw03.ard`, or the examples listed above.

### Command line

Download the Arend JAR and a compatible `arend-lib` archive using the [installation guide](https://arend-lang.github.io/documentation/getting-started/download). Put the library archive in your Arend libraries directory.

From the repository root, replace the paths below with your actual locations:

```bash
java -jar /path/to/Arend.jar . -L/path/to/arend-libraries
```

This loads the project described by `arend.yaml` and invokes typechecking. See the official [project setup guide](https://arend-lang.github.io/documentation/getting-started/started) for details.

## Repository layout

| Path | Contents |
| --- | --- |
| [src/hw01.ard](src/hw01.ard)–[src/hw13.ard](src/hw13.ard) | Homework statements, implementations, and proofs |
| [src/lect01.ard](src/lect01.ard)–[src/lect13.ard](src/lect13.ard) | Lecture examples and supporting definitions |
| [lect01.pdf](lect01.pdf) | Introductory lecture slides |
| [src/Test.ard](src/Test.ard), [src/TestDir](src/TestDir) | Small examples of modules and imports |
| [arend.yaml](arend.yaml) | Source directory, binary output directory, and library dependency |

## Completion and verification

The repository contains substantial homework solutions alongside unfinished exercises. Some homework and lecture files still contain **`{?}` proof holes**, including optional tasks in `hw04.ard` and parts of `hw13.ard`.

Use the Arend typechecker to inspect each definition and its dependencies. A definition with an unresolved goal is not a completed proof. Whole-project checking may report remaining goals and compatibility issues; this repository does not provide a CI typechecking workflow or a separate automated test suite.

## Credits

- **Course material and exercise templates:** [ProgMiner/deptypes](https://github.com/ProgMiner/deptypes), maintained by Eridan Domoratskiy.
- **Homework solutions in this fork:** [Alexander Bozhnyuk](https://github.com/bozhnyukAlex).
- **Language and tooling:** [Arend](https://arend-lang.github.io/) and [arend-lib](https://github.com/JetBrains/arend-lib).
