---

copyright:
  years: 2015, 2017
lastupdated: "2017-12-19"

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

This documentation is for {{site.data.keyword.knowledgestudiofull}} on {{site.data.keyword.cloud}}. To see the documentation for the previous version of {{site.data.keyword.knowledgestudioshort}} on {{site.data.keyword.IBM_notm}} Marketplace, [click this link ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/docs/services/knowledge-studio/tutorials-create-rule-model.html){: new_window}.
{: tip}

# Creating a rule-based model
{: #wks_tutrule_intro}

This tutorial helps you understand how to create a rule-based model that you can use to find text patterns that you define in documents.
{: shortdesc}

You will build a model that can find text in documents that matches the pattern `month day, year`. For example, the model would find the date reference *May 1, 2010*. Before you define the rule pattern itself, you will create artifacts that will help you build the pattern, including a dictionary class that recognizes month mentions and a regular expression class that recognizes year mentions in text.

## Learning objectives

After you complete this tutorial, you will know how to perform the following tasks:

- Create classes
- Add documents for defining rules
- Associate dictionaries with classes
- Define regular expressions to capture sequences of characters
- Define rules

This tutorial should take approximately 30 minutes to finish. If you explore other concepts related to this tutorial, it could take longer to complete.

## Before you begin

- You're using a supported browser. For information, see [Browser requirements](/docs/services/watson-knowledge-studio/system-requirements.html).
- You successfully completed [Tutorial: Creating a workspace](/docs/services/watson-knowledge-studio/tutorials-create-project.html).
- You must have at least one user ID in either the Admin or ProjectManager role. For information about user roles, see [Assembling a team](/docs/services/watson-knowledge-studio/team.html).

## Results

After you create the rule-based model, you can use it in one of the following ways to find text patterns in documents:

- [Pre-annotate your documents](/docs/services/watson-knowledge-studio/preannotation.html#wks_preannotrule) before you create a machine learning model
- [Deploy or export the model](/docs/services/watson-knowledge-studio/rule-annotator-model-use.html) to other {{site.data.keyword.watson}} services or products

## Lesson 1: Adding a dictionary of months
{: #wks_tutless_rule1}

In this lesson, you will learn how to add a dictionary to a workspace in {{site.data.keyword.knowledgestudioshort}}. The dictionary contains terms related to the months of the year.

### About this task

In a later lesson, you will define a class based on this dictionary. When you create that class, all terms in this dictionary that are found in documents will be automatically annotated as a mention of the associated class type. For more information about dictionaries, see [Adding dictionaries to a workspace](/docs/services/watson-knowledge-studio/dictionaries.html#wks_projdictionaries).

### Procedure

1. Download the <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/knowledge-studio/dictionary-items-month.csv" download>`dictionary-items-month.csv`<img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a> file to your computer. This file contains dictionary terms in CSV format, suitable for importing into a {{site.data.keyword.knowledgestudioshort}} dictionary.
1. From the **Assets & Tools** > **Pre-Annotators** sidebar, select the **Dictionaries** tab, and click **Manage Dictionaries**.
1. Click the **Create Dictionary** button to add a dictionary.
1. In the **Name** field, type `Month dictionary` and click **Save** to create the (empty) dictionary. The new dictionary is created and automatically opened for editing.
1. In the dictionary pane, click **Upload**.
1. In the Upload Dictionary Entries window, select the `dictionary-items-month.csv` file from your computer and then click **Upload**.

    The terms in the file are imported into the dictionary.

## Lesson 2: Adding sample documents
{: #wks_tutless_rule2}

In this lesson, you will learn how to add documents with linguistic patterns that illustrate the types of rules you want to define.

### About this task

For more information about adding documents, see [Adding documents for defining rules](/docs/services/watson-knowledge-studio/rule-annotator-add-doc.html).

### Procedure

1. Download the <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/knowledge-studio/documents-new.csv" download>`documents-new.csv`<img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a> file to your computer. This file contains example documents suitable for importing.
1. From the sidebar, click **Document Annotation** > **Rules**.
1. Click the **Add a document** icon next to **Documents**.
1. Click the **Import CSV file** tab.
1. Click to browse for the `documents-new.csv` file that you downloaded to your computer earlier, and then click **Upload**.

    A set of documents is displayed in the main Documents page.

    ![Shows three of the fourteen documents that were added to the rule editor. Shows the document title and an excerpt from the beginning of each document. There is also a delete icon next to each document that you can use to delete the document.](images/rule-doc-add3.jpg)

## Lesson 3: Creating classes
{: #wks_tutless_rule3}

In this lesson, you will learn how to define classes that you will use when you define a rule.

### About this task

For more information about classes, see [Rules](/docs/services/watson-knowledge-studio/rule-annotator.html).

### Procedure

1. From the **Rules** page of your workspace, click the **Add a class** icon next to **Class** in the right side panel.

1. Enter `DictMonth` as the class name, and then click **Add**.

    The new class is displayed in the Class side panel.

## Lesson 4: Associating a dictionary with a class
{: #wks_tutless_rule4}

In this lesson, you will learn how to use a dictionary in the rule editor.

### Procedure

1. From the sidebar, select **Document Annotation** > **Dictionaries**, and then click the **Month dictionary** that you created previously.

1. From the **Class** list, select `DictMonth` and then click **Save**.

    The class is associated with the dictionary.

    ![Shows that the DictMonth class is associated with the Month dictionary in the Dictionaries panel of the Rule page.](images/rule-dict-map2.jpg)

### Results

For documents that are associated with the rule editor, any references to terms in the dictionary are annotated as `DictMonth` class mentions. You will see proof that these references have been annotated in the next lesson.

## Lesson 5: Finding class annotations in documents
{: #wks_tutless_rule5}

In this lesson, you will learn how to find class annotations in rule editor documents.

### Procedure

1. From the sidebar, select **Document Annotation** > **Rules**.
1. From the Class panel, find the `DictMonth` class that you defined earlier, and click the **Search annotations in documents** icon that's next to it.

    The Find Annotations page is displayed and shows all the documents that contain text references to months.

1. Click the `Technology - computerworld.com` document to view the full document. Notice that the text `February` is highlighted, which means it was annotated as a mention of the `DictMonth` class.

## Lesson 6: Defining a regular expression
{: #wks_tutless_rule6}

In this lesson, you will learn how to define a regular expression.

### About this task

You will define a regular expression that can find year patterns like *2009*.

For more information about defining regular expressions, see [Defining a rule](/docs/services/watson-knowledge-studio/rule-annotator-define-rule.html).

### Procedure

1. From the **Rules** page, click the **Add a class** icon (![_](images/wks_tut_dict_add.jpg)) next to **Class** from the right side panel.
1. Enter `RegExpYear` as the class name, and click **Add**.
1. From the sidebar, click **Regex**, and then click the **Create a regular expression** icon next to **Regular Expressions**.
1. Click the **Add Entry** button.
1. In the **Regular Expression** field, enter the following expression:

    ```
    (?:(?:19|20)[0-9]{2})
    ```
    {: screen}

    > **Note:** This regular expression finds years between 1900 and 2099.

1. Set **Minimum Word Tokens** to `1` and **Maximum Word Tokens** to `1`.
1. Click **Add** to save the regular expression entry.
1. Enter `MyYearExp` as the regular expression name, and then, from the **Class** menu, select the *RegExpYear* class that you defined earlier.
1. Click **Save**.

    After you save the regular expression, it is automatically applied to the sample documents. Any text strings that follow the pattern that you defined in the regular expression are annotated as mentions of the **RegExpYear** class.

1. To check whether the expression you defined is capturing time occurrences correctly, you can search for mentions. Click the **Search annotations in documents** icon next to the **RegExpYear** class in the Class side panel.

    ![Shows the user clicking the magnifying glass icon next to the RegExpYear class in the Class side panel of the Rules page.](images/rule-regex-add5.jpg)

    The Find Annotations page is displayed. Occurrences of year mentions are highlighted in the sample documents in which they occur.

    ![Shows years highlighted in excerpts from 8 of the sample documents.](images/rule-regex-add6.jpg)

## Lesson 7: Defining a rule
{: #unique_1166829415}

In this lesson, you will learn how to define a rule.

### About this task

You already defined a dictionary-based class for annotating month mentions. You also defined a regular expression that finds numeric values which represent a year. Now, you will define a rule that captures the sequence of a month followed by a number, a comma, and then a year. You will define a rule for date expressions like *September 21, 2016*.

For more information about defining rules, see [Defining a rule](/docs/services/watson-knowledge-studio/rule-annotator-define-rule.html).

### Procedure

1. From the sidebar, select **Document Annotation** > **Rules**, and open the `Technology - computerworld.com` document.
1. Select the text *February 3, 2009* in the document. Make sure you select the comma, too.

    ![Shows the text February 3, 2009 as being selected in the document.](images/rule-add1.jpg)

1. Click the **Add a rule** icon.

    The rule editor shows a depiction of the rule pattern that you identified.

    The text *February 3, 2009* is visible. A gray line that connects the cells in the depiction identifies which cells are currently part of the pattern.
    - The *DictMonth* class is part of the rule pattern instead of the text *February*. This selection is preferred because you want the model to find any month that is annotated by the *DictMonth* class as the first token in the date pattern instead of the text *February* only.
    - At the end of the rule, the year *2009* is already annotated as being a mention of the *RegExpYear* class. The *RegExpYear* class is part of the rule pattern instead of the number 2009. This selection is also preferred because you want the model to find any year that is annotated by the *RegExpYear* class as the last token in the date pattern instead of the specific text *2009* only.

    The number 3 and the comma (,) after it are shown as the second and third tokens in the pattern. As the pattern is currently specified, the model will find only occurrences of dates that specify the 3rd day of a month. We want the model to find dates that specify any day of the month, so next we will change the feature settings for the day token.

1. Above the day `3` cell, click the **Text** icon to open the feature settings for the token.

    ![Shows the user clicking the Text Feature Settings icon.](images/rule-add4.jpg)

    Currently, the rule is set to match the exact text, `3`. Instead, we want it to match any number.

1. Change the feature setting to be numeric by selecting **Character Type : Numeric**, and then deselecting **Text : 3**.

    ![Shows the user clicking the Character Type : Number option as the feature setting for the 3 token.](images/rule-add5.jpg)

    You changed the definition for the number `3` cell.

    ![Shows the cell that represents the 3 token now has an Aa icon above it to indicate that any numeric value can match that token in the pattern.](images/rule-add6.jpg)

    The **Aa** icon indicates that instead of requiring the number to be equal to 3 exactly, it can be any number.

1. Do not change any settings for the comma token.

    We want the third token in the pattern to be a comma, so the current feature setting of **text : ,** is appropriate. In addition to a feature setting, each token has a repeat setting. The repeat setting specifies how many times the token can be repeated in the text for it to match the pattern. The current repeat setting of **Required (Exactly 1)** is also appropriate as specified.

    ![Shows the repeat settings for the comma token which are set to Exactly 1. ](images/rule-add7.jpg)

1. Assign a class to represent the pattern `DictMonth + numeric token + comma + RegExpYear`.

    Notice the four empty cells that represent the four tokens that you selected from the document. To select all the cells, select the first cell, and then press Shift + click each additional cell. Enter `RuleDate` as the class name, and then click it to create the new class.

    ![Shows that all four cells in the top row have been selected and the span is being defined as the RuleDate class.](images/rule-add8.jpg)

    You have successfully defined the pattern for the rule.

1. In the **Rule name** field, enter `MyDateRule` and click **Save**.

    After you save the rule, it is automatically applied to the sample documents. If the `Technology - computerworld.com` document is still open in the rule editor, you will see that the `February 3, 2009` text in the document is now annotated as a mention of the RuleDate class.

    ![Shows text from in the Technology - computerworld.com document with only the text February 3, 2009 annotated as being a mention of the RuleDate class.](images/rule-add10.jpg)

    You can search for all occurrences of RuleDate class mentions in the sample documents by clicking the **Search annotation in documents** icon ( ![A magnifying glass to represent a search](images/filter_gray.png)) next to the `RuleDate` class from the Class panel. It is a good practice to check whether all dates are being captured properly to confirm that you defined the pattern correctly.

    ![Shows the Find Annotations page with two documents that contain dates that match the rule pattern you just defined.](images/rule-add11.jpg)

## Lesson 8: Creating a rule annotator
{: #wks_tutless_rule8}

In this lesson, you will learn how to create a rule annotator.

### About this task

For more information about creating a rule annotator, see [Creating the rule-based model](/docs/services/watson-knowledge-studio/rule-annotator-model-create.html).

### Procedure

1. From the sidebar, select **Model Management** > **Versions** and click the **Rule-based model type mapping** tab.

1. Map the `RuleDate` class that you defined corresponding to the `DATE` entity from the type system.

    1. Find the **DATE** entity, and click **Edit**.

        ![Shows the user clicking Edit for the DATE entity type in the Class mappingn tab of the Annotator Component page.](images/rule-anno2.jpg)

    1. Choose the `RuleDate` class from the drop-down list and click **Save**.

        ![Shows the user choosing the RuleDate class from the drop-down list.](images/rule-anno3.jpg)

1. To run the rule-based model select the **Rule-based** tab and click **Run this model**.

## Tutorial summary
{: #wks_tutrule_sum}

While learning about {{site.data.keyword.knowledgestudioshort}}, you created a rule-based annotator.

### Lessons learned

By completing this tutorial, you learned about the following concepts:

- Classes
- Regular expressions
- Rules
