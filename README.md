# Rake Language Support for VS Code

Syntax highlighting and language support for [Rake](https://github.com/KaiStarkk/rake-lang), a vector-first language for CPU SIMD with divergent control flow.

## Features

- Syntax highlighting for `.rk` files
- Comment toggling (`~~`)
- Bracket matching and auto-closing
- Code folding for definitions and blocks

## Rake Syntax Preview

```rake
~~ Ray-sphere intersection with divergent control flow
rake intersect ray_ox ray_oy ray_oz ray_dx ray_dy ray_dz
  <sphere_cx> <sphere_cy> <sphere_cz> <sphere_r>
  -> t_result:

  let disc = b * b - <4.0> * a * c

  ~~ Tine declarations partition the lanes
  | #miss  := (disc < <0.0>)
  | #hit   := (!#miss)

  ~~ Through blocks execute under mask
  through #hit:
    let sqrt_disc = sqrt(disc)
    (- b - sqrt_disc) / (<2.0> * a)
  -> t_value

  through #miss:
    <-1.0>
  -> miss_value

  ~~ Sweep collects results
  sweep:
    | #miss -> miss_value
    | #hit  -> t_value
  -> t_result
```

## Installation

### From VSIX (recommended)
1. Download the latest `.vsix` from releases
2. Open VS Code
3. Run `Extensions: Install from VSIX...` from command palette

### From source
```bash
cd rake-vscode
npm install -g @vscode/vsce
vsce package
code --install-extension rake-lang-0.2.0.vsix
```

## Related

- [Rake Language](https://github.com/KaiStarkk/rake-lang) - The Rake compiler
- [tree-sitter-rake](https://github.com/KaiStarkk/tree-sitter-rake) - Tree-sitter grammar
