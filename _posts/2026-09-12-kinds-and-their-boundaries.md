---
layout: post
title: "Kinds and Their Boundaries"
date: 2026-09-12
description: "Where does a natural kind end and an arbitrary grouping begin — and what happens when a boundary is only approximately true?"
categories:
  - Metaphysics
tags:
  - Natural Kinds
  - Classification
---

Some categories seem to carve the world at its joints: gold, water, the elements of the periodic table. Others feel more like conveniences we impose on a continuous reality for our own purposes. The interesting cases sit in between, and most categories, looked at closely, turn out to sit in between.

## The problem of boundaries

A kind with a sharp boundary tells you, for any object, a definite yes or no: it is gold, or it is not. But most of the categories we actually use — species, disease, planet, even "water" once you get down to isotopes — resist that treatment. The boundary is real, but it is drawn through a region of genuine ambiguity rather than around a clean edge.

> A boundary drawn too sharply hides the fact that nature drew none at all.

## Some examples, ranked by how badly they misbehave

1. **Gold** — about as clean as kinds get; defined by atomic number, with no borderline cases in practice.
2. **Water** — clean at the level of the molecule, messier once you ask whether ice, vapor, and heavy water all count as "the same stuff."
3. **Biological species** — boundaries drift over time and space; ring species make the problem vivid.
4. **Planet** — revised by vote in 2006, which is itself a sign that the boundary was never fully in the world to begin with.

## A formal aside

One way to make the idea of a "fuzzy but real" boundary precise is to treat kind-membership as a threshold on similarity to some prototype, rather than as a strict rule:

```
function is_member(x, kind):
    d = distance(x, kind.prototype)
    return d < kind.threshold
```

In slightly more formal terms, an object $$x$$ counts as a member of kind $$k$$ just when its distance from the kind's prototype is small enough — that is, when $$d(x, k) < \epsilon$$ for some threshold $$\epsilon$$. A natural choice of distance, if the properties in question are numeric, is ordinary Euclidean distance across each property $$i$$:

$$
d(x, k) = \sqrt{\sum_i (x_i - k_i)^2}
$$

This does not resolve the philosophical question of *why* some threshold rather than another should count as the boundary of a kind. But it at least separates two claims that are easy to run together: that a kind has a real center, and that a kind has a real edge. Many disputes about natural kinds are really disputes about the second claim, dressed up as disputes about the first.

![Three overlapping, soft-edged circles labeled gold, water, and species](assets/images/kinds-and-their-boundaries/overlapping-kinds.svg)

Overlap, in this picture, is not a defect in our categories. It is what you should expect if the categories are tracking something continuous.

For a fuller treatment of the underlying debate, see the Stanford Encyclopedia of Philosophy's entry on [natural kinds](https://plato.stanford.edu/entries/natural-kinds/).
