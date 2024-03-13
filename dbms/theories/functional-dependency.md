[Home](../../README.md)

# Functional Dependency

Functional dependency is a relationship between two attributes `x` and `y` where for every instance of `x`, the value of `x` can uniquely identify the value of `y`.

It can be denoted as

```
x → y
```

Where the left hand side is called the **determinant** and the right hand side is called the **dependant**.

## Rules of Functional Dependency:

### Armstrong's Axioms:

- **Axiom of Reflexivity**: If A is a set of attributes and B is a subset of A, then B is functionally dependent on A.

  `If B ⊆ A then A → B`

- **Axiom of Augmentation**: If A → B is true and Y is the attribute set, then AY → BY is also true.

  `If A → B then AY → BY`

- **Axiom of Transitivity**: If A → B and B → C, then A → C.

  `If A → B and B → C then A → C`

### Some other rules:

- **Union rule**: If A → B and A → C, then A → BC.
- **Composition rule**: If A → B and X → Y, then AX → BY.
- **Decomposition rule**: If A → BC, then A → B and A → C.
- **Pseudo Transitivity rule**: If A → BC and BC → D, then AC → D.
