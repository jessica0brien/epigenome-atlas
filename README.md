# Epigenome Atlas — demo

A single-page reference tool for the proteins that write, erase and read chromatin marks. Search a protein, then look at it two ways: its predicted 3D structure, and an animated walk-through of the methylation → silencing → inhibition → re-expression sequence.

**Live:** `https://jessica0brien.github.io/epigenome-atlas/`

---

## What this is

- A **working demo**, not a finished tool. Two lenses are built (Structure, Mechanism); four are stubbed.
- Structures are fetched **live** from AlphaFold DB at page load, via a UniProt accession resolved from the gene symbol. Nothing is bundled, nothing is cached, nothing is hardcoded.
- The 3D view is an interactive **cartoon/ribbon representation** rendered with 3Dmol.js and coloured by pLDDT using the AlphaFold DB convention.

## What this is not

- **The mechanism animation is schematic, not a simulation.** No molecular dynamics, no docking, no structural prediction. What it asserts is the *sequence of events*; the shapes and positions are diagrammatic. Each step carries its own citation.
- **AlphaFold models are predictions, not experimental structures.** Low-confidence (yellow/orange) regions are frequently intrinsically disordered — absence of a confident fold there is information, not model failure.
- If a structure cannot be fetched, the viewer **draws nothing** and states why. A decorative molecule standing in for the real one would be worse than an empty panel.

## Data sources

| Source | Used for | Licence |
|---|---|---|
| [AlphaFold Protein Structure Database](https://alphafold.ebi.ac.uk/) (EMBL-EBI / Google DeepMind) | Predicted structures and pLDDT | CC-BY-4.0 |
| [UniProt](https://www.uniprot.org/) | Accession resolution, protein names | CC-BY-4.0 |
| [RCSB PDB](https://www.rcsb.org/) | Experimental structures loaded by ID | Public domain |
| [3Dmol.js](https://3dmol.org/) | Interactive WebGL cartoon/ribbon rendering | BSD-3-Clause |

AlphaFold DB and UniProt are used under CC-BY-4.0 and are credited here as that licence requires. See the [AlphaFold DB licence and disclaimer](https://alphafold.ebi.ac.uk/assets/License-Disclaimer.pdf).

## Citations in the mechanism lens

The step captions reference well-established primary literature on nucleosome structure, PRC2 catalysis and allosteric activation, chromodomain reading of H3K27me3, PRC1-mediated compaction, KDM6 demethylation, and EZH2 inhibition as differentiation therapy. **Verify each reference against the primary source before relying on it or citing it onward.**

## How it works

One HTML file, no build step. Open `index.html` in a browser and it runs; the pinned 3Dmol.js viewer is loaded from cdnjs.

1. Gene symbol → UniProt REST → reviewed human accession
2. Accession → AlphaFold DB API → model file URL → PDB text
3. PDB text loaded into 3Dmol.js for interactive secondary-structure cartoon rendering
4. AlphaFold pLDDT values read from the PDB B-factor field and applied to the cartoon with the standard confidence colours

The mechanism lens is a parameter-tweened canvas animation with an eased interpolator between eight defined states.

## AI assistance

This demo was built with assistance from Claude (Anthropic). All scientific claims should be verified against the cited primary sources before use in academic work.

## Licence

MIT — see [LICENSE](LICENSE). The licence covers this code only, not the third-party data it retrieves at runtime, which carries its own terms as listed above.
