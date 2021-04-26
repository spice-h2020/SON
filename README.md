# SPICE Ontology Network

This repository contains the source code of the SPICE Ontology Network.


## Ontology Modules

Each directory contains an ontology module.
The name of the directory must correspond to the ID part of the  ontology IRI.
Therefore, the ontology IRI must comply with the following rule:

```
https://w3id.org/spice/SON/[Name of the folder]
```

Please use camel case for folder names.

The prefix of the ontology must be ``https://w3id.org/spice/SON/[Name of the folder]/`` (i.e. the IRI of the ontology followed by ``/``).

The file containing the ontology must be serialized in RDF/XML format and named ``ontology.owl``.

### Versioning

The SPICE ontology network is versioned, therefore the ontology modules must comply with the following rules.

1. Each ontology module *must declare* a version IRI and a prior version.

2. The version IRI *must comply* with the following rule:

```
https://w3id.org/spice/SON/[Name of the folder]/[version ID]
```
where ``version ID`` is the identifier of the version under development (currently the ``0.0.1``).

3. Each ontology module *must import* the ontologies with the same version ID.

4. Version ID should follow [Semantic Versioning 2.0.0 Policy](https://semver.org/).

Releases will be taggeed with version IDs.
*Latest* release points to the latest *stable release* (it will not be updated at every ontology release).

## Ontology network backbone

The SPICE Ontology network uses [DOLCE+DnS Ultralite](http://www.ontologydesignpatterns.org/ont/dul/DUL.owl) and [D0](http://www.ontologydesignpatterns.org/ont/dul/d0.owl) as foundational backbone.


## Knowledge Areas Overview

TODO: Create SON entry point

### Brand new ontologies

This is a list of the brand new ontologies developed for the SPICE project:

Scripting
- [Curatorial Context](https://w3id.org/spice/SON/curatorialContext) ``https://w3id.org/spice/SON/curatorialContext``
- [Fruition context](https://w3id.org/spice/SON/fruitionContext) ``https://w3id.org/spice/SON/fruitionContext``
- [Scripting manifest](https://w3id.org/spice/SON/scripting) ``https://w3id.org/spice/SON/scripting``
- [Affordance](https://w3id.org/spice/SON/affordance) ``https://w3id.org/spice/SON/affordance``

Emotion
- [Emotion](https://w3id.org/spice/SON/emotion) ``https://w3id.org/spice/SON/emotion``
- [Emotion in cultural context](https://w3id.org/spice/SON/emotionInCulturalContext) ``https://w3id.org/spice/SON/emotionInCulturalContext``
- [Ekman emotions](https://w3id.org/spice/SON/ekmanEmotions) ``https://w3id.org/spice/SON/ekmanEmotions``
- [Plutchik emotion](https://w3id.org/spice/SON/PlutchikEmotion) ``https://w3id.org/spice/SON/PlutchikEmotion``
- [OCC emotion](https://w3id.org/spice/SON/OCCEmotion) ``https://w3id.org/spice/SON/OCCEmotion``

### Existing ontologies re-used 

The SPICE ontology network doesn't want to reinvent the wheel.
Lots of [awesome ontologies](Awesome_ontologies.md) are avaible at the state-of-the-art.
SON relies and possibly extends these ontologies. 
Here, we provide a list of ontologies reused or recommended for the SPICE project together with a link to the issue where the need of the ontology emerged.
The issue discusses the requirement that motivates the use of the ontology and provides an example of use.

Linguistic data

- [semiotics](http://ontologydesignpatterns.org/cp/owl/semiotics.owl#) (cf. [#30](https://github.com/spice-h2020/SON/issues/30))
- [Earmark](http://www.essepuntato.it/2008/12/earmark#) (cf. [#30](https://github.com/spice-h2020/SON/issues/30)) 
- [POS](http://www.ontologydesignpatterns.org/ont/fred/pos.owl#) (cf. [#30](https://github.com/spice-h2020/SON/issues/30))

Artwork-related data

- [ArCo ontology network](https://w3id.org/arco/ontology/arco) (cf. [#31](https://github.com/spice-h2020/SON/issues/31))
- [CulturalON](http://dati.beniculturali.it/cis/) (cf. [#31](https://github.com/spice-h2020/SON/issues/31))
- [Getty vocabularies](http://vocab.getty.edu/) (cf. [#31](https://github.com/spice-h2020/SON/issues/31))
- [Building Topology Ontology (BOT)](https://w3id.org/bot#) (cf. [#31](https://github.com/spice-h2020/SON/issues/31)) (for describing the structure of the museums or the exhibitions)

### Testing protocol

SON Ontologies are continuosly tested. The testing protocol is described  [here](TESTING).

## How to contribute

You can contribute to the SPICE Ontology Network either by defining a new scenario (that can be submitted as [issues](https://github.com/spice-h2020/SON/issues/new/choose)) or  proposing an extension of the ontology.


## Contributors and Roles

- Luigi Asprino (UNIBO) - Maintainer
- Rossana Damiano (UNITO)
- Marilena Daquino (UNIBO)
- Stefano De Giorgis (UNIBO)
- Aldo Gangemi (CNR-UNIBO)
- Antonio Lieto (UNITO)
- Bruno Sartini (UNIBO)


## License

The content of this repository is distributed under [CC-BY 4.0](https://creativecommons.org/licenses/by/4.0/) license.
