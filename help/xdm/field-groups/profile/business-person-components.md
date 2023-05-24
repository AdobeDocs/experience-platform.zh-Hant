---
title: XDM業務人員元件方案欄位組
description: 本文檔提供XDM業務人員元件架構欄位組的概述。
exl-id: 965b89f4-59f5-43f4-8778-3549e15b44d4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 2%

---

# [!UICONTROL XDM業務人員元件] 架構欄位組

[!UICONTROL XDM業務人員元件] 是標準架構欄位組 [[!DNL XDM Individual Profile] 類](../../classes/individual-profile.md) 捕獲人員的多個源記錄以及人員細分所需的其他屬性。

為人員建立配置檔案時 [即時客戶配置檔案](../../../profile/home.md) 在Real-Time CDPB2B版中，用於建立該配置檔案的資訊可能來自許多源記錄。 例如，如果一個人為兩個不同的公司工作，則許多CRM系統會建立該人的故意複製副本，以便一個副本連結到公司A，而另一個副本連結到公司B。將資料帶入Adobe Experience Platform時，此欄位組用於將這些不同的源記錄合併為單個表示。

欄位組提供根級別 `personComponents` 欄位，即對象陣列。 陣列中的每個對象都表示不同的源記錄。

>[!IMPORTANT]
>
>必須遵循中所述的攝取模式 [源文檔](../../../rtcdp/sources/b2b.md)。 其他的欄位映射方法無法保證有效。
>
>例如， `personComponents` 陣列在標準接收模式期間單獨提交，然後由平台添加到陣列。 將對象陣列手動添加到業務人員元件將返回錯誤。
>在為B2B資料建立架構時，應使用自動生成實用程式。 有關如何使用 [B2B命名空間和架構自動生成實用程式](../../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md)。 如果您沒有使用自動生成實用程式並打算手動映射資料模型，請務必閱讀 [Adobe Real-time Customer Data PlatformB2B版XDM類](../../../rtcdp/schemas/b2b.md) 映射資料之前。
>
>查看 [端到端教程](../../../rtcdp/b2b-tutorial.md) 有關建議的B2B資料工作流的資訊。

![](../../images/field-groups/business-person-components.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `sourceAccountKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 與人員關聯的帳戶的組合標識符。 |
| `sourceConvertedContactKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 如果轉換了此潛在顧客，則相關聯繫人的組合標識符。 |
| `sourceExternalKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 源系統的組合標識符，該人員的資料源於。 |
| `sourcePersonKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 人員的複合標識符。 |
| `workEmail` | [[!UICONTROL 電子郵件地址]](../../data-types/b2b-source.md) | 人員的工作電子郵件ID。 |
| `personGroupID` | 字串 | 人員的組標識符。 |
| `personScore` | 字串 | 由CRM系統為人員生成的分數。 |
| `personSource` | 字串 | 基於字串的唯一標識符，用於源系統，該人員的資料源自。 |
| `personStatus` | 字串 | 人員的當前市場營銷或銷售狀態。 |
| `personType` | 字串 | B2B上下文中的人員類型。 |
| `sourceAccountID` | 字串 | 源系統中與人員關聯的帳戶的唯一標識符。 該欄位被系統用作外鍵，用於查找此人為之工作的不同公司。 |
| `sourceConvertedContactID` | 字串 | 如果轉換了此潛在顧客，則相關聯繫人的唯一標識符。 |
| `sourceExternalID` | 字串 | 源系統的基於字串的唯一標識符，該人員的資料源於該標識符。 |
| `sourcePersonID` | 字串 | 人員的唯一標識符。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.schema.json)
