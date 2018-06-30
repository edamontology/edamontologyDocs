Technical details
=================

.. note::
  An outline of the technical implementation of EDAM is below.  EDAM makes light use of `OWL <https://www.w3.org/OWL/>`_ logic/modelling and focuses on providing quality information for a basic set of *concepts*, with *relations* between these concepts and a very simple set of *rules* governing the conceptual relationships.  Concepts have unique IDs and persistently resolvable URLs.

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
is_a
^^^^
Defines a concept as a specialisation of another concept. If A *is_a* B, then A is a specialisation (child) of B, and B is a generalisation (parent) of A.

The *is_a* relation is transitive: if A *is_a* B and B *is_a* C then A *is_a* C.

All relations are transitive over *is_a*: *e.g.* if A *has_input* B and B *is_a* C then A *has_input* C, and if A *is_a* B and B *has_input* C then A *has_input* C.

*e.g.* *"Pairwise sequence alignment"* *is_a* *"Sequence alignment"*

has_input
^^^^^^^^^
Defines an **Operation** concept as reading (inputting) a **Data** concept.

*e.g.* *"Sequence analysis"* *has_input* *"Sequence"*

has_output
^^^^^^^^^

Defines an **Operation** concept as writing (outputting) a **Data** concept.

*e.g.* *"Sequence alignment"* *has_output* *"Sequence alignment"*

has_topic
^^^^^^^^^

Defines a **Data** or **Operation** concept as being within the scope of a **Topic** concept.

*e.g.* *"Peptide identification"* *has_topic* *"Proteomics"*

is_identifier_of
^^^^^^^^^^^^^^^^

Defines that an **Identifier** concept identifies a **Data** concept.

*e.g.* *"Sequence accession"* *is_identifier_of* *"Sequence"*

is_format_of
^^^^^^^^^^^^

Defines that a **Format** concept is the format of a **Data** concept.

*e.g.* *"Sequence record format"* *is_format_of* *"Sequence record"*



Rules
-----
Rules define how concepts are related.

Rules by concept type
^^^^^^^^^^^^^^^^^^^^^
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

Rules by relation type
^^^^^^^^^^^^^^^^^^^^^^
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


Identifiers & persistent URLs
-----------------------------
Each EDAM concept has an alphanumerical identifier that uniquely identifies that concept. The general form is:

* ``<namespace>_<4-digit-ID>``

where ``<namespace>`` is one of:
* ``topic``
* ``operation``
* ``data``
* ``format``

and ``<4-digit-ID>`` uses numbers from 0 to 9, *e.g.*

* ``topic_0121``

The IDs are used in URLs that resolve to information about the concept, *e.g.*:  

http://edamontology.org/topic_0121

These identifiers (and the URLs) persist between versions: a given identifier and URI are guaranteed to continue identifying the same concept. This does **not** imply that terms, definitions and other information remains constant, but the IDs *will* remain essentially true to the original concept.

Occasionally, concepts become *deprecated* - designated as not being recommended for use.  Deprecated concepts also persist; they are removed and will maintain their identifier and URI.  A replacement concept, or suggested replacement is given for all deprecated concepts; see the rules on `deprecatation <http://edamontologydocs.readthedocs.io/en/latest/editors_guide.html#deprecating-concepts>`_ 
