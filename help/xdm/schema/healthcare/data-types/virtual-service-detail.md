---
title: 虛擬服務詳細資料型別
description: 瞭解虛擬服務詳細資料體驗資料模型(XDM)資料型別。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: bde7363c-43b7-402d-96b2-7aa0160cd2ea
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 5%

---

# [!UICONTROL 虛擬服務詳細資料]資料型別

[!UICONTROL 虛擬服務詳細資料]是描述虛擬服務聯絡詳細資訊的標準Experience Data Model (XDM)資料型別。 此資料型別是根據HL7 FHIR Release 5規格建立的。

![虛擬服務詳細資料資料型別結構](../../../images/healthcare/data-types/virtual-service-detail.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 位址連絡視窗] | `addressContactPoint` | [[!UICONTROL 聯絡視窗]](../data-types/contact-point.md) | 技術媒介的聯絡視窗，例如電話、傳真或電子郵件的細節。 |
| [!UICONTROL 位址延伸連絡人詳細資料] | `addressExtendedContactDetail` | [[!UICONTROL 延伸連絡人詳細資料]](../data-types/extended-contact-detail.md) | 延伸連絡資訊。 |
| [!UICONTROL 頻道型別] | `channelType` | [[!UICONTROL 編碼]](../data-types/coding.md) | 要連線的虛擬服務型別，例如Teams、Zoom或WhatsApp。 |
| [!UICONTROL 其他資訊] | `additionalInfo` | 字串陣列 | 用來檢視替代連線詳細資料的地址，以URI表示。 |
| [!UICONTROL 位址字串] | `addressString` | 字串 | 用來連線至虛擬服務的位址。 |
| [!UICONTROL 位址Url] | `addressUrl` | 字串 | 用於連線至虛擬服務的URL，以URI表示。 |
| [!UICONTROL 最大參與者] | `maxParticipants` | 整數 | 支援的參與者數目上限，最小值為`0`。 |
| [!UICONTROL 工作階段索引鍵] | `sessionKey` | 字串 | 虛擬服務所需的工作階段金鑰。 |

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.schema.json)
