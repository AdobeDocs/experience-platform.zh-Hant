---
keywords: Experience Platform；首頁；熱門主題；綱要；綱要；XDM；個人設定檔；欄位；綱要；綱要；電信；訂閱；電信；綱要設計；欄位群組；欄位群組；
solution: Experience Platform
title: 電信訂閱結構描述欄位群組
description: 瞭解Telecom Subscription結構欄位群組。
exl-id: 00c20081-09d0-425c-9894-0f957558bd43
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 5%

---

# [!UICONTROL 電信訂閱]結構描述欄位群組

>[!NOTE]
>
>數個結構描述欄位群組的名稱已變更。 如需詳細資訊，請參閱[欄位群組名稱更新](../name-updates.md)的檔案。

[!UICONTROL 電信訂閱]是[[!DNL XDM Individual Profile] 類別](../../classes/individual-profile.md)的標準結構描述欄位群組，說明客戶的電信訂閱方案，包括定價、套件和個別產品訂閱。

欄位群組提供單一物件型別欄位`telecomSubscription`，其屬性如下所述。

![電信訂閱結構](../../images/field-groups/telecom-subscription/structure.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `internetSubscription` | 物件陣列 | 說明資料上限、連線型別和速度詳細資訊等網際網路訂閱方案細節。 如需詳細資訊，請參閱[&#128279;](#internetSubscription)下方的區段。 |
| `landlineSubscription` | 物件陣列 | 說明有線電話訂閱方案詳細資料，包括選取的功能、分鐘數和撥接方案。 如需詳細資訊，請參閱[&#128279;](#landlineSubscription)下方的區段。 |
| `mediaSubscription` | 物件陣列 | 說明媒體訂閱計畫詳細資料，包括頻道數和包含的串流服務。 如需詳細資訊，請參閱[&#128279;](#mediaSubscription)下方的區段。 |
| `mobileSubscription` | 物件陣列 | 說明行動訂閱計畫詳細資料，包括線路數、資料費率、成本等。 如需詳細資訊，請參閱[&#128279;](#mobileSubscription)下方的區段。 |
| `primarySubscriber` | [[!UICONTROL 人員]](../../data-types/person.md) | 說明訂閱的擁有者。 |
| `bundleName` | 字串 | 擷取客戶註冊的任何型別訂閱套件組合的名稱，例如`Internet + Media`。 |
| `primaryPartyID` | 字串 | 負責訂閱的主要人員識別碼，通常可能是他們的裝置電話號碼。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)

## `internetSubscription` {#internetSubscription}

`internetSubscription`是以物件陣列的形式提供。 每個物件的結構如下所述。

![internetSubscription](../../images/field-groups/telecom-subscription/internetSubscription.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `subscriptionDetails` | [[!UICONTROL 電信訂閱]](../../data-types/telecom-subscription.md) | 說明訂閱的一般詳細資料，包括訂閱長度、費用、狀態等。 說明訂閱的一般詳細資料，包括訂閱長度、費用、狀態等。 |
| `connectionType` | 字串 | 訂閱的連線型別。 |
| `dataCap` | 整數 | 帳戶的資料上限（百萬位元組，簡稱MB）。 |
| `downloadSpeed` | 整數 | 訂閱可用的最大下載速度（百萬位元組，簡稱MB）。 |
| `selfSetup` | 布林值 | 指出客戶是否有資格在沒有技術人員造訪的情況下進行網際網路設定。 |
| `uploadSpeed` | 整數 | 訂閱可用的最大上傳速度（百萬位元組，簡稱MB）。 |

{style="table-layout:auto"}

## `landlineSubscription` {#landlineSubscription}

`landlineSubscription`是以物件陣列的形式提供。 每個物件的結構如下所述。

![有線電話訂閱](../../images/field-groups/telecom-subscription/landlineSubscription.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `phoneNumber` | [[!UICONTROL 電話號碼]](../../data-types/telecom-subscription.md) | 指派給此訂閱的電話號碼。 |
| `subscriptionDetails` | [[!UICONTROL 電信訂閱]](../../data-types/telecom-subscription.md) | 說明訂閱的一般詳細資料，包括訂閱長度、費用、狀態等。 |
| `callBlocking` | 布林值 | 指出有線電話訂閱功能是否包含來電封鎖。 |
| `callForwarding` | 布林值 | 指出有線電話訂閱功能是否包含來電轉接。 |
| `callWaiting` | 布林值 | 指出有線電話訂閱功能是否包含來電等候。 |
| `callerID` | 布林值 | 表示有線電話訂閱功能是否包含來電顯示。 |
| `internationalCalling` | 布林值 | 指出有線電話訂閱功能是否包含國際通話。 |
| `minutes` | 整數 | 訂閱內可用的每月分鐘數。 |
| `threeWayCalling` | 布林值 | 指出有線電話訂閱功能是否包含三方通話。 |
| `unlimitedDomesticLongDistance` | 布林值 | 表示有線電話訂閱功能是否包含不限次數的國內長途電話。 |
| `unlimitedLocalCalling` | 布林值 | 指出有線電話訂閱功能是否包含不限次數的當地通話。 |
| `voicemail` | 布林值 | 指出有線電話訂閱功能是否包含語音信箱。 |

{style="table-layout:auto"}

## `mediaSubscription` {#mediaSubscription}

`mediaSubscription`是以物件陣列的形式提供。 每個物件的結構如下所述。

![mediaSubscription](../../images/field-groups/telecom-subscription/mediaSubscription.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `streamingServices` | 物件陣列 | 訂閱所包含的所有串流服務的清單。 每個陣列專案都包含下列屬性： <ul><li>`promotionLength`：如果串流服務已新增為促銷優惠的一部分，則促銷優惠的長度（月數）。</li><li>`promotionalAddition`：指出是否將串流服務新增為促銷優惠的一部分。</li><li>`serviceName`：串流服務的名稱。</li></ul> |
| `subscriptionDetails` | [[!UICONTROL 電信訂閱]](../../data-types/telecom-subscription.md) | 說明訂閱的一般詳細資料，包括訂閱長度、費用、狀態等。 |
| `channels` | 整數 | 媒體訂閱包含的頻道數。 |

{style="table-layout:auto"}

## `mobileSubscription` {#mobileSubscription}

`mobileSubscription`是以物件陣列的形式提供。 每個物件的結構如下所述。

![mobileSubscription](../../images/field-groups/telecom-subscription/mobileSubscription.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `phoneNumber` | [[!UICONTROL 電話號碼]](../../data-types/telecom-subscription.md) | 指派給此訂閱的電話號碼。 |
| `subscriptionDetails` | [[!UICONTROL 電信訂閱]](../../data-types/telecom-subscription.md) | 說明訂閱的一般詳細資料，包括訂閱長度、費用、狀態等。 |
| `earlyUpgradeEnrollment` | 布林值 | 指出客戶是否選擇提早升級。 |
| `planLevel` | 字串 | 指派給此訂閱的行動方案名稱。 |
| `portedNumber` | 布林值 | 指出客戶是否從其他電信業者移轉其號碼。 |

{style="table-layout:auto"}
