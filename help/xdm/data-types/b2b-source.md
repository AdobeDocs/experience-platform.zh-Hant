---
title: B2B源資料類型
description: 本檔案概述B2B來源Experience Data Model(XDM)資料類型。
exl-id: 01b7d41c-1ab6-4cbc-b9b3-77b6af69faf3
source-git-commit: e602f78470fe4eeb2a42e6333ba52096d8a9fe8a
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 3%

---

# [!UICONTROL B2B源] 資料類型

[!UICONTROL B2B源] 是標準的Experience Data Model(XDM)資料類型，代表B2B實體的複合識別碼(例如 [帳戶](../classes/b2b/business-account.md), [商機](../classes/b2b/business-opportunity.md)，或 [行銷活動](../classes/b2b/business-campaign.md))。

僅依賴字串型識別碼時，跨多個系統的ID之間可能會有重疊（例如，一個CRM系統上可能會為機會指定字串ID，但同一ID可能指的是完全不同的機會）。 這樣會在將資料合併到 [即時客戶個人檔案](../../profile/home.md).

此 [!UICONTROL B2B源] 資料類型可讓您使用實體的原始字串ID，並將其與來源專屬的內容資訊結合，以確保其在Platform系統中完全不重複，無論其來源為何。

![B2B源結構](../images/data-types/b2b-source.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `sourceID` | 字串 | 源記錄的唯一ID。 |
| `sourceInstanceID` | 字串 | 來源資料的例項或組織ID。 |
| `sourceKey` | 字串 | 由 `sourceId`, `sourceInstanceId`，和 `sourceType` 以下列格式串連： `[sourceID]@[sourceInstanceID].[sourceType]`.<br><br>某些來源連接器(例如Marketo)會針對特定識別碼自動串連此值。 其他必須使用 [資料準備 `concat` 函式](../../data-prep/functions.md#string)，例如： `concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | 字串 | 提供來源資料的平台名稱。 |

{style=&quot;table-layout:auto&quot;}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
