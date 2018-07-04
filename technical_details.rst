Technical details
=================

.. note::
  An outline of the technical implementation of EDAM is below.  EDAM makes light use of `OWL <https://www.w3.org/OWL/>`_ logic/modelling and focuses on providing quality information for a basic set of *concepts*, with *relations* between these concepts and a very simple set of *rules* governing the conceptual relationships.  Concepts have unique IDs and persistent URLs which resolve to a Web page providing all the information for that concept.


  
Concepts
--------

Topic
^^^^^
**"A general bioinformatics subject or category, such as a field of study, data, processing, analysis or technology."**

*e.g.* *"Biology"*, *"Nucleic acid sites, features and motifs"*, *"Sequencing"*.

**Topic** concepts provide very broad categories for annotation of diverse bioinformatics resources. There will only ever be a few hundred EDAM topics: biology or computer science is not exhaustively covered!

Operation
^^^^^^^^^
**"A function or process performed by a tool; what is done, but not (typically) how or in what context."**

*e.g.* *"Sequence alignment"*, *"Genome indexing"*, *"Sequence database search"*.

**Operation** concepts enable the annotation of software tool functions, from quite broad to very specific.  There will be as many EDAM Operations as required to support pratical applications, *e.g.* description / finding tools in `bio.tools <https://biotools>`_.

Data
^^^^
**"A type of data in common use in bioinformatics."**

*e.g.* *"Sequence alignment"*, *"Comparison matrix"*, *"Phylogenetic tree"*.

**Data** concepts enable the annotation of types of data, *e.g.* inputs and ouputs of tools.  There are some categories of data (for structuring EDAM), and some common tool parameters, but mostly they correspond to specific data formats (see below), *i.e.* complex biological data.  Note: a single type of data can be serialised in multiple data formats! 


Identifier
^^^^^^^^^^
**"A label that identifies (typically uniquely) something such as data, a resource or a biological entity."**

*e.g.* *"UniProt accession"*, *"EC number"*, *"Gene symbol"*.

**Identifier** concepts enable the annotation of identifiers of data.  There are some categories (for structuring EDAM), but mostly they correspond to specific data identifiers.  Identifiers are typically simple strings and EDAM includes regular expressions defining valid string values.  Identifiers are formally related in EDAM to **Data** concepts (see `is_identifier_of <http://edamontologydocs.readthedocs.io/en/latest/technical_details.html#is-identifier-of>`_).

Format
^^^^^^
**"A specific layout for encoding a specific type of data in a computer file or memory."**

*e.g.* *"FASTA format"*, *"PDB format"*, *"mmCIF"*.

**Format** concepts enable the annotation of specific data formats / syntaxes; some general purpose ones but mostly biological data formats.

To be included, a format must be in common use and formally specified or documented; EDAM includes links to these things.  
Formats are formally related in EDAM to **Data** concepts (see `is_format_of <http://edamontologydocs.readthedocs.io/en/latest/technical_details.html#is-format-of>`_).

Relations
---------

Relation types
^^^^^^^^^^^^^^

is_a
....
Defines a concept as a specialisation of another concept. If A *is_a* B, then A is a specialisation (child) of B, and B is a generalisation (parent) of A.

The *is_a* relation is transitive: if A *is_a* B and B *is_a* C then A *is_a* C.

All relations are transitive over *is_a*: *e.g.* if A *has_input* B and B *is_a* C then A *has_input* C, and if A *is_a* B and B *has_input* C then A *has_input* C.

*e.g.* *"Pairwise sequence alignment"* *is_a* *"Sequence alignment"*

has_input
.........
Defines an **Operation** concept as reading (inputting) a **Data** concept.

*e.g.* *"Sequence analysis"* *has_input* *"Sequence"*

has_output
.........

Defines an **Operation** concept as writing (outputting) a **Data** concept.

*e.g.* *"Sequence alignment"* *has_output* *"Sequence alignment"*

has_topic
.........

Defines a **Data** or **Operation** concept as being within the scope of a **Topic** concept.

*e.g.* *"Peptide identification"* *has_topic* *"Proteomics"*

is_identifier_of
................

Defines that an **Identifier** concept identifies a **Data** concept.

*e.g.* *"Sequence accession"* *is_identifier_of* *"Sequence"*

is_format_of
............

Defines that a **Format** concept is the format of a **Data** concept.

*e.g.* *"Sequence record format"* *is_format_of* *"Sequence record"*


Rules
^^^^^
Rules define how concepts are related.

Rules by concept
................
**Topic**

*   **Topic** *is_a* **Topic**  (specialisation of a topic)

**Operation**

*   **Operation** *is_a* **Operation** (specialisation of an operation)
*   **Operation** *has_input* **Data** (inputs a type of data)
*   **Operation** *has_output* **Data** (outputs a type of data)
*   **Operation** *has_topic* **Topic** (within a topic)

**Data**

*   **Data** *is_a* **Data** (specialisation of a type of data)
*   **Data** *has_topic* **Topic** (within a topic)

**Format**

*   **Format** *is_a* **Format** (specialisation of a data format)
*   **Format** *is_format_of* **Data** (a format specification of a data type)

**Identifier**

*   **Identifier** *is_identifier_of* **Data** (identifier of a data type)

Rules by relation
.................
*is_a*

*   **Topic** *is_a* **Topic**
*   **Operation** *is_a* **Operation**
*   **Data** *is_a* **Data**
*   **Format** *is_a* **Format**

*has_input*

*   **Operation** *has_input* **Data**

*has_output*

*   **Operation** *has_output* **Data**

*has_topic*

*   **Operation** *has_topic* **Topic**
*   **Data** *has_topic* **Topic**

*is_identifier_of*

*   **Identifier** *is_identifier_of* **Data**

*is_format_of*

*   **Format** *is_format_of* **Data**


Concept types
-------------
EDAM concepts are defined internally as one of two types:
   
- **Placeholder concepts** are high-level (conceptually broad), and used primarily to structure EDAM, providing placeholders for *concrete concepts*. They're not intended to be used much, or at all, for annotation.
- **Concrete concepts** are lower-level (conceptually more narrow) and are intended for annotation.  *All* leaf nodes are concrete.

These notion depend upon the subontology (see below).

.. note::
   EDAM topics are conceptually very broad categories with no clearly defined borders between each other: the notion of placeholder and concrete concepts doesn't apply! 
  
Placholder concepts
^^^^^^^^^^^^^^^^^^^
- **Operation placeholders** include high-level (abstract) operations *e.g.* *Analysis*, *Prediction and recognition*, and sometimes variants *e.g.* *Sequence analysis*.

- all Tier 1 (children of `Operation <http://edamontology.org/data_0004>`_) and some Tier 2 operations are placholders.
    
- **Data placeholders** are basic types of data:

  - technical types, *e.g.* *Score*
  - broad biological types *e.g.* *Phylogenetic data*

- they mostly appear in Tier 1 (children of `Operation <http://edamontology.org/data_0004>`_), rarely in Tier 2, and never below that.  Note, not all Tier 1 **Data** concepts are placeholders.

- **Identifier placeholders** include: 

    - *basic identifier type* one of `Accession <http://edamontology.org/data_2091>`_ or `Name <http://edamontology.org/data_2099>`_.  All concrete identifiers are a child of one of these.
    - *data type placeholders* under `Identifier (typed) <http://edamontology.org/data_0976>`_ *e.g.* "Sequence accession (protein)". These mirror the **Data** subontology.  All concrete identifiers are a child of one of these.
    - `Identifier (hybrid) <http://edamontology.org/data_2109>`_.  A concrete identifier is a child of this if it's re-used for data objects of fundamentally different types (typically served from a single database).

- **Format placeholders** include:

    - *general data formats* currently `Textual format <http://edamontology.org/format_2330>`_, `Binary format <http://edamontology.org/format_2333>`_, `XML <http://edamontology.org/format_2332>`_, `HTML <http://edamontology.org/format_2331>`_, `JSON <http://edamontology.org/format_3464>`_, `RDF format <http://edamontology.org/format_2376>`_ and `YAML <http://edamontology.org/format_3750>`_. All concrete formats are a child of one of these (see `to-do <>`_).
    - *data type placeholders* for types of data listed under `Format (by type of data) <http://edamontology.org/format_2350>`_ *e.g.* *Alignment format*, *Image format* *etc.*.  


.. note::
   The *data type placeholders* used in the **Identifier** and **Format** subontologies reflect the EDAM **Data** subontology.  They serve purely to aid navigation, by providing an additional axis over (the same set of) concepts under *"Accesion"* and *"Name"* (**Identifier**) or *"Binary format"*, *"Textual format"* and *"XML"* (**Format**).  Once ontology browsers better support rendering of conceptual relationships, it may no longer be necessary to support in EDAM the `Format (by typed of data) <http://edamontology.org/format_2350>`_ and `Identifier (by type of data)<http://edamontology.org/data_0976>`_ patterns. 

	
Concrete concepts
^^^^^^^^^^^^^^^^^

- **Concrete operations** have a specific input and/or output
  - have at least one **Operation** *has_input* | *has_output* **Data** relation (see `todo <>`_ and `todo <>`_)
  - include low-level (specific) operations (*e.g.* `Protein feature detection <http://edamontology.org/operation_3092>`_) and in some cases variants (*e.g.* `Protein binding site prediction <http://edamontology.org/operation_2575>`_) and sub-variants (*e.g.* `Protein-nucleic acid binding prediction <http://edamontology.org/operation_0420>`_)
  - maximum of 3 concrete operations in a chain (see `todo <>`_).

- **Concrete data types** have a specific serialisation format
  - have one **Format** *is_format_of* **Data** relation (see `todo <>`_ and `todo <>`_)
  - maximum of 2 concrete data types in a chain (see `todo <>`_)

- **Concrete identifers** have a corresponding data type
  - have one **Identifier** *is_identifier_of* **Data** relation (see `todo <>`_ and `todo <>`_)
  - normally have a regular expression pattern defining valid syntax of identifier instances (see `todo <>`_)
  - no maximum chain (it depends on extant identifiers)
      
- **Concrete data formats** have a formal, public syntax specification
  - have one ``<specification>`` annotation linking to the format specification (see `todo <>`_)
  - in some cases, as practical necessity, there are format variants and sub-variants, *e.g.* *EMBL-like (XML)* and *FASTA-like (text)*
  - no maximum chain (it depends on extant formats)

.. note::
   The notions of "placeholder", "concrete", "broad", "narrow" *etc.* are of course not hard and fast.  As a work in progress, all placholders and concrete concepts will be formally annotated as such, this `under discussion <https://github.com/edamontology/edamontology/issues/265>`_.  The addition of *has_input* and *has_output* relations is also a work in progress.




Terms and synonyms
------------------
EDAM uses the following types of synonym:

- **Exact** synonym  - a standard synonym (same meaning) of the primary term
- **Narrow** synonym - specialisms of the primary term
- **Broad** synonym - generalisations of the primary term

All terms (primary and synonyms) are unique within a subontology, and (with a few exceptions) are unique *between* subontologies, too.  




    
Identifiers & persistent URLs
-----------------------------
Each EDAM concept has an alphanumerical identifier that uniquely identifies that concept. The general form is:

* ``<namespace>_<4-digit-ID>``

where ``<namespace>`` refers to an EDAM subontology, one of:

* ``topic``
* ``operation``
* ``data``
* ``format``

and ``<4-digit-ID>`` uses numbers from 0 to 9.  Note this number is unique across all subontologies.

The IDs are used in URLs that resolve to information about the concept, *e.g.*:  
* ``topic_0121``
* http://edamontology.org/topic_0121

These identifiers (and the URLs) persist between versions: a given ID and URI are guaranteed to continue identifying the same concept. This does *not* imply that terms, definitions and other information remains constant, but the IDs *will* remain essentially true to the original concept.

Occasionally, concepts become *deprecated* - designated as not being recommended for use.  Deprecated concepts also persist; they are removed and will maintain their ID and URI. EDAM developers adhere to rules on `deprecatation <http://edamontologydocs.readthedocs.io/en/latest/editors_guide.html#deprecating-concepts>`_, *e.g.* a replacement concept, or suggested replacement is given for all deprecated concepts.  
