# WissenschaftsSTANDARD :bow_and_arrow:
A German dataset for few-shot relation extraction.

## Data Source
The sentences in WissenschaftsSTANDARD are drawn from the [10kGNAD dataset](https://github.com/tblock/10kGNAD).
10kGNAD is a topic classification dataset with journalistic articles from the Austrian newspaper ["Der STANDARD"](https://derstandard.at).
WissenschaftsSTANDARD only uses sentences from the "Wissenschaft" (science) topic category in 10kGNAD.
Therefore, the sentences mainly treat scientific discoveries and events in academia.

## Annotation Process
This dataset was created for the master thesis "Few-Shot Relation Extraction for German" by Anna Sauer.

The sentences were annotated by a marvellous crowdsourcing team including Chris, Christl, Florian, Hans, Jean-Francois, Julia, Kristin, Marco, Marina, Marius, MG and Sandra.
Thanks to you all! :cupid:

The minimalist annotation tool [Locksley](https://github.com/acid_ann/locksley) was used in the creation of WissenschaftsSTANDARD.

## Relation set
WissenschaftsSTANDARD contains the following eight relations:

| id | German name | English name | description | number of instances |
|----|-----|--------|--------|------|
| 0 | andere | OTHER | | 1,496 |
| 1 | veröffentlicht in | publishes in | a person publishes a text in a scientific journal | 61 |
| 2 | Leiter:in |  director | a person is at the head of an organisation | 76 |
| 3 | gehört an |  affiliation | a person is affiliated with an organisation (workplace, membership etc.) | 519 |
| 4 | Kollegin, Kollege | colleague | two people work together | 208 |
| 5 | nachgeordnete Organisation | subsidiary | an organisation belongs to a larger parent organisation | 145 |
| 6 | Partnerorganisation | partner organisation | two organisations work together | 216 |
| 7 | Standort in | located in | an organisation is situated in a location | 261 |
| 8 | Teilort | geographical part of | a location is part of a larger geographical entity | 116 |
| 9 | verleiht Preis an | awards prize to | an organisation awards a prize to a person | 13 |
| 10 | Gründer:in | founder | a person has founded an organisation | 6 |

In the dataset file, they are all referred to by their id. The total of labeled relation instances amounts to 3,117.
Note that one sentence from 10kGNAD can be labeled with several relations and can therefore appear several times in WissenschaftsSTANDARD.

The relations are assumed to have a fixed direction from one entity to another one.
Nevertheless, there are also two symmetric relations, colleague and partner organisation, that go both ways. 
For example, consider the sentence "Robin Hood and Friar Tuck are colleagues.". 
There is a colleague relation from Robin Hood to Friar Tuck. In addition, there is also a colleague relation from Friar Tuck.
In cases like this, WissenschaftsSTANDARD contains an separate instance for both directions.

## Dataset Format
The format of the JSON file is modeled after the data format of the [FewRel benchmark](https://thunlp.github.io/1/fewrel1.html) for few-shot relation extraction.
Each file contains a dictionary whose keys are the names of the relations in the dataset.
For each relation key, the corresponding value is a list of the labeled instances of that relation.
This list contains a dictionary for each individual instance with
* "tokens": a list with the token string sequence in the sentence
* "h": information on the head entity in a list with
  * a string with the entity mention in lower case
  * a string with the Wikidata id of the entity (cf. wikidata.org). In WissenschaftsSTANDARD, this string is left empty because no entity linking between the head and tail entity and their Wikidata equivalent is performed.
  * a list with a nested list that contains the indices of the entity mention tokens in the sentence
* "t": information on the tail entity in a list with the same structure as "h"
* "ner": a list with information obtained from the task of named entity recognition (NER). The list contains the BIOES entity type tag for each token in the sentence. The BIOES tagging has been created using the German NER model in [Stanza](https://github.com/stanfordnlp/stanza) with the CoNLL 2003 tag set. This tag set contains the entity types PER (person), ORG (organisation) and LOC (location) (cf. https://stanfordnlp.github.io/stanza/available_models.html#available-ner-models).

Consider the following made-up example:
```json
{
  "tokens": ["Robin", "Hood", "lebt", "in", "Sherwood", "Forest", "."],
  "h": ["sherwood forest", "", [[4, 5]]],
  "t": ["robin hood", "", [[0, 1]]],
  "ner": ["B-PER", "E-PER", "O", "O", "B-PER", "E-PER", "O"]
}
```

## License
10kGNAD is licensed under a [Creative Commons BY-NC-SA 4.0 license](https://creativecommons.org/licenses/by-nc-sa/4.0/).
Therefore, WissenschaftsSTANDARD is also released under the [Creative Commons BY-NC-SA 4.0 license](https://creativecommons.org/licenses/by-nc-sa/4.0/).
