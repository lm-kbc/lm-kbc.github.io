---
title: LM-KBC
description: Knowledge Base Construction from Pre-trained Language Models
---

### Task Description

Pre-trained language models (LMs) have advanced a range of semantic tasks and have also shown promise for knowledge extraction from the models itself. Although several works have explored this ability in a setting called probing or prompting, the viability of _knowledge base construction_ from LMs has not yet been explored.
In this challenge, participants are asked to build actual knowledge bases from LMs, for given subjects and relations. In crucial difference to existing probing benchmarks like LAMA (<a href="https://arxiv.org/pdf/1909.01066.pdf" target="_blank">Petroni et al., 2019</a>), we make no simplifying assumptions on relation cardinalities, i.e., a subject-entity can stand in relation with zero, one, or many object-entities. Furthermore, submissions need to go beyond just ranking the predictions, and materialize outputs, which are evaluated by established KB metrics of precision and recall. The challenge comes with two tracks: (i) a BERT-type LM track with low computational requirements, and (ii) an open track, where participants can use any LM of their choice.

### Dataset

Download the dataset <ul class="list-unstyled"><li><a class="btn actionBtn inverseBtn" href="/lm-kbc.github.io/dataset/dataset" download>.

### Evaluation Metrics

### Submission Details

### Communication

For general questions please use the Google group: <a href="https://groups.google.com/g/lm-kbc" target="_blank">https://groups.google.com/g/lm-kbc</a>

### Important Dates
| Activity | Dates |
|:---|:---:|
| Dataset release              | 13 May 2022         |
| System submission deadline   | 14 July 2022        |
| Winner Announcement          | 15 August 2022      |
| ISWC Invitations             | 15 August 2022      |
| ISWC Presentations           | 23-27 October 2022  |

### Organizers
- <a href="https://people.mpi-inf.mpg.de/~ssinghan/" target="_blank">Sneha Singhania</a>, Max Planck Institute for Informatics, Germany
- <a href="https://www.tuan-phong.com/" target="_blank">Tuan-Phong Nguyen</a>, Max Planck Institute for Informatics, Germany
- <a href="http://simonrazniewski.com/" target="_blank">Simon Razniewski</a>, Max Planck Institute for Informatics, Germany