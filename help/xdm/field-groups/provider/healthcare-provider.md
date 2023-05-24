---
title: 醫療保健提供程式架構欄位組
description: 本文檔概述了醫療保健提供商架構欄位組。
exl-id: e39b4082-4b66-47b3-a8e2-951d8a96f742
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 4%

---

# [!UICONTROL 醫療保健提供商] 架構欄位組

[!UICONTROL 醫療保健提供商] 是標準架構欄位組 [[!UICONTROL 提供程式] 類](../../classes/provider.md)。 它提供單個對象類型欄位 `healthcareProvider` 它捕獲與個人健康專業人員或衛生設施組織相關的屬性，該組織已獲得許可以提供醫療保健診斷和治療服務。

![](../../images/field-groups/healthcare-provider.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `addressDetails` | 對象陣列 | 列出提供程式的地址詳細資訊。 每個對象都包括以下屬性： <ul><li>`address`:([[!UICONTROL 郵政地址]](../../data-types/postal-address.md)):提供商的郵政地址。</li><li>`addressType`:（字串）地址類型，指示提供方提供服務的位置。</li></ul> |
| `emailAddress` | [[!UICONTROL 電子郵件地址]](../../data-types/email-address.md) | 提供程式的電子郵件地址。 |
| `fax` | [[!UICONTROL 電話號碼]](../../data-types/phone-number.md) | 提供商的傳真號碼。 |
| `phoneNumber` | [[!UICONTROL 電話號碼]](../../data-types/phone-number.md) | 提供商的電話號碼。 |
| `qualifications` | 對象陣列 | 列出與提供護理相關的認證、許可證或培訓。 每個對象都包括以下屬性： <ul><li>`issuer`:([[!UICONTROL 帳戶詳細資訊]](../../data-types/account-details.md)):規範和發放資格的組織。</li><li>`activePeriod`:（整數）資格有效的年份。</li><li>`code`:（字串）資格的編碼表示。</li></ul> |
| `classification` | 字串 | 服務提供商基於類別或類別（如患者護理、非患者護理等）的分類。 |
| `isActive` | 布林值 | 指示提供程式是否處於活動狀態。 |
| `languages` | 字串陣列 | 提供程式執行操作的語言清單。 |
| `practiceGroupName` | 字串 | 服務提供商的實踐組名稱。 |
| `practiceGroupType` | 字串 | 服務提供商的實踐組類型。 |
| `practiceType` | 字串 | 服務提供商的實踐類型。 |
| `specialties` | 字串陣列 | 此提供商提供的專業產品清單。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱 [公共XDM儲存庫](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json)。
