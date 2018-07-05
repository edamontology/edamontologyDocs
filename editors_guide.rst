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
These rules of thumb are to guide the technical and scientific development of EDAM, to help ensure structural and conceptual simplicity and that EDAM is fit for purpose and will scale to annotate athe growing bio.tools.  Before proposing or making any major changes, make sure you understand the `principles <http://edamontologydocs.readthedocs.io/en/latest/what_is_edam.html#principles>`_ on which EDAM is based.

.. note::

   The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in `RFC 2119 <http://www.ietf.org/rfc/rfc2119.txt>`_:

   - **"MUST"**, **"REQUIRED"** or **"SHALL"** mean that the guideline is an absolute requirement of the specification.
   - **"MUST NOT"** or **"SHALL NOT"** mean that the guideline is an absolute prohibition of the specification.
   - **"SHOULD"** or **"RECOMMENDED"** mean that there may exist valid reasons in particular circumstances to ignore a particular guideline, but the full implications must be understood and carefully weighed before doing so.
   - **"SHOULD NOT"** or the phrase **"NOT RECOMMENDED"** mean that there may exist valid reasons in particular circumstances when acting contrary to the geuideline is acceptable or even useful, but the full implications should be understood and the case carefully weighed before doing so.
   - **"MAY** or **"OPTIONAL"** mean that the guideline is truly optional; you can choose to follow it or not.

.. important::
   If you are editing the EDAM.owl file directly (in a text editor or Protege) there are a number of additional things you need to do when, which are not described in these guidelines, including:
   - specification of concepts as "placeholder" or "concrete" (see `Concept types <http://edamontologydocs.readthedocs.io/en/latest/technical_details.html#concept-types>`_)
   - assignment of concepts to subsets (see `todo <>`_)
   - other technical housekeeping
   
   For further information see `todo <>`_.

     
General
^^^^^^^

Concepts & Terms
................
*Concepts:*

- **MUST** be conceptually clearly distinct from one another. The exception is **Topic** ontology where most concepts are overlapping.
- **MUST** be genuine specialisms, wherever a concept is defined as the child of another.

*Primary term and synonyms:*

- **MUST** be a short name or phrase in common use
- **MUST** be unique within a sub-ontology
- **SHOULD** be unique across all sub-ontologies (rare exceptions are allowed)

*Primary term:*

- **MUST** reflect the vernacular, *i.e.* the term that's most commonly used when referring to the concept; you **SHOULD** use google (number of hits) to help you choose, where necessary
- **MUST** use Britsh spelling
- **MUST** not include buzzwords and marketting-spiel *e.g.* "Big data", "NGS" *etc.* 

*Synonyms:*

- **MUST NOT** overlap conceptually, to a significant extent, with an already existing concept; be especially mindful of ancestors and descendants of the concept for which a synonym is defined.
- **SHOULD** use Britsh spelling
- **MAY** capture spelling variations, including American spellings, case and hyphenation variants *etc* (as exact synonyms)
- **MAY** include buzzwords if really prevalent and relevant

*Definitions and comments:*

- **SHOULD** use Britsh spelling

*Definitions:*

- **MUST** be a concise and lucid description of the concept, without acronyms, and avoiding jargon.
- **MUST** reflect the primary term.

*Comments:*

- **MAY** include peripheral but important information not captured by the definition.
- **MAY** reflect narrow and broad synonyms of the primary term.
  
*When adding a new concept, in addition to above:*

- **SHOULD** provide all common *exact synonyms* of the primary term
- **MAY** provide any number of *narrow synonyms* (but be wary of conceptual overal with child concepts). The exception is **Format** subontology which **MUST NOT** include any narrow synonyms at all.
- **SHOULD NOT** provide any *broad synonyms* unless these are really needed (but be wary of conceptual overal with parent concepts)



.. note::
   EDAM must always evolve, which means additions, edits, and occasionally *deprecations*: marking-up concepts as not recommended for use: the EDAM developers follow special `deprecation guidelines <todo>`_ for this.

Hierarchy
.........

.. important::
   EDAM has the notion of *placeholder* and *concrete* concepts (see `todo <>`_):
   
   - *placeholders* are intended primarily to organise the EDAM tree
   - *concrete* concepts are intended primarily for annotation purposes.

   There are rules for how many *placeholders* and *concrete* concepts can be chained togther (via *is_a*) relationships, and thus, the maximum depths of the subontology hierarchies (see `todo <http://edamontologydocs.readthedocs.io/en/latest/technical_details.html#hierarchy-depth>`_).
   In practice, as an Editor, you should be aware of the general structure of EDAM and the conceptual granularity in each subontology.  If in doubt, mail the `EDAM developers <mailto:edam-dev@elixir-dk.org>`_ for advice.


When adding a new concept:

- if the addition introduces a new level of depth, you **MUST** be sure it's realistic to also add and maintain, in due course, all relevant siblings (*i.e.* related concepts with the same parent).  This is to ensure EDAM coverage does not get patchy.
- **SHOULD NOT** introduce any "single childs" (concepts without siblings) unless you already know of potential sublings (to add in due course), or think it's likely such sibling concepts will appear in the future
- **SHOULD NOT** add (or imply the addition, as per above) multiple concepts if this would mean a big overlap with an existing, well-developed ontology.  If in doubt, discuss this first with the `EDAM developers <mailto:edam-dev@elixir-dk.org>`_.
- **SHOULD NOT** define multiple parents of a concept (except where indicated `below <>`_) unless there is a very unambivalent case. This rule is even stronger for **Topics** (many topics overlap with each other, but as a rule you must pick one parent only)

Subontology-specific
^^^^^^^^^^^^^^^^^^^^

Topic
.....

.. note::
   EDAM **topics** are conceptually very broad (see `todo <>`_).  There will only ever include a few hundred concepts in total, semantic richness is captured through synonyms (which are unlimited in number). This ensures sustainability and practical applications.  In contrast see *e.g.* `MeSH <https://www.nlm.nih.gov/bsd/disted/meshtutorial/introduction/>`_.
    
 
- Respect the `scope <todo>`_, specifically:
   
   - **MUST NOT** include fine-grained operations or types of data.  As a rare exception, very high-level operations *e.g.* *Sequence analysis* **MAY** be included.
   - **MUST NOT** include any topic tied to a concrete project or product.
   - **SHOULD NOT** include anything that is more tangible than a very general topic, *e.g.* specific cell types, diseases, biological processes, environment types *etc*.  Such fine-grained concepts belong in their own ontology, but **MAY** be captured, where desirable, as synonyms in EDAM.  Rare exceptions are allowed where a term really is in extremely prevalent usage (pragmatism rules!)

- **MUST NOT** define multiple parents of a topic, with the exception of the strongest cases only, where it would be incongruous not to do so *e.g.* *Biochemistry* is a child of both *Biology* and *Chemistry*.
- **MUST NOT** conflate terms in a concept label where these terms exist as independent topics already, *e.g.* *Disease pathways* is disallowed because there are already concepts for *Disease* (synonym of *Pathology*) and *Pathways* (synonym of *Molecular interactions, pathways and networks*).  Instead, if such conflations are required, they **MAY** be added as synonyms of one concept or the other.  
- **SHOULD** provide a link to `Wikipedia <https://en.wikipedia.org/wiki/Main_Page>`_ if a relevant page exists.  Most EDAM topics are sufficiently broad to already have Wikipedia pages.  Exceptions are OK, but if a Wikipedia page does not exist, consider carefully whether the concept is too fine-grained.
     
.. note::
  Links to Wikipedia are desirable, for the primary term but also synonyms. In a future refactoring, EDAM may distinguish such cases.    
   
Operation
.........
.. note::
   Concrete **operations** (see `todo <>`_) range from conceptually quite broad to quite narrow.  There will be as many as required to capture the *essential functions* of current bioinformatics software tools.  Note *essential*: the Operation subontology will not descend to a level of conceptual granularity that is impractical from a maintenance or usage perspective.
   
- **MUST** state in the definition *what* is done by the operation but not *how* 
- **SHOULD** never be more fine-grained than is useful for practical search purposes
- **SHOULD NOT** include fine-grained specialisations of a basic function, individiaul algorithms *etc.* (a few exceptions are allowed for very highly prevalent concepts)
   
Data
....
.. note::
   Concrete **Data** concepts range from conceptually quite broad to quite narrow.  There will be as many as required to capture the *basic types* of bioinformatsics data.  The Data subontology does (and will) not reflect individual data structures, and like **Operation**, will maintain a level of conceptual granularity that is maintable and usable.  **Data** concepts are formally related to **Identifier** and **Format** concepts:
   - **Identifier** *is_identifier_of* **Data**
   - **Format** *is_format_of* **Data**

- **MUST** have a corresponding concept in the **Format** subontology, *i.e.* the serialisation format(s) of the data.  New formats can be added, if needed.
- **MUST** have a corresponding concept in the **Identifier** subontology, *i.e.* identifier(s) of the data, if these exist.  New identifiers can be added, if needed.
- **MUST** include in the definition a very basic description of the data, usualy in biological terms.
   
Data->Identifier
................
.. note::
   Concrete **Identifier** concepts are very specific.  There will be as many as required to capture the unique types of identifiers in use.  Uniqueness means that a regular expression pattern can, in principle, meaningfully be created describing the identifier instance snytax.  Identifier and data concepts are formally related:
   
   - **Identifier** *is_identifier_of* **Data**

   Concrete formats appear in Tier 3 and below:

   - *Format* (root) -> (*Textual format* | *Binary format* | *XML* | *HTML* | *JSON* | *RDF format* | *YAML*) -> Format ...
     
- **MUST** have a corresponding concept in the **Data** subontology, *i.e.* the type of data that is identified.  New data concepts can be added, if needed.   
- **MUST** include in the definition what type of data and/or name of database the identifier is used for.
- **SHOULD** include a link to relevant documentation for the identifier, if available
- **SHOULD** specify a regular expression pattern, defining valid values of instances of that identifier

Format
......

.. note::
   Concrete **Format** concepts are very specific.  There will be as many as required to capture all of the data formats currently in use.  By *data format" we mean a syntax for which a rigorous, comprehensive description is provided, typically either an XML Schema (XSD) or comprehensive textual specification.  Format and data concepts are formally related:
   
   - **Format** *is_format_of* **Data**

- **MUST** only include a format if it's in common use, for example by public databases or multiple tools
- **MUST NOT** include formats which are specific to single tools only
- **MUST NOT** include formats for which a formal specification does not exist
- **MUST** specify a link to the formal specification (*e.g.* an XML Schema (XSD) or rigorous documentation) of the format syntax
- **MUST** have a corresponding concept in the **Data** subontology, *i.e.* the type of data that the format applies to.  New data concepts can be added, if needed.
- **MUST** mention in the definition the type of data the format is used for.
- **MUST NOT** include any narrow synonyms; if you think specialisations are needed then these can be covered by adding new concepts.
- **SHOULD** annotate file extensions where in common use; these **MUST** preserve the common capitalisation and **MUST NOT** include period ('.'), *e.g.* "txt" not ".txt".
- **SHOULD** annotate the `media type <https://www.iana.org/assignments/media-types/media-types.xhtml>`_ (MIME type) if available


   
   
.. note::


    





