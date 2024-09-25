# Datasheet for dataset "QueerReclaimLex"

Questions from the [Datasheets for Datasets](https://arxiv.org/abs/1803.09010) paper, v7.

Jump to section:

- [Motivation](#motivation)
- [Composition](#composition)
- [Collection process](#collection-process)
- [Preprocessing/cleaning/labeling](#preprocessingcleaninglabeling)
- [Uses](#uses)
- [Distribution](#distribution)
- [Maintenance](#maintenance)

## Motivation

### For what purpose was the dataset created? 
The dataset _QueerReclaimLex_ was created towards understanding how language models make sense of gender-queer reclaimed slurs. More details are here.

### Who created the dataset (e.g., which team, research group) and on behalf of which entity (e.g., company, institution, organization)?
The dataset was created by a team at the University of Southern California's Information Science Institute.

### Who funded the creation of the dataset? 
This dataset is not associated with any grant.

### Any other comments?

## Composition

_Most of these questions are intended to provide dataset consumers with the
information they need to make informed decisions about using the dataset for
specific tasks. The answers to some of these questions reveal information
about compliance with the EU’s General Data Protection Regulation (GDPR) or
comparable regulations in other jurisdictions._

### What do the instances that comprise the dataset represent (e.g., documents, photos, people, countries)?
Each instance represents an instance of potentially inoffensive LGBTQ+ slur use and its levels of harm as measured by humans and models.

### How many instances are there in total (of each type, if appropriate)?
1442 instances. There are 103 templates, each of which 'explodes' into one instance for each of 14 terms (8 slurs, 6 identity terms).

### Does the dataset contain all possible instances or is it a sample (not necessarily random) of instances from a larger set?

We use [NB-TwitCorpus3M](https://arxiv.org/pdf/2303.04837), a collection of  3 million tweets authored by approximately 3,000 Twitter users who have non-binary pronouns in their profile biography. The presence of pronouns in this dataset is determined by the user's specification. In particular, pronouns are gleaned from any combination of {he, him, his, she, her, hers, they, them, theirs, their, xe, xem, ze, zem} separated by forward slashes or commas, with any or no white space in their profile descriptions. We compile potentially non-derogatory uses of slurs posted by non-binary users that are judged highly toxic by Detoxify.


### What data does each instance consist of? 

- template_idx: index for the template used
- term: the identity term or slur used to substantiate the template
- text: the actual instantation, the english sentence featuring a (possibly) reclaimed LGBTQ+ slur.


### Is there a label or target associated with each instance?

Annotations for each instance:

Instances are labeled for two definitions of harm depending on speaker identity. Scores are one of {0, 0.5, 1} where 0 means no harm, .5 means uncertain and 1 means harmful.
- `HARMFUL_IN`: Whether the post is harmful, given that the author is an *ingroup* member
- `HARMFUL_OUT`: Whether the post is harmful, given that the author is an *outgroup* member.
Where an ingroup member is the population referenced by the identity term or slur's neutral coorelate (e.g. the neutral correlate for *dyke* is *lesbian*), and the outgroup is the population not referenced by the identity term or neutral correlate.

Each type of harm has variables for 4 different values. The same can be extended for `HARMFUL_OUT`.
- `HARMFUL_IN_1` denotes annotator 1's score, `HARMFUL_IN_2` for annotator 2's score
- `HARMFUL_IN_mu` for the mean of the two annotator's harm scores 
- `HARMFUL_IN_gold` is a binary variable reflecting whether the harm score's mean is above a threshold of 0.5.

**Ingroup Implication**
Variable `impliedingroup` describes whether the text includes an indication that the author was a member of the ingroup. Values are binary. The variable is translated to the following columns:
- `IMPLIED_INGROUP_1`, `IMPLIED_INGROUP_2` for each annotator's score
- `IMPLIED_INGROUP_mu` for mean of annotator's scores
- `IMPLIED_INGROUP_gold` for whether average annotator score is above 0.5 (in this case, both annotators agree)

**Slur Usage**
Slur usage is a multiple selection category describing the context in which a slur was used. Each instance is assigned a binary variable for whether this slur usage is present in the instance.
- `Recollection`: Recollection of a time a slur was used.
- `Neologism`: Slur contorted to a new linguistic format, such as using a noun as a verb or creating a new word entirely.
- `Self Label`: Speaker uses slur to reference themselves as a member of the ingroup.
- `Other Label`: Slur ascribed to someone who is not the speaker.
- `Group Label`: Slur used to describe a group of people.
- `Reclamation`: Slur use that places power with ingroup members.
- `Counter Speech`: Response to an instance of derogation, in defense against a comment made by a single speaker or group.
- `Quote`: Reference to a slur embedded in a quote or paraphrase. 
- `Homonym`: A slur with one or more non-derogatory meanings.
- `Discussion of Slur`: Discussion of a slur, its origin, or acceptable use cases.
- `Discussion of Identity`: Discussion of in-group identity dynamics and related concepts.
- `Sexualization`: Speaker uses slur to reference themselves as a member of the ingroup.
- `Sarcasm`: A slur used ironically, contrary to its original meaning.

### Is any information missing from individual instances?

Information identifying which annotator scored each instance is omitted.

### Are relationships between individual instances made explicit (e.g., users’ movie ratings, social network links)?

Yes, using template index and term fields.

### Are there any errors, sources of noise, or redundancies in the dataset?

Some instances have annotator disagreement, creating noisy labels. 

### Is the dataset self-contained, or does it link to or otherwise rely on external resources (e.g., websites, tweets, other datasets)?

An external resource was used in the dataset's creation but has been anonymized and does not need to be accessed to use this dataset.

### Does the dataset contain data that might be considered confidential (e.g., data that is protected by legal privilege or by doctor-patient confidentiality, data that includes the content of individuals’ non-public communications)?

The dataset includes short-form texts authored by self-disclosed gender-queer Twitter/X users. This holds potential to out potentially closeted people.

### Does the dataset contain data that, if viewed directly, might be offensive, insulting, threatening, or might otherwise cause anxiety?

Yes, half the dataset uses slurs.

### Does the dataset relate to people? 

Yes

### Does the dataset identify any subpopulations (e.g., by age, gender)?

All tweets are authored by someone who uses non-binary pronouns.

### Is it possible to identify individuals (i.e., one or more natural persons), either directly or indirectly (i.e., in combination with other data) from the dataset?

Yes, one could identify from the original tweets used to create this dataset.

### Does the dataset contain data that might be considered sensitive in any way (e.g., data that reveals racial or ethnic origins, sexual orientations, religious beliefs, political opinions or union memberships, or locations; financial or health data; biometric or genetic data; forms of government identification, such as social security numbers; criminal history)?

Yes, trans* identity.

### Any other comments?

## Collection process

### How was the data associated with each instance acquired?

From earlier answer: We use [NB-TwitCorpus3M](https://arxiv.org/pdf/2303.04837), a collection of  3 million tweets authored by approximately 3,000 Twitter users who have non-binary pronouns in their profile biography. The presence of pronouns in this dataset is determined by the user's specification. In particular, pronouns are gleaned from any combination of {he, him, his, she, her, hers, they, them, theirs, their, xe, xem, ze, zem} separated by forward slashes or commas, with any or no white space in their profile descriptions. We compile potentially non-derogatory uses of slurs posted by non-binary users that are judged highly toxic by Detoxify.

### What mechanisms or procedures were used to collect the data (e.g., hardware apparatus or sensor, manual human curation, software program, software API)?

Manual human curation. These procedures were validated by having gender-queer community members separately score the instances for harm.

### Who was involved in the data collection process (e.g., students, crowdworkers, contractors) and how were they compensated (e.g., how much were crowdworkers paid)?
The annotators were a combination of students and professors. They were not paid.

### Over what timeframe was the data collected?

Original tweets from 2021-2022.

### Were any ethical review processes conducted (e.g., by an institutional review board)?

No.

### Does the dataset relate to people?
Yes

### Did you collect the data from the individuals in question directly, or obtain it via third parties or other sources (e.g., websites)?
Data was collected from then Twitter (now X) using the company's API.

### Were the individuals in question notified about the data collection?

No.

### Did the individuals in question consent to the collection and use of their data?

No.

### Has an analysis of the potential impact of the dataset and its use on data subjects (e.g., a data protection impact analysis) been conducted?

No.

### Any other comments?

## Preprocessing/cleaning/labeling
### Was any preprocessing/cleaning/labeling of the data done (e.g., discretization or bucketing, tokenization, part-of-speech tagging, SIFT feature extraction, removal of instances, processing of missing values)?

Not applicable, as the dataset was manually curated.

### Was the “raw” data saved in addition to the preprocessed/cleaned/labeled data (e.g., to support unanticipated future uses)?

Yes original tweets are still stored.

### Is the software used to preprocess/clean/label the instances available?

N/A

### Any other comments?

## Uses

### Has the dataset been used for any tasks already?

Yes. The dataset has been used for testing how large language models interpret toxicity of reclaimed slurs.

### Is there a repository that links to any or all papers or systems that use the dataset?

Yes, this very github repository!

### What (other) tasks could the dataset be used for?

Measuring fairness in a toxicity or content moderation model. 

### Is there anything about the composition of the dataset or the way it was collected and preprocessed/cleaned/labeled that might impact future uses?

No more than already discussed (aka slurs)

### Are there tasks for which the dataset should not be used?

Actively biasing a model

### Any other comments?

## Distribution

### Will the dataset be distributed to third parties outside of the entity (e.g., company, institution, organization) on behalf of which the dataset was created? 

Yes!

### How will the dataset will be distributed (e.g., tarball on website, API, GitHub)?

GitHub


### Will the dataset be distributed under a copyright or other intellectual property (IP) license, and/or under applicable terms of use (ToU)?

No

### Have any third parties imposed IP-based or other restrictions on the data associated with the instances?

No

### Do any export controls or other regulatory restrictions apply to the dataset or to individual instances?

No

### Any other comments?

## Maintenance

_These questions are intended to encourage dataset creators to plan for dataset maintenance
and communicate this plan with dataset consumers._

### Who is supporting/hosting/maintaining the dataset?

Rebecca Dorn, graduate student at the time of this datasheet

### How can the owner/curator/manager of the dataset be contacted (e.g., email address)?
rdorn(at)usc(dot)edu

### Is there an erratum?
No

### Will the dataset be updated (e.g., to correct labeling errors, add new instances, delete instances)?
At this time there is no plan for update. However, if adding more instances is something that becomes a plan later, I imagine users would be notified on GitHub.

### If the dataset relates to people, are there applicable limits on the retention of the data associated with the instances (e.g., were individuals in question told that their data would be retained for a fixed period of time and then deleted)?

No

### Will older versions of the dataset continue to be supported/hosted/maintained?

In the case of updates, GitHub will maintain old versions of the dataset.

### If others want to extend/augment/build on/contribute to the dataset, is there a mechanism for them to do so?

That would be super cool! I believe I have provided everything needed to do that.

### Any other comments?
