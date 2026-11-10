# CODION: Cognitive Operations, Disinformation and Influence Ontology

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.24103509.svg)](https://doi.org/10.5281/zenodo.24103509)

CODION is an OWL 2 ontology for knowledge-graph representation of disinformation campaigns, influence operations and cognitive warfare. It connects content, actors, targets, operations, consequences, countermeasures and evidence in one model, and aligns with DISARM, FIMI, STIX 2.1, MITRE ATT&CK, ABCDE, ENISA, AMAS, RESIST and ETSI TR 104 159.

CODION separates persistent domain entities from contextual relations and from analytical or evidentiary constructs. Relationships that carry role, confidence, time or evidence are modelled as qualified relations (`ActorParticipation`, `ActorRelationship`, `TargetingRelation`, `Assertion` and its specialisations), so that attribution, targeting and effect can be represented as contested or probabilistic claims rather than unconditional facts.

## Files

| File | Content |
|---|---|
| `CODION-v1.0.ttl` | The ontology: OWL 2 in RDF Turtle, self-contained (no `owl:imports`). |
| `CODION-v1.0-competency-queries.rq` | Six SPARQL competency queries, as described in the accompanying publication. |
| `CODION-v1.0-test-graph.ttl` | A small fictitious population that exercises the six queries, with the expected result for each. |

## Namespaces

| Prefix | Namespace | Content |
|---|---|---|
| `codion:` | `https://ontology.cogops.eu/codion#` | CODION classes and properties |
| `disarm:` | `https://ontology.cogops.eu/codion/disarm#` | DISARM v1.6 alignment |

Ontology IRI: `https://ontology.cogops.eu/codion` · Version IRI: `https://ontology.cogops.eu/codion/1.0.0`

## Structure

CODION is organised in five modules. Every top-level class records its module through the annotation `codion:belongsToModule`.

| Module | Content |
|---|---|
| A. Information and Meaning | ContentItem, Claim, Narrative, Topic, Channel |
| B. Actors and Targeting | Actor (nine intrinsic classes), Account, OperationalAsset, ActorParticipation, ActorRelationship, TargetingRelation, AudienceSegment |
| C. Operations | Campaign, Incident, Activity, Objective, Motivation, ManipulationTechnique, Infrastructure |
| D. Consequences and Response | Effect (ImmediateEffect, Outcome, Impact, Harm), Vulnerability, Countermeasure, DetectionEvent |
| E. Evidence, Assessment and Context | Assertion and its specialisations, Evidence, Event, Location, AffectiveProfile, SemanticCluster, SimilarityRelation |

| Element | Count |
|---|---|
| Classes | 187 |
| Datatype properties | 472 |
| Object properties | 252 |
| Annotation properties | 11 |
| DISARM phases, tactics, techniques, sub-techniques, countermeasures | 4, 16, 76, 12, 10 |

The DISARM individuals are a representative subset of DISARM v1.6, which defines 103 techniques, 288 sub-techniques and 140 countermeasures.

## Using CODION

Open `CODION-v1.0.ttl` in an ontology editor such as Protégé, or load it with any RDF library. The example below uses Python and rdflib to load the ontology and the test graph, and runs the six competency queries:

```python
import re
import rdflib

g = rdflib.Graph()
g.parse("CODION-v1.0.ttl", format="turtle")
g.parse("CODION-v1.0-test-graph.ttl", format="turtle")

queries = re.split(r"^#### ", open("CODION-v1.0-competency-queries.rq").read(), flags=re.M)[1:]
for q in queries:
    title, body = q.split("\n", 1)
    print(title, "->", len(list(g.query(body))), "row(s)")
```

Expected result: 1, 2, 1, 1, 1 and 6 rows. Without an OWL reasoner, the symmetric property `codion:coordinatedWith` matches only in the asserted direction; with a reasoner, the first query returns each pair in both directions.

## Citation

The accompanying article, "CODION: An OWL Ontology for Knowledge-Graph Representation of Disinformation Campaigns and Cognitive Warfare" by T. Tagarev and G. Sharkov, is under review. Until it is published, please cite this release:

Tagarev, T.; Sharkov, G. *CODION: Cognitive Operations, Disinformation and Influence Ontology*, version 1.0.0. Zenodo, 2026. https://doi.org/10.5281/zenodo.24103509

See also `CITATION.cff`.

## Earlier name

CODION was first released under the name CODO (https://doi.org/10.5281/zenodo.24086889). Before publication it was renamed, to avoid confusion with an unrelated COVID-19 ontology of the same name. The content is identical; only the name and the identifiers changed.

## Licence

CODION is licensed under [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/). You may share and adapt it for any purpose, provided you give appropriate credit.

## Authors

Todor Tagarev and George Sharkov.
