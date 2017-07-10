What is EDAM?
=============

EDAM is a simple ontology of well established, familiar concepts that are prevalent within bioinformatics, including types of data and data identifiers, data formats, operations and topics. EDAM provides a set of terms with synonyms and definitions, organised into an intuitive hierarchy for convenient use.


Browsing
--------
You can browse EDAM here:

- `NCBO BioPortal <http://bioportal.bioontology.org/ontologies/EDAM/>`_
- `OLS <http://www.ebi.ac.uk/ols/ontologies/edam>`_
- `AberOWL Repository <http://aber-owl.net/ontology/EDAM>`_
- `RAINBio browser <https://biosphere.france-bioinformatique.fr/edamontology/browser/>`_

Download
--------
Latest stable version

- http://edamontology.org/EDAM.owl

Versioned releases:

- https://github.com/edamontology/edamontology/releases

OBO format is no longer supported.

Scope
-----
EDAM includes 4 main sub-ontologies or 'branches' of concepts:

- **Data** - *“Information, represented in an information artefact (data record) that is 'understandable' by dedicated computational tools that can use the data as input or produce it as output.”*
- **Format** - *“A defined way or layout of representing and structuring data in a computer file, blob, string, message, or elsewhere.”*
- **Operation** - *“A function that processes a set of inputs and results in a set of outputs, or associates arguments (inputs) with values (outputs).”*
- **Topic** - *“A category denoting a rather broad domain or field of interest, of study, application, work, data, or technology. Topics have no clearly defined borders between each other.”*

- **Data->Identifier** - *“A text token, number or something else which identifies an entity, but which may not be persistent (stable) or unique (the same identifier may identify multiple things).”*

.. image:: http://edamontology.org/EDAMconcepts.png 

As a general rule, the **Data**, **Format** and **Operation** branches include concepts strictly in domain of bioinformatics and computational biology: concepts purely concerning biology, computer science *etc.* are not included. The **Topic** branch, in contrast, includes broader interdisciplinary concepts from the biological and biomedical domains.


Architecture
------------
EDAM has 3 components:

- **Concepts** - All concepts have a preferred label (or 'term') and definition. Further, a concept may have simple relations (see below) to other EDAM concepts, as well other intrinsic properties, *e.g.* an identifier may have a regular expression defining its syntax.
- **Hierarchy** - Every concept (excluding top-level concepts) is related to one or more other concepts within the same branch by an **is a** (specialisation) relation. Hence EDAM has 4 primary hierarchies (for *Data*, *Format*, *Operation*, and *Topic*).
- **Relations** - Concepts are related by defined relation types (see figure below), which reflect well established or self-evident principles, and are used primarily to define internal consistency of EDAM.

.. image:: http://edamontology.org/EDAMrelations.png


Status
------
EDAM is a maturing ontology under active development.  Development is use-case driven, primarily by the ELIXIR Tools & Data Services Registry (`bio.tools <https://bio.tools>`_).  Future versions will not depart fundamentally from the current sub-ontologies or relations.  The development of EDAM can be followed at `GitHub <https://github.com/edamontology/edamontology>`_.

For ways to contribute, please see the `Contributors Guide <http://edamontology.readthedocs.org/en/latest/contributors_guide.html>`_. 

Priorities
----------

Our core priority is to be responsive to users of EDAM. Furthermore, to establish a more sustainable footing for essential EDAM maintenance and developments, including:

- Content review and refactoring to ensure structural and semantic simplicity ensuring high usability
- Community build-up and development including more formal, but agile, governance and maintenance models and mechanisms
- Agile and responsive development of content in close collaboration with end-users and serving concrete use-cases
- Technical refactoring to minimise the cost of routine housekeeping and content development 
- Implementation of tooling for routine maintenance to serve the needs of end-users, *e.g.* harvesting change requests and mappings between concepts


Principles
----------

EDAM strives to uphold a few founding principles including:

- **Quality** - a controlled vocabulary that is moderated
- **Openness** - development in collaboration with the community
- **Relevance** - prioritising use-case-driven development towards comprehensive but practical coverage
- **Practicality** - practical utility is valued over ontological “strictness” or any metaphysical doctrine
- **Clear scope** - respecting the scope of other complementary, well-developed ontologies
- **Familiarity** - including only concepts that are well established; familiar are prevalent and jargon is discouraged
- **Usability** - conceptual hierarchy with sufficient richness but only necessary complexity
- **Maintainability** - development must be efficient and sustainably up to date in the long term

EDAM is working towards implementing these principles fully and is open to suggestions.


Motivation
----------
Bioinformaticians handle an increasingly large and diverse set of tools and data. Meanwhile, researchers demand ever more powerful and convenient means to organise, find, understand, compare, select, use and connect the available resources. These tasks often rely on consistent, machine-understandable descriptions of the underlying components, but these have been generally lacking in *ad hoc* resource descriptions. The urgent need - filled by EDAM - is for an ontology that unifies semantically the bioinformatics concepts in common use, provides the curator with a comprehensive controlled vocabulary that is broadly applicable, and supports new and powerful search, browse and query functions.

Applications 
------------
EDAM is suitable for large-scale semantic annotations and categorization of diverse bioinformatics resources, including:

- Web services including REST and SOAP APIs
- Application software
- Tool collections and packages
- Workflows / pipelines
- Databases
- XML Schemata and data objects
- Data syntax and file formats
- Web portals and pages
- Resource catalogues
- Training materials 
- Courses, tutorials, and other events
- Areas of scientific interest
- Documents, such as scientific publications

EDAM is also suitable for diverse application including for example within workbenches and workflow-management systems, software distributions, and resource registries.

Citing EDAM
-----------
If you use EDAM or its part, please cite:

Ison, J., Kalaš, M., Jonassen, I., Bolser, D., Uludag, M., McWilliam, H., Malone, J., Lopez, R., Pettifer, S. and Rice, P. (2013). EDAM: an ontology of bioinformatics operations, types of data and identifiers, topics and formats. *Bioinformatics*, **29** (10): 1325-1332.

The article is `freely available <http://bioinformatics.oxfordjournals.org/content/29/10/1325.full>`_.

doi: `10.1093/bioinformatics/btt113 <http://doi.org/10.1093/bioinformatics/btt113>`_ 
 
PMID: `23479348 <http://www.ncbi.nlm.nih.gov/pubmed/23479348>`_

