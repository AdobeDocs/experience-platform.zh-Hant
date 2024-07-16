---
title: 醫療保健提供者結構欄位群組
description: 瞭解醫療保健提供者結構欄位群組。
exl-id: e39b4082-4b66-47b3-a8e2-951d8a96f742
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 3%

---

# [!UICONTROL 醫療保健提供者]結構描述欄位群組

[!UICONTROL 醫療保健提供者]是[[!UICONTROL 提供者]類別](../../classes/provider.md)的標準結構描述欄位群組。 它提供單一物件型別欄位`healthcareProvider`，可擷取與授權提供醫療保健診斷與治療服務的個人健康專業人員或健康設施組織相關的屬性。

![](../../images/field-groups/healthcare-provider.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `addressDetails` | 物件陣列 | 列出提供者的地址詳細資料。 每個物件包含下列屬性： <ul><li>`address`： （[[!UICONTROL 郵寄地址]](../../data-types/postal-address.md)）：提供者的郵寄地址。</li><li>`addressType`： （字串）位址型別，指出提供者提供服務的位置。</li></ul> |
| `emailAddress` | [[!UICONTROL 電子郵件地址]](../../data-types/email-address.md) | 提供者的電子郵件地址。 |
| `fax` | [[!UICONTROL 電話號碼]](../../data-types/phone-number.md) | 提供者的傳真號碼。 |
| `phoneNumber` | [[!UICONTROL 電話號碼]](../../data-types/phone-number.md) | 提供者的電話號碼。 |
| `qualifications` | 物件陣列 | 列出與提供照護相關的認證、授權或培訓。 每個物件包含下列屬性： <ul><li>`issuer`： （[[!UICONTROL 帳戶詳細資料]](../../data-types/account-details.md)）：規範並發出資格的組織。</li><li>`activePeriod`： （整數）資格有效的年份。</li><li>`code`： （字串）資格的編碼表示法。</li></ul> |
| `classification` | 字串 | 根據類別或類別（例如病人護理、非病人護理等）的服務提供者分類。 |
| `isActive` | 布林值 | 指出提供者是否為使用中。 |
| `languages` | 字串陣列 | 提供者在其下執行作業的語言清單。 |
| `practiceGroupName` | 字串 | 服務提供者的實務群組名稱。 |
| `practiceGroupType` | 字串 | 服務提供者的實務群組型別。 |
| `practiceType` | 字串 | 服務提供者的實務型別。 |
| `specialties` | 字串陣列 | 此提供者提供的專業清單。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱[公用XDM存放庫](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json)。
