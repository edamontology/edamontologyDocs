Technical details
=================

Concepts
--------

Operation
^^^^^^^^^
**"A function or process performed by a tool; what is done, but not (typically) how or in what context."**

*e.g.* *"Sequence alignment"*, *"Pairwise sequence alignment"*, *"Sequence database search"*.

*"Operation"* concepts provide mostly fine-grained concepts for annotation of tool functions.

The top-level operations are necessarily coarse-grained (abstract) providing a navigable top-level. They serve as placeholders for other, more specific concepts lower down in the tree.

Data
^^^^
**"A type of data in common use in bioinformatics."**

*e.g.* *"Sequence alignment"*, *"Comparison matrix"*, *"Phylogenetic tree"*.

Data concepts:

*   Provide coarse and fine-grained concepts for annotating types of data
*   Cover everything from primitive types and simple parameters, through to derived types and complex, bioinformatics datatypes
*   Reflect but do not describe how the data is specified or represented (syntax)
*   Can be somewhat (necessarily) overlapping

Topic
^^^^^
**"A general bioinformatics subject or category, such as a field of study, data, processing, analysis or technology."**

*e.g.* *"Sequence analysis"*, *"Alignment"*, *"Sequencing"*.

*"Topic"* concepts provide coarse-grained categories for annotation of diverse bioinformatics resources. They do not cover biology or computer science exhaustively.

Format
^^^^^^
**"A specific layout for encoding a specific type of data in a computer file or memory."**

*e.g.* *"FASTA format"*, *"PDB format"*, *"mmCIF"*.

*"Format"* concepts:

*   Provide mostly fine-grained concepts for annotation of data formats / syntaxes.
*   Formats are generally only listed if they are in common use, for example by public databases or multiple tools.
*   Concept statements may include a reference (typically a URL) to the format specification proper.

Most concepts are nested under *"Binary format"*, *"Textual format"* and *"XML"*. The *"Format (typed)"* branch arranges formats by type of data and provides an additional axis over (the same set of) concepts under *"Binary format"*, *"Textual format"* and *"XML"*.

Identifier
^^^^^^^^^^
**"A label that identifies (typically uniquely) something such as data, a resource or a biological entity."**

*e.g.* *"UniProt accession"*, *"EC number"*, *"Gene symbol"*.

*"Identifier"* concepts:

*   Provide mostly fine-grained concepts for annotation of identifiers of data.
*   Typically correspond to simple strings.
*   Have concept definitions which may include a regular expression defining valid string values.

As for *"Format"*, the *"Identifier (typed)"* branch provides an additional axis over (the same set of) concepts under *"Accession"* and *"Name"*.


Relations
---------
is a
^^^^
Defines a concept as a specialisation of another concept. If A **is a** B, then A is a specialisation of B, and B is a generalisation of A.

The **is a** relation is transitive: if A **is a** B and B **is a** C then A **is a** C.

All relations are transitive over **is a**: *e.g.* if A **has input** B and B **is a** C then A **has input** C, and if A **is a** B and B **has input** C then A **has input** C.

*e.g.* *"Pairwise sequence alignment"* **is a** *"Sequence alignment"*

has input
^^^^^^^^^
Defines an *"Operation"* concept as reading (inputting) a *"Data"* concept.

*e.g.* *"Sequence alignment"* **has input** *"Sequence"*

has output
^^^^^^^^^

Defines an *"Operation"* concept as writing (outputting) a *"Data"* concept.

*e.g.* *"Sequence alignment"* **has output** *"Sequence alignment"*

has topic
^^^^^^^^^

Defines a *"Data"* or *"Operation"* concept as being within the scope of a *"Topic"* concept.

*e.g.* *"PolyA signal identification"* **has topic** *"Sequence sites, features and motifs"*

is identifier of
^^^^^^^^^^^^^^^^

Defines that an *"Identifier"* concept identifies a *"Data"* concept.

*e.g.* *"Sequence accession number"* **is identifier of** *"Sequence"*

is format of
^^^^^^^^^^^^

Defines that a *"Format"* concept is the format of a *"Data"* concept.

*e.g.* *"Sequence format"* **is format of** *"Sequence record"*



Rules
-----
Rules define how concepts are related.

Rules by concept type
^^^^^^^^^^^^^^^^^^^^^
**"Topic"**

*   *"Topic"* **is a** *"Topic"*  (specialisation of a topic)

**"Operation"**

*   *"Operation"* **is a** *"Operation"* (specialisation of an operation)
*   *"Operation"* **has input** *"Data"* (inputs a type of data)
*   *"Operation"* **has output** *"Data"* (outputs a type of data)
*   *"Operation"* **has topic** *"Topic"* (within a topic)

**"Data"**

*   *"Data"* **is a** *"Data"* (specialisation of a type of data)
*   *"Data"* **has topic** *"Topic"* (within a topic)

**"Format"**

*   *"Format"* **is a** *"Format"* (specialisation of a data format)
*   *"Format"* **is format of** *"Data"* (a format specification of a data type)

**"Identifier"**

*   *"Identifier"* **is identifier of** *"Data"* (identifier of a data type)

Rules by relation type
^^^^^^^^^^^^^^^^^^^^^^
**is a**

*   *"Topic"* **is a** *"Topic"*
*   *"Operation"* **is a** *"Operation"*
*   *"Data"* **is a** *"Data"*
*   *"Format"* **is a** *"Format"*

**has input**

*   *"Operation"* **has input** *"Data"*

**has output**

*   *"Operation"* **has output** *"Data"*

**has topic**

*   *"Operation"* **has topic** *"Topic"*
*   *"Data"* **has topic** *"Topic"*

**is identifier of**

*   *"Identifier"* **is identifier of** *"Data"*

**is format of**

*   *"Format"* **is format of** *"Data"*


Concept deprecation
-------------------
*   EDAM uses numerical alphaidentifiers to uniquely identify concepts. These identifiers will persist between versions: a given identifier and URI are guaranteed to continue identifying the same concept. This does **not** imply names (terms), definitions and other fields will remain constant, but they will remain true to concept.
*   Concepts that are deprecated will also persist; they will not be removed and will maintain their identifier and URI.  A replacement concept, or suggested replacement is given for all deprecated concepts.

edamontology.org 
----------------
The *edamontology.org* site provides content negotiation with respect to the desired media type (*i.e.* format, *e.g.* HTML, OWL, *etc.*). This applies also to the URIs of EDAM concepts that are in this way dereferencable, concise, and stable. Alternatively to requesting the format in the HTTP header, users can retrieve the desired content from a web browser by inserting ``?format=<desiredformat>`` query into the URL.
