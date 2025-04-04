---
title: B2B Source資料型別
description: 瞭解B2B Source Experience Data Model (XDM)資料型別。
exl-id: 01b7d41c-1ab6-4cbc-b9b3-77b6af69faf3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 3%

---

# [!UICONTROL B2B Source]資料型別

[!UICONTROL B2B Source]是標準的體驗資料模型(XDM)資料型別，代表B2B實體（例如[帳戶](../classes/b2b/business-account.md)、[機會](../classes/b2b/business-opportunity.md)或[行銷活動](../classes/b2b/business-campaign.md)）的複合識別碼。

當僅依賴字串型識別碼時，跨多個系統的ID之間可能會重疊（例如，可以在一個CRM系統上為某個機會指定字串ID，但同一ID可能會引用完全不同的機會）。 這可能會在合併[即時客戶個人檔案](../../profile/home.md)中的資料時造成資料衝突。

[!UICONTROL B2B Source]資料型別可讓您使用實體的原始字串ID，並將其與來源特定的內容資訊結合，以確保其在Experience Platform系統中保持完全唯一，無論其來源為何。

![B2B Source結構](../images/data-types/b2b-source.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `sourceID` | 字串 | 來源記錄的唯一ID。 |
| `sourceInstanceID` | 字串 | 來源資料的執行個體或組織ID。 |
| `sourceKey` | 字串 | 由`sourceId`、`sourceInstanceId`和`sourceType`組成的唯一識別碼會以下列格式串連在一起： `[sourceID]@[sourceInstanceID].[sourceType]`。<br><br>某些來源聯結器(如Marketo)會自動針對特定識別碼串連此值。 其他必須使用[資料準備`concat`函式](../../data-prep/functions.md#string)手動串連，例如： `concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | 字串 | 提供來源資料的平台名稱。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
