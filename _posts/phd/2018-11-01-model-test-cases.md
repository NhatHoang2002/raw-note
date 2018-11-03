---
title: "PhD: Models & Test cases"
categories: [phd]
tags: [phd,biofilm]
toc: 1
maths: 1
---

{% assign file-src = "/files/phd" %}

<p markdown="1" class="thi-warning">
<i class="material-icons mat-icon">error</i>
Because I cannot find the place I stored the notes for the models I have beed tested, this note is for them. I rewrite this for short!
</p>

This note was created while testing with Chopp's model (_chopp06combine_). In this test, If we use Ghost Penalty method, the results become bad in some steps. I had modified some points in the code of Ghost penalty. That's why I need to check again if there is something wrong with the old models?

## NXFEM test cases

- File `main.m` with file `main_eachStep.m`.
- Models in `nxfem\func\func_model`:
    - Sinha
    - Becker
    - Barrau
- See the models [here](/files/phd/model_nxfem.pdf).

### Sinha's test case

- Article _unfitted fem ellip para sinha.pdf_
- Check more info in [this part of note](/papers#sinha).
- Semilinear + interface but use IIM method.
- Solution does NOT depend on the diffusion coefficients.
