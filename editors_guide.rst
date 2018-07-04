Editors Guide
=============

.. caution::
   **UNDER CONSTRUCTION**
   This document is undergoing heavy edits right now ... you may want to come back in a few days!

   
If you're not sure how to do something please ask edam@elixir-dk.org.  You'll need to `subscribe <http://elixirmail.cbs.dtu.dk/mailman/listinfo/edam>`_ to the list first.


General considerations
----------------------

Terminology
^^^^^^^^^^^
We use the following terms when talking about EDAM:

- *EDAM* refers to the ontology in totality (all subontologies).
- *Subontology* and occasionally *branch* refers to an EDAM subontology, *i.e.* **Topic**, **Operation**, **Data** or **Format**.  Also **Data->Identifier** (a branch of **Data**).
- *Concept* is the basic unit of information in EDAM: including concept definition, terms and other metadata 
- *Primary term*, *Primary label* or simply *Label* is the primary term by which the concept is referred to.  They're used for annotation purposes.
- *Synonym* means an exact, narrow, broad or related synonym (see `todo <https://todo>`_).  They can also be used for annotation.
- *Term* and *terms* refer to primary labels and synonyms collectively.
- *Hierarchy* refers to the EDAM tree structure, resulting from EDAM concepts being defined as specialisations/generalisations of one another (PS. EDAM isn't a tree, it's a `DAG <https://en.wikipedia.org/wiki/Directed_acyclic_graph>`_.)
- *Root* refers to the top-most concept in a subontology, *i.e.* `Topic <http://edamontology.org/topic_0003>`_, `Operation <http://edamontology.org/operation_0004>`_, `Data <http://edamontology.org/data_0006>`_, and `Format <http://edamontology.org/format_1915>`_.  And (depending on context) `Identifier <http://edamontology.org/data_0842>`_.
- *Tier* refers to a particular level in the hierarchy, excluding the subontology root, *e.g.* "Tier 1 data concepts" means everything immediately under `Data <http://edamontology.org/data_0006>`_.
- *Top level* and *Top tier* refers to Tier 1 concepts.
- *Child*, *Children of*, *Kids* *etc.* refers to concept(s) defined as an immediate specialisation of another (*i.e.* "is_a", or the OWL geek "subClass").  Conversely *Parent* means the opposite (a generalisation of a concept).
- *Ancestor* means *Parent* or the parent's parent *etc.* Conversely *Descendant* means *Child* or the children's children *etc.*
- *related to* means a concept in one subontology is formally defined as related (in various ways) to a concept in another, but excluding basic specialisation/generalisation relationships.
- *Node* refers to a concept when it's being discussed in context of the hierachy.
- *Leaf* refers to a concept at the bottom of the tree (without children).


For a technical definition of these things, see `todo <http://todo>`_.

   
Rules of thumb for EDAM development 
-----------------------------------
These rules of thumb are to guide the technical and scientific development of EDAM, to help ensure structural and conceptual simplicity and that EDAM is fit for purpose and will scale to annotate athe growing bio.tools.
Before proposing or making any major changes, make sure you understand the `principles <http://edamontologydocs.readthedocs.io/en/latest/what_is_edam.html#principles>`_ on which EDAM is based.

.. note::

   The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in `RFC 2119 <http://www.ietf.org/rfc/rfc2119.txt>`_:

   - **"MUST"**, **"REQUIRED"** or **"SHALL"** mean that the guideline is an absolute requirement of the specification.
   - **"MUST NOT"** or **"SHALL NOT"** mean that the guideline is an absolute prohibition of the specification.
   - **"SHOULD"** or **"RECOMMENDED"** mean that there may exist valid reasons in particular circumstances to ignore a particular guideline, but the full implications must be understood and carefully weighed before doing so.
   - **"SHOULD NOT"** or the phrase **"NOT RECOMMENDED"** mean that there may exist valid reasons in particular circumstances when acting contrary to the geuideline is acceptable or even useful, but the full implications should be understood and the case carefully weighed before doing so.
   - **"MAY** or **"OPTIONAL"** mean that the guideline is truly optional; you can choose to follow it or not.

General
^^^^^^^

Concepts & Terms
................
Concepts:

- **MUST NOT** overlap conceptually, to a significant extent, with each other. The exception is **Topic** ontology where most concepts are overlapping.

*Primary term and synonyms:*

- **MUST** be a short name or phrase in common use
- **MUST** be unique within a sub-ontology
- **SHOULD** be unique across all sub-ontologies (rare exceptions are allowed)

*Primary term:*

- **MUST** reflect the vernacular, *i.e.* the term that's most commonly used when referring to the concept; you **SHOULD** use google (number of hits) to help you choose, where necessary
- **MUST** use Britsh spelling
- **MUST** not include buzzwords and marketting-spiel *e.g.* "Big data", "NGS" *etc.* 

*Synonyms:*

- **SHOULD** use Britsh spelling
- **MAY** capture spelling variations, including American spellings, case and hyphenation variants *etc* (as exact synonyms)
- **MAY** include buzzwords if really prevalent and relevant
- **MUST NOT** overlap conceptually, to a significant extent, with an already existing concept; be especially mindful of ancestors and descendants of the concept for which a synonym is defined.

*Definitions and comments:*

- definition **MUST** be a concise and lucid description of the concept, without acronyms, and avoiding jargon.  Peripheral but important information **MAY** be added as a comment.
- **SHOULD** use Britsh spelling

*When adding a new concept, in addition to above:*

- **MUST** specify all mandatory attributes and **SHOULD** specify all optional ones (see `todo <>`_)
- **SHOULD** provide all common *exact synonyms* of the primary term
- **MAY** provide any number of *narrow synonyms* (but be wary of conceptual overal with child concepts). The exception is **Format** subontology where **MUST NOT** include any narrow synonyms at all.
- **SHOULD NOT** provide any *broad synonyms* unless these are really needed (but be wary of conceptual overal with parent concepts)

  


Hierarchy
.........
- each subontology must not descend beyond a certain depth (see below).  Specifically, this means that each concept **MUST** have at least one path to root (*i.e.* to `Topic <http://edamontology.org/topic_0003>`_, `Operation <http://edamontology.org/operation_0004>`_, `Data <http://edamontology.org/data_0006>`_, or `Format <http://edamontology.org/format_1915>`_) no deeper than indicated.   It's OK for a concept to have other paths to root that are deeper than this.
  
  - **Topic:** 3 levels deep max. *i.e.* *Topic* (root) -> Topic -> Subtopic -> Subsubtopic (leaves)
  - **Operation:** 6 levels deep max. 
  - **Data:** 4 levels deep max. 
  - **Format:** 3 levels deep max. 

When adding a new concept

- if the addition introduces a new level of depth, you **MUST** be sure it's realistic to also add and maintain, in due course, all relevant siblings (*i.e.* related concepts with the same parent).  This is to ensure EDAM coverage does not get patchy.
- **SHOULD NOT** introduce any "single childs" (concepts without siblings) unless you already know of potential sublings (to add in due course), or think it's likely such sibling concepts will appear in the future
- you **MUST NOT** add a concept if additional new concepts are also needed (above point) and this extension in total, would seriously overlap with an existing, well-developed ontology that already serves the area better.  If in doubt you **MUST** discuss this with the `EDAM developers <mailto:edam-dev@elixir-dk.org>`_.
- **SHOULD NOT** define multiple parents of a concept unless there is a very unambivalent case. This rule is even stronger for **Topics** (where most overlap with each other).
6. If you add a concept which you expect to remain a leaf node, *i.e.* EDAM will not include finer-grained concepts, then - if other well-developed ontologies exist that serve this conceptual niche - you **SHOULD** annotate this junction (see `todo <>`_).

Deprecations
............
EDAM must always evolve, which means additions, edits, and occasionally *deprecations*: marking-up concepts as not recommended for use: there are special `deprecation guidelines <todo>`_ for this.


Subontology-specific
^^^^^^^^^^^^^^^^^^^^

Topic
.....

.. note::
   EDAM **Topic** concepts are conceptually very broad.  There will only ever include a few hundred concepts in total, semantic richness is captured through synonyms (which are unlimited in number). This ensures sustainability and practical applications.  In contrast see *e.g.* `MeSH <https://www.nlm.nih.gov/bsd/disted/meshtutorial/introduction/>`_.
    
- Topics usually have a corresponding page in `Wikipedia <https://en.wikipedia.org/wiki/Main_Page>`_ and a link to this **MUST** be provided, if one exists.  Exceptions are OK, but if a Wikipedia page does not exist, one **MUST** consider carefully whether the concept is too fine-grained.
- **MUST** respect the scope, specifically:
   
   - **MUST NOT** include fine-grained operations or types of data.  As a rare exception, very high-level operations *e.g.* *Sequence analysis* **MAY** be included.
   - **MUST NOT** include any concept tied to a concrete project or product.
   - **SHOULD NOT** include anything that is more tangible than a very general topic, *e.g.* specific cell types, diseases, biological processes, environment types *etc*.  Such fine-grained concepts belong in their own ontology, but **MAY** be captured, where desirable, as synonyms in EDAM.  Rare exceptions are allowed where a term really is in extremely prevalent usage (pragmatism rules!)
   
- **MUST NOT** conflate terms in a concept label where these terms exist as independent topics already, *e.g.* *Disease pathways* is disallowed because there are already concepts for *Disease* (synonym of *Pathology*) and *Pathways* (synonym of *Molecular interactions, pathways and networks*).  Instead, if such conflations are required, they **MAY** be added as synonyms of one concept or the other.
- **MUST NOT** define multiple parents of the concept, with the exception of the strongest cases only, where it would be incongruous not to do so *e.g.* *Biochemistry* is a child of both *Biology* and *Chemistry*.
- Links to Wikipedia are desirable everywhere there is a relevant page, but especially for EDAM **Topics**, where one or more pages may be linked to, depending on the primary term and synonyms. In a future refactoring, we may distinguish these cases.    


   
Operation
.........
.. note::
   Concrete **Operation** concepts range from conceptually quite broad to quite narrow.  There will be as many as required to capture the *essential functions* of current bioinformatics software tools.  Note *essential*: the Operation subontology will not descend to a level of conceptual granularity that is impractical from a maintenance or usage perspective.
   
- Concepts **MUST** conceptually be clearly distinct from other (non-placeholder) Operations, and this **MUST** be reflected in the label and definition of the concept.
- Concepts **SHOULD** should never be more fine-grained than is useful for practical search purposes, and **SHOULD NOT** include fine-grained specialisations of a basic function, individiaul algorithms etc. (a few exceptions are allowed for very highly prevalent concepts)
- The definition **MUST** state *what* is done but not *how*.
- Pick the single, most relevant operation. In some (exceptional) cases, a broad operation type (top-level operation) *e.g.* "Comparison", "Calculation" *etc.* (see http://edamontology.org/operation_0004) may also be specified.
   
Data
....
.. note::
   Concreate **Data** concepts range from conceptually quite broad to quite narrow.  There will be as many as required to capture the *basic types* of bioinformatsics data.  The Data subontology does (and will) not reflect individual data structures, and like **Operation** will maintain a level of conceptual granularity that is remain maintable and usable.
   
- Placholder concepts **MUST** be annotated with ``<usageGuideline>Not recommended for annotation in bio.tools.</usageGuideline>``.
- **SHOULD NOT** contain any chains of placeholder concepts, *i.e.* placholders are normally allowed (with a few rare exceptions) in the first tier.
- **MUST NOT** define multiple parents of the concept.
   
   
Data->Identifier
................
.. note::
   Concrete **Identifier** concepts are very specific.  There will be as many as required to capture the unique types of identifiers in use.  Uniqueness means that a regular expression pattern can, in principle, meaningfully be created describing the identifier instance snytax.
   
- A new identifier (or it's ancestor) **MUST** be annotated (via *is_identifier_of*) to indicate the type of data that is identified but you **MUST NOT** duplicate this annotation if it's already stated on an ancestor concept.
- Definition **MUST** state what type of data and/or name of database the identifier is used for.
- Identifier concepts normally have two parents: 1) either "Accession" (http://edamontology.org/data_2091) or "Name" (http://edamontology.org/data_2099) and 2) indicating the type of identifier *e.g.* "Sequence accession (protein)", *i.e.* a concept descended from "Identifier (typed)" (http://edamontology.org/data_0976).  In exceptional cases (where an identifier is re-used for data objects of fundamentally different types, typically served from a single database) the parent of "Identifier (hybrid)" (http://edamontology.org/data_2109) may also be given.
- **SHOULD** include a link to relevant documentation for the identifier.
- **MUST** specify the EDAM Data concept(s) for the type(s) of data identified by the identifier.  If you are not sure, or if you can't find the Data concept you need, you can use free text *e.g.* "Protein sequence" instead of the URI.
-.   A regular expression pattern, defining valid values of instances of that identifier **SHOULD** be defined.(``Regular expression``) : 

Format
......

.. note::
   Concrete **Format** concepts are very specific.  There will be as many as required to capture all of the data formats currently in use.  By *data format" we mean a syntax for which a rigorous, comprehensive description is provided, typically either an XML Schema (XSD) or comprehensive textual specification.
   
- Leaf nodes **MUST** be concrete data formats, see `to-do <>`_ and `to-do <>`_).
- Concrete data formats **MUST** descend from *Textual format*, *Binary format*, *XML*, *HTML*, *JSON*, *RDF format* or *YAML*, but you **MUST NOT** duplicate this ancestry in format variants.  For example *FASTA-like (text)* is defined as a child of *Textual format*, but the kids of *FASTA-like (text)* format are not.
- Concrete data formats **MUST** descended from `Format (by type of data) <http://edamontology.org/format_2350>`_ (or it's kids), but again, you **MUST NOT** duplicate this ancestry in format variants.  For example *FASTA-like (text)* is defined as a child of *Sequence record format* -> *FASTA-like*, but the kids of *FASTA-like (text)* format are not.
- **MUST NOT** add new placeholder concepts (kids of `Format (by type of data) <http://edamontology.org/format_2350>`_) unless there is a corresponding concrete data format descending from it.
- Where file extensions are in common use, all of these **SHOULD** be annotated and you **MUST** preserve the common capitalisation and **MUST NOT** include period ('.') in the annotation, *e.g.* "txt" not ".txt".
- A new format (or it's ancestor) **MUST** be annotated (via *is_format_of*) to indicate the type of data that is formatted but you **MUST NOT** duplicate this annotation if it's already stated on an ancestor concept. 
- **SHOULD** annotate the `media type <https://www.iana.org/assignments/media-types/media-types.xhtml>`_ (MIME type) if available, seee `todo <>`_.
- **MUST** annotate the specification or documentation of concrete data formats (see `todo <>`_)
- The definition **SHOULD** describe the type of data the format is used for.
- **MUST NOT** include any narrow synonyms; if you think specialisations are needed then these can be covered by adding new concepts.
- Definition **MUST** mention state what type of data the format is used for.
- Formats are generally only listed if they are in common use, for example by public databases or multiple tools.
- Concept statements may include a reference (typically a URL) to the format specification proper.
   
   
.. note::
   The 3-level depth of **Format** depth is achieved:

   *Format* (root) -> (*Textual format* | *Binary format* | *XML* | *HTML* | *JSON* | *RDF format* | *YAML*) -> Format (leaves)

   See `to-do <>`_ below.
    





