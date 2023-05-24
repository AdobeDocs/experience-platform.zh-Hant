---
title: B2B源資料類型
description: 本文檔概述了B2B源體驗資料模型(XDM)資料類型。
exl-id: 01b7d41c-1ab6-4cbc-b9b3-77b6af69faf3
source-git-commit: e602f78470fe4eeb2a42e6333ba52096d8a9fe8a
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 2%

---

# [!UICONTROL B2B源] 資料類型

[!UICONTROL B2B源] 是標準體驗資料模型(XDM)資料類型，它表示B2B實體(如 [帳戶](../classes/b2b/business-account.md)的 [機會](../classes/b2b/business-opportunity.md)或 [活動](../classes/b2b/business-campaign.md))。

當僅依賴基於字串的標識符時，跨多個系統的ID之間可能存在重疊（例如，可以在一個CRM系統上為機會指定字串ID，但該ID可以指代完全不同的機會）。 在中合併資料時，這可能會導致資料衝突 [即時客戶配置檔案](../../profile/home.md)。

的 [!UICONTROL B2B源] 資料類型允許您使用實體的原始字串ID，並將其與特定於源的上下文資訊組合，以確保它在平台系統中保持完全唯一，而不管它源自什麼源。

![B2B源結構](../images/data-types/b2b-source.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `sourceID` | 字串 | 源記錄的唯一ID。 |
| `sourceInstanceID` | 字串 | 源資料的實例或組織ID。 |
| `sourceKey` | 字串 | 由 `sourceId`。 `sourceInstanceId`, `sourceType` 以下格式連接在一起： `[sourceID]@[sourceInstanceID].[sourceType]`。<br><br>某些源連接器(如Marketo)自動連接某些標識符的值。 必須使用 [資料準備 `concat` 函式](../../data-prep/functions.md#string)，例如： `concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | 字串 | 提供源資料的平台的名稱。 |

{style="table-layout:auto"}

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
