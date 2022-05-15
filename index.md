---
title: LM-KBC
description: Knowledge Base Construction from Pre-trained Language Models
---

Pre-trained language models (LMs) have advanced a range of semantic tasks and have also shown promise for knowledge extraction from the models itself. Although several works have explored this ability in a setting called LM probing using prompting or prompt-based learning (<a href="https://arxiv.org/pdf/2107.13586.pdf" target="_blank">Liu et al., 2021</a>), the viability of _knowledge base construction_ from LMs has not yet been explored. In this challenge, we invite participants to build actual knowledge bases from LMs, for given subjects and relations. In crucial difference to existing probing benchmarks like LAMA (<a href="https://arxiv.org/pdf/1909.01066.pdf" target="_blank">Petroni et al., 2019</a>), we make no simplifying assumptions on relation cardinalities, i.e., a subject-entity can stand in relation with zero, one, or many object-entities. Furthermore, submissions need to go beyond just ranking the predictions, and materialize outputs, which are evaluated by established KB metrics of precision and recall.

## Table of Contents

- [Table of Contents](#table-of-contents)
  - [Task Definition](#task-definition)
  - [Dataset](#dataset)
  - [Task Evaluation](#task-evaluation)
  - [Submission Details](#submission-details)
  - [Important Dates](#important-dates)
  - [Organizers](#organizers)

<div id='sec-task-definition'/>

### Task Definition

Formally, given the input subject-entity (<code>s</code>) and relation (<code>r</code>), the task is to predict all the correct object-entities ({<code>o<sub>1</sub></code>, <code>o<sub>2</sub></code>, ..., <code>o<sub>k</sub></code>}) using LM probing. The challenge comes with two tracks: (i) a <a href="https://aclanthology.org/N19-1423/" target="_blank">BERT</a> (BERT-base or BERT-large) track with low computational requirements, and (ii) an open track, where participants can use any LM (e.g., <a href="https://arxiv.org/pdf/1907.11692.pdf" target="blank">RoBERTa</a>, <a href="https://arxiv.org/pdf/1901.02860.pdf" target="blank">Transformer-XL</a>, <a href="https://d4mucfpksywv.cloudfront.net/better-language-models/language-models.pdf" target="_blank">GPT-2</a>, <a href="https://arxiv.org/pdf/1910.13461.pdf" target="blank">BART</a> etc.) of their choice.

</div>

<div id='sec-dataset'/>

### Dataset

We release a dataset (train and development) for a diverse set of 12 relations, each covering a different set of subject-entities and along with complete list ground truth object-entities per subject-relation-pair. The total number of object-entities varies for a given subject-relation pair. The train dataset subject-relation-object triples can be used for training the language models in any form, while development can be used for hyperparameter tuning. Futher details on the relations are given below:

 <table style="background-color:#ebe2ea;
            font-family:Lucida Console,Courier New,monospace;
            font-size:13px;
            border-spacing:0;
            border-collapse:collapse;">
    <tr>
        <th><strong>Relation</strong></th>
        <th><strong>Description</strong></th>
    </tr>
    <tr>
        <td>CountryBordersWithCountry</td>
        <td>country (s) shares a land border with another country (o)</td>
    </tr>
    <tr>
        <td>CountryOfficialLanguage</td>
        <td>country (s) has an official language (o)</td>
    </tr>
    <tr>
        <td>RiverBasinsCountry</td>
        <td>country (s) basins in a country (o)</td>
    </tr>
    <tr>
        <td>StateSharesBorderState</td>
        <td>state (s) of a country shares a land border with another state (o)</td>
    </tr>
    <tr>
        <td>ChemicalCompoundElement</td>
        <td>chemical compound (s) consists of an element (o)</td>
    </tr>
    <tr>
        <td>PersonInstrument</td>
        <td>person (s) plays an instrument (o)</td>
    </tr>
    <tr>
        <td>PersonLanguage</td>
        <td>person (s) speaks in a language (o)</td>
    </tr>
    <tr>
        <td>PersonEmployer</td>
        <td>person (s) is or was employed by a company (o)</td>
    </tr>
    <tr>
        <td>PersonProfession</td>
        <td>person (s) held a profession (o)</td>
    </tr>
    <tr>
        <td>PersonPlaceOfDeath</td>
        <td>person (s) died at a location (o)</td>
    </tr>
    <tr>
        <td>PersonCauseOfDeath</td>
        <td>person (s) died due to a cause (o)</td>
    </tr>
    <tr>
        <td>CompanyParentOrganization</td>
        <td>company (s) has another company (o) as its parent organization</td>
    </tr>
</table>

Each row in the dataset files constitutes one triple, of (1) subject-entity, (2) relation, and (3) object-entity. For (3), we sometimes provide multiple aliases, where outputing any one of them is sufficient. In particular, to faciliate usage of LMs like BERT (which are constrained by single-token predictions), we provide atleast one valid single-token form for every object.
To represent subjects with zero valid objects, we introduce a special value <em>NONE</em>. Those subjects will then have one row with that value, e.g., ( Apple Inc., CompanyParentOrganization, <em>NONE</em> ).

<div style="text-align:center;margin-top:48px;">
 <a href="https://github.com/lm-kbc/lm-kbc.github.io/blob/main/dataset" 
    target="_blank"
    class="btn"
    style="background-color:#1e6bb8;color:#ffffff;">
  <strong>
   Download dataset
   </strong>
 </a>
</div>

</div>

<div id='sec-task-evaluation'/>

### Task Evaluation

We use a standard KBC evaluation metric, the F1-score (based on the combination of precision and recall), to compare the predicted object-entities with true object-entities on the hidden test dataset. We release a <a href="/models/bert.py">baseline</a> implementation and <a href="/evaluation.py">evaluation</a> script. The baseline model probes the BERT language model using a sample prompt like _"China shares border with \[MASK\]"_ and selects object-entities predicted in the \[MASK\] position with greater than or equal to 0.5 likelihood as outputs. Participants can use the evaluation script to compute the F1-score for assessing the performance of their systems.

For general questions or discussion please use the Google group: <a href="https://groups.google.com/g/lm-kbc" target="_blank">https://groups.google.com/g/lm-kbc</a>.

</div>

<div id='sec-submission-details'/>

### Submission Details

Participants are required to submit (1) their system implementing the LM probing approach, (2) the output for the test dataset subject-entites, (3) a system description in PDF format (no longer than 12 pages, LNCS style). The test dataset is initially hidden to preserve the integrity of results, and is released 3 days before system submission deadline. The output files for the test subject-entities must be formatted like the train dataset files (one for each relation), and submitted along with the system. Top performing systems will get an opportunity to present their ideas and results during the ISWC 2022 conference, and will be published in the CEUR challenge proceedings. System descriptions should be submitted on <a href="https://easychair.org/conferences/?conf=lmkbc2022">Easychair</a>.

</div>

<div id='sec-important-dates'/>

### Important Dates

| Activity | Dates |
|:---|:---:|
| Dataset (train and val) release    | 17 May 2022         |
| Dataset (test) release             | 11 July 2022        |
| System + test dataset predictions submission         | 14 July 2022        |
| Winner Announcement                | 15 August 2022      |
| ISWC Invitations                   | 15 August 2022      |
| ISWC Presentations                 | 23-27 October 2022  |

</div>

<div id='sec-organizers'>

### Organizers

- <a href="https://people.mpi-inf.mpg.de/~ssinghan/" target="_blank">Sneha Singhania</a>, Max Planck Institute for Informatics, Germany
- <a href="https://www.tuan-phong.com/" target="_blank">Tuan-Phong Nguyen</a>, Max Planck Institute for Informatics, Germany
- <a href="http://simonrazniewski.com/" target="_blank">Simon Razniewski</a>, Max Planck Institute for Informatics, Germany

</div>
