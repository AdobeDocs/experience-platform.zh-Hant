---
solution: Experience Platform
title: 一般行銷偏好設定欄位資料類型
topic-legacy: overview
description: 本檔案概述一般行銷偏好欄位XDM資料類型。
exl-id: d4c53885-f34f-4721-aa34-1fe02dc7006f
source-git-commit: bd312024a1a3fb6da840a38d6e9d19fcbd6eab5a
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 2%

---

# [!UICONTROL 一般行銷偏好設] 定欄位資料類型

[!UICONTROL 一般行銷] 偏好設定欄位是描述客戶選擇特定行銷偏好設定的標準XDM資料類型。

>[!NOTE]
>
>此資料類型旨在使用[[!UICONTROL 同意和偏好設定]欄位群組](../field-groups/profile/consents.md)作為基線，自訂組織同意結構。
>
>如果您需要特定行銷偏好設定欄位的`subscriptions`對應，則必須改用訂閱資料類型](./marketing-field-subscriptions.md)的[行銷欄位。

![](../images/data-types/marketing-field.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `reason` | 字串 | 當客戶選擇退出行銷使用案例時，此字串欄位代表客戶選擇退出的原因。 |
| `time` | DateTime | 行銷偏好設定變更時的ISO 8601時間戳記（若適用）。 |
| `val` | 字串 | 此行銷使用案例由客戶提供的偏好選擇。 請參閱下表，了解接受的值和定義。 |

{style=&quot;table-layout:auto&quot;}

下表概述`val`的接受值：

| 值 | 標題 | 說明 |
| --- | --- | --- |
| `y` | 是 | 客戶已選擇加入偏好設定。 換言之，他們&#x200B;**do**&#x200B;同意使用其資料，如相關偏好所示。 |
| `n` | 無 | 客戶已選擇退出首選項。 換言之，他們&#x200B;**不**&#x200B;同意使用其資料，如相關偏好所示。 |
| `p` | 待定驗證 | 系統尚未收到最終首選項值。 這通常用於需要兩步驗證的同意。 例如，如果客戶選擇接收電子郵件，則該同意會設為`p`，直到客戶選擇電子郵件中的連結以確認他們提供了正確的電子郵件地址，此時同意會更新為`y`。<br><br>如果此首選項不使用兩個設定的驗證過程，則 `p` 可以改用該選項指示客戶尚未響應同意提示。例如，您可以在客戶回應同意提示之前，自動將網站第一頁的值設為`p`。 在不需要明確同意的司法管轄區中，您也可以使用該司法管轄區來指出客戶尚未明確選擇退出（亦即假設同意）。 |
| `u` | 未知 | 客戶的首選項資訊未知。 |
| `LI` | 合法利益 | 收集和處理這些資料以達到特定目的的合法商業利益，比它對個人造成的潛在傷害要大。 |
| `CT` | 合約 | 為滿足與個人的合同義務，需要收集特定用途的資料。 |
| `CP` | 遵守法律義務 | 為符合企業的法律義務，需要收集特定用途的資料。 |
| `VI` | 個人的切身利益 | 為了保護個人的切身利益，需要收集資料。 |
| `PI` | 公共利益 | 為特定目的收集資料是為了公共利益或行使官方權力而執行的。 |

{style=&quot;table-layout:auto&quot;}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
