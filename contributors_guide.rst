Contributors Guide
==================
EDAM is a community project: everyone is encouraged to get involved.



Mailing lists
-------------
To find the most efficient way to contribute to EDAM, to get in help using EDAM for resource annotation and in software implementations, and for general discussions, mail:

edam@elixir-dk.org

We'll make every effort to be responsive, given our limited resources, and will work with you to find the most efficient way to proceed, depending on your requirements, expertise and bandwidth.  

To post or receive mail from the list above, subscribe here:

http://elixirmail.cbs.dtu.dk/mailman/listinfo/edam

For low-traffic announcements, subscribe here:

http://elixirmail.cbs.dtu.dk/mailman/listinfo/edam-announce


Requests
--------
Suggestions for addition, corrections, and other improvements to EDAM are always welcome! 

To suggest new concepts, please use the `GitHub tracker <https://github.com/edamontology/edamontology/issues/new>`_

Please specify for each concept:

- EDAM sub-ontology (Topic, Operation, Format, Data, Identifier)
- Term (the most common term used to refer to the concept)

It will speed up things a lot if you can also provide:

- short description (a couple of sentences)
- URL of suggested parent
- exact synonyms (other commonly-used terms, acronyms etc. by which the concept is referred to)
- narrow synonyms (terms reflecting specialisations of the concept.  Narrow synonyms can be defined to avoid creating overly-specialised concepts.)

If it turns out you need a lot of new concepts, we can find a more efficient way (*e.g.* shared Google sheet), and you can join us as an `EDAM Editor <http://edamontologydocs.readthedocs.io/en/latest/governance.html>`_

More specific guidelines for EDAM Format requests follow.

EDAM Format requests
^^^^^^^^^^^^^^^^^^^^

- **Format name:** Name of format, *e.g.* "PNG". This is the most commonly used term.  Do not prefix with "." unless the prefixed version e.g. ".nib" really is in prevalent use.  
- **Short description:** Short description, e.g. "PNG is a file format for image compression." A sentence or two describing the format, notably what type of data is used for.  See http://edamontology.org/format_1915 for examples.
- **Parent URI(s):** # URI(s) of suggested EDAM Format parent(s) delimited by pipe ('|') *e.g.* "http://edamontology.org/format_3547|http://edamontology.org/format_2333". Format concepts normally have two parents: 1) indicating the basic type *e.g.* "Binary format", "Textual format" *etc.* (see http://edamontology.org/format_1915) and 2) indicating the type of data *e.g.* "Image format" (see http://edamontology.org/format_2350)
- **exactSynonym(s):**.  Exact synonym(s) delimited by pipe ('|') *e.g.* "png". Other commonly-used terms, acronyms *etc.* by which the concept is referred to.  This can also include capitalisation variations (as in above example) and use of "." prefix. 
- **Specification/documentation:**.  URL(s) to formal specification or documentation delimited by pipe ('|') *e.g.* http://www.w3.org/TR/PNG/. Please provide a link to the official specification of the format (if available) and / or to the most pertinent documentation.
- **Data represented:**.  URI(s) of EDAM Data concept(s) the format represents delimited by pipe ('|') *e.g.* "http://edamontology.org/data_2968".  Please specify the EDAM Data concept(s) for the type(s) of data represented by the format.  If you are not sure, or if you can't find the Data concept you need, you can use free text *e.g.* "Image data" instead of the URI.
- **File extension(s):**.  File extension(s) in common use delimited by pipe ('|') *e.g.* "png". Please specify all file name extensions that are commonly used.
- **Media type:**  Media type *e.g.* "image/png". Specify the formal media type (if available) as per https://www.iana.org/assignments/media-types/media-types.xhtml
- **DOI:** Citation DOI or URL e.g. "https://www.iso.org/standard/29581.html". Specify a DOI of an article (if available) that describes the format, and should be used to cite mentions or usage of the format.  If a DOI is not available, a URL may be specified.




GitHub issue tracker (preferred)
--------------------------------
If you have a GitHub account, you can make requests by opening a GitHub issue:

- Go to https://github.com/edamontology/edamontology/issues and click on "New issue".
- If you are not logged in, you will be asked first to log in or create an account.
- Provide a title, and a report that is concise but sufficiently detailed to be actionable.

Suggestions form
----------------
Simple requests for one or a few changes can be made using this form:

http://tinyurl.com/EDAMChangeRequest 

If you require many changes and additions, there's probably a more efficient way to proceed: please contact edam@elixir-dk.org.  You'll need to `subscribe <http://elixirmail.cbs.dtu.dk/mailman/listinfo/edam>`_ to the list first.

Joining the team
----------------
We very much welcome you to join the EDAM team.  Please first read about the `Governance of EDAM <https://github.com/edamontology/edamontology#governance-of-edam>`_ to find the level that is right for you.  Then mail edam-dev@elixir-dk.org to get started. 

Hackathons
----------
EDAM developers participate in regular events, which you are welcome to attend.  For more details see https://bio.tools/events.
