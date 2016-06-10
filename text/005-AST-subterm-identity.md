- Title: Give an identity to every subterm and propagate it down to pretty-printing

- Driver: Valentin Robert

- Status: (Early) Draft

----

# Summary

If the `constr` type had a way of uniquely identifying its subterms, and if
this information was propagated down to `glob_constr`, `constr_expr`,
`notation_constr` and the `std_ppcmds`, it would allow for user interfaces to
quickly, unambiguously, refer to any part of a kernel term.

## Problems

* This will require changing many datatypes. `constr` itself could stay
unchanged, as the identifier could be the index of the subterm in a tree
traversal.

## Benefits

* IDEs could easily understand the mapping between `constr`, `notation_constr`,
and the final pretty-printed strings (coqtop could expose the subterms as
string ranges).

## Caveat

* This would require some changes in a lot of datatypes downstream from
`constr`.

* Some indices in `constr` won't have a corresponding index in the other types,
either because they will be elided or merged with other. I'm not sure whether
this is an issue.

## Ideas

## Further features

* Once subterms have an identity, one could consider displaying those to the
user, and adding those identities as first-class values in Ltac, as a way to
refer to a subterm without having to type it out.

This would resolve issues where notations make the numbering of expressions
awkward when using `rewrite ... at <n>.` and such.

However, this would make proofs more brittle to changes in `constr`. A more
robust solution would be to let the user specify which index they care for in
the IDE, and have it perform a query to coqtop that would return the expression
they should place in the tactic.

