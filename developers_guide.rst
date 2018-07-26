Developers Guide
================

Welcome to the EDAM Developers Guide.  It contains best-practice guidelines for the technical processes of EDAM development;  modifying EDAM files on GitHub, creation of releases, deprecation of concepts *etc.*
   
If you're not sure how to do something please ask edam@elixir-dk.org.  You'll need to `subscribe <http://elixirmail.cbs.dtu.dk/mailman/listinfo/edam>`_ to the list first.



Technical recipes
-----------------
.. note::

   The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in `RFC 2119 <http://www.ietf.org/rfc/rfc2119.txt>`_:

   - **"MUST"**, **"REQUIRED"** or **"SHALL"** mean that the guideline is an absolute requirement of the specification.
   - **"MUST NOT"** or **"SHALL NOT"** mean that the guideline is an absolute prohibition of the specification.
   - **"SHOULD"** or **"RECOMMENDED"** mean that there may exist valid reasons in particular circumstances to ignore a particular guideline, but the full implications must be understood and carefully weighed before doing so.
   - **"SHOULD NOT"** or the phrase **"NOT RECOMMENDED"** mean that there may exist valid reasons in particular circumstances when acting contrary to the geuideline is acceptable or even useful, but the full implications should be understood and the case carefully weighed before doing so.
   - **"MAY** or **"OPTIONAL"** mean that the guideline is truly optional; you can choose to follow it or not.




General guidelines
^^^^^^^^^^^^^^^^^^

1. As much as you can, try to make atomic changes and commit them independently. this improves greatly traceability in the long term
2. Make trivial modifications using a text editor if possible, rather than Protege, because the actual modification is not hidden in haystack of Protege reformattings
3. Include an informative message when you commit a change and (ideally) add a description of your modifications in the changelog.
4. Check and double-check your changes: errors can be hard to track and fix later

Adding concepts
^^^^^^^^^^^^^^^

Mandatory attributes
....................
When adding new concepts, you **MUST** specify the following:

.. csv-table::
   :header: "Attribute", "OWL attribute", "Note"
   :widths: 20, 40, 60
   
   "Concept URI", "``rdf:about``", "In the right namespace and with the latest numerical ID."
   "Primary term", "``rdfs:label``", "See `Editors Guide <http://edamontologydocs.readthedocs.io/en/latest/editors_guide.html#concepts-terms>`_."
   "Definition", "``oboInOwl:hasDefinition``", "See `Editors Guide <http://edamontologydocs.readthedocs.io/en/latest/editors_guide.html#concepts-terms>`_."
   "Parent(s)", "``rdfs:subClassOf``", Immediate parent(s) of the concept (normally one only)."
   "Version", "``created_in``", "Current EDAM dev version, *e.g.* ``1.21``."
   "Type subset", "``oboInOwl:inSubset``", "One of ``concrete`` or ``placeholder``, see `Technical details <http://edamontologydocs.readthedocs.io/en/latest/technical_details.html#concept-types>_`."
   "EDAM subset", "``oboInOwl:inSubset``", "Always ``edam``."
   "Branch subset", "``oboInOwl:inSubset``", "One of ``topic``, ``data``, ``format`` or ``operation``."
   "Type subset", "``oboInOwl:inSubset``", "One of ``concrete`` or ``placeholder``."
   "Next ID", "``<next_id>``", "Increment the current count by 1."

For **Format** additions you **MUST** also specify:

.. csv-table::
   :header: "Attribute", "OWL attribute", "Note"
   :widths: 20, 40, 60
	    
   "Type of data", "``<is_format_of>``", "URI of EDAM Data concept."
   "Specification", "``<documentation>``", "URL of format specification.  See `todo <>`_."
   "Basic type", "``rdfs:subClassOf``", "One of `Textual format <http://edamontology.org/format_2330>`_, `Binary format <http://edamontology.org/format_2333>`_, *etc.*.  See `Technical details <http://edamontologydocs.readthedocs.io/en/latest/technical_details.html#placholder-concepts>`_."
   "Type of data", "``rdfs:subClassOf``", "Some child of `Format (by type of data) <http://edamontology.org/format_2350>`_.  See `Technical details <http://edamontologydocs.readthedocs.io/en/latest/technical_details.html#placholder-concepts>`_."

For **Identifier** additions you **MUST** also specify:

.. csv-table::
   :header: "Attribute", "OWL attribute", "Note"
   :widths: 20, 40, 60
	    
   "Type of data", "``<is_identifier_of>``", "URI of EDAM Data concept."
   "Basic type", "``rdfs:subClassOf``", "One of `Accession <http://edamontology.org/data_2091>`_ or `Name <http://edamontology.org/data_2099>`_.  See `Technical details <http://edamontologydocs.readthedocs.io/en/latest/technical_details.html#placholder-concepts>`_."
   "Type of data", "``rdfs:subClassOf``", "Some child of `Identifier (hybrid) <http://edamontology.org/data_2109>`_. See `Technical details <http://edamontologydocs.readthedocs.io/en/latest/technical_details.html#placholder-concepts>`_."

   
Optional attributes
...................
When adding new concepts, you **SHOULD** specify the following:

.. csv-table::
   :header: "Attribute", "OWL attribute", "Note"
   :widths: 20, 40, 60
	    
   "Exact synonym", "``oboInOwl:hasExactSynonym``", "See `Technical details <http://edamontologydocs.readthedocs.io/en/latest/technical_details.html#terms-and-synonyms>`_."
   "Narrow synonym", "``oboInOwl:hasNarrowSynonym``", "See `Technical details <http://edamontologydocs.readthedocs.io/en/latest/technical_details.html#terms-and-synonyms>`_."
   "Broad synonym", "``oboInOwl:hasBroadSynonym``", "See `Technical details <http://edamontologydocs.readthedocs.io/en/latest/technical_details.html#terms-and-synonyms>`_."
   "Comment", "``rdfs:comment``", "See `Editors Guide <http://edamontologydocs.readthedocs.io/en/latest/editors_guide.html#concepts-terms>`_."
   "Wikipedia", "``<documentation>``", "URL of Wikipedia page."


For **Operation** additions you **MAY** also specify:

.. csv-table::
   :header: "Attribute", "OWL attribute", "Note"

   "Top-level operation", "``rdfs:subClassOf``", "One of the Tier 1 operations (see `todo <>`_) *unless* this already subsumed adequately by the parent."

For **Format** additions you **SHOULD** also specify:

.. csv-table::
   :header: "Attribute", "OWL attribute", "Note"

   "Documentation", "``<documentation>``", "URL of documentation about the format."
   "Publication", "``<documentation>``", "DOI of publication about the format."   

For **Identifier** additions you **SHOULD** also specify:

.. csv-table::
   :header: "Attribute", "OWL attribute", "Note"

   "Regexp", "``<regex>``", "Regular expression pattern for identifier instances."
   "Documentation", "``<documentation>``", "URL of documentation about the identifier."




Hierarchy
.........
The following rules maintain the integrity of the conceptual hierarchy and ensure a consistent level of conceptual granularity.

- **All subontologies**

  - leaf nodes **MUST** be concrete concepts (see `Technical details <http://edamontologydocs.readthedocs.io/en/latest/technical_details.html#concept-types>`_)

- **Topic:**
  
  - **MUST** have a path to root of 4 levels deep maximum
  - **MUST NOT** have a path to root exceeding 5 levels deep
    
- **Operation:**

  - **MUST** ensure placeholders appear in Tiers 1 and 2 (usually) and 3 (rarely - in exceptional cases) only
  - **MUST NOT** chain more than 3 placeholders 
  - **MUST NOT** chain more than 3 concrete operations
  
- **Data:**

  - **MUST NOT** chain more than 2 placeholders 
  - **MUST NOT** chain more then 2 concrete data concepts
  - **MUST** ensure placeholders occur in Tier 1 (usually) and 2 (rarely) only

  
- **Identifier:**

  - **MUST NOT** chain more than 4 placeholders 
  - **MUST NOT** chain more than 2 concrete identifiers
  - **MUST** be related (via *is_identifier_of*) to a **Data** concept, but **MUST NOT** duplicate this annotation if it's already stated on an ancestor concept.   
  - concrete identifiers **MUST** descend (via ``subClassOf`` relations) from:

    - `Accession <http://edamontology.org/data_2091>`_ or `Name <http://edamontology.org/data_2099>`_  *and*
    - `Identifier (typed) <http://edamontology.org/data_0976>`_ (or its kids)

    but **MUST NOT** duplicate these annotations if already stated on an ancestor concept.

    Additionally, concrete identifier re-used for data objects of fundamentally different types (typically served from a single database) **MUST** descend from:

    - "Identifier (hybrid)" (http://edamontology.org/data_2109) may also be given.
    
- **Format:**

  - **MUST NOT** chain more than 4 placeholders 
  - **MUST NOT** chain more than 2 concrete identifiers
  - **MUST** be related (via *is_format_of*) to a **Format** concept, but **MUST NOT** duplicate this annotation if it's already stated on an ancestor concept.
  - **MUST** descend (via ``subClassOf``) concrete formats from *Textual format*, *Binary format*, *XML*, *HTML*, *JSON*, *RDF format* or *YAML*, but you **MUST NOT** duplicate this ancestry in format variants.  For example *FASTA-like (text)* is defined as a child of *Textual format*, but the kids of *FASTA-like (text)* format are not.
  - **MUST** descend (via ``subClassOf``) concrete formats from `Format (by type of data) <http://edamontology.org/format_2350>`_ (or it's kids), but again, you **MUST NOT** duplicate this ancestry in format variants.  For example *FASTA-like (text)* is defined as a child of *Sequence record format* -> *FASTA-like*, but the kids of *FASTA-like (text)* format are not.
  - **MUST NOT** add new placeholder concepts (kids of `Format (by type of data) <http://edamontology.org/format_2350>`_) unless there is a corresponding concrete data format descending from it.
  
If you add a concept which you expect to remain a leaf node, *i.e.* EDAM will not include finer-grained concepts, then - if other well-developed ontologies exist that serve this conceptual niche - you **SHOULD** annotate this junction (see `todo <>`_).




Deprecating concepts
^^^^^^^^^^^^^^^^^^^^ 
When deprecating concepts, you **MUST** specify the following:

.. csv-table::
   :header: "Attribute", "OWL attribute", "Note"

   "EDAM version", "``obsolete_since``", "Current version *e.g.* `1.21`"
   "Subset", "``oboInOwl:inSubset``", "Set this to ``obsolete`` (pick the value)"
   "Deprecation flag", "``owl:deprecated``", "Type the value of ``true``"
   "Replacement concept", "``oboInOwl:replacedBy``", "The alternative 'replacement' concept to firmly use. Pick one."
   "Replacement concept", "``oboInOwl:consider``", "Replacement concept when less certain.  Pick one."
   "Old parent", "``oldParent``", "Specify the URI(s) of the erstwhile parent(s) of the now-deprecated concept (using one or more attributes as needed)."
   "Comment", "``deprecation_comment``", "Optional comment as to why the concept is deprecated."
   "New parent", "``rdfs:subClassOf``", "Set the parent concept to be ``ObsoleteClass``"

Also:

1. **MUST** remove all other class annotations (subsets, comments, synonyms *etc.*) and axioms (including parent concepts)
2. **MUST** refactor all references (*e.g.* ``SubClassOf``) to the concept being deprectated from other concepts (you can see these using Protege)
3. **SHOULD** preserve comments and synonyms, as new annotations either in the old parent(s), or the replacement(s) of the deprecated concept, as appropriate.


.. note::
   You can see all references to a concept in Protege in the "Class Usage" window; each reference will need updating in turn: in case of very many such references, this can be easier to do globally in a text editor rather than Protege.

   
Use of Protege
^^^^^^^^^^^^^^
`Protege <https://protege.stanford.edu/>`_ is a nice OWL Editor, but has it's quirks, so it's recommended you first get a crash course from the `EDAM Developers <>`_ before using it.  A commercial alternative is `TopBraid Composer <https://www.topquadrant.com/tools/ide-topbraid-composer-maestro-edition/>`_.

Editing
.......

.. important::
   When editing EDAM using Protege:
   
   - URLs should be entered using the Protege IRI editor.
   - General text is entered using the Protege 'Constant" editor.
   - Subsets (``oboInOwl:inSubset`` annotation): you must pick (don't type!) an appropriate value.

   Don't mix this up, as it makes a mess of the RDF/XML!


Ensuring logical consistency
............................
Before committing changes, to ensure logical consistency of EDAM, please do the following within Protege:

1. Click *Reasoner->Hermit*
2. Click *Reasoner->Start reasoner* (it may take a few seconds)
3. In the *Entities* tab, select the *Class hierarchy (inferred) tab*
4. Select the *nothing* branch

If nothing (no classes) are shown under the *nothing* branch, then all is well.  If one or more classes are shown, then there is a logical inconsistency which must be fixed.  You might see lots of classes, but usually the problem is in one or a few classes.  

Common problems include:

- classes assigned as a ``subClass`` of some deprecated concept
- end-point of relations are in the wrong branch, *e.g.* `class has_topic some operation`.  These can easily occur if you use the *Class expression editor* in Protege to define such axioms: this is **NOT** EDAM namespace-aware, and in cases where a concept with the same primary label exists in both classes, can easily pick the wrong one.

The problems are easily fixed within Protege: ask on the `mailing list <>`_ if you're not sure how.

.. caution::
   Do not be tempted to click *Reasoner->Synchronise reasoner* between changes: it tends to hang Protege.  Instead, use *Reasoner->Stop reasoner* than *Reasoner->Start reasoner*.



EDAM release process
--------------------

Modifying GitHub main repo.
^^^^^^^^^^^^^^^^^^^^^^^^^^^
`EDAM Developers <http://edamontologydocs.readthedocs.io/en/latest/governance.html>`_ can edit the main repository.  The workflow is:

1. Get the "editing token" 

   - contact edam-dev@elixir-dk.org and claim the "editing token" after first checking that it is not currently taken :)
   - say briefly what you are doing, why, and about how long it will take

2. Update your local repo with the latest files from the GitHub master:

    ``git pull`` (or "Synch" from the Desktop client)
   
   If you've not already done so, you will first need to clone the master repo:

    ``git clone https://github.com/edamontology/edamontology.git`` (or "Clone" from the Desktop client)

3. Make and commit your local changes. You **must** be working with the "dev" version, ``EDAM_dev.owl``.
   
   - check your changes and that the OWL file looks good in Protege
   - ensure the ``next_id`` attribute is updated
   - ensure that ``oboOther:date`` is updated to the current GMT/BST before the commit
   - add the edited file to the commit
   
      ``git add <filepath>``
   - Commit your local changes, including a concise but complete summary of the major changes:
   
      ``git commit -m ¡±commit message here¡±``

4. Push your changes to the GitHub master:

    ``git push origin``

5. Release the editing token for the other developers:

   - contact edam-dev@elixir-dk.org and release the "editing token"
   - summarise what you actually did and why

.. important::    
   Please provide a **meaningful report** on changes so that we can easily generate the ChangeLog upon next release

   - in the Git commit message, including the GitHub issue number of any issues addressed (use ``fix #xxx`` syntax, see `GitHub docs <https://help.github.com/articles/closing-issues-via-commit-messages>`_)
   - directly in the `changelog.md <https://github.com/edamontology/edamontology/blob/master/changelog.md>`_


     
Creating a new official EDAM release
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

EDAM release schedule
.....................

From January 2016, EDAM tries to follow a bi-monthly release cycle to this schedule:

1.  First Wed of every month
   - EDAM team skype to discuss plans for this month.  Announcement (to edam-announcence) including short summary of plans, invitation for suggestions.
2.  Last Mon of every month
   - Announcement (to edam-announcence) saying that release is immiment, invitation for last-minute suggestions.
3.  Last Wed of every month
   - Complete the work for the release.  Make the release.  Ensure it works in BioPortal, OLS, AgroPortal and in bio.tools.
4.  Last Fri of every month
   -  Announcee the release, incuding summary of changes.

.. note::
   Releases have been quarterly but bi-monthly, even monthly remains the aspiration.  Please help out move faster by `getting involved <http://edamontologydocs.readthedocs.io/en/latest/getting_involved.html>`_.
      
Process
.......
Before creating a new release, please make sure you have the approval of leader of EDAM-dev, and that the `changelog.md <https://github.com/edamontology/edamontology/blob/master/changelog.md>`_ and `changelog-detailed.md <https://github.com/edamontology/edamontology/blob/master/changelog-detailed.md>`_ files are up-to-date with the changes of the new release.  See `Editing the ChangeLog <http://edamontologydocs.readthedocs.io/en/latest/developers_guide.html#editing-the-changelog>`_ below.  Once you're clear to go, do the following:

1. update your local version of the repository:

    ``git pull`` (or "Synch" in desktop client)
2. assuming you are releasing version n+1, n being the current version:

   - you initially have ``EDAM_dev.owl`` in the repository
   - make sure to update ``oboOther:date`` in this file
   - copy the file ``EDAM_dev.owl`` to ``releases/EDAM_n+1.owl``

     - ``cp EDAM\_dev.owl releases/EDAM_n+1.owl``
     - ``git add releases/EDAM\_n+1.owl``

   - modify the ``doap:version`` property to **n+1** in ``releases/EDAM_n+1.owl`` and to **n+2_dev** in ``EDAM_dev.owl``
   
3. commit and push your changes

    - ``git commit -a`` (or "Commit to master" in the desktop client)
    - ``git push origin`` (or "Synch" in the desktop client)

4. update the `detailed changelog <https://github.com/edamontology/edamontology/blob/master/changelog-detailed.md>`_ by running `Bubastis <http://www.ebi.ac.uk/efo/bubastis/>`_ to compare the release against the previous version.
5. update the `changelog <https://github.com/edamontology/edamontology/blob/master/changelog.md>`_ with a summary of the major changes.
6. create the release on GitHub (use the `_draft a new release_ <https://github.com/edamontology/edamontology/releases/new>`_ button of the `_releases_ <https://github.com/edamontology/edamontology/releases>`_ tab).
7. update http://edamontology.org.
8. submit this new release to BioPortal.  OLS will pull the file automatically from edamontology.org every night.
9. close GitHub issues labelled *done - staged for release*.
10. confirm everything is working in `bio.tools <http://bio.tools>`_ by mailing `bio.tools Lead Curator <mailto:hans@bio.tools>`_.
11. announce the new release on Twitter and mailing lists (edam-announce@elixir-dk.org, edam@elixir-dk.org) including thanks and a summary of changes.
12. help applications that implement EDAM to update to the new version.


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

  The Travis-CI website shows you the current status `here <https://travis-ci.org/edamontology/edamontology>`_. The fact that the continuous integration task succeeds does not guarantee there are no remaining bugs, but a failure means that you must take action to correct the problem, either fix it, fix the ``edamxpathvalidator`` program, or ask the mailing list if you're unsure.

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


