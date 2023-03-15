---
title: 醫療保健提供商架構欄位組
description: 本文檔提供醫療保健提供程式架構欄位組的概述。
exl-id: e39b4082-4b66-47b3-a8e2-951d8a96f742
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 4%

---

# [!UICONTROL 醫療保健提供商] 方案欄位組

[!UICONTROL 醫療保健提供商] 是的標準架構欄位組 [[!UICONTROL 提供者] 類](../../classes/provider.md). 它提供單一物件類型欄位 `healthcareProvider` ，擷取與個別健康專業人士或獲授權提供健康診斷及治療服務之健康設施組織有關之屬性。

![](../../images/field-groups/healthcare-provider.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `addressDetails` | 物件陣列 | 列出提供程式的地址詳細資訊。 每個物件都包含下列屬性： <ul><li>`address`:([[!UICONTROL 郵遞區號]](../../data-types/postal-address.md)):提供者的郵遞區號。</li><li>`addressType`:（字串）地址類型，指出提供者提供服務的位置。</li></ul> |
| `emailAddress` | [[!UICONTROL 電子郵件地址]](../../data-types/email-address.md) | 提供者的電子郵件地址。 |
| `fax` | [[!UICONTROL 電話號碼]](../../data-types/phone-number.md) | 提供商的傳真號碼。 |
| `phoneNumber` | [[!UICONTROL 電話號碼]](../../data-types/phone-number.md) | 提供商的電話號碼。 |
| `qualifications` | 物件陣列 | 列出與提供護理相關的認證、許可或培訓。 每個物件都包含下列屬性： <ul><li>`issuer`:([[!UICONTROL 帳戶詳細資訊]](../../data-types/account-details.md)):規範和發放資格的組織。</li><li>`activePeriod`:（整數）資格有效的年份。</li><li>`code`:（字串）資格的編碼表示。</li></ul> |
| `classification` | 字串 | 根據類別或類別（如患者護理、非患者護理等）的服務提供商分類。 |
| `isActive` | 布林值 | 指示提供程式是否處於活動狀態。 |
| `languages` | 字串陣列 | 提供商在下運行的語言清單。 |
| `practiceGroupName` | 字串 | 服務提供商的慣例組名稱。 |
| `practiceGroupType` | 字串 | 服務提供商的慣例組類型。 |
| `practiceType` | 字串 | 服務提供商的慣例類型。 |
| `specialties` | 字串陣列 | 此提供商提供的專業清單。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json).
