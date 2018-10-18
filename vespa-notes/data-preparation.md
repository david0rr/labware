# Data preparation for VESPA


## Required input for VESPA 'end stages'

1. **Aligned orthologous gene families** in fasta format (one aligned fast per gene family)
2. **Species tree** with names corresponding to sequences present in each gene family (*see below*)
3. **Branch file** specifying taxa or groups thereof for detecting lineage-specific +ve selection (optional)


## File specifications

- Filenames should end in `.fa` or `.fasta`
- Filenames should not contain spaces
- Safe special characters include `_`, `.`



## Sequence specifications

- > 7 taxa per gene family. This is an absolute minimum (see https://academic.oup.com/mbe/article/19/6/950/1094968)
- Minimum of 20-50 codons in length according to https://www.ncbi.nlm.nih.gov/pubmed/21087944
- Fasta sequence headers should contain a human readable **taxonomic identifier** followed by an accession number or other distinct alphanumeric identifer, separated by a`|` character
  - e.g. `>human|ENSG00000012048`
- Need to create distinct identifier after pipe in absence of accession
- Taxonomic identifiers in sequence headers must ALL be present in the species tree  (else 💩☔️)
- *Maximum header length? (limit increased in recent Codeml versions?)*


## Species tree specifications 

- Newick format
- Names must match taxonomic identifiers (before `|` character) in fasta headers
- *Bifurcating only?*


## Branch file specifications

- Text file
- One line per lineage
- Name of leaf node if labelling a leaf node
  - e.g. `human`
- If labelling ancestral branch, define an arbitrary name, and reference child leaves
  - e.g. `mammals: human, mouse, whale`