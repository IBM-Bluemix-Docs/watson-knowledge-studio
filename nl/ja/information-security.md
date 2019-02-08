---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-27"

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

# 機密保護
{: #information-security}

IBM は、お客様やパートナーに、データ・プライバシー、セキュリティー、およびガバナンスに関する革新的なソリューションを提供します。
{: shortdesc}

**注意:**
お客様は、EU 一般データ保護規則を含む各法律および規制の遵守をお客様ご自身で確保する責任があります。お客様のビジネスに影響を及ぼす可能性のある関連法令の特定およびそれらの解釈、ならびにかかる関連法令を遵守するためにお客様が講ずるべき必要措置に関する助言は、お客様の責任により適格な弁護士から得るものとします。

ここに記載された製品、サービス、その他の機能は、すべてのお客様の状況に適しているわけではなく、利用が制限される可能性があります。IBM は法律上、会計上、または監査上の助言を提供することはしません。また、IBM のサービスまたは製品が、お客様のあらゆる法令遵守の裏付けとなる表明または保証もいたしません。

以下の場所で作成された {{site.data.keyword.cloud}} {{site.data.keyword.watson}} リソースの GDPR サポートを要請する必要がある場合の手順

- EU 内の場合、[Requesting support for IBM Cloud Watson resources created in the European Union ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/docs/services/watson/getting-started-gdpr-sar.html#request-EU){: new_window} を参照してください。
- EU 外の場合、[Requesting support for resources outside the European Union ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/docs/services/watson/getting-started-gdpr-sar.html#request-non-EU){: new_window} を参照してください。

## EU 一般データ保護規則 (GDPR)
{: #gdpr}

IBM は、お客様やパートナーに、データ・プライバシー、セキュリティー、およびガバナンスに関する革新的なソリューションを提供して、GDPR に対する準拠が完了するまでの過程を支援します。

GDPR に対する準備を整えるための IBM 独自の過程と、準拠が完了するまでの過程をサポートする弊社の GDPR 機能とオファリングについて詳しくは、[ここ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/gdpr){: new_window} を参照してください。

## {{site.data.keyword.knowledgestudioshort}} での GDPR
{: #gdpr-wks}

{{site.data.keyword.knowledgestudiofull}} には、データを含んだアップロード済み成果物にアクセスしてそれを削除するための、グラフィカル・インターフェースが用意されています。以下の成果物を {{site.data.keyword.knowledgestudioshort}} にアップロードできます。
- タイプ・システム
- 辞書
- 文書

データを削除する要請を受け取った場合は、以下の手順を実行してください。
1. [該当する成果物を削除します](/docs/services/watson-knowledge-studio/artifacts.html)。
2. [モデルをリトレーニングして再デプロイします](/docs/services/watson-knowledge-studio/train-ml.html)。
3. [削除されたデータを使用していた前のバージョンのモデルを削除します](/docs/services/watson-knowledge-studio/improve-ml.html#wks_maversions)。
