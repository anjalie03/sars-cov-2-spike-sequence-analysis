# SARS-CoV-2 Spike Sequence Analysis

Comparative analysis of SARS-CoV-2 spike (S) protein sequences from the Alpha, Delta, and Omicron variants against the Wuhan reference. The project covers multiple sequence alignment, mutation calling, pairwise comparison, sequence property statistics, and maximum-likelihood phylogenetics.

## Overview

- **Sequences:** 10 spike protein sequences: the Wuhan reference (`Reference_WuHan`, 1273 aa), 3 Alpha, 3 Delta, and 3 Omicron sequences
- **Alignment:** 1276 amino-acid sites, 96.9% constant sites, 37 parsimony-informative sites
- **Phylogeny:** IQ-TREE 2.0.7 with ModelFinder (best-fit model FLU+I by BIC) and 1000 ultrafast bootstrap replicates

## How to run

1. Open `spike_protein_variant_analysis.ipynb` in Google Colab (in Colab: **File → Open notebook → GitHub**, then select this repository).
2. Run the cells from top to bottom.
3. Outputs are written to `data/processed/`, `Results/Tables/`, and `Results/Figures/`.

## Repository structure

```
├── data/
│   └── processed/          # MAFFT alignment and IQ-TREE output files
├── Results/
│   ├── Figures/            # trees, mutation plots, length and composition plots
│   └── Tables/             # mutations, pairwise comparison, sequence statistics
├── spike_protein_variant_analysis.ipynb
├── LICENSE
└── README.md
```

Each data and results folder has its own README describing its files.

## Results tables

| File | Description |
|------|-------------|
| `Results/Tables/mutations.csv` | Amino acid differences from the reference (`sample`, `lineage`, `position`, `ref`, `alt`, `mutation`) |
| `Results/Tables/pairwise_vs_reference.csv` | Pairwise alignment of each sequence to the reference (`score`, `identities`, `mismatches`, `gaps`, `percent_identity`) |
| `Results/Tables/sequence_stats.csv` | Length, molecular weight, isoelectric point, instability index, and GRAVY hydrophobicity per sequence |

## Key findings

- **Omicron is the most divergent lineage.** Each Omicron sequence carries 30 amino acid changes relative to the Wuhan reference, compared with 5-9 for Delta and 7-8 for Alpha (ambiguous X residues excluded).

| Lineage | Sequences | Mutations per sequence (excluding X) |
|---------|-----------|--------------------------------------|
| Alpha | 3 | 7, 8, 7 |
| Delta | 3 | 9, 6, 5 |
| Omicron | 3 | 30, 30, 30 |

- **Sequence quality varies.** Of 287 rows in `mutations.csv`, 155 involve ambiguous X residues and 132 are called substitutions. This matters most for Alpha_1, which is 1209 aa long (reference: 1273) and shows 68 mismatches (94.42% identity) in the pairwise table but only 7 substitutions. Identity values count X residues as mismatches, so they understate similarity for incomplete sequences.
- **The spike is highly conserved.** Across the alignment, 96.9% of sites are constant and only 37 are parsimony-informative.
- **Phylogeny.** A maximum-likelihood tree with bootstrap support is shown in `Results/Figures/spike_tree_bootstrap.png`.

## Tools

- Python (Google Colab), Biopython, pandas, matplotlib
- Alignment: MAFFT v7.505
- Phylogenetics: IQ-TREE 2.0.7 (ModelFinder, 1000 ultrafast bootstrap replicates)

## Limitations

- With only 10 sequences and 37 informative sites, the tree topology is indicative rather than definitive, and closely related sequences may not resolve with strong support.
- Several sequences are incomplete or contain ambiguous residues, which affects mismatch counts and identity values.

## License

See [LICENSE](LICENSE).

## Citations

- Minh et al. (2020) IQ-TREE 2: new models and efficient methods for phylogenetic inference in the genomic era. *Mol. Biol. Evol.*
- Kalyaanamoorthy et al. (2017) ModelFinder: fast model selection for accurate phylogenetic estimates. *Nature Methods*
- Hoang et al. (2018) UFBoot2: improving the ultrafast bootstrap approximation. *Mol. Biol. Evol.*
- Katoh and Standley (2013) MAFFT multiple sequence alignment software version 7. *Mol. Biol. Evol.*
