---
title: B2B源資料類型
description: 本檔案概述B2B來源Experience Data Model(XDM)資料類型。
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 3%

---

# [!UICONTROL B2B源資] 料類型

>[!NOTE]
>
>此資料類型僅適用於可存取B2B版即時客戶資料平台的組織。

[!UICONTROL B2B來] 源是標準的Experience Data Model(XDM)資料類型，代表B2B實體(例如帳戶 [](../classes/b2b/business-account.md)、機 [會](../classes/b2b/business-opportunity.md)或促銷活 [動](../classes/b2b/business-campaign.md))的複合識別碼。

僅依賴字串型識別碼時，跨多個系統的ID之間可能會有重疊（例如，一個CRM系統上可以為機會指定字串ID，但同一ID可能指的是完全不同的機會）。 在[即時客戶設定檔](../../profile/home.md)中合併資料時，這可能會導致資料衝突。

[!UICONTROL B2B源]資料類型允許您使用實體的原始字串ID，並將其與源特定上下文資訊組合，以確保它在Platform系統中保持完全唯一，而無論其源自何。

![B2B源結構](../images/data-types/b2b-source.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `sourceID` | 字串 | 源記錄的唯一ID。 |
| `sourceInstanceID` | 字串 | 來源資料的例項或組織ID。 |
| `sourceKey` | 字串 | 由`sourceId`、`sourceInstanceId`和`sourceType`以下列格式串連在一起的唯一識別碼：`[sourceID]@$[sourceInstanceID].[sourceType]`。<br><br>某些來源連接器(例如Marketo)會針對特定識別碼自動串連此值。必須使用[資料準備`concat`函式](../../data-prep/functions.md#string)手動串連其他項目，例如：`concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | 字串 | 提供來源資料的平台名稱。 |

{style=&quot;table-layout:auto&quot;}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
