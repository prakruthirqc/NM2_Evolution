# NM2 Evolution Analysis Pipeline

---

## 1. Sequence Retrieval

Protein sequences of non-muscle myosin II homologs were retrieved manually from the UniProt database in FASTA format.

### Species and Accession Numbers

- Homo sapiens
  - MYH9 — P35579
  - MYH10 — P35580
  - MYH14 — Q7Z406

- Mus musculus
  - MYH9 — Q8VDD5
  - MYH10 — Q61879
  - MYH14 — Q6URW6

- Danio rerio
  - myh9a — A0A8M1NEM1
  - myh10 — I3ISA3

- Gallus gallus
  - MYH9 — P14105
  - MYH10 — Q789A4

- Drosophila melanogaster
  - zip — Q99323

- Caenorhabditis elegans
  - nmy-2 — Q22869

- Dictyostelium discoideum
  - mhcA — P08799

### Notes

- Only conserved motor/head domains were retained
- Variable tail regions were excluded
- Human MYO6 was tested initially as an outgroup but removed from final analysis due to excessive divergence

---

## 2. Multiple Sequence Alignment

### Tool Used

**MAFFT v7.505**

### Command

```bash
mafft --auto all_nmii_motor.fasta > aligned_nmii.fasta
```

### Default/Internal Parameters

- Sequence type automatically detected as protein
- Substitution matrix: BLOSUM62
- Progressive alignment enabled
- Iterative refinement enabled
- UPGMA guide tree generated internally
- Gap opening penalty automatically optimized
- Local pairwise alignment information used
- Final strategy selected automatically: L-INS-i
- Iterative refinement cycles: <16
- Single-thread execution

### Results

- Total sequences aligned: 13
- Alignment converged successfully

### Output

```bash
aligned_nmii.fasta
```

---

## 3. Alignment Trimming

### Tool Used

**ClipKIT**

### Command

```bash
clipkit aligned_nmii.fasta -m smart-gap -o trimmed_nmii.fasta
```

### Parameters

- Trimming mode: smart-gap
- Sequence type: Protein
- Gap threshold: 0.9231
- Codon processing: Disabled
- Terminal-only trimming: Disabled
- Complementary output: Disabled
- Log generation: Disabled

### Results

- Original length: 772
- Sites retained: 717
- Sites removed: 55
- Alignment trimmed: 7.124%

### Output

```bash
trimmed_nmii.fasta
```

---

## 4. Phylogenetic Tree Construction

### Tool Used

**IQ-TREE2 v2.3.6**

### Command

```bash
iqtree2 -s trimmed_nmii.fasta -m MFP -bb 1000 -alrt 1000
```

### Parameters

- `-m MFP`
  - Automatic model selection using ModelFinder Plus

- `-bb 1000`
  - Ultrafast bootstrap with 1000 replicates

- `-alrt 1000`
  - SH-aLRT branch support with 1000 replicates

### Default/Internal Parameters

- Protein sequence detection automatic
- Maximum likelihood tree search enabled
- NNI optimization enabled
- Branch length optimization enabled
- Automatic seed generation enabled

### Alignment Statistics

- Number of sequences: 13
- Alignment length: 717 amino acids
- Distinct patterns: 438
- Parsimony informative sites: 211
- Singleton sites: 238
- Constant sites: 268

### Tree Search Results

- Total iterations: 102
- Initial log-likelihood: -6498.237
- Optimized log-likelihood: -6497.906
- Gamma shape alpha: 1.030
- Proportion of invariant sites: 0.161

### Notes

- Mouse MYH10 and human MYH10 motor domains were nearly identical after trimming due to highly conserved nature of motor domain
- No sequences failed the composition chi-square test

### Output Files

```bash
trimmed_nmii.fasta.treefile
trimmed_nmii.fasta.contree
trimmed_nmii.fasta.iqtree
trimmed_nmii.fasta.log
trimmed_nmii.fasta.splits.nex
trimmed_nmii.fasta.mldist
```

---

## 5. Tree Visualization

### Tool Used

**iTOL (Interactive Tree Of Life)**

### Visualization Settings

- Rectangular layout
- Bootstrap values displayed
- SH-aLRT values displayed separately
- Minimal black-and-white formatting

### Exported Files

```bash
Bootstrap.svg
SH-aLRT.png
```

---

## 6. Biological Interpretation

- Vertebrate MYH9 orthologs clustered together, indicating strong evolutionary conservation across species.

- MYH10 orthologs formed a distinct conserved clade separate from MYH9 proteins.

- MYH14 proteins grouped independently, supporting functional divergence within the NM2 family.

- Zebrafish and chicken homologs clustered close to mammalian homologs, consistent with vertebrate evolutionary relationships.

- Drosophila ZIP and C. elegans NMY-2 branched outside vertebrate NM2 clades, reflecting greater evolutionary divergence in invertebrates.

- Dictyostelium discoideum mhcA formed the most basal branch and served as an effective outgroup for rooting the tree.

- High bootstrap and SH-aLRT support values were observed for major vertebrate clades, indicating strong statistical confidence in the inferred phylogenetic relationships.

- Mouse MYH10 and human MYH10 motor domains showed extremely high sequence conservation after trimming, resulting in very short branch distances between them.

---

 All commands, parameters, intermediate files, and output trees were documented in `workflow_commands.md` to ensure reproducibility of the complete analysis pipeline.
