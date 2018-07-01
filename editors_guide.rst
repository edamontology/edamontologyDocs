Editors Guide
=============

.. caution::
   **UNDER CONSTRUCTION**
   This document is undergoing heavy edits right now ... you may want to come back in a few days!

   
If you're not sure how to do something please ask edam@elixir-dk.org.  You'll need to `subscribe <http://elixirmail.cbs.dtu.dk/mailman/listinfo/edam>`_ to the list first.

Terminology
-----------
We use the following terms when talking about EDAM:

- *EDAM* refers to the ontology in totality (all subontologies).
- *Subontology* and occasionally *branch* refers to an EDAM subontology, *i.e.* **Topic**, **Operation**, **Data** or **Format**.  Also **Data->Identifier** (a branch of **Data**).
- *Concept* is the basic unit of information in EDAM: including concept definition, terms and other metadata 
- *Primary label* or simply *Label* is the primary term by which the concept is referred to.  They're used for annotation purposes.
- *Synonym* means an exact, narrow, broad or related synonym (see `todo <https://todo>`_).  They can also be used for annotation.
- *Term* and *terms* refer to primary labels and synonyms collectively.
- *Hierarchy* refers to the EDAM tree structure, resulting from EDAM concepts being defined as specialisations/generalisations of one another (PS. EDAM isn't a tree, it's a `DAG <https://en.wikipedia.org/wiki/Directed_acyclic_graph>`_.)
- *Root* refers to the top-most concept in a subontology, i.e. `Topic <http://edamontology.org/topic_0003>`_, `Operation <http://edamontology.org/operation_0004>`_, `Data <http://edamontology.org/data_0006>`_, and `Format <http://edamontology.org/format_1915>`_.  And (depending on context) `Identifier <http://edamontology.org/data_0842>`_.
- *Tier* refers to a particular level in the hierarchy, excluding the subontology root, *e.g.* "Tier 1 data concepts" means everything immediately under `Data <http://edamontology.org/data_0006>`_.
- *Top-level* refers to Tier 1 concepts.
- *Child*, *Children of*, *Kids* *etc.* refers to concept(s) defined as an immediate specialisation of another (*i.e.* "is_a", or the OWL geek "subClass").  Conversely *Parent* means the opposite (a generalisation of a concept).
- *Ancestor* means *Parent* or the parent's parent *etc.* Conversely *Descendant* means *Child* or the children's children *etc.*
- *related to* means a concept in one subontology is formally defined as related (in various ways) to a concept in another, but excluding basic specialisation/generalisation relationships.
- *Node* refers to a concept when it's being discussed in context of the hierachy.
- *Leaf* refers to a concept at the bottom of the tree (without children).


For a technical definition of these things, see `todo <http://todo>`_.

General considerations
----------------------  
1. EDAM concepts are of two types:
   
- **Placeholder concepts** are high-level (conceptually broad), and used primarily to structure EDAM, providing placeholders for concrete concepts (below). They're not intended to be used much, or at all, for annotation.
- **Concrete concepts** are lower-level (conceptually more narrow) and are intended for annotation.  With the exception of **Topic** subontology (which has no concreate concepts), *all* leaf nodes are concrete.

The types are clarified for different EDAM subontologies (see sections below).
  
2. EDAM must always evolve, which means additions, edits, and occasionally *deprecations*: marking-up concepts as not recommended for use: there are special `deprecation guidelines <todo>`_ for this.
   
.. note::
   The notions of "placeholder", "concrete", "broad", "narrow" *etc.* are of course not hard and fast.  As a work in progress, all placholders and concrete concepts will be formally annotated as such, this `under discussion <https://github.com/edamontology/edamontology/issues/265>`_.


   
Topic
^^^^^

The **Topic** subontology will only ever include a few hundred concepts in total, semantic richness is captured through synonyms (which are unlimited in number). This ensures sustainability and practical applications. Hence EDAM **topics** are conceptually very broad categories with no clearly defined borders between each other (the notion of placeholder and concrete concepts doesn't apply).  This somewhat contrasts *e.g.* `MeSH <https://www.nlm.nih.gov/bsd/disted/meshtutorial/introduction/>`_.

   
Operation
^^^^^^^^^
The **Operation** subontology includes:

- **Placeholder operations** currently include *all* concepts at the first tier, *e.g.* `Analysis <http://edamontology.org/operation_2945>`_, `Prediction and recognition <http://edamontology.org/operation_2423>`_ *etc.*, and some second tier concepts *e.g.* `Sequence analysis <http://edamontology.org/operation_2403>`_.
- **Concrete operations** (*e.g.* `Protein feature detection <http://edamontology.org/operation_3092>`_) and in some cases variants (*e.g.* `Protein binding site prediction <http://edamontology.org/operation_2575>`_ and sub-variants (*e.g.* `Protein-nucleic acid binding prediction <http://edamontology.org/operation_0420>`_) of these.

Data
^^^^
The **Data** subontology includes:

- **Placeholder data concepts** are basic types of data, either technical (*e.g.* `Score <http://edamontology.org/data_1772>`_) or biological (*e.g.* `Phylogenetic data <http://edamontology.org/data_2523>`_).  They mostly appear in the **first tier** (but not all Tier 1 **Data** concepts are placeholders), rarely in Tier 2, and never below that.
- **Concrete types of data** *i.e.* for which a corresponding data format concept exists, and in some cases variants and sub-variants of these (all the leaf nodes are concrete).
   
Data->Identifier
^^^^^^^^^^^^^^^^
, the *"Identifier (typed)"* branch provides an additional axis over (the same set of) concepts under *"Accession"* and *"Name"*.


Format
^^^^^^
The EDAM **Format** subontology includes the following types of concept

- **Concrete data formats** have a clear and public specification or documentation of the format. In some cases there are variants and sub-variants of these (all the leaf nodes are concrete).  In rare cases, for convenience, this includes broad placeholder concepts like *EMBL-like (XML)* and *FASTA-like (text)*.
- **General data formats** currently *Textual format*, *Binary format*, *XML*, *HTML*, *JSON*, *RDF format* and *YAML*. All concrete formats are a child of one of these (see `to-do <>`_).
- **Placeholder concepts** listed under `Format (by type of data) <http://edamontology.org/format_2350>`_ *e.g.* *Alignment format*, *Image format* *etc.*.  These reflect the EDAM **Data* subontology and are purely to aid navigation (until developments in ontology browsers render this device uneccessary).  Placeholder concepts are explicitly annotated as such (see `todo <>`_).

Most concepts are nested under *"Binary format"*, *"Textual format"* and *"XML"*. The *"Format (typed)"* branch arranges formats by type of data and provides an additional axis over (the same set of) concepts under *"Binary format"*, *"Textual format"* and *"XML"*.

   
Rules of thumb for EDAM development 
-----------------------------------
These rules of thumb are to guide the technical and scientific development of EDAM, to help ensure structural and conceptual simplicity and that EDAM is fit for purpose and will scale to annotate athe growing bio.tools.
Before proposing or making any major changes, make sure you understand the `principles <http://edamontologydocs.readthedocs.io/en/latest/what_is_edam.html#principles>`_ on which EDAM is based.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in `RFC 2119 <http://www.ietf.org/rfc/rfc2119.txt>`_:

- **"MUST"**, **"REQUIRED"** or **"SHALL"** mean that the guideline is an absolute requirement of the specification.
- **"MUST NOT"** or **"SHALL NOT"** mean that the guideline is an absolute prohibition of the specification.
- **"SHOULD"** or **"RECOMMENDED"** mean that there may exist valid reasons in particular circumstances to ignore a particular guideline, but the full implications must be understood and carefully weighed before doing so.
- **"SHOULD NOT"** or the phrase **"NOT RECOMMENDED"** mean that there may exist valid reasons in particular circumstances when acting contrary to the geuideline is acceptable or even useful, but the full implications should be understood and the case carefully weighed before doing so.
- **"MAY** or **"OPTIONAL"** mean that the guideline is truly optional; you can choose to follow it or not.

General
^^^^^^^
1. Jargon and buzzwords *e.g.* "Big data", "NGS" *etc.* **SHOULD** be avoided, but if really prevalent and relevant, **MAY** be added via synonyms but **MUST NOT** be the primary term.
2. Each subontology must not descend beyond a certain depth (see below).  Specifically, this means that each concept **MUST** have at least one path to root (*i.e.* `Topic <>`_, `Operation <>`_, `Data <>`_ or `Format <>`_ no deeper than indicated.   It's OK for a concept to have other paths to root that are deeper than this.
   2.1 **Topics** 3 levels deep max. *i.e.* *Topic* (root) -> Topic -> Subtopic -> Subsubtopic (leaves)
   2.2 **Operations** 6 levels deep max. 
   2.3 **Data** 4 levels deep max. 
   2.4 **Format** - 3 levels deep max. 
3. When adding a concept that introduces a new level of depth, you **MUST** be sure it's realistic to also add and maintain, in due course, all relevant siblings (*i.e.* related concepts with the same parent).  This is to ensure EDAM coverage does not get patchy.
4. You **SHOULD NOT** introduce any "single childs" (concepts without siblings) unless you already know of potential sublings (to add in due course), or think it's likely such sibling concepts will appear in the future: you **MUST** consider this before adding a single child.
5. You **MUST NOT** add a concept if this implies that additional new concepts are needed (above point), but this extension in total would seriously overlap with an existing well-developed ontology that already serves this area better.  If in doubt you **MUST** discuss this with the `EDAM developers <mailto:edam-dev@elixir-dk.org>`_.
6. If you add a concept which you expect to remain a leaf node, *i.e.* EDAM will not include finer-grained concepts, then - if other well-developed ontologies exist that serve this conceptual niche - you **SHOULD** annotate this junction (see `todo <>`_).
7. Concept labels **MUST** be unique within a sub-ontology and **SHOULD** be unique across all of EDAM (rare exceptions are allowed).
8. With the exception of **topics**, you **MUST NOT** add a concept with significant conceptual overlap to an existing concept, which you means you **MUST** check carefully, especially the siblings of the new concept.
9. **SHOULD NOT** define multiple parents of a concept unless there is a very unambivalent case. This rule is even stronger for **Topics** (where most overlap with each other). 

.. note::
   The 3-level depth of **Format** depth is achieved:

   *Format* (root) -> (*Textual format* | *Binary format* | *XML* | *HTML* | *JSON* | *RDF format* | *YAML*) -> Format (leaves)

   See `to-do <>`_ below.

Topic
^^^^^
1. **SHOULD** have a corresponding term in `Wikipedia <https://en.wikipedia.org/wiki/Main_Page>`_ and **MUST** provide a link (*via* **seeAlso** annotation) to the relevant Wikipedia page, if one exists.  Exceptions are OK, but if a Wikipedia page does not exist, one **MUST** consider carefully whether the concept is too fine-grained.
2. **MUST** respect the scope, specifically:
   
   2.1 **MUST NOT** include fine-grained operations or types of data.  As a rare exception, very high-level operations *e.g.* *Sequence analysis* **MAY** be included.
   2.2 **MUST NOT** include any concept tied to a concrete project or product.
   2.3 **SHOULD NOT** include anything that is more tangible than a very general topic, *e.g.* specific cell types, diseases, biological processes, environment types *etc*.  Such fine-grained concepts belong in their own ontology, but **MAY** be captured, where desirable, as synonyms in EDAM.  Rare exceptions are allowed where a term really is in extremely prevalent usage (pragmatism rules!)
   
3. **MUST NOT** conflate terms in a concept label where these terms exist as independent topics already, *e.g.* *Disease pathways* is disallowed because there are already concepts for *Disease* (synonym of *Pathology*) and *Pathways* (synonym of *Molecular interactions, pathways and networks*).  Instead, if such conflations are required, they **MAY** be added as synonyms of one concept or the other.
4. **MUST NOT** define multiple parents of the term, with the exception of the strongest cases only, where it would be incongruous not to do so *e.g.* *Biochemistry* is a child of both *Biology* and *Chemistry*.
   
Operation
^^^^^^^^^
1. Concepts **MUST** conceptually be clearly distinct from other (non-placeholder) Operations, and this **MUST** be reflected in the label and definition of the concept.
2. Concepts **SHOULD** should never be more fine-grained than is useful for practical search purposes, and **SHOULD NOT** include fine-grained specialisations of a basic function, individiaul algorithms etc. (a few exceptions are allowed for very highly prevalent concepts)
   
Data
^^^^
1. Placholder concepts **MUST** be annotated with ``<usageGuideline>Not recommended for annotation in bio.tools.</usageGuideline>``.
2. **SHOULD NOT** contain any chains of placeholder concepts, *i.e.* placholders are normally allowed (with a few rare exceptions) in the first tier.
   
Data->Identifier
^^^^^^^^^^^^^^^^
1. A new identifier (or it's ancestor) **MUST** be annotated (via *is_identifier_of*) to indicate the type of data that is identified but you **MUST NOT** duplicate this annotation if it's already stated on an ancestor concept. 


Format
^^^^^^
1. Leaf nodes **MUST** be concrete data formats, see `to-do <>`_ and `to-do <>`_).
2. Concrete data formats **MUST** descend from *Textual format*, *Binary format*, *XML*, *HTML*, *JSON*, *RDF format* or *YAML*, but you **MUST NOT** duplicate this ancestry in format variants.  For example *FASTA-like (text)* is defined as a child of *Textual format*, but the kids of *FASTA-like (text)* format are not.
3. Concrete data formats **MUST** descended from `Format (by type of data) <http://edamontology.org/format_2350>`_ (or it's kids), but again, you **MUST NOT** duplicate this ancestry in format variants.  For example *FASTA-like (text)* is defined as a child of *Sequence record format* -> *FASTA-like*, but the kids of *FASTA-like (text)* format are not.
4. **MUST NOT** add new placeholder concepts (kids of `Format (by type of data) <http://edamontology.org/format_2350>`_) unless there is a corresponding concrete data format descending from it.
5. Concepts which are not concrete data formats **MUST** be annotated with ``<usageGuideline>Not recommended for annotation in bio.tools.</usageGuideline>`` - this annotation type will soon be refactored (to be made more specific).
6. Where file extensions are in common use, all of these **SHOULD** be annotated and you **MUST** preserve the common capitalisation and **MUST NOT** include period ('.') in the annotation, *e.g.* "txt" not ".txt".
7. A new format (or it's ancestor) **MUST** be annotated (via *is_format_of*) to indicate the type of data that is formatted but you **MUST NOT** duplicate this annotation if it's already stated on an ancestor concept. 
8. **SHOULD** annotate the `media type <https://www.iana.org/assignments/media-types/media-types.xhtml>`_ (MIME type) if available, seee `todo <>`_.
9. **MUST** annotate the specification or documentation of concrete data formats (see `todo <>`_)


   *   Formats are generally only listed if they are in common use, for example by public databases or multiple tools.
*   Concept statements may include a reference (typically a URL) to the format specification proper.
   
   
    





