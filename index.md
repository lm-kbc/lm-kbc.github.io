---
title: LM-KBC
description: Knowledge Base Construction from Pre-trained Language Models
---

### Task Description

Pre-trained language models (LMs) have advanced a range of semantic tasks and have also shown promise for knowledge extraction from the models itself. Although several works have explored this ability in a setting called LM probing using prompting, the viability of _knowledge base construction_ from LMs has not yet been explored. In this challenge, we invite participants to build actual knowledge bases from LMs, for given subjects and relations. In crucial difference to existing probing benchmarks like LAMA (<a href="https://arxiv.org/pdf/1909.01066.pdf" target="_blank">Petroni et al., 2019</a>), we make no simplifying assumptions on relation cardinalities, i.e., a subject-entity can stand in relation with zero, one, or many object-entities. Furthermore, submissions need to go beyond just ranking the predictions, and materialize outputs, which are evaluated by established KB metrics of precision and recall.

Formally, given the input subject-entity ($\mathtt{s}$) and relation ($\mathtt{r}$), the task is to predict all the correct object-entities ($\mathtt{\{o_1, o_2, ..., o_k\}}$) using LM probing. The challenge comes with two tracks: (i) a BERT-type (e.g., <a href="https://arxiv.org/pdf/1907.11692.pdf" target="blank">RoBERTA</a>, <a href="https://arxiv.org/pdf/1901.02860.pdf" target="blank">Transformer-XL</a>, etc.) LM track with low computational requirements, and (ii) an open track, where participants can use any LM (e.g., <a href="https://d4mucfpksywv.cloudfront.net/better-language-models/language-models.pdf" target="_blank">GPT-2</a>, <a href="https://arxiv.org/pdf/1910.13461.pdf" target="blank">BART</a> etc.) of their choice.

### Dataset

We release a dataset (train and validation) for a diverse set of 12 relations, each covering a different set of subject-entities and along with complete list ground truth object-entities per subject-relation-pair. The total number of object-entities varies for a given subject-relation pair. The train dataset subject-relation-object triples can be used for training the language models in any form, while validation can be used for hyperparameter tuning. Futher details on the relations are given below:


 **Relation**     | **Description**
---------------------------|------------------------------------------------------------------------
 CountryBordersWithCountry | country ($s$) shares a land border with another country ($o$)
 CountryOfficialLanguage   | country ($s$) has an official language ($o$)
 RiverBasinsCountry        | country ($s$) basins in a country ($o$)
 StateSharesBorderState    | state ($s$) of a country shares a land border with another state ($o$)
 ChemicalCompoundElement   | chemical compound ($s$) consists of an element ($o$)
 PersonInstrument          | person ($s$) plays an instrument ($o$)
 PersonLanguage            | person ($s$) speaks in a language ($o$)
 PersonEmployer            | person ($s$) is or was employed by a company ($o$)
 PersonProfession          | person ($s$) held a profession ($o$)
 PersonPlaceOfDeath        | person ($s$) died at a location ($o$)
 PersonCauseOfDeath        | person ($s$) died due to a cause ($o$)
 CompanyParentOrganization | company ($s$) has another company ($o$) as its parent organization


The dataset file contains three columns, (1) subject-entity, (2) object-entity, and (3) relation. To faciliate usage of LMs like BERT which are constrained by single-token predictions, we provide a valid single-token form for multi-token object-entities, and either of them can be given as an output.


<a class="btn actionBtn inverseBtn" href="/dataset" download>Download the Dataset</a>.


### Evaluation Metrics

We use precision, recall and f1-score as evaluation metrics to compare the predicted object-entities with true object-entities on the hidden test dataset. We release a <a href="/models/bert.py">baseline</a> implementation and <a href="/evaluation.py">evaluation</a> script. The baseline model probes the BERT langauge model using a sample prompt like _"Germany shares border with \[MASK\]"_ and selects object-entities predicted in the \[MASK\] position with $>= 0.5$ likelihood as outputs on validation subject-entities. Participants can use evaluation script to compute the precision, recall and f1-score to assess the performance of their systems.

### Submission Details

Participants are required to submit their system implemeting the LM probing approach and the output for test dataset subject-entites. The test dataset is initially hidden to preserve the integrity of results, and is released closer to the system submission deadline. The output file for the test subject-entities should be formatted similar to the train dataset files (one for each relation). Top performing systems will get an opportunity to present their ideas and results during the ISWC 2022 conference.

### Communication

For general questions or discussion please use the Google group: <a href="https://groups.google.com/g/lm-kbc" target="_blank">https://groups.google.com/g/lm-kbc</a>

### Important Dates
| Activity | Dates |
|:---|:---:|
| Dataset (train and val) release    | 13 May 2022         |
| Dataset (test) release             | 11 July 2022        |
| System submission deadline         | 14 July 2022        |
| Winner Announcement                | 15 August 2022      |
| ISWC Invitations                   | 15 August 2022      |
| ISWC Presentations                 | 23-27 October 2022  |

### Organizers
- <a href="https://people.mpi-inf.mpg.de/~ssinghan/" target="_blank">Sneha Singhania</a>, Max Planck Institute for Informatics, Germany
- <a href="https://www.tuan-phong.com/" target="_blank">Tuan-Phong Nguyen</a>, Max Planck Institute for Informatics, Germany
- <a href="http://simonrazniewski.com/" target="_blank">Simon Razniewski</a>, Max Planck Institute for Informatics, Germany