# NM2 Evolution Analysis

## Evolutionary Conservation and Diversification of Non-Muscle Myosin II Motor Domains Across Eukaryotes

---

## Overview

Non-muscle myosin II (NM2) proteins are highly conserved actin-based molecular motors involved in essential cellular processes including cytokinesis, cell migration, adhesion, intracellular transport, tissue morphogenesis, and maintenance of cell polarity. In vertebrates, the NM2 family has diversified into multiple paralogs — primarily MYH9, MYH10, and MYH14 — each contributing specialized functional roles in different tissues and developmental contexts.

This project investigates the evolutionary relationships among NM2 homologs across diverse eukaryotic organisms through multiple sequence alignment and phylogenetic reconstruction using conserved motor domains.

The analysis particularly focuses on how increasing organismal complexity correlates with expansion of paralogous NM2 genes through gene duplication events, allowing functional specialization and fine-tuned cellular regulation.

---

# Biological Motivation

Gene duplication is one of the major driving forces of molecular evolution. As organisms become more complex, duplicated genes can diverge over evolutionary time and acquire specialized or partially redundant functions.

The non-muscle myosin II family provides an excellent model for studying this phenomenon:

- Simpler eukaryotes generally possess a single NM2-like homolog
- Invertebrates contain limited diversification
- Vertebrates possess multiple paralogs including MYH9, MYH10, and MYH14

These paralogs likely originated through ancestral gene duplication events followed by functional divergence.

The conservation of the ATPase motor domain across species reflects strong evolutionary pressure to preserve core motor activity, while diversification of paralogs supports increasingly specialized cellular functions in higher organisms.

---

# Why Non-Muscle Myosin II Was Selected Instead of Muscle Myosin

The broader myosin superfamily contains multiple classes of motor proteins with highly diverse cellular functions. Although the assigned protein family for this project was broadly “myosin,” the analysis specifically focused on non-muscle myosin II (NM2) proteins rather than conventional muscle myosins.

This choice was made because NM2 proteins provide a better model for studying evolutionary conservation, paralog diversification, and functional specialization across eukaryotes.

Unlike muscle myosins, which are highly specialized for skeletal and cardiac muscle contraction, NM2 proteins are universally involved in fundamental cellular processes including:

- Cytokinesis
- Cell migration
- Cell adhesion
- Maintenance of cell polarity
- Tissue morphogenesis
- Intracellular force generation

These functions are conserved across a broad evolutionary range from unicellular eukaryotes to vertebrates, making NM2 proteins particularly suitable for comparative phylogenetic analysis.

In addition, vertebrate NM2 proteins have diversified into multiple paralogs (MYH9, MYH10, and MYH14) through ancestral gene duplication events. This paralog expansion provides an opportunity to study how increasing organismal complexity drives functional diversification while maintaining strong conservation of essential motor domains.

Muscle myosins were not selected because they are highly tissue-specific and evolutionarily specialized for contractile systems, whereas NM2 proteins better reflect core cellular evolutionary mechanisms shared across eukaryotic life.

Therefore, non-muscle myosin II proteins were chosen as an ideal system to investigate evolutionary conservation, paralog emergence, and functional divergence within the larger myosin superfamily.

---

# Why These Organisms Were Selected

The organisms used in this analysis were intentionally chosen to represent major evolutionary transitions across eukaryotic life.

## Vertebrates

### Homo sapiens (Human)

Human MYH9, MYH10, and MYH14 proteins were included as representative vertebrate NM2 paralogs with highly specialized cellular functions.

### Mus musculus (Mouse)

Mouse homologs were selected because of their close evolutionary relationship to humans and extensive use as mammalian model organisms.

### Danio rerio (Zebrafish)

Zebrafish proteins were included to represent early vertebrate evolution and aquatic vertebrates.

### Gallus gallus (Chicken)

Chicken homologs provided an additional non-mammalian vertebrate lineage for comparison.

---

## Invertebrates

### Drosophila melanogaster

The Drosophila ZIP homolog represents a more ancestral invertebrate NM2-like protein.

### Caenorhabditis elegans

NMY-2 from *C. elegans* was included as a nematode representative with reduced paralog complexity.

---

## Basal Eukaryote / Outgroup

### Dictyostelium discoideum

The mhcA homolog from *Dictyostelium* was selected as a distant eukaryotic outgroup because it contains a primitive myosin II homolog while remaining evolutionarily distant from metazoans.

Its inclusion helps root the phylogenetic tree and provides evolutionary context for divergence among animal NM2 paralogs.

---

# Sequence Selection Strategy

Only conserved motor/head domains were retained for analysis.

Variable coiled-coil tail regions were excluded because:

- Tail regions evolve more rapidly
- Tail length varies substantially across species
- Highly divergent regions can introduce alignment artifacts
- Conserved motor domains provide stronger phylogenetic signal
- All sequences were retrieved from manually annotated UniProt entries corresponding to non-muscle myosin II homologs.

Human MYO6 was initially tested as an outgroup candidate. However, it was excluded from the final dataset because MYO6 belongs to a fundamentally different myosin class with excessive sequence divergence that distorted phylogenetic reconstruction.

---

# Species and UniProt Accessions

| Species | Gene | UniProt Accession |
|---|---|---|
| Homo sapiens | MYH9 | P35579 |
| Homo sapiens | MYH10 | P35580 |
| Homo sapiens | MYH14 | Q7Z406 |
| Mus musculus | MYH9 | Q8VDD5 |
| Mus musculus | MYH10 | Q61879 |
| Mus musculus | MYH14 | Q6URW6 |
| Danio rerio | myh9a | A0A8M1NEM1 |
| Danio rerio | myh10 | I3ISA3 |
| Gallus gallus | MYH9 | P14105 |
| Gallus gallus | MYH10 | Q789A4 |
| Drosophila melanogaster | zip | Q99323 |
| Caenorhabditis elegans | nmy-2 | Q22869 |
| Dictyostelium discoideum | mhcA | P08799 |

---

# Methodology

## 1. Multiple Sequence Alignment

Protein sequences were aligned using **MAFFT v7.505**.

### Command

```bash
mafft --auto all_nmii_motor.fasta > aligned_nmii.fasta
```

### Alignment Features

- Automatic strategy selection
- BLOSUM62 substitution matrix
- Iterative refinement
- Local pairwise alignment information
- UPGMA guide tree generation
- L-INS-i alignment strategy selected automatically

---

## 2. Alignment Trimming

Poorly aligned and gap-rich regions were removed using **ClipKIT**.

### Command

```bash
clipkit aligned_nmii.fasta -m smart-gap -o trimmed_nmii.fasta
```

### Trimming Results

- Original alignment length: 772
- Retained positions: 717
- Trimmed positions: 55
- Percentage trimmed: 7.124%

---

## 3. Phylogenetic Reconstruction

Maximum-likelihood phylogenetic analysis was performed using **IQ-TREE2**.

### Command

```bash
iqtree2 -s trimmed_nmii.fasta -m MFP -bb 1000 -alrt 1000
```

### Analysis Features

- Automatic model selection using ModelFinder Plus
- Ultrafast bootstrap analysis (1000 replicates)
- SH-aLRT branch support analysis (1000 replicates)
- Maximum-likelihood optimization
- Branch length optimization
- Nearest-neighbor interchange optimization

---

# Major Findings

- MYH9, MYH10, and MYH14 formed distinct vertebrate paralog clades
- Vertebrate NM2 proteins clustered separately from invertebrate homologs
- Zebrafish and chicken homologs grouped closely with mammalian orthologs
- *Dictyostelium* mhcA formed the basal outgroup branch
- Major vertebrate branches showed strong bootstrap and SH-aLRT support

One particularly interesting observation was that mouse MYH10 and human MYH10 motor domains were nearly identical after trimming, reflecting extremely strong evolutionary conservation of the catalytic motor domain.

---

# Evolutionary Interpretation

The phylogenetic structure strongly supports the hypothesis that vertebrate NM2 paralogs originated through ancestral gene duplication events followed by evolutionary divergence.

As multicellular organisms evolved increasing developmental and cellular complexity, expansion of NM2 paralogs likely enabled:

- Tissue-specific specialization
- Functional redundancy
- Distinct regulatory mechanisms
- More precise cytoskeletal control
- Increased adaptability of cellular mechanics

Despite diversification, the remarkable conservation of the ATPase motor domain across distant taxa demonstrates strong purifying selection acting on core motor function throughout eukaryotic evolution.

---

# Tree Visualization

Phylogenetic trees were visualized using **iTOL (Interactive Tree Of Life)**.

Two separate visualizations were generated:

- Bootstrap support tree
- SH-aLRT support tree

Minimal black-and-white formatting was intentionally used to maintain clarity and emphasize evolutionary topology rather than graphical styling.

---

# Repository Structure

```text
alignment/
├── aligned_nmii.fasta
├── trimmed_nmii.fasta

raw_data/
├── all_nmii_motor.fasta

trees/
├── Bootstrap.svg
├── SH-aLRT.svg
├── trimmed_nmii.fasta.treefile
├── trimmed_nmii.fasta.contree
├── trimmed_nmii.fasta.iqtree
├── trimmed_nmii.fasta.log
├── trimmed_nmii.fasta.mldist
├── trimmed_nmii.fasta.splits.nex
```

---

# Tools Used

- MAFFT v7.505
- ClipKIT
- IQ-TREE2 v2.3.6
- iTOL
- UniProt Database

---

# Conclusion

This analysis demonstrates how gene duplication and evolutionary divergence contributed to the expansion of the non-muscle myosin II family in vertebrates.

The resulting paralogs retain highly conserved motor functionality while supporting increasingly specialized cellular roles in complex multicellular organisms.

The study highlights the balance between evolutionary conservation and functional diversification that shapes essential cytoskeletal protein families across eukaryotic evolution.

---
