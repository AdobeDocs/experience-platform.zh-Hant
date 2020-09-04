---
keywords: Experience Platform;home;IAB;IAB 2.0;consent;Consent
solution: Experience Platform
title: 即時客戶資料平台中的IAB TCF 2.0支援
topic: privacy events
description: 本文檔提供了設定兩個收集IAB TCF 2.0許可資料所需資料集的步驟。
translation-type: tm+mt
source-git-commit: 172710c62b6f60de74e05364edb1191fbba0ff64
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 0%

---


# 建立資料集，以擷取IAB TCF 2.0同意資料

為了根 [!DNL Real-time Customer Data Platform] 據IAB [!DNL Transparency & Consent Framework] (TCF)2.0處理客戶同意資料，必須將該資料發送到方案包含TCF 2.0許可欄位的資料集。

具體來說，捕獲TCF 2.0許可資料需要兩個資料集：

* 基於類的資料 [!DNL XDM Individual Profile] 集，可在中使用 [!DNL Real-time Customer Profile]。
* 基於類的資料 [!DNL XDM ExperienceEvent] 集。

本文檔提供了設定這兩個資料集以收集IAB TCF 2.0許可資料的步驟。 有關為TCF 2.0配置的完 [!DNL Real-time CDP] 整工作流程的概述，請參閱 [IAB TCF 2.0合規性概述](./overview.md)。

## 必要條件

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [體驗資料模型(XDM)](../../../xdm/home.md):組織客戶體驗資料 [!DNL Experience Platform] 的標準化架構。
   * [架構構成基礎](../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊。
   * [在UI中建立結構](../../../xdm/tutorials/create-schema-ui.md):教學課程，介紹使用架構編輯器的基本知識。
* [Adobe Experience Platform Identity Service](../../../identity-service/home.md):可讓您跨裝置和系統，從不同的資料來源橋接客戶身份。
* [即時客戶個人檔案](../../../profile/home.md):利用 [!DNL Identity Service] 這些工具，您可以即時從資料集建立詳細的客戶個人檔案。 [!DNL Real-time Customer Profile] 從資料湖提取資料，並將客戶個人檔案保留在其個別的資料儲存中。

## 許可方案結構 {#structure}

TCF 2.0支援需要提供兩個XDM混合，它們提供客戶許可欄位：一個用於記錄型資料([!DNL XDM Individual Profile])，另一個用於基於時間序列的資料([!DNL XDM ExperienceEvent]):

| 結構 | 說明 |
| --- | --- |
| 描述檔隱私權混合 | 此混音擷取客戶目前的同意偏好。 在啟用的方 [!DNL Profile]案中使用時，此混合中提供的值被視為許可執行應如何應用於客戶資料的真理來源。 |
| [!DNL Experience Event] 隱私混音 | 此混音會擷取客戶在特定時間點的同意偏好。 在這些欄位中擷取的資料可用於追蹤客戶隨時間變更的同意偏好。 |

雖然每個混音的使用案例不同，但它們提供的特定欄位大致相同。 下節將進一步說明這些欄位。

### 領域中的許可混合 {#privacy-mixin}

雖然每個隱私混合在結構和包含的欄位類型上都有所不同，但它們都提供屬性 `xdm:consentString` ,TCF 2.0強制實施需要子欄位。 這些欄位的結構如下所示，以及它們預期的值類型：

```json
{
  "xdm:consentString": {
    "xdm:consentStandard": "IAB TCF",
    "xdm:consentStandardVersion": "2.0",
    "xdm:consentStringValue": "BObdrPUOevsguAfDqFENCNAAAAAmeAAA.PVAfDObdrA.DqFENCAmeAENCDA",
    "xdm:gdprApplies": true,
    "xdm:containsPersonalData": false
  }
}
```

| 屬性 | 說明 |
| --- | --- |
| `xdm:consentString` | 包含客戶的更新同意資料和其他情境資訊。 |
| `xdm:consentStandard` | 資料適用的同意框架。 對於TCF合規性，值應為&quot;IAB TCF&quot;。 |
| `xdm:consentStandardVersion` | 所示同意框架的版本號 `xdm:consentStandard`。 對於TCF 2.0合規性，值應為&quot;2.0&quot;。 |
| `xdm:consentStringValue` | 根據客戶所選取的許可設定生成的許可字串。 |
| `xdm:gdprApplies` | 一個布爾值，指示GDPR是否適用於此客戶。 值必須設定為&quot;true&quot;才能執行TCF 2.0。 若未包含，預設為「false」。 |
| `xdm:containsPersonalData` | 指示許可更新是否包含個人資料的布爾值。 若未包含，預設為「false」。 |

## 建立客戶同意方案 {#create-schemas}

在平台UI中，按一下左 **[!UICONTROL 側導覽中]** ，以開啟 *[!UICONTROL 結構]工作區*。 從這裡，請依照下列各節中的步驟建立每個必要的架構。

>[!NOTE]
>
>如果您有想要用來擷取同意資料的現有XDM結構，您可以編輯這些結構，而不是建立新的結構。 但是，編輯現有的架構時，請務必遵循架構演 [化的原則](../../../xdm/schema/composition.md#evolution) ，以避免中斷變更。

### 建立記錄型同意方案 {#profile-schema}

從「方 **[!UICONTROL 案]** 」工作區的「瀏 **[!UICONTROL 覽]」標籤中，根據類別建立新**&#x200B;方案 **[!DNL XDM Individual Profile]**。 在「架構編輯器」中開啟架構後，按一 **[!UICONTROL 下畫布左側]** 「 **[!UICONTROL Mixins]** 」區段下的「新增」。

![](../assets/iab/add-mixin-profile.png)

此時將 **[!UICONTROL 顯示「添加混音]** 」對話框。 從這裡，從清 **[!UICONTROL 單中選擇]** 「設定檔隱私權」。 您可選擇使用搜尋列縮小結果，以更輕鬆地找到混音。 在選取混音後，按一下「新 **[!UICONTROL 增混音」]**。

![](../assets/iab/add-profile-privacy.png)

「架構編輯器」畫布會重新出現，可讓您檢視新增同意字串欄位的結構。

![](../assets/iab/profile-privacy-structure.png)

從這裡，重複上述步驟，將下列其他混音新增至架構：

* [!UICONTROL IdentityMap]
* [!UICONTROL 描述檔的資料擷取區域]
* [!UICONTROL 個人資料詳細資訊]
* [!UICONTROL 個人資料詳細資訊]

![](../assets/iab/profile-all-mixins.png)

如果您正在編輯已啟用供使用的現有架構，請按一下「儲存」 [!DNL Real-time Customer Profile]以確認您所做的變更，然後跳至「根據您的同意架構 **[!UICONTROL 建立資料集」一節]**[](#dataset)。 如果要建立新模式，請繼續遵循下面子部分中概述的步驟。

#### 啟用模式以用於 [!DNL Real-time Customer Profile]

為了將其 [!DNL Real-time CDP] 接收的許可資料與特定客戶配置檔案關聯，必須啟用許可方案以便在中使用 [!DNL Real-time Customer Profile]。

>[!NOTE]
>
>本節中顯示的示例方案使用其 `identityMap` 欄位作為主標識。 如果您想要將另一個欄位設為主要身分識別，請確定您使用的是Cookie ID等間接識別碼，而不是禁止在喜好式廣告（例如電子郵件地址）中使用的直接識別欄位。 如果您不確定哪些欄位受限制，請洽詢您的法律顧問。
>
>有關如何為架構設定主標識欄位的步驟，請參見架構創 [建教程](../../../xdm/tutorials/create-schema-ui.md#identity-field)。

要啟用架構 [!DNL Profile]，請按一下左側邊欄中的架構名稱，以開啟右側邊欄中的 **[!UICONTROL 架構屬性]** 對話框。 在這裡，按一下「描述 **[!UICONTROL 檔]** 」切換按鈕。

![](../assets/iab/profile-enable-profile.png)

出現一個快顯視窗，指出遺失主要識別。 選中用於使用備用主要標識的複選框，因為主要標識將包含在identityMap欄位中。

<img src="../assets/iab/missing-primary-identity.png" width="600" /><br>

最後，按一 **[!UICONTROL 下「儲存]** 」以確認變更。

![](../assets/iab/profile-save.png)

### 建立基於時間序列的許可模式 {#event-schema}

從「方 **[!UICONTROL 案]** 」工作區的「瀏 **[!UICONTROL 覽]」標籤中，根據類別建立新**&#x200B;方案 **[!DNL XDM ExperienceEvent]**。 在「架構編輯器」中開啟架構後，按一 **[!UICONTROL 下畫布左側]** 「 **[!UICONTROL Mixins]** 」區段下的「新增」。

![](../assets/iab/add-mixin-event.png)

此時將 **[!UICONTROL 顯示「添加混音]** 」對話框。 在此處，從清 **[!UICONTROL 單中選取「體驗事件隱私權]** 混合」。 您可選擇使用搜尋列縮小結果，以更輕鬆地找到混音。 在選取混音後，按一下「新 **[!UICONTROL 增混音」]**。

![](../assets/iab/add-event-privacy.png)

重新出現「結構編輯器」畫布，顯示新增的同意字串欄位。

![](../assets/iab/event-privacy-structure.png)

從這裡，重複上述步驟，將下列其他混音新增至架構：

* [!UICONTROL IdentityMap]
* [!UICONTROL ExperienceEvent環境詳細資訊]
* [!UICONTROL ExperienceEvent網頁詳細資訊]
* [!UICONTROL ExperienceEvent實作詳細資訊]

加入混音後，按一下「儲存」即 **[!UICONTROL 可完成]**。

![](../assets/iab/event-all-mixins.png)

## 根據您的同意方案建立資料集 {#datasets}

對於上述每個必要的結構描述，您必須建立資料集，以最終收錄客戶的同意資料。 必須為啟用基於 [!DNL XDM Individual Profile] 模式的資料集 [!DNL Real-time Customer Profile]，而不應為啟用基於 [!DNL XDM ExperienceEvent] 模式的資料集 [!DNL Profile]。

首先，在左側導 **[!UICONTROL 覽中選取「資料集]** 」，然後按一下右上角 **[!UICONTROL 的「建立資料集]** 」。

![](../assets/iab/dataset-create.png)

在下一頁，選擇「從 **[!UICONTROL 架構建立資料集」]**。

![](../assets/iab/dataset-create-from-schema.png)

將出 **[!UICONTROL 現「從架構建立資料集]** 」工作流，從「選擇 **[!UICONTROL 架構」步驟開始]** 。 在提供的清單中，找出您先前建立的其中一個同意方案。 您可以選擇使用搜尋來縮小結果範圍，並更輕鬆地尋找結構。 按一下方案旁邊的單選按鈕以選擇它，然後按一下「下 **[!UICONTROL 一步]** 」繼續。

![](../assets/iab/dataset-select-schema.png)

此時會 **[!UICONTROL 顯示「設定資料集]** 」步驟。 在按一下「完成」前，請為資料集提供唯一、可輕鬆識別的名稱和 **[!UICONTROL 說明]**。

![](../assets/iab/dataset-configure.png)

此時會顯示新建立資料集的詳細資料頁面。 如果資料集是以您的方 [!DNL XDM ExperienceEvent] 案為基礎，則程式已完成。 如果資料集是以您的方 [!DNL XDM Individual Profile] 案為基礎，則程式的最後步驟是啟用資料集以供使用 [!DNL Real-time Customer Profile]。 在右側邊欄中，按一下「描述檔 **[!UICONTROL 切換]** 」按鈕以啟用資料集。

![](../assets/iab/dataset-enable-profile.png)

請再次遵循上述步驟，以建立符合TCF 2.0規範的其他必要資料集。

## 後續步驟

按照本教程，您已建立了兩個資料集，現在可用於收集客戶同意資料：

* 根據 [!DNL Profile]您的架構啟用的資 [!DNL XDM Individual Profile] 料集。
* 根據未啟用的 [!DNL XDM ExperienceEvent] 架構的資料集 [!DNL Profile]。

您現在可以返回 [IAB TCF 2.0概觀](./overview.md#merge-policies) ，以繼續設定 [!DNL Real-time CDP] TCF 2.0合規性的程式。