## Contents:

The database itself:

* ``vdjdb.slim.txt`` - VDJdb slim version snapshot of main repo (July 18 2017). Only HomoSapiens TRB.

Variable-Joining segment usage:

* ``vj_nf_aging.txt`` - VJ usage for our aging dataset. Whole-size repertoires from 79 donors (no down-sampling, incl. UCB), non-functional clonotypes only.
* ``vj_nf_robins.txt`` - VJ usage for Robins data, only VJ **families** unfortunately. Perhaps it is better to use Murugan model as is?? Its likely based on ImmunoSEQ technology with all its V/J usage normalization tricks.

Annotated data for aging. Note that the pooled aging dataset has ``N=17,955,918`` unique CDR3 amino acid sequences from ``R=29,989,055`` rearrangements (this is the sum of the observed diversity, i.e. number of clonotypes V+J+CDR3nt, from all samples).

* The annotation was performed by allowing 0, 1 and 2 amino acid substitutions. The results are stored in ``aging_annot_0.txt.gz`` (around 3000 hits), ``aging_annot_1.txt.gz`` and ``aging_annot_2.txt.gz`` (very large, almost 4 mln hits).

Each entry in the ``aging_annot_X.txt.gz`` file has the following important fields:

* ``v,j,cdr3nt,cdr3aa`` - the actual amino acid variant as seen in the repertoire. Note that for cases with convergent recombination ``v,j,cdr3nt`` are the representative fields, i.e. the ones corresponding to the most frequent variant.
* ``v.segm,j.segm,cdr3`` - matched V/J/CDR3 amino acid sequence from VDJdb.
* ``antigen.epitope,antigen.species`` - specific epitope and its parent species
* ``mhc.a,mhc.b,mhc.class`` - HLA context details
* ``occurrences`` - the number of occurrences of the actual amino acid variant in the pooled repertoire. Thus, the frequency of a given variant that should be compared to the rearrangement probability is ``f=occurrences/R=occurrences/29,989,055``.

> N.B. the same amino acid variant can be present in the table multiple times if it matched several VDJdb records

### Rationale for allowing mismatches and consequences:

The rationale is that when looking for exact match more than half of VDJdb entries are not found in the entire aging study. We can use 1- and 2-MM variants safely (according to benchmark on VDJdb itself), however this means we need to adjust the rearrangement probabilities respectively.

* First, the observed frequency for a given VDJdb variant becomes ``f=sum(occurrences)/R`` where sum is over all matches (with 1- and 2-MMs we will have multi-hits).
* Next, when counting the rearrangement probability using Monte Carlo simulations we must allow the same number of mismatches as the one we've used for VDJdb matching.

## Ideas:

* Compute VJ choice-agnostic rearrangement probabilities for VDJdb TRB CDR3 amino acid sequences.
* Re-normalize to VJ usage in aging, compare to observed incidence frequency (*TODO:* will upload overlap with aging & aging summary statistics later).
* Compare rearrangement probs across epitopes, HLA, species (ANOVA, etc).
* Compare odds-ratios between incidence expected from overlap with real data and assembly probabilities. The real data has a lower bound of 1 per 10^8 clonotypes incidence.
* Compare odds-ratios across epitopes, HLA, species to baseline. This will reveal negative and positive selection.

### More complex ideas

* The 1- and 2-MM stuff can be done later.
* Use HLA typing for Robins data to delineate HLA factor. This will require a good model for Robins data.
* We can do this for B27 donors with model built using our Aging data.
