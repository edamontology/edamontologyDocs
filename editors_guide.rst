Editors Guide
=============

.. caution::
   **UNDER CONSTRUCTION**
   This document is undergoing heavy edits right now ... you may want to come back in a few days!

   
If you're not sure how to do something please ask on edam@elixir-dk.org.  You'll need to `subscribe <http://elixirmail.cbs.dtu.dk/mailman/listinfo/edam>`_ to the list first.

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

Format
^^^^^^
The EDAM **Format** subontology includes the following types of concept

- **Concrete data formats** have a clear and public specification or documentation of the format. In some cases there are variants and sub-variants of these (all the leaf nodes are concrete).  In rare cases, for convenience, this includes broad placeholder concepts like *EMBL-like (XML)* and *FASTA-like (text)*.
- **General data formats** currently *Textual format*, *Binary format*, *XML*, *HTML*, *JSON*, *RDF format* and *YAML*. All concrete formats are a child of one of these (see `to-do <>`_).
- **Placeholder concepts** listed under `Format (by type of data) <http://edamontology.org/format_2350>`_ *e.g.* *Alignment format*, *Image format* *etc.*.  These reflect the EDAM **Data* subontology and are purely to aid navigation (until developments in ontology browsers render this device uneccessary).  Placeholder concepts are explicitly annotated as such (see `todo <>`_).



   
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
   2.2 **MUST NOT** include any concept tied to a concrete project or product
   2.3 **SHOULD NOT** include anything that is more tangible than a very general topic, *e.g.* specific cell types, diseases, biological processes, environment types *etc*.  Such fine-grained concepts belong in their own ontology, but **MAY** be captured, where desirable, as synonyms in EDAM.  Rare exceptions are allowed where a term really is in extremely prevalent usage (pragmatism rules!)
2. **MUST NOT** conflate terms in a concept label where these terms exist as independent topics already, *e.g.* *Disease pathways* is disallowed because there are already concepts for *Disease* (synonym of *Pathology*) and *Pathways* (synonym of *Molecular interactions, pathways and networks*).  Instead, if such conflations are required, they **MAY** be added as synonyms of one concept or the other.
3. **MUST NOT** define multiple parents of the term, with the exception of the strongest cases only, where it would be incongruous not to do so *e.g.* *Biochemistry* is a child of both *Biology* and *Chemistry*.
   
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

   
   
EDAM release process
--------------------

Modifying GitHub main repo.
^^^^^^^^^^^^^^^^^^^^^^^^^^^
`EDAM Developers <http://edamontologydocs.readthedocs.io/en/latest/governance.html>`_ can edit the main repository.  The workflow is:

1. Get the "editing token" 

   - Contact edam-dev@elixir-dk.org and claim the "editing token" after first checking that it is not currently taken :)
   - Say what you are doing, why, and about how long it will take

2. Update your local repo with the latest files from the GitHub master:

    ``git pull`` (or "Synch" from the Desktop client)
   
   If you've not already done so, you will first need to clone the master repo:

    ``git clone https://github.com/edamontology/edamontology.git`` (or "Clone" from the Desktop client)

3. Make and commit your local changes. You **must** be working with the "dev" version, ``EDAM_dev.owl``.
   - Check your changes and that the OWL file looks good in Protege
   - Ensure the ``next_id`` attribute is updated
   - Ensure that ``oboOther:date`` is updated to the current GMT/BST before the commit
   - Add the edited file to the commit
   
      ``git add <filepath>``
   - Commit your local changes, including a concise but complete summary of the major changes:
   
      ``git commit -m ”commit message here”``

4. Push your changes to the GitHub master:

    ``git push origin``

**Please provide a meaningful reporting on changes so that we can easily generate the ChangeLog upon next releas**

   - in the Git commit message, including the GitHub issue number of any issues addressed (use ``fix #xxx`` syntax see https://help.github.com/articles/closing-issues-via-commit-messages.
   - directly in the `changelog.md <https://github.com/edamontology/edamontology/blob/master/changelog.md>`_
   
     

5. Release the editing token for the other developers:

   - Contact edam-dev@elixir-dk.org and release the "editing token" .
   - Summarise what you actually did and why.

Creating a new official EDAM release
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
From January 2016, EDAM tries to follow a bi-monthly release cycle to this schedule:

1.  First Wed of every month
   - EDAM team skype to discuss plans for this month.  Announcement (to edam-announcence) including short summary of plans, invitation for suggestions.
2.  Last Mon of every month
   - Announcement (to edam-announcence) saying that release is immiment, invitation for last-minute suggestions.
3.  Last Wed of every month
   - Complete the work for the release.  Make the release.  Ensure it works in BioPortal, OLS, AgroPortal and in bio.tools.
4.  Last Fri of every month
   -  Announcee the release, incuding summary of changes.

Before creating a new release, please make sure you have the approval of leader of EDAM-dev, and that the `changelog.md <https://github.com/edamontology/edamontology/blob/master/changelog.md>`_ and `changelog-detailed.md <https://github.com/edamontology/edamontology/blob/master/changelog-detailed.md>`_ files are up-to-date with the changes of the new release.  See section below on creating the ChangeLog files.  Once you're clear to go, do the following:

1. Update your local version of the repository:

    ``git pull``
2. Assuming you are releasing version n+1, n being the current version:

   - you initially have ``EDAM_dev.owl`` in the repository
   - make sure to update ``oboOther:date`` in this file
   - copy the file ``EDAM_dev.owl`` to ``releases/EDAM_n+1.owl``

    ``cp EDAM\_dev.owl releases/EDAM_n+1.owl``
    ``git add releases/EDAM\_n+1.owl``

   - modify the ``doap:version`` property to **n+1** in ``releases/EDAM_n+1.owl`` and to **n+2_dev** in ``EDAM_dev.owl``
   
   - commit and push your changes

    ``git commit -a``

    ``git push origin``

4. Update the `detailed changelog <https://github.com/edamontology/edamontology/blob/master/changelog-detailed.md>`_ by running `Bubastis <http://www.ebi.ac.uk/efo/bubastis/>`_ to compare the release against the previous version.
5. Update the `changelog <https://github.com/edamontology/edamontology/blob/master/changelog.md>`_ with a summary of the major changes.
6. Create the release on GitHub (use the `_draft a new release_ <https://github.com/edamontology/edamontology/releases/new>`_ button of the `_releases_ <https://github.com/edamontology/edamontology/releases>`_ tab).
7. Update http://edamontology.org.
8. Submit this new release to BioPortal.  OLS will pull the file automatically from edamontology.org every night.
9. Close GitHub issues labelled *done - staged for release*.
10. Confirm everything is working in `bio.tools <http://bio.tools>`_ by mailing `bio.tools Lead Curator <mailto:hans@bio.tools>`_.
11. Announce the new release on Twitter and mailing lists (edam-announce@elixir-dk.org, edam@elixir-dk.org) including thanks and a summary of changes.
12. Help apps that implement EDAM to update to the new version.


Editing the ChangeLog
^^^^^^^^^^^^^^^^^^^^^
The ChangeLog includes:

1. `changelog <https://github.com/edamontology/edamontology/blob/master/changelog.md>`_ - a summary of the major changes and what motivated them
2. `detailed changelog <https://github.com/edamontology/edamontology/blob/master/changelog-detailed.md>`_ - fine-grained details obtained using `Bubastis <http://www.ebi.ac.uk/efo/bubastis/>`_

The changelog should include:

1. (as 1st paragraph) an "executive summary" suitable for consumption by technical managers, describing the motivation for major changes, including *e.g.* requests at recent hackathons, requests via GitHub, strategic directions etc.
2. summary of changes distilled from the output of `Bubastis <http://www.ebi.ac.uk/efo/bubastis/>`_  (see below). 
3. summary of GitHub commit messages.  **please ensure meaningful commit messages are provided on every commit**

Some hacking of bubastis output is needed to identify (at least):
  - number of new concepts
  - number of deprecations
  - summary of activity, i.e. in which branches was most work focucssed ?


Continuous Integration
----------------------
Every modification on the ontology pushed to GitHub triggers an automated test in Travis CI. It checks:
- a few rules using the `edamxpathvalidator tool <https://github.com/edamontology/edamxpathvalidator>`_.
- the consistency of the ontology by running the Hermit reasoner automatically.
The Travis-CI website shows you the current status `here <https://travis-ci.org/edamontology/edamontology>`_. The fact that the continuous integration task succeeds does not guarantee that it there are no remaining bugs, but a failure means that you must take action to correct the problem, either fix it, fix the ``edamxpathvalidator`` program, or ask the mailing list if you're unsure.

Modifications in a GitHub fork
------------------------------
GitHub makes it possible for any developer to make modifications in a copy of EDAM and suggest these modifications are included in the original.  Please note that we discourage using this mechanism for large modifications made using Protege, because merging OWL files which have been reformatted by Protege is notoriously unreliable (see "Best practices for edition" below).

The workflow is:

- Fork the edamontology repository in your own account.
- Make the modifications you want to suggest for inclusion in EDAM in this forked repository.
- Open pull requests for each modification you make.

Please make sure to:

- Keep your forked repository synchronized with the core repository, to avoid inconsistencies.
- Make sure to follow the "Best practices for edition" below.

    

Technical recipes
-----------------


General guidelines
^^^^^^^^^^^^^^^^^^

1. As much as you can, try to make atomic changes and commit them independently. this improves greatly traceability in the long term
2. Make trivial modifications using a text editor if possible, rather than Protege, because the actual modification is not hidden in haystack of Protege reformattings
3. **Immediately** add a description of your modifications in the changelog to facilitate tracking.
4. Check and double-check your changes: errors are hard to track and fix later

Adding concepts
^^^^^^^^^^^^^^^

When adding new terms, you **MUST** specify the following (attributes are in parenthesis):

1. Correct concept URI, i.e. in the right namespace and with the latest ID
2. Preferred term (``rdfs:label``)
3. Definition (``oboInOwl:hasDefinition``) 
4. Parent concept (``rdfs:subClassOf``)
5. Current dev version into ``created_in`` : type a value e.g.  ``1.5``
6. The 'edam' subset (``oboInOwl:inSubset``): in Protege, pick (don't type!) the value of ``edam``
7. The branch subset (``oboInOwl:inSubset``): pick one of ``topic``, ``data``, ``format`` or ``operation``
8. Any specialised subset (pick as above, only if required)

Additionally, you **MUST** increment the next ID ontology attribute (``next_id``) in the header.

Note that :

- The **preferred label** should be a short name or phrase in common use.
- Consider providing common **synonyms** of the term:

   - Exact synonym (``oboInOwl:hasExactSynonym``) - bog-standard synyonsm
   - Narrow synonym (``oboInOwl:hasNarrowSynonym``) - specialisms of the term
   - Broad synonym (``oboInOwl:hasBroadSynonym``) - generalisations of the term

NB: Use Britsh spelling and do **not** include American spellings or case variants as synonyms.

- The **definition** should be a concise and lucid description of the concept, without acronyms, and avoiding jargon.
- Peripheral but important information can go in the **comment** (``rdfs:comment``).

In addition, for **Format** concepts, please specify:

1. The Data concept which the format applies to : define this relation in Protege using the pattern 'Format is_format_of some Data'
2. The URL of the format documentation, if available (``Documentation`` attribute) : in Protege, type a URL using the Protege IRI editor.  

In addition, for **Identifier** concepts, specify:

1. The Data concept which the identifier applies to : define this relation in Protege using the pattern 'Identifier is_identifier_of some Data'  
2. The regular expression defining valid values of that identifier (``Regular expression``) : type the regex into the Protege 'Constant" editor 

In addition, for **Topic** concepts, specify:

1. The corresponding Wikipedia page that exact matches the term (``Documentation`` attribute) : in Protege, type a URL using the IRI editor.  This method will change when we eventually link via Wikidata.




Deprecating concepts
^^^^^^^^^^^^^^^^^^^^ 
When deprecating concepts, you **MUST** specify the following:

1. Current dev version into ``obsolete_since``.
2. The 'obsolete' subset (``oboInOwl:inSubset``): pick ``obsolete``.
3. The ``deprecated`` attribute (``owl:deprecated``): type the value of ``true``.
4. The alternative 'replacement' term to firmly use (``oboInOwl:replacedBy``), or to consider when less certain (``oboInOwl:consider``): pick a concept.
5. The ``oldParent`` attribute : specify the URI of the erstwhile parent of the now-deprecated concept.  If the concept had more than one parent, you should specify more than one ``oldParent`` attribute.
6. Optionally, specify a comment as to why the concept was deprecated in the ``deprecation_comment`` attribute.
7. Set the parent concept (``rdfs:subClassOf``) to the ``ObsoleteClass``. 
8. Remove all other class annotations (subsets, comments, synonyms etc.) and axioms (including parent concepts): comments and synonyms should be preserved as appropriate in the old parents or replacements of the deprecated concept.
8. **Importantly** remember to refactor all references (e.g. ``SubClassOf``) to this concept from other concepts.  You can see all such references in Protege in the "Class Usage"; each reference will need updating in turn: in case of very many such references, this can be easier to do globally in a text editor rather than Protege.

Ensuring logical consistency
^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Before committing changes, to ensure logical consistency of EDAM, please do the following within Protege:

1. Click *Reasoner->Hermit*
2. Click *Reasoner->Start reasoner* (it may take a few seconds)
3. In the *Entities* tab, select the *Class hierarchy (inferred) tab*
4. Select the *nothing* branch

If nothing (no classes) are shown under the *nothing* branch, then all is well.  If one or more classes are shown, then there is a logical inconsistency which must be fixed.  You might see lots of classes, but usually the problem is in one or a few classes.  

Common problems include:

- classes assigned as a ``subClass`` of some deprecated term
- end-point of relations are in the wrong branch, e.g. `class has_topic some operation`.  These can easily occur if you use the *Class expression editor* in Protege to define such axioms: this is NOT EDAM namespace aware, and in cases where a concept with the same preferred label exists in both classes, can easily pick the wrong one.

The problems are easily fixed within Protege: ask on the mailing list if you're not sure how.  Finally, do not be tempted to click *Reasoner->Synchronise reasoner* between changes: it tends to hang Protege.  Instead, use *Reasoner->Stop reasoner* than *Reasoner->Start reasoner*.




