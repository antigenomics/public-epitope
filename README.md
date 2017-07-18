## public-epitope
Selection &amp; assembly prob TCRs specific to different epitopes

### Contents:

* ``vdjdb.slim.txt`` - VDJdb slim version snapshot of main repo (July 18 2017). Only HomoSapiens TRB.
* ``vj_nf_aging.txt`` - VJ usage for our aging dataset. Whole-size repertoires from 79 donors (no down-sampling, incl. UCB), non-functional clonotypes only.
* ``vj_nf_robins.txt`` - VJ usage for Robins data, only VJ **families** unfortunately. Perhaps it is better to use Murugan model as is?? Its likely based on ImmunoSEQ technology with all its V/J usage normalization tricks.

### Ideas:

* Compute VJ choice-agnostic rearrangement probabilities for VDJdb TRB CDR3 amino acid sequences.
* Re-normalize to VJ usage in aging, compare to observed incidence frequency (*TODO:* will upload overlap with aging & aging summary statistics later).
* Compare rearrangement probs across epitopes, HLA, species (ANOVA, etc).
* Compare odds-ratios between incidence expected from overlap with real data and assembly probabilities. The real data has a lower bound of 1 per 10^8 clonotypes incidence.
* Compare odds-ratios across epitopes, HLA, species to baseline. This will reveal negative and positive selection.

### More complex ideas

* Use HLA typing for Robins data to delineate HLA factor. This will require a good model for Robins data.
* We can do this for B27 donors with model built using our Aging data.
