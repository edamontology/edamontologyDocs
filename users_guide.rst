Users Guide
===========

EDAM provides different semantic 'axes' for annotation. For example, annotation of a software tool might include:

- **Topic** - general scientific domain the software serves, *e.g.* *"Structural biology"*
- **Operation** - the precise function of the tool, *e.g.* "*Homology modelling*"
- **Data** - the primary input and output, *e.g.* "*Protein structure*"
- **Format** - the supported format(s) of the input and output, *e.g.* "*PDB format*"


The edamontology.org site provides content negotiation with respect to the desired media type (*i.e.* format ``HTML`` or ``OWL`` currently). This applies also to the URIs of EDAM concepts that are in this way dereferencable, concise, and stable. Alternatively to requesting the format in the HTTP header, users can retrieve the desired content from a web browser by inserting ``?format=\<desiredformat\>`` query into the URL.
