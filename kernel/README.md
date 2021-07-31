# Kernel

Defines and provides services for:
* paper (structure + term)
* proof nodes 
* theory
* proof actions (apply, deduce, rewrite, ...)
  

## API

| Entry point | Sig | Desc |
| -- | -- | -- |
| from_string | string -> paper | deserialize paper (compiler) |
| to_string | paper -> string | serialize paper (pretty print) |
| to_json | paper -> json | converts paper AST to json structure |
| from_json | json -> paper | builds |
| paper_to_nodes | paper -> node list | builds list of proofs nodes |
| apply | json_paper -> id -> theorem_id -> paper -> paper |
| add_theory | string -> theory | ... | 

## Type `term`

The type [term](https://github.com/edukera/formalpaper/blob/master/core/term.ml) defines a paper as a term. The following is a paper term:

```
Solution (fun (A : Set) =>
  let s1 := (fun x (s1_1:elof x (diff A A)) =>
    let s1_2 := definition diff s1_1 : elof x A in
    let s1_3 := definition diff s1_1 : not (elof x A) in
    let s1_4 := non_contradiction s1_2 s1_3: elof x void in s1_4
  ) : subset (diff A A) void in
  let s2 := (fun x (s2_1:elof x void) =>
    let s2_2 := tobejustified : elof x (diff A A) in s2_2
  ) : subest void (diff A A) in
  let s3 := definition eqset s1 s2 : (diff A A) = void in s3
) : ex_2.
```

This term, in Fitch form:
```
 ┌──                                │ 
 │ Let x be an element              │  Declaration                  
 │ s1_1  elof x (diff A A)          │  Assumption
 │ s1_2  elof x A                   │  by s1_1 by definition of diff
 │ s1_3  not (elof x A)             │  by s1_1 by definition of diff
 │ s1_4  elof x void                │  by s1_2 s1_3 by non contradiction
 └──                                │
s1  subset (diff A A) void          │  by scope s1_1 to s1_4
 ┌──                                │ 
 │ Let x be an element              │  Declaration                 
 │ s2_1  elof x void                │  Assumption
 │ s2_2 elof x (diff A A)           │  To be justified
 └──                                │  
s2  subset void (diff A A)          │  by scope s1_2 to s2_2
s3  (diff A A) = void               │  by s1 s2 by definition of set equality
```

## Implementation

### Plugins
Instrument code with plugins:
* [ppx_deriving](https://github.com/ocaml-ppx/ppx_deriving)
* [pp](https://github.com/ocaml-dune/pp)
  
