# Proposal for YAML list of static instances for the FontTools Instancer

This is part of a proposal for a YAML structure that could be used to specific static fonts to instantiate from a variable font. This YAML structure includes only the data relevant to this need, and so it can be much more compact than a designspace or GlyphsApp file.

This YAML list has the following general structure:

```yaml
Family:
    SubFamily:
        Weight 1:        "AXSX: X, AXSY: Y, AXSZ: Z"
        Weight 1 Italic: "AXSX: X, AXSY: Y, AXSZ: Z"
        Weight 2:        "AXSX: X, AXSY: Y, AXSZ: Z"
        Weight 2 Italic: "AXSX: X, AXSY: Y, AXSZ: Z"
```

This could be parsed and used as arguments for the FontTools Instancer in order to generate static fonts, e.g. for Google Fonts static font downloads.

## Reference projects

As a potential references, related projects are:

* [Recursive Code Config](https://github.com/arrowtype/recursive-code-config). It has user-configurable YAML files, which are used as an interface to specify custom styles for RIBBI font families.

* [gftools gen-statics](https://github.com/googlefonts/gftools/pull/264/files). This generates static font instances from the Google Fonts fallbacks cross products, and could use the YAML Instance List to improve its output.

## Example YAML Lists

- The list at `recursive-instances.yaml` is a relatively-compact but relatively-flexible way to specify the static instances expected from a variable font. 
- The list at `fraunces-instances.yaml` is compact list of instances for the Fraunces font project (caveat: because Fraunces has separate Roman & Italic VFs, it may ultimately require an extra transformation step in an instancing script).

## Filenames

Generated filenames should avoid characters that can trip up shell scripting, such as spaces, commas, square brackets, etc.

Generally, filenames should have a structure like:

```
SubFamilyName-StyleStyleStyle.ttf
```

Examples:

```
Fraunces9ptSoft-SemiBold.ttf
RecursiveMonoLinear-ExtraBoldItalic.ttf
```

## Shorthand potential

These YAML lists are very quick to write in a text editor with multi-selection editing tools.

However, these YAML lists could potentially have a shorthand syntax and a script to convert them into the full lists. E.g. instead of listing all weights, one could potentially give a weight range, and the script could expand that to 100-unit values with known weight names, as recorded in the Google Fonts Axis Registry.

This format is beyond the purview of this list proposal, however, and could be a subsequent effort.

