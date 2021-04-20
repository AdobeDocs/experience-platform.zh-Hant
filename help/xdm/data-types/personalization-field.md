---
solution: Experience Platform
title: 一般個人化偏好設定欄位資料類型
topic: overview
description: 本檔案提供一般個人化偏好設定欄位XDM資料類型的概述。
translation-type: tm+mt
source-git-commit: 9ca0978cdf42926303d622a4d536ac48bca32e70
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 2%

---


# [!UICONTROL Generic Personalization Preference Field] 資料類型

[!UICONTROL Generic Personalization Preference Field] 是標準的XDM資料類型，它描述了客戶對特定個人化首選項的選擇。

>[!NOTE]
>
>此資料類型旨在使用[[!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)] mixin](../mixins/profile/consents.md)作為基準，自訂組織的同意結構。

![](../images/data-types/personalization-field.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `val` | 字串 | 此個人化使用案例的客戶提供的偏好選擇。 請參閱下表以取得接受的值和定義。 |

下表概述`val`的接受值：

| 值 | 標題 | 說明 |
| --- | --- | --- |
| `y` | 是 | 客戶已選擇加入偏好設定。 換言之，他們&#x200B;**do**&#x200B;同意使用其資料，如有關偏好所示。 |
| `n` | 無 | 客戶已選擇退出偏好設定。 換言之，他們&#x200B;**不同意按照有關偏好使用其資料。** |
| `p` | 待覈實 | 系統尚未收到最終偏好值。 這通常是需要兩步驟驗證的同意的一部分。 例如，如果客戶選擇接收電子郵件，則該同意會設為`p`，直到他們在電子郵件中選擇連結以確認他們提供了正確的電子郵件地址，此時該同意會更新為`y`。<br><br>如果此偏好不使用兩組驗證程式，則該選 `p` 擇可用於指示客戶尚未響應許可提示。例如，您可以在客戶回應同意提示之前，自動將網站第一頁的值設為`p`。 在不需要明確同意的司法管轄區中，您也可以使用該司法管轄區來指出客戶未明確選擇退出（換言之，假定同意）。 |
| `u` | 未知 | 客戶的偏好資訊未知。 |
| `LI` | 合法利益 | 收集並處理資料以達到特定目的的正當商業利益，比其對個人的潛在傷害要大。 |
| `CT` | 合約 | 為達到特定目的而收集資料，是為了履行與個人的合同義務。 |
| `CP` | 遵守法律義務 | 為達到特定目的而收集資料，是為了履行企業的法律義務。 |
| `VI` | 個人的切身利益 | 為了保護個人的切身利益，必須收集符合特定目的的資料。 |
| `PI` | 公共利益 | 為特定目的收集資料，是為了公共利益或行使官方權力而執行的。 |

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/personalization-field.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/personalization-field.schema.json)