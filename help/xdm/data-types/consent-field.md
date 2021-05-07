---
solution: Experience Platform
title: 通用同意欄位資料類型
topic-legacy: overview
description: 本檔案概述「通用同意欄位XDM」資料類型。
exl-id: f1f14eb7-21dd-45ca-8fb4-68f397cfa697
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 1%

---

# [!UICONTROL Generic Consent Field] 資料類型

[!UICONTROL Generic Consent Field] 是一種標準的XDM資料類型，它描述了客戶對特定許可偏好的選擇。

>[!NOTE]
>
>此資料類型旨在使用[[!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)]欄位群組](../field-groups/profile/consents.md)做為基準，自訂您組織的同意結構。

![](../images/data-types/consent-field.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `val` | 字串 | 客戶為此使用案例提供的許可選擇。 請參閱下表以取得接受的值和定義。 |

下表概述`val`的接受值：

| 值 | 標題 | 說明 |
| --- | --- | --- |
| `y` | 是 | 客戶已選擇同意。 換言之，他們&#x200B;**do**&#x200B;同意使用其資料，如有關同意所示。 |
| `n` | 無 | 客戶已選擇不同意。 換言之，他們&#x200B;**不**&#x200B;同意使用其資料，如有關同意所示。 |
| `p` | 待覈實 | 系統尚未獲得最終許可值。 這通常是需要兩步驟驗證的同意的一部分。 例如，如果客戶選擇接收電子郵件，則該同意會設為`p`，直到他們在電子郵件中選擇連結以確認他們提供了正確的電子郵件地址，此時該同意會更新為`y`。<br><br>如果此許可不使用兩組驗證過程，則 `p` 該選擇可用於指示客戶尚未響應許可提示。例如，您可以在客戶回應同意提示之前，自動將網站第一頁的值設為`p`。 在不需要明確同意的司法管轄區中，您也可以使用該司法管轄區來指出客戶未明確選擇退出（換言之，假定同意）。 |
| `u` | 未知 | 客戶的許可資訊未知。 |
| `LI` | 合法利益 | 收集並處理資料以達到特定目的的正當商業利益，比其對個人的潛在傷害要大。 |
| `CT` | 合約 | 為達到特定目的而收集資料，是為了履行與個人的合同義務。 |
| `CP` | 遵守法律義務 | 為達到特定目的而收集資料，是為了履行企業的法律義務。 |
| `VI` | 個人的切身利益 | 為了保護個人的切身利益，必須收集符合特定目的的資料。 |
| `PI` | 公共利益 | 為特定目的收集資料，是為了公共利益或行使官方權力而執行的。 |

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-field.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-field.schema.json)
