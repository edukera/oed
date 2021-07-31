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

## Implementation

### Plugins
Instrument code with plugins:
* [ppx_deriving](https://github.com/ocaml-ppx/ppx_deriving)
* [pp](https://github.com/ocaml-dune/pp)
  
