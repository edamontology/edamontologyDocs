Developers Guide
================

.. caution::
   **UNDER CONSTRUCTION**
   This document is undergoing heavy edits right now ... you may want to come back in a few days!

   
If you're not sure how to do something please ask edam@elixir-dk.org.  You'll need to `subscribe <http://elixirmail.cbs.dtu.dk/mailman/listinfo/edam>`_ to the list first.



Technical recipes
-----------------


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
When adding new concepts, you **MUST** specify the following (attributes are in parenthesis):


   

.. csv-table::
   :header: "Attribute", "OWL attribute", "Note"
   :widths: 20, 40, 60
   
   "Concept URI"   , "``rdf:about`` "            , "In the right namespace and with the latest numerical ID."
   "Primary term"  , "``rdfs:label``"            , "See `todo <>`_."
   "Definition"    , "``oboInOwl:hasDefinition``", "See `todo <>`_."
   "Parent(s")     , "``rdfs:subClassOf``"       , "See `todo <>`_."
   "Version"       , "``created_in``"            , "Current EDAM dev version, *e.g.* ``1.21``."
   "'edam' subset" , "``oboInOwl:inSubset``"     , "Always ``edam``."
   "Branch subset" , "``oboInOwl:inSubset``"     , "One of ``topic``, ``data``, ``format`` or ``operation``."
   "Type subset"   , "``oboInOwl:inSubset``"     , "One of ``concrete`` or ``placeholder``."
   "Next ID"       , "``<next_id>``"             , "Increment the current count by 1."

For **Format** additions you **MUST** also specify:

.. csv-table::
   :header: "Attribute", "OWL attribute", "Note"
   :widths: 20, 40, 60
	    
   "Type of data"  , "``<is_format_of>``"        , "See `todo <>`_."
   "Specification" , "``<documentation>``"       , "URL of format specification.  See `todo <>`_."


For **Identifier** additions you **MUST** also specify:

.. csv-table::
   :header: "Attribute", "OWL attribute", "Note"
   :widths: 20, 40, 60
	    
   "Type of data"  , "``<is_identifier_of>``"    , "See `todo <>`_."

  

Optional attributes
...................

.. csv-table::
   :header: "Attribute", "OWL attribute", "Note"
   :widths: 20, 40, 60
	    
   "Exact synonym"  , "``oboInOwl:hasExactSynonym``", "See `todo <>`_."
   "Narrow synonym" , "``oboInOwl:hasNarrowSynonym``, "See `todo <>`_."
   "Broad synonym"  , "``oboInOwl:hasBroadSynonym``", "See `todo <>`_."
   "Comment"        , "``rdfs:comment``"            , "See `todo <>`_."
   "Wikipedia"      , "``<documentation>``"         , "URL of Wikipedia page.  See `todo <>`_."

   
For **Format** additions you **SHOULD** also specify:

.. csv-table::
   :header: "Attribute", "OWL attribute", "Note"
	    
   "Type of data"  , "``<is_format_of>``"        , "Applicable **Data** concept. See `todo <>`_."



For **Identifier** additions you **SHOULD** also specify:

.. csv-table::
   :header: "Attribute", "OWL attribute", "Note"

   "Regexp"        , "``<regex>``"    , "Regular expression pattern for identifier instances. See `todo <>`_."

   

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


Use of Protege
^^^^^^^^^^^^^^
`Protege <https://protege.stanford.edu/>`_ is a nice OWL Editor, but has it's quirks, so it's recommended you first get a crash course from the `EDAM Developers <>`_ before using it.  A commercial alternative is `TopBraid Composer <https://www.topquadrant.com/tools/ide-topbraid-composer-maestro-edition/>`_.

Editing
.......


.. important::
   When using Protege
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
   
      ``git commit -m ¡±commit message here¡±``

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


