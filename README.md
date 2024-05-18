# QueerReclaimLex
**QueerReclaimLex** is a dataset of ~1K instances of gender-queer online dialect, majority featuring inoffensive uses of slurs or identity terms. Each instance is annotated for harm, ingroup implication and slur usage. The dataset is in `QueerReclaimLex.csv`.

## **Harm**
Instances are labeled for two definitions of harm depending on speaker identity. Scores are one of {0, 0.5, 1} where 0 means no harm, .5 means uncertain and 1 means harmful.
- `HARMFUL_IN`: Whether the post is harmful, given that the author is an *ingroup* member
- `HARMFUL_OUT`: Whether the post is harmful, given that the author is an *outgroup* member.

Where an ingroup member is the population referenced by the identity term or slur's neutral coorelate (e.g. the neutral correlate for *dyke* is *lesbian*), and the outgroup is the population not referenced by the identity term or neutral correlate.

Each type of harm has variables for 4 different values. The same can be extended for `HARMFUL_OUT`.
- `HARMFUL_IN_1` denotes annotator 1's score, `HARMFUL_IN_2` for annotator 2's score
- `HARMFUL_IN_mu` for the mean of the two annotator's harm scores 
- `HARMFUL_IN_gold` is a binary variable reflecting whether the harm score's mean is above a threshold of 0.5.

## Ingroup Implication
Variable `impliedingroup` describes whether the text indicated that the author was a member of the ingroup.


## Slur Usage
![Examples of QueerReclaimLex](./images/template_examples3.png)
