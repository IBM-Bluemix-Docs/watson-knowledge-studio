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

This documentation is for {{site.data.keyword.knowledgestudiofull}} on {{site.data.keyword.cloud}}. To see the documentation for the previous version of {{site.data.keyword.knowledgestudioshort}} on {{site.data.keyword.IBM_notm}} Marketplace, [click this link ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/docs/services/knowledge-studio/alchemylanguage-gif.html){: new_window}.
{: tip}

# How to deploy a model
{: #alchemylanguage-gif}

The graphic illustrates how to deploy a machine learning annotator for use by {{site.data.keyword.alchemylanguagefull}}.
{: shortdesc}

![Shows the user opening machine learning annotator Details, clicking Deploy. After deployment processing completed, the user click the Status link, and sees it is available, and gets the model ID.](images/deploy1.gif)

After the model is available, you can pass the model ID and API key as parameters to the {{site.data.keyword.IBM_notm}} {{site.data.keyword.alchemylanguageshort}} REST API endpoints. The code uses your trained model to extract information from text.

**Related tasks**:

[Deploying a machine learning annotator to {{site.data.keyword.IBM_notm}} {{site.data.keyword.alchemylanguageshort}}](/docs/services/watson-knowledge-studio/publish-ml.html#wks_mabluemix)
