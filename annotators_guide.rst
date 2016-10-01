Annotators Guide
================

Annotators may email the `EDAM mailing list <mailto:edam@elixir-dk.org>`_ or the `EDAM core developers <mailto:edam-core@elixir-dk.org>`_ for help.

General guidelines
------------------

Which EDAM sub-ontology to use?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1.  *"Topic"* for coarse-grained annotation of diverse entities
2.  *"Operation"* for fine-grained annotation of tool functions
3.  *"Data"* for annotation of data in semantic terms
4.  *"Format"* for annotation of the syntax or format of data
5.  *"Identifier"* (as a special type of *"Data"*) for annotation of identifiers (names and accessions) of data or other entities


EDAM provides different semantic 'axes' for annotation. For example, annotation of a software tool might include:

*   *Topic* - general scientific domain the software serves, *e.g.* *"Structural biology"*
*   *Operation* - the precise function of the tool, *e.g.* *"Homology modelling"*
*   *Data* - the primary input and output, *e.g.* *"Protein structure"*
*   *Format* - the supported format(s) of the input and output, *e.g.* *"PDB format"*


Use of other ontologies
^^^^^^^^^^^^^^^^^^^^^^^
The expectation is for EDAM to be used alongside other ontologies for annotation where possible and desirable. For example, an operation that predicts specific features of a molecular sequence could be annotated with concepts from SO (Sequence Ontology) for the features.

Picking concepts
^^^^^^^^^^^^^^^^
If you have many annotations to do, it will help to familiarise yourself with EDAM first using a `browser <http://edamontologydocs.readthedocs.io/en/latest/what_is_edam.html#browsing>`_ .

1.  Identify the correct sub-ontology (*"Operation"*, *"Data"* *etc.*) of concepts considering what is being annotated (see above)
2.  Search EDAM using keywords to find candidate concepts. Multiple searches using synonyms, alternative spellings and so are preferable.
3.  Pick the most specific concept(s) available, bearing in mind some concepts are necessarily overlapping or general.
4.  Only pick a correct concept. If it doesn't exist, request it's added to EDAM

Annotation of Web services
--------------------------

Model of a Web service
^^^^^^^^^^^^^^^^^^^^^^
A Web service is considered as an arbitrary (but usually related) set of one or more operations, reducing the problem of Web service interoperation to one of compatibility between operations.

**Operation**

*   Discrete unit of functionality performing (typically) one or more definite functions
*   Reads an input
*   Writes an output
*   Uses zero or more data resources

**Input**

*   Payload (*e.g.* of HTTP or SOAP message) passed in operation call
*   Name and (ideally) description is given (*e.g.* in WSDL file)
*   Input has one or more XML elements which must be set (input values)

**Output**

*   Payload (*e.g.* of HTTP or SOAP message) returned from operation call
*   Name and (ideally) description is given (*e.g.* in WSDL file)
*   Output has one or more XML elements which are written (output values)

**XML elements**

*   Correspond to the inputs (parameters) and outputs of a service
*   Are simple or complex XSD types given in an XML Schema (within or referenced from a WSDL file)
*   Have values that are instances of specific semantic type.
*   Have values in a specific syntax, either fully specified by the schema, or (occasionally) text in a specific file format which is not specified by the schema.

Levels of annotation
^^^^^^^^^^^^^^^^^^^^
Annotation of a WSDL file or associated XSD schema is possible at several levels. Assuming SAWSDL annotation (http://www.w3.org/TR/sawsdl/), the XML elements that may be annotated by EDAM concepts are:

1.  **Web service** (as a whole) (``<kbd><wsdl:portType></kbd>``)

    *   One (or more) *"Topic"* concepts to describe the general area(s) the service concerns
    *   If applicable, one (or more) *"Operation"* concepts to describe the functions of the service (if all operations peform essentially the same function)

2.  **Operation** (``<kbd><wsdl:operation></kbd``> inside ``<kbd><wsdl:portType></kbd>``)

    *   One (or more) *"Operation"* concepts for each WSDL operation (more than one in exceptional circumstances)
3.  **Input parameters and their sub-parts** (``<kbd><xs:element></kbd>``, ``<kbd><xs:complexType></kbd>``, ``<kbd><xs:simpleType></kbd>``, ``<kbd><xs:attribute></kbd>``)
    *   One (or more) *"Data"* concepts
    *   One (or more) *"Format"* concepts

4.  **Output parameters and their sub-parts** (``<kbd><xs:element></kbd>``, ``<kbd><xs:complexType></kbd>``, ``<kbd><xs:simpleType></kbd>``, ``<kbd><xs:attribute></kbd>``)

    *   One (or more) *"Data"* concepts
    *   One (or more) *"Format"* concepts

*NB.* The input and output parameters should be annotated inside the XML Schema that defines them. In case of services that are not following the highly recommended *document/literal wrapped* SOAP-binding style, the ``<kbd><wsdl:part></kbd>`` inside ``<kbd><wsdl:message></kbd>`` can be annotated (the same applies to *faults*, but meanings of faults are not modelled by EDAM)

The following annotations might be useful but are not directly recommended by SAWSDL:

1.  **Enumerated values of input/output parameters** (``<kbd><xs:enumeration></kbd>``)

    *   One (or more) *"Format"* or *"Data"* concepts defining the particular enumerated value

For details of incorporating the SAWSDL annotations into WSDLs and XSDs, see below.

EDAM URIs and SAWSDL annotation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
SAWSDL mandates the use of (``<kbd>sawsdl:modelReference</kbd>``) attributes for annotation. The format of EDAM URIs used inside this attribute includes the ontology name (*http://edamontology.org*), main sub-ontology, and the unique identifier (ID) of the particular concept:

.. code-block:: xml

 <xmp> 
 <xs:element name="elementName" sawsdl:modelReference="http://edamontology.org/subontology_id">
 </xmp>


Where ...

*   ``<kbd>xs:element</kbd>`` is the XML element being annotated (can be also ``<kbd>xs:attribute</kbd>``, ``<kbd>xs:complexType</kbd>``, ``<kbd>xs:simpleType</kbd>``, ``<kbd>sawsdl:attrExtension</kbd>``, ``<kbd>wsdl:portType</kbd>``, in special cases ``<kbd>wsdl:part</kbd>``, or eventually ``<kbd>xs:enumeration</kbd>``)
*   ``<kbd>elementName</kbd>`` is the name of the XML element

The value of the ``<kbd>sawsdl:modelReference</kbd>`` attribute is a URI pointing to the concept definition. The URI to use is in case of EDAM includes the concept's sub-ontology:

*   ``<kbd>sub-ontology</kbd>`` is the **top-level sub-ontology** of the EDAM concept; one of ``<kbd>topic</kbd>``, ``<kbd>data</kbd>``, ``<kbd>format</kbd>``, or ``<kbd>operation</kbd>``
*   ``<kbd>id</kbd>`` is the unique local identifier of the concept, *e.g.* ``<kbd>"0295"</kbd>``

So for these 3 concepts:

.. code-block:: xml

 <xmp>
 EDAM_topic:0182
 EDAM_operation:0292
 EDAM_data:0863
 </xmp>

We'd have

.. code-block:: xml

 <xmp>
 http://edamontology.org/topic_0182
 http://edamontology.org/operation_0292
 http://edamontology.org/data_0863
 </xmp>

Which can be used in SAWSDL annotation, *e.g.*

.. code-block:: xml

 <xmp>
 <wsdl:portType name="myService" sawsdl:modelReference="http://edamontology.org/topic_0182">
 <sawsdl:attrExtension sawsdl:modelReference="http://edamontology.org/operation_0292>
 <xs:element name="outfile" sawsdl:modelReference="http://edamontology.org/data_0863>
 </xmp>

If more than one annotation of an element is required, these can be given in the ``<kbd>sawsdl:modelReference</kbd>`` attribute delimited by space characters:

.. code-block:: xml

 <xmp><wsdl:portType name="myService" sawsdl:modelReference="http://edamontology.org/topic_0182 http://edamontology.org/operation_0292">
 </xmp>

*NB.* Such multiple annotations need not be in the same namespace, and need not at all to refer to the same ontology.

SAWSDL guidelines for annotating operations
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
One peculiarity of the SAWSDL specification is that annotations on ``<wsdl:operation>`` element inside ``<wsdl:portType>`` should be handled using a ``<sawsdl:attrExtensions>`` element. This is not a requirement for other elements.

Importantly, the ``<sawsdl:attrExtension>`` element inside the wsdl:operation **must be before** ``<wsdl:input>``, ``<wsdl:output>`` and ``<wsdl:fault>`` elements (so typically after the ``<wsdl:documentation>`` element).

For example:

.. code-block:: xml

 <xmp> <wsdl:portType name="Clustalw2PortType" sawsdl:modelReference="http://edamontology.org/topic_0186 http://edamontology.org/operation_0496">
  <wsdl:operation name="submitClustalw2">
  <wsdl:documentation>Submit a sequence and get a jobID</wsdl:documentation>
  <sawsdl:attrExtensions sawsdl:modelReference="http://edamontology.org/operation_0496"/>
  <wsdl:input message="submitClustalw2Msg"/>
  <wsdl:output message="submitClustalw2ResponseMsg"/>
  </wsdl:operation>
 </xmp>

Some WSDL/XSD validators or SOAP libraries do not check for it, but some do require the strict order of these elements.
