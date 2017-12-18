---

copyright:
  years: 2015, 2017
lastupdated: "2017-12-11"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

This documentation is for {{site.data.keyword.knowledgestudiofull}} on {{site.data.keyword.cloud}}. To see the documentation for the previous version of {{site.data.keyword.knowledgestudioshort}} on {{site.data.keyword.IBM_notm}} Marketplace, [click this link ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/docs/services/knowledge-studio/preannotation.html){: new_window}.
{: tip}

# Bootstrapping annotation
{: #preannotation}

Simplify the job of the human annotator by pre-annotating the documents in a workspace. A pre-annotator is an {{site.data.keyword.knowledgestudiofull}} dictionary-, rule-base, or machine learning-based annotator component that you can run to find and annotate mentions automatically.
{: shortdesc}

Pre-annotation makes the job of human annotators easier because it covers the straight-forward annotations, and gets the job of annotating the documents underway.

The method that you use to pre-annotate documents in no way restricts the ways that you can use the resulting model. For example, just because you use the {{site.data.keyword.alchemylanguageshort}} service to pre-annotate documents does not mean you must deploy the final machine-learning model that you build to the {{site.data.keyword.alchemylanguageshort}} service. Pre-annotation is solely meant to bootstrap the human annotation process.

## Important notes

- Never run a pre-annotator on documents that human annotators have annotated because the annotations added by the human annotators will be removed.
- You can run one pre-annotator on documents only. If you run one pre-annotator, and then run a second pre-annotator, the second run will strip the annotations that were added by the first pre-annotator from the documents. Pick the pre-annotation method that best fits your use case, and use that one only.

## Pre-annotation methods

The following pre-annotators are available:

- **{{site.data.keyword.alchemylanguageshort}}**

    Powerful pre-annotator that uses a private knowledge base that was built from a vast amount of web-crawled data to recognize mentions of common entities. Because its source data is public web sites, it is good at recognizing entities in general knowledge areas. If your source documents have general knowledge subject matter, then this pre-annotator is a good choice for you. If you are working with highly specialized documents that focus on a specific field, such as patent law research, for example, the dictionary pre-annotator or rule annotator might be a better choice.
    >Note: The {{site.data.keyword.alchemylanguageshort}} service has been deprecated. This pre-annotator might not be listed as an annotator component option.

- **Dictionary**

    Uses a dictionary of terms that you provide and associate with an entity type to find mentions of that entity type in the documents. This choice is best for fields with unique or specialized terminology because this pre-annotator does not analyze the context in which the term is used in the way a machine-learning pre-annotator does; it instead relies on the term being distinct enough to have a decipherable meaning regardless of the context in which it is used. For example, it is easier to recognize *asbestos* as a mineral entity type than to determine the entity type of *squash*, which can refer to a vegetable, a sport, or a verb meaning to crush something.

- **Machine-learning**

    Uses a machine-learning model to automatically annotate documents. This option is only available to you if you have created a machine learning model with {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} already. If you add a new document set, you can run the machine-learning annotator that you created previously to pre-annotate the new documents. If the new set of documents are similar to the documents that were used to train the machine-learning annotator originally, then this is probably your best choice for pre-annotation.

- **Rule**

    Uses a rule-based model to automatically annotate documents. This option is only available if you have created a rule-based model with {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} already. If your documents contain common patterns of tokens from which you can derive meaning, this model might be a good choice. It can incorporate some of the function of the dictionary pre-annotator if you enable it, by identifying class types for dictionary terms that it finds in the documents also.

Alternatively, you can import already-annotated documents, and use them to start training the machine-learning model. You cannot run a pre-annotator on annotated documents that you import or the existing annotations will be stripped from the documents and replaced with annotations produced by the pre-annotator only.

> **Note:** You *can* run a pre-annotator on documents that were added to the ground truth as part of the current workspace. Annotations that were added to the documents, reviewed, accepted, and promoted to ground truth within the current workspace are not stripped out.

## Pre-annotating documents with IBM Watson AlchemyLanguage
{: #wks_preannotalchemy}

You can use the {{site.data.keyword.alchemylanguageshort}} service to pre-annotate documents that you add to your corpus.
>Note: The {{site.data.keyword.alchemylanguageshort}} service has been deprecated. This pre-annotator might not be available for use.

### Before you begin

Determine whether the {{site.data.keyword.alchemylanguageshort}} pre-annotator is likely to add value for your use case. Review the entity types that are recognized by {{site.data.keyword.alchemylanguageshort}}. To see a list, log in as a {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} administrator and open the **Annotator Component** page. On the {{site.data.keyword.alchemylanguageshort}} tile, click **Create this type of pre-annotator**. Review the list of supported {{site.data.keyword.alchemylanguageshort}} entity types to determine if there is a natural overlap between them and the types in your type system. If so, continue with this procedure. If not, choose a different pre-annotator to use.

### About this task

{{site.data.keyword.alchemylanguageshort}} is a collection of APIs that offer text analysis through natural language processing. When you use the {{site.data.keyword.alchemylanguageshort}} pre-annotator, it calls the {{site.data.keyword.alchemylanguageshort}} entity extraction service to find and annotate entities in your documents.

You must specify the entity types that you want the service to look for by mapping the {{site.data.keyword.alchemylanguageshort}} entity types that you want to find and annotate to corresponding {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} entity types that you have added to the {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} type system. Only mentions of entity types that you map will be found and annotated. You can review the entity types that the {{site.data.keyword.alchemylanguageshort}} service recognizes by reviewing the list that is displayed in the {{site.data.keyword.alchemylanguageshort}} Type Matching page, which is displayed when you perform the following procedure.

> **Note:** You cannot use the {{site.data.keyword.alchemylanguageshort}} pre-annotator on documents that are written in Arabic, Japanese, or Korean, because those languages are not currently supported by the {{site.data.keyword.alchemylanguageshort}} entity extraction service.

### Procedure

To use the {{site.data.keyword.alchemylanguageshort}} service to pre-annotate documents, complete the following steps:

1. Log in as a {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} administrator and open the **Annotator Component** page.
1. Under the **{{site.data.keyword.alchemylanguageshort}}** pre-annotator type, click **Create this type of pre-annotator**.
1. Map entity types that you defined in the {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} type system to corresponding {{site.data.keyword.alchemylanguageshort}} entity types.

    - The drop-down list of the **{{site.data.keyword.alchemylanguageshort}}** Entity Type field is pre-populated with entity types that are recognized by the {{site.data.keyword.alchemylanguageshort}} entity extraction service.
    - You must map at least one entity type.
    - You cannot map an {{site.data.keyword.alchemylanguageshort}} entity type to a {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} entity role, only {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} entity types.
    - You can map more than one {{site.data.keyword.alchemylanguageshort}} entity type to a single {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} entity type, or the other way around. For example, the following mappings are permitted:

    <table cellpadding="4" cellspacing="0" summary="Sample mapping of entity types" border="1" class="simpletable"><tr class="sthead"><th valign="bottom" align="left" id="d20428e292" class="stentry thleft thbot">Watson Knowledge Studio Entity Type</th>
        <th valign="bottom" align="left" id="d20428e298" class="stentry thleft thbot">AlchemyLanguage Entity Type</th>
      </tr>
      <tr class="strow"><td valign="top" headers="d20428e292" class="stentry"><ul class="ul bullets"><li class="li"><p class="p wrapper">ENGINEER</p></li>
            <li class="li"><p class="p wrapper">SCIENTIST</p></li>
          </ul>
        </td>
        <td valign="top" headers="d20428e298" class="stentry"><p class="p wrapper">Person</p></td>
      </tr>
      <tr class="strow"><td valign="top" headers="d20428e292" class="stentry"><p class="p wrapper">LOCATION</p></td>
        <td valign="top" headers="d20428e298" class="stentry"><ul class="ul bullets"><li class="li"><p class="p wrapper">City</p></li>
            <li class="li"><p class="p wrapper">Country</p></li>
          </ul>
        </td>
      </tr>
    </table>
    {: #wks_preannotalchemy__datasimpletable_cm1_y3g_fx}

1. After mapping all of the entity types that you want to capture, click **Create** &gt; **Create &amp; Run** to run the pre-annotator.

    The **Run** option is not available until you map at least one entity type.

1. Select the check box for each document set that you want to pre-annotate.

    If you are running this pre-annotator for the first time, first validate that the pre-annotator can find mentions of the mapped entities as expected. Create one document set that contains a representative document or documents from each distinct data source.
    {: tip}

1. Click **Run**.

    If you are doing a validation check of the pre-annotator, then open the annotated documents and review the annotations that were added. Make sure a sufficient number of accurate annotations were created. If the annotations are accurate, then you can run the annotator again on more and larger document sets. If the annotations are not accurate, then consider mapping different {{site.data.keyword.alchemylanguageshort}} entity types to your types. If the types do not naturally overlap, then the {{site.data.keyword.alchemylanguageshort}} pre-annotator is not the best pre-annotator for you to use.

    Pre-annotation is applied to individual documents without regard for the various document sets that a document might belong to. A document that overlaps between a selected document set and an unselected document will appear pre-annotated in both document sets.

1. After you run the pre-annotator once, you can click **Run** any time that you want to use it to pre-annotate additional document sets that you add to the corpus.

    > **Restriction:** If you edit the type mapping definition of the {{site.data.keyword.alchemylanguageshort}} pre-annotator, then you must re-create annotation tasks that include the pre-annotated document sets. Pre-annotation based on the changes that you make to the pre-annotator mapping definition cannot be applied to document sets that are already assigned to an annotation task.

### Results
{: #wks_preannotalchemy__export-warning}

Ground truth that is produced by documents that were pre-annotated by the {{site.data.keyword.alchemylanguageshort}} service cannot be used directly outside of {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}}. You can export the ground truth (in non-readable form) to move it from one {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} workspace to another. And you can continue to develop the ground truth and use it to build a machine-learning or rule-based model that can be deployed for use in services outside of the {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} tool.

> **Restriction:** Only documents that were pre-annotated with {{site.data.keyword.alchemylanguageshort}} are obscured into a non-readable format at export time. But, all annotations in those documents are obscured, including annotations that were added to the documents by human annotators.

**Related information**:

[http://www.ibm.com/watson/developercloud/alchemy-language.html ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/watson/developercloud/alchemy-language.html){: new_window}

## Pre-annotating documents with the Dictionary pre-annotator
{: #wks_preannot}

To help human annotators get started with their annotation tasks, you can create a Dictionary pre-annotator to pre-annotate documents that you add to the corpus.

### About this task

When a human annotator begins work on documents that were pre-annotated, it is likely that a number of mentions will already be marked by entity types based on the dictionary entries. The human annotator can change or remove the pre-annotated entity types and assign entity types to unannotated mentions. Pre-annotation by a Dictionary annotator does not annotate relations and coreferences; human annotators must manually assign these types of annotations.

### Procedure

To create a Dictionary annotator and pre-annotate documents:

1. Log in as a {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} administrator or project manager and open the **Annotator Component** page.
1. Under the **Dictionary** annotator type, click **Create this type of pre-annotator**.
1. Associate the dictionaries that you want the pre-annotator to use with the entity type of the dictionary entries.

    The pre-annotator uses the type information of dictionary terms to find mentions of the entity type and annotate them.
    1. Find the entity type that you want to associate with a dictionary, and then click **Edit**.
    1. Choose a dictionary from the drop-down menu.
    1. Click the plus sign (+) to add it.
    1. Repeat the previous steps to associate more dictionaries with the entity type.

1. Click **Create** &gt; **Create &amp; Run** .
1. Select the check box for each document set that you want to pre-annotate and click **Run**.

    Pre-annotation is applied to individual documents without regard for the various document or annotation sets that a document might belong to. A document that overlaps between a selected document set and an unselected document set will appear pre-annotated in both sets.

1. After the Dictionary annotator is created, click **Run** any time that you want to use it to pre-annotate additional document sets that you add to the corpus.

    > **Restriction:** If you edit the Dictionary annotator to add or remove dictionaries, you must re-create annotation tasks that include the pre-annotated document sets. Pre-annotation based on the changes that you make to the Dictionary annotator cannot be applied to annotation sets that are already assigned to an annotation task.

**Related concepts**:

[Dictionaries](/docs/services/watson-knowledge-studio/dictionaries.html#wks_dictionaries)

## Pre-annotating documents with a machine-learning annotator
{: #wks_preannotsire}

You can use an existing machine-learning annotator to pre-annotate documents that you add to your corpus.

### About this task

After 10 to 30 documents are annotated, a machine-learning model can be trained on the data. Such a minimally-trained model should not be used in a production, but can be used as a pre-annotation model that can help speed up the human annotation of subsequent documents. For example, if you add documents to the corpus after you train a machine-learning annotator, you can use the trained annotator to pre-annotate the new document sets. Never run a pre-annotator on the same documents that have been annotated by a person; it removes the human annotation.

### Procedure

To use an existing machine-learning annotator to pre-annotate documents:

1. Log in as a {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} administrator and open the **Annotator Component** page.
1. In the **Machine Learning** annotator area, select the document sets that you added to the corpus and click **Run** to start the pre-annotation process. You don't need to select the existing document sets because these documents have already been annotated by human annotators.
1. After pre-annotation is completed, open the **Human Annotation** page. Create a new task and assign the new document sets to human annotators. Human annotation should require much less time because the machine-learning annotator applied annotations based on the learning it acquired through training.
1. After human annotators complete their work, approve and adjudicate the document sets, as usual.
1. On the **Annotator Component** page, click **Details** to view machine-learning annotator details. On the Training/Test/Blind page, click **Edit Sets** and ensure that the document sets that you added are included in the data that you use to train the annotator component.

    Initially, a typical goal is to improve the machine-learning annotator by adding more training data. In this case, add the new document sets to the Training set. In future iterations, also add new document sets to the Test set and Blind set. See [Document set management](/docs/services/watson-knowledge-studio/improve-ml.html#wks_mamanagedata) for more information.
    {: tip}

1. Click **Train** to re-train the machine-learning annotator, or click **Train &amp; Evaluate** to re-train and evaluate the performance results.

## Pre-annotating documents with the rule annotator
{: #wks_preannotrule}

You can use the rule annotator that you built to pre-annotate documents that you add to your corpus.

### Procedure

To use the rule annotator to pre-annotate documents, complete the following steps:

1. Log in as a {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} administrator and open the **Annotator Component** page.
1. Under the **Rule** annotator type, click **Create this type of annotator**.
1. Map entity types that you defined in the {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} type system to one or more Rule annotator classes.

    - The drop-down list of the Class field is pre-populated with classes that are associated with the Rule annotator.
    - You must map at least one entity type to a class.

1. After mapping all of the entity types that you want to capture, click **Create** &gt; **Create &amp; Run** to pre-annotate the documents with the rule annotator.

    The **Run** option is not available until you map at least one entity type to a class.

1. Select the check box for each document set that you want to pre-annotate.
1. Click **Run**.

    Pre-annotation is applied to individual documents without regard for the various document sets that a document might belong to. A document that overlaps between a selected document set and an unselected document will appear pre-annotated in both document sets.

1. After you run the pre-annotator once, you can click **Run** any time that you want to use it to pre-annotate additional document sets that you add to the corpus.

    > **Restriction:** If you edit the entity type-to-class mapping of the rule annotator, then you must re-create annotation tasks that include the pre-annotated document sets. Pre-annotation based on the changes that you make to the pre-annotator mapping definition cannot be applied to document sets that are already assigned to an annotation task.

## Importing pre-annotated documents
{: #wks_uima}

You can jump-start the training of your annotator component by importing documents that were pre-annotated through an Unstructured Information Management Architecture ( UIMA ) analysis engine.

The pre-annotated documents must be in the XMI serialization form of UIMA Common Analysis Structure ( UIMA CAS XMI). The ZIP file that you import must include the UIMA TypeSystem descriptor file and a file that maps the UIMA types to entity types in your {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} type system.

UIMA CAS XMI is a standard format of Apache UIMA. Guidelines are provided for how to create files in the correct format from analyzed collections in {{site.data.keyword.IBM_notm}} {{site.data.keyword.watson}}&trade; Explorer. If you use another Apache UIMA implementation, adapt these guidelines for your purposes. Regardless of how you create the XMI files, the requirements for creating the type system mapping file and ZIP file are the same for everyone.

If you assign the imported documents to human annotators, the documents appear pre-annotated in the Ground Truth Editor and a number of mentions might already be annotated. The human annotator thus has more time to focus on applying the annotation guidelines to unmarked mentions. Alternatively, you can bypass the human annotation step and use the pre-annotated documents to immediately start training and evaluating a machine-learning annotator.

### Exporting analyzed documents from Watson Explorer Content Analytics
{: #wks_uimawexca}

You can export documents that were crawled and analyzed in {{site.data.keyword.IBM_notm}} {{site.data.keyword.watson}} Explorer Content Analytics , and import the analyzed documents as XMI files into a {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} workspace.

#### Procedure

To get analyzed documents from a {{site.data.keyword.watson}} Explorer Content Analytics collection:

1. Open the Content Analytics administration console in a web browser.
1. On the Collections view, expand the collection that you want to export documents from. In the Parse and Index pane, ensure that the parse and index process is running, and then click the arrow icon for **Export analyzed document content and metadata**.
1. In the **Analyzed document export options** area, select **Export documents as XML files**, select the **Enable CAS as XMI format export** check box, specify the output path for where the exported data is to be written, and click **OK**.
1. Stop and restart the parse and index services for the collection, and then do one of the following steps:

    - If the collection already contains indexed documents that you want to use for training the machine-learning annotator in the document cache, restart a full index build.
    - If the collection does not contain indexed documents that you want to use for training the machine-learning annotator, import documents, configure at least one crawler to crawl the documents, and start the crawler.

1. In the **Export** area, check the status of the export request. The progress indicates how many documents are exported.
1. Go to the output folder that you specified when you configured export options. When documents are exported as XML files, the output folder name is based on the time stamp when the export occurs. The output folder contains XMI files (`*.xmi`) and the UIMA TypeSystem descriptor file (`exported_typesystem.xml`).

#### What to do next
{: #wks_uimawexca__preUIMAimport}

You must define a mapping between the UIMA types and {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} entity types. You must also create a ZIP file that contains all of the files that are required to import the analyzed data into a {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} workspace.

**Related information**:

[Exporting crawled or analyzed documents ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/support/knowledgecenter/SS8NLW_11.0.0/com.ibm.discovery.es.ad.doc/iiysatexportca.htm){: new_window}

[Output paths for exported documents ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/support/knowledgecenter/SS8NLW_11.0.0/com.ibm.discovery.es.ad.doc/iiysaexportoutput.htm){: new_window}

### Exporting an analyzed collection from Content Analytics Studio
{: #wks_uimawexstudio}

You can export a collection of analyzed documents from {{site.data.keyword.IBM_notm}} {{site.data.keyword.watson}} Explorer Content Analytics Studio , and import the analyzed documents as XMI files into a {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} project.

#### Procedure

To get analyzed documents from a Content Analytics Studio collection:

1. Launch Content Analytics Studio and open the Studio project.
1. Right-click a folder that contains documents that you want to use for training a machine-learning annotator and select **Analyze Collection**.
1. Select a UIMA pipeline configuration file.
1. Go to the Collection Analysis view and click the **Save** icon in the Collection Analysis view. Specify the folder where the saved results are to be written and specify the file name.
1. Open the folder that you specified. The file extension of the saved file is `.annotations`.
1. Copy the `.annotations` file to your local file system and rename the file extension from `.annotations` to `.zip`.
1. Extract all files from the ZIP file. The extracted contents include XMI files (`*.xmi`), the UIMA TypeSystem descriptor file (`TypeSystem.xml`), and other files.

#### What to do next

You must define a mapping between the UIMA types and {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} entity types. You must also create a ZIP file that contains all of the files that are required to import the analyzed data into a {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} workspace.

### Mapping UIMA types to entity types
{: #wks_uimawexmap}

Before you import XMI files into a {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} workspace, you must define mappings between the UIMA types and {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} entity types.

#### Before you begin

The type system in your {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} workspace must include the entity types that you want to map the UIMA types to.

#### Procedure

To map UIMA types to {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} entity types:

1. Create a file named `cas2di.tsv` in the folder that contains the UIMA TypeSystem descriptor file, such as `exported_typesystem.xml` or `TypeSystem.xml`.
1. Open the `cas2di.tsv` file with a text editor. Each line in the file specifies a single mapping. The format of the mapping depends on which annotator's annotations you want to map:

    - You can create mappings by using the basic format:

        `UIMA_Type_Name[TAB]WKS_Entity_Type`

        The following example defines mappings between UIMA types produced by the Named Entity Recognition annotator in {{site.data.keyword.IBM_notm}} {{site.data.keyword.watson}} Explorer Content Analytics and entity types defined in a {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} type system:

        ```
        com.ibm.langware.Organization  ORGANIZATION
        com.ibm.langware.Person  PERSON
        com.ibm.langware.Location  LOCATION
        ```
        {: screen}

        Another example defines a mapping between UIMA types produced by custom annotator that was created in {{site.data.keyword.IBM_notm}} {{site.data.keyword.watson}} Explorer Content Analytics Studio and {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} entity types:

        ```
        com.ibm.Person  PERSON
        com.ibm.Date  DATE
        ```
        {: screen}

    - You can create mappings based on facets that are used in the Pattern Matcher annotator or Dictionary Lookup annotator in {{site.data.keyword.watson}} Explorer Content Analytics. In text analysis rule files (`*.pat`), the facet is represented as the category attribute. To define a mapping, use the following syntax:

        ```
        com.ibm.takmi.nlp.annotation_type.ContiguousContext:category={FACET_PATH}[TAB]{WKS_ENTITY_TYPE}
        ```
        {: screen}

        The following example, which applies to the Pattern Matcher and Dictionary Lookup annotators, defines a mapping between the category $.mykeyword.product and the {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} entity type PRODUCT:

        ```
        com.ibm.takmi.nlp.annotation_type.ContiguousContext:category=$.mykeyword.product PRODUCT
        ```
        {: screen}

#### What to do next

You must create a ZIP file that contains all of the files that are required to import the analyzed data into a {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} workspace.

**Related information**:

[Pattern Matcher annotator ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/support/knowledgecenter/SS8NLW_11.0.0/com.ibm.discovery.es.ta.doc/iiystapattmatch.htm){: new_window}

[Dictionary Lookup annotator ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/support/knowledgecenter/SS8NLW_11.0.0/com.ibm.discovery.es.ta.doc/iiystadictlookup.htm){: new_window}

[Named Entity Recognition annotator ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/support/knowledgecenter/SS8NLW_11.0.0/com.ibm.discovery.es.ta.doc/iiystasystemt.htm){: new_window}

### Importing UIMA CAS XMI files into a workspace
{: #wks_uimaweximport}

To use the pre-annotated documents that you exported to train an annotator component, you must create a ZIP file that contains all of the files required to import the XMI files, and then import the ZIP file into a {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} workspace.

#### Before you begin

Before you import the ZIP file, ensure that the type system in your {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} workspace includes the entity types that you mapped the UIMA types to.

> **Warning:** UIMA analysis engines allow annotations to span sentences. In {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} , annotations must exist within the boundaries of a single sentence. If the XMI files that you import include annotations that span sentences, those annotations do not appear in the Ground Truth Editor.

#### Procedure

To import pre-annotated documents into a {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} workspace:

1. Create a ZIP file that contains all of the files that are required by {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}}.

    1. Select the folder that contains the XMI files, UIMA type system descriptor file, and `cas2di.tsv` file, or select all of the files in the folder.
    1. Create a ZIP file that includes all files. Make sure the `cas2di.tsv` and UIMA type system descriptor files are stored in the root directory of the ZIP file. These files cannot be stored in a subfolder within the ZIP file or {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} will not be able to read them, and nothing will be imported.

        In Windows, you can right-click and select **Send to** &gt; **Compressed (zipped) folder** .

1. Import the ZIP file into a {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} workspace.

    1. Log in as a {{site.data.keyword.watson}} {{site.data.keyword.knowledgestudioshort}} administrator or project manager, open the workspace that you want to add the documents to, and open the **Documents** page.
    1. Click the icon to add documents to the corpus.
    1. Drag the ZIP file that you created or click to locate and select the file.
    1. Select the check box to indicate that the ZIP file contains UIMA CAS XMI files.
    1. Click **Import**.

