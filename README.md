# NM2 Evolution

Phylogenetic analysis of non-muscle myosin II evolution and duplication events across diverse eukaryotic organisms.

---

# Objective

The aim of this project was to study the evolutionary relationships of non-muscle myosin II (NMII) proteins across different eukaryotic species using phylogenetic analysis. The workflow included sequence retrieval, dataset curation, multiple sequence alignment, alignment trimming, phylogenetic tree construction, and biological interpretation of the resulting evolutionary patterns.

---

# Why Non-Muscle Myosin II?

Non-muscle myosin II (NMII) is an actin-based motor protein involved in several essential cellular processes including:

- Cytokinesis
- Cell migration
- Cell polarity
- Adhesion
- Intracellular tension generation
- Morphogenesis

Unlike muscle myosins, NMII proteins are present in a wide range of eukaryotic organisms and are evolutionarily conserved. Studying NMII evolution helps in understanding:

- Conservation of cytoskeletal mechanisms across species
- Functional divergence after gene duplication
- Emergence of paralog-specific specialization
- Evolution of multicellularity and cellular complexity

The myosin family was selected because it represents an ideal model to study both evolutionary conservation and diversification of cytoskeletal proteins.

---

# Species Selection Rationale

Species were selected to represent a broad evolutionary distribution across eukaryotes, allowing comparison between vertebrates, invertebrates, and lower eukaryotes.

| Species | Reason for Inclusion |
|---|---|
| *Homo sapiens* | Representative mammalian vertebrate with multiple NMII paralogs |
| *Mus musculus* | Closely related mammalian model organism used for evolutionary comparison |
| *Danio rerio* | Representative vertebrate fish lineage |
| *Gallus gallus* | Representative avian lineage |
| *Drosophila melanogaster* | Well-studied invertebrate model organism |
| *Caenorhabditis elegans* | Evolutionarily distant nematode model |
| *Dictyostelium discoideum* | Social amoeba representing early-diverging eukaryotes |

This species selection enabled analysis of:
- Conservation of NMII proteins across vertebrates
- Divergence between vertebrate and invertebrate homologs
- Evolutionary distance between higher and lower eukaryotes
- Potential duplication events in vertebrate NMII genes

---

# Repository Structure

```text
NM2_Evolution/
│
├── raw_data/
│   └── all_nmii.fasta
│
├── alignment/
│   ├── aligned_nmii.fasta
│   └── trimmed_nmii.fasta
│
├── trees/
│   ├── nmii_tree.treefile
│   ├── nmii_tree.contree
│   ├── nmii_tree.iqtree
│   ├── nmii_tree.log
│   ├── nmii_tree.splits.nex
│   └── nmii_phylogenetic_tree.svg
│
├── results/
│   └── workflow screenshots
│
├── workflow_commands.md
│
└── README.md
```

---

# Dataset Curation

Protein sequences were retrieved from the UniProt database in FASTA format.

Only curated non-muscle myosin II homologs were selected. Muscle-specific myosins and incomplete sequences were excluded to maintain dataset consistency.

The dataset included:

| Species | Gene | UniProt ID |
|---|---|---|
| *Homo sapiens* | MYH9 | P35579 |
| *Homo sapiens* | MYH10 | P35580 |
| *Homo sapiens* | MYH14 | Q7Z406 |
| *Mus musculus* | MYH9 | Q8VDD5 |
| *Mus musculus* | MYH10 | Q61879 |
| *Mus musculus* | MYH14 | Q6URW6 |
| *Danio rerio* | myh9a | A0A8M2BCY6 |
| *Danio rerio* | myh10 | I3ISA3 |
| *Gallus gallus* | MYH9 | P14105 |
| *Gallus gallus* | MYH10 | Q789A4 |
| *Drosophila melanogaster* | zip | Q99323 |
| *Caenorhabditis elegans* | nmy-2 | Q22869 |
| *Dictyostelium discoideum* | mhcA | P08799 |

---

# Workflow Summary

## 1. Multiple Sequence Alignment

Tool used: MAFFT

```bash
mafft --auto raw_data/all_nmii.fasta > alignment/aligned_nmii.fasta
```

### Important Parameters

- `--auto` enabled automatic alignment strategy selection
- Amino acid mode automatically detected
- BLOSUM62 substitution matrix used
- Iterative refinement alignment performed

### Output

`aligned_nmii.fasta`

---

## 2. Alignment Trimming

Tool used: ClipKIT

```bash
~/.local/bin/clipkit alignment/aligned_nmii.fasta -o alignment/trimmed_nmii.fasta
```

### Important Parameters

- smart-gap trimming mode
- Gap threshold: 0.9231

### Results

- Original alignment length: 2321
- Sites retained: 2031
- Sites trimmed: 290
- Percentage trimmed: 12.495%

### Output

`trimmed_nmii.fasta`

---

## 3. Phylogenetic Tree Construction

Tool used: IQ-TREE2

```bash
iqtree2 -s alignment/trimmed_nmii.fasta -m MFP -B 1000 --alrt 1000 -T AUTO --prefix trees/nmii_tree --redo
```

### Important Parameters

- `-m MFP` → automatic model selection using ModelFinder Plus
- `-B 1000` → ultrafast bootstrap analysis with 1000 replicates
- `--alrt 1000` → SH-aLRT branch support with 1000 replicates
- `-T AUTO` → automatic CPU thread detection

### Best-fit Evolutionary Model

`Q.insect+F+R3`

### Output Files

- `nmii_tree.treefile`
- `nmii_tree.contree`
- `nmii_tree.iqtree`
- `nmii_tree.log`

---

# Tree Visualization

The phylogenetic tree was visualized using iTOL (Interactive Tree Of Life).

Output:
`nmii_phylogenetic_tree.svg`

---

# Biological Interpretation

The phylogenetic analysis revealed clear clustering of homologous NMII proteins according to evolutionary lineage.

## Key Observations

### 1. Vertebrate Paralogs Clustered Together

Human, mouse, chicken, and zebrafish MYH9, MYH10, and MYH14 proteins formed closely related clusters, suggesting strong evolutionary conservation among vertebrate NMII paralogs.

Non-muscle myosin II in vertebrates is mainly represented by three paralogs:

- MYH9 (NMII-A)
- MYH10 (NMII-B)
- MYH14 (NMII-C)

The clustering pattern observed in the phylogenetic tree suggests that these paralogs originated through ancestral gene duplication events.

---

### 2. Evidence for Gene Duplication Events

Invertebrates typically possess only one ancestral non-muscle myosin II gene, whereas vertebrates contain multiple specialized paralogs.

The phylogenetic tree supports the hypothesis that an ancestral NMII gene underwent duplication during vertebrate evolution, leading to the emergence of:

- MYH9
- MYH10
- MYH14

Following duplication, these paralogs diverged independently and acquired specialized cellular functions while still retaining conserved motor domains.

This evolutionary expansion likely occurred as multicellular organisms became more complex and required more specialized regulation of:

- Cell migration
- Cytokinesis
- Tissue organization
- Intracellular force generation

Thus, the observed branching pattern reflects both:
- evolutionary conservation of core cytoskeletal mechanisms
- functional diversification after duplication

---

### 3. Mammalian Sequences Showed Highest Similarity

Human and mouse homologs clustered very closely together, reflecting their recent common ancestry and high sequence conservation.

---

### 4. Invertebrate Homologs Were More Divergent

*Drosophila melanogaster* and *Caenorhabditis elegans* NMII proteins branched separately from vertebrate clusters, indicating greater evolutionary divergence.

These organisms likely retain sequences more similar to the ancestral non-muscle myosin II form before vertebrate duplication events occurred.

---

### 5. Dictyostelium Represented an Early-Diverging Lineage

The *Dictyostelium discoideum* sequence occupied a distant branch in the tree, consistent with its position as an early-diverging eukaryote.

This supports the idea that non-muscle myosin II proteins originated early during eukaryotic evolution and were later diversified through lineage-specific adaptations and duplication events.

---

# Conclusion

This analysis demonstrated that non-muscle myosin II proteins are highly conserved across eukaryotes while also showing lineage-specific diversification.

The phylogenetic relationships observed in the tree support:

- evolutionary conservation of cytoskeletal motor proteins
- duplication-driven expansion of vertebrate NMII paralogs
- divergence of NMII homologs across major eukaryotic lineages
- increasing specialization of NMII proteins during evolution of complex multicellular organisms

The workflow successfully generated a reproducible phylogenetic pipeline including dataset curation, alignment, trimming, tree construction, and evolutionary interpretation.
