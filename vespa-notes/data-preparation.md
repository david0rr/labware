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



### Commands

1. `vespa.py infer_genetree -input=gene_families_dir/ -species_tree=tree.nwk > infer_genetree.stdout`
2. `vespa.py codeml_setup -input=Inferred_Genetree_gene_families_dir/ -branch_file=branches.txt > codeml_setup.stdout`

3. Run commands in `codeml_taskfarm.txt`
4. 

```
vespa.py codeml_reader -input=Codeml_Setup_Inferred_Genetree_gene_families_dir/ -branch_file=branches.txt -alignment_path=gene_families_dir/ > codeml_reader.stdout
# Creates Report_Codeml_Setup_Inferred_Genetree_gene_families_dir
```



  ### Sample taskfarm runner script `codeml.sge.sh`

Where `999` is the number of lines in `codeml_taskfarm.txt`

```shell
#$ -cwd -V
#$ -P omics
#$ -l h_rt=10:00:00
#$ -t 1-999
#$ -tc 100

CMD=$(awk "NR==$SGE_TASK_ID" codeml_taskfarm.txt)
eval $CMD
```



### Sample branch file `branches.txt`

```
Dendrobatoidea: allo, amee, rani
Dendrobatidae: amee, rani
```

Avoid trailing newlines