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

This documentation is for {{site.data.keyword.knowledgestudiofull}} on {{site.data.keyword.cloud}}. To see the documentation for the previous version of {{site.data.keyword.knowledgestudioshort}} on {{site.data.keyword.IBM_notm}} Marketplace, [click this link ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/docs/services/knowledge-studio/artifacts.html){: new_window}.
{: tip}

# Types of artifacts
{: #artifacts}

First create or import artifacts to use to train the annotators.
{: shortdesc}

The annotators learn about the following types of artifacts that you add to the workspace:

- **Type system**

    A type system defines the entities and relationships between entities that matter to you. See [Establishing a type system](/docs/services/watson-knowledge-studio/typesystem.html).

- **Dictionaries**

    A dictionary groups together words and phrases that should be treated equivalently by an annotator component. See [Creating dictionaries](/docs/services/watson-knowledge-studio/dictionaries.html).

- **Documents**

    Documents serve a different purpose depending on whether you are creating a machine learning annotator or a rule-based annotator. See the following topics for more information:
    - Machine-learning annotator documents: [Adding documents for annotation](/docs/services/watson-knowledge-studio/documents-for-annotation.html#wks_t_docs_intro)
    - Rule-based annotator documents: [Adding documents for defining rules](/docs/services/watson-knowledge-studio/rule-annotator-add-doc.html)

You can import many of these artifacts from external resources, including artifacts that you exported from other {{site.data.keyword.watson}}&trade; {{site.data.keyword.knowledgestudioshort}} workspaces. See [Importing resources from another workspace](/docs/services/watson-knowledge-studio/exportimport.html) for information about importing artifacts from other workspaces.

See [Summary of inputs, outputs, and limitations](/docs/services/watson-knowledge-studio/create-project.html#wks_formats) for key facts about artifacts, such as size limits and supported file types for imported artifacts.

