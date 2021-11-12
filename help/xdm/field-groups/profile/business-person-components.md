---
title: XDM企業人員元件結構欄位組
description: 本檔案概述「XDM企業人員元件」結構欄位群組。
exl-id: 965b89f4-59f5-43f4-8778-3549e15b44d4
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 3%

---

# [!UICONTROL XDM企業人員元件] 方案欄位組

[!UICONTROL XDM企業人員元件] 是的標準架構欄位組 [[!DNL XDM Individual Profile] 類](../../classes/individual-profile.md) 會擷取人員的多個來源記錄，以及人員分段所需的其他屬性。

為人員建立設定檔時透過 [即時客戶個人檔案](../../../profile/home.md) 在B2B版的即時CDP中，用於建立該配置檔案的資訊可能來自許多源記錄。 例如，如果某人為兩家不同的公司工作，則許多CRM系統會建立該人刻意重複的副本，使其中一份連結至公司A，而另一份連結至公司B。將該資料帶入Adobe Experience Platform時，此欄位群組可用來將這些不同的來源記錄合併為單一表示。

欄位群組提供根層級 `personComponents` 欄位，此欄位是物件的陣列。 陣列中的每個對象表示不同的源記錄。

![](../../images/field-groups/business-person-components.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `sourceAccountKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 與人員關聯的帳戶的複合標識符。 |
| `sourceConvertedContactKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 如果此銷售線索已轉換，則相關聯繫人的複合標識符。 |
| `sourceExternalKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 源系統的複合標識符，該人員的資料源自於。 |
| `sourcePersonKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 人員的複合標識符。 |
| `workEmail` | [[!UICONTROL 電子郵件地址]](../../data-types/b2b-source.md) | 人員的工作電子郵件ID。 |
| `personGroupID` | 字串 | 人員的群組識別碼。 |
| `personScore` | 字串 | 由CRM系統為人員產生的分數。 |
| `personSource` | 字串 | 源系統的唯一字串型標識符，該用戶的資料源自於該系統。 |
| `personStatus` | 字串 | 人員的當前行銷或銷售狀態。 |
| `personType` | 字串 | B2B內容中的人員類型。 |
| `sourceAccountID` | 字串 | 與人員相關聯的來源系統中帳戶的唯一字串型識別碼。 此欄位被系統用作外鍵，以查找此人所工作的不同公司。 |
| `sourceConvertedContactID` | 字串 | 如果轉換了此銷售機會，則相關聯繫人的唯一字串型標識符。 |
| `sourceExternalID` | 字串 | 源系統的唯一基於字串的標識符，該人員的資料源自該標識符。 |
| `sourcePersonID` | 字串 | 人員的唯一字串型識別碼。 |

{style=&quot;table-layout:auto&quot;}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.schema.json)
