# NM2 Evolution Analysis Pipeline

---

## 1. Sequence Retrieval

Protein sequences of non-muscle myosin II homologs were retrieved from the UNIPROT database in FASTA format.

Species included, their genes and UNIPROTIDs:

1. Homo sapiens - MYH9(P35579), MYH10(P35580), MYH14(Q7Z406)

2. Mus musculus - MYH9(Q8VDD5), MYH10(Q61879), MYH14(Q6URW6)

3. Danio rerio - myh9a(A0A8M2BCY6), myh10(I3ISA3)

4. Gallus gallus - MYH9(P14105), MYH10(Q789A4)

5. Drosophila melanogaster - zip(Q99323)

6. Caenorhabditis elegans - nmy-2(Q22869)

7. Dictyostelium discoideum - mhcA(P08799)

---

## 2. Multiple Sequence Alignment

**Tool used:** MAFFT

**Command used:**

```bash
mafft --auto raw_data/all_nmii.fasta > alignment/aligned_nmii.fasta
```

### Parameters

- Alignment strategy automatically selected using `--auto`
- Sequence type detected: Amino acid (protein)
- Substitution matrix used: BLOSUM62
- Progressive alignment with iterative refinement performed
- UPGMA guide tree constructed internally
- Gap opening penalty automatically optimized by MAFFT
- Iterative refinement cycles: 16
- Thread usage: Single-thread execution

### Results

- Total sequences aligned: 13
- Alignment completed successfully
- Convergence achieved during iterative refinement

**Output:** `aligned_nmii.fasta`

---

## 3. Alignment Trimming

**Tool used:** ClipKIT

**Command used:**

```bash
~/.local/bin/clipkit alignment/aligned_nmii.fasta -o alignment/trimmed_nmii.fasta
```

### Parameters

- Sequence type detected: Protein
- Trimming mode: smart-gap
- Gap threshold: 0.9231
- Codon processing: Disabled
- Trim terminal ends only: False
- Log file generation: Disabled

### Results

- Original length: 2321
- Number of sites kept: 2031
- Number of sites trimmed: 290
- Percentage of alignment trimmed: 12.495%

**Output:** `trimmed_nmii.fasta`

---

## 4. Phylogenetic Tree Construction

**Tool used:** IQ-TREE2

**Command used:**

```bash
iqtree2 -s alignment/trimmed_nmii.fasta -m MFP -B 1000 --alrt 1000 -T AUTO --prefix trees/nmii_tree --redo
```

### Parameters

- Sequence type automatically detected: Protein
- Number of sequences: 13
- Alignment length: 2031 amino acid positions
- CPU threads automatically detected using `-T AUTO`
- MFP: ModelFinder Plus used for automatic model selection
- Ultrafast bootstrap replicates: 1000
- SH-aLRT replicates: 1000

### Best-fit model selected

`Q.insect+F+R3`

### Results

- Total tree search iterations: 102
- Final optimized log-likelihood: -25085.630
- Bootstrap consensus tree generated successfully

### Major files generated

- `nmii_tree.treefile`
- `nmii_tree.contree`
- `nmii_tree.iqtree`
- `nmii_tree.log`

---

## 5. Tree Visualization

**Tool used:** iTOL (Interactive Tree Of Life)

### Output

`nmii_phylogenetic_tree.svg`
