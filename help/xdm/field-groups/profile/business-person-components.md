---
title: XDM商業人士元件結構描述欄位群組
description: 瞭解XDM商業人士元件結構描述欄位群組。
exl-id: 965b89f4-59f5-43f4-8778-3549e15b44d4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 2%

---

# [!UICONTROL XDM商業人士元件]結構描述欄位群組

[!UICONTROL XDM商業人士元件]是[[!DNL XDM Individual Profile] 類別](../../classes/individual-profile.md)的標準結構描述欄位群組，可擷取個人的多個來源記錄以及個人細分所需的其他屬性。

透過Real-Time CDP B2B版中的[即時客戶設定檔](../../../profile/home.md)為個人建立設定檔時，用來建立該設定檔的資訊可能會來自許多來源記錄。 例如，如果某人供職於兩家不同的公司，則許多CRM系統都會刻意建立該人的重複復本，因此其中一個復本會連結至公司A，而另一個則連結至公司B。將該資料引進Adobe Experience Platform時，此欄位群組用於將這些不同的來源記錄合併為單一表示法。

欄位群組提供根層級`personComponents`欄位，這是物件的陣列。 陣列中的每個物件代表不同的來源記錄。

>[!IMPORTANT]
>
>您必須遵循[來原始檔](../../../rtcdp/sources/b2b.md)中所述的擷取模式。 其他欄位對應方法無法保證有效。
>
>例如，`personComponents`陣列的每個物件會在標準擷取模式期間個別提交，然後由Platform新增至陣列。 手動將物件陣列新增至業務人員元件將傳回錯誤。
>建立B2B資料的結構描述時，您應該使用自動產生公用程式。 請參閱檔案，瞭解如何使用[B2B名稱空間和結構描述自動產生公用程式](../../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md)的說明。 如果您未使用自動產生公用程式，且打算手動對應您的資料模型，請務必在對應資料前先閱讀[Adobe Real-time Customer Data Platform B2B Edition XDM類別](../../../rtcdp/schemas/b2b.md)的檔案。
>
>如需有關B2B資料的建議工作流程的資訊，請參閱[端對端教學課程](../../../rtcdp/b2b-tutorial.md)。

![](../../images/field-groups/business-person-components.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `sourceAccountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 與個人相關之帳戶的複合識別碼。 |
| `sourceConvertedContactKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 如果此潛在客戶已轉換，則為相關聯絡人的複合識別碼。 |
| `sourceExternalKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 此人的資料源自的來源系統的複合識別碼。 |
| `sourcePersonKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 個人的複合識別碼。 |
| `workEmail` | [[!UICONTROL 電子郵件地址]](../../data-types/b2b-source.md) | 個人的工作電子郵件ID。 |
| `personGroupID` | 字串 | 適用於個人的群組識別碼。 |
| `personScore` | 字串 | CRM系統產生的個人分數。 |
| `personSource` | 字串 | 適用於個人資料來源的來源系統的唯一字串型識別碼。 |
| `personStatus` | 字串 | 個人的目前行銷或銷售狀態。 |
| `personType` | 字串 | B2B內容中的人員型別。 |
| `sourceAccountID` | 字串 | 來源系統中與個人相關聯之帳戶的唯一字串型識別碼。 此欄位會作為系統的外部索引鍵，用於查詢此人工作的不同公司。 |
| `sourceConvertedContactID` | 字串 | 如果此潛在客戶已轉換，則為相關聯絡人的唯一字串型識別碼。 |
| `sourceExternalID` | 字串 | 適用於人員資料來源的來源系統的唯一字串型識別碼。 |
| `sourcePersonID` | 字串 | 適用於個人的唯一字串型識別碼。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.schema.json)
