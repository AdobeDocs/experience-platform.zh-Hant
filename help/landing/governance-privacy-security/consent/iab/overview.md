---
keywords: Experience Platform；首頁；IAB;IAB 2.0；同意；同意
solution: Experience Platform
title: IAB TCF 2.0支援Experience Platform
topic-legacy: privacy events
description: 了解如何設定資料操作和結構，以在Adobe Experience Platform中的目的地啟用區段時傳達客戶同意選擇。
exl-id: af787adf-b46e-43cf-84ac-dfb0bc274025
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '2558'
ht-degree: 1%

---

# IAB TCF 2.0支援Experience Platform

此 [!DNL Transparency & Consent Framework] (TCF)，如 [!DNL Interactive Advertising Bureau] (IAB)是開放標準的技術架構，旨在讓組織能夠依照歐盟的 [!DNL General Data Protection Regulation] (GDPR)。 框架的第二次迭代TCF 2.0為消費者提供或拒絕同意提供了更大的靈活性，包括供應商是否和如何使用資料處理的某些功能，如精確的地理位置。

>[!NOTE]
>
>如需TCF 2.0的詳細資訊，請參閱 [IAB歐洲網站](https://iabeurope.eu/tcf-2-0/)，包括支援資料和技術規格。

Adobe Experience Platform是 [IAB TCF 2.0廠商清單](https://iabeurope.eu/vendor-list-tcf-v2-0/)，在ID下 **565**. 為符合TCF 2.0要求，Platform可讓您收集客戶同意資料，並將其整合至您儲存的客戶設定檔中。 然後，可根據設定檔的使用案例，將此同意資料納入匯出的受眾區段中。

>[!IMPORTANT]
>
>Platform僅能符合TCF 2.0版（或更新版本）。 不支援舊版TCF。

本檔案概述如何設定您的資料操作和設定檔結構，以接受CMP產生的客戶同意資料，以及Platform在匯出區段時如何傳達使用者同意選擇。

## 先決條件

若要遵循本指南，您必須使用已整合且符合IAB TCF的同意管理平台(CMP)，商業版或自有版皆可。 請參閱 [符合CMP的清單](https://iabeurope.eu/cmp-list/) 以取得更多資訊。

>[!IMPORTANT]
>
>如果CMP的ID無效，Platform會持續依原樣處理您的資料。 若要強制執行TCF 2.0，您必須先確認CMP具有已向IAB TCF 2.0註冊的有效ID，才能將資料傳送至Platform。

此外，本指南也需要妥善了解下列平台服務：

* [Experience Data Model(XDM)](../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
* [Adobe Experience Platform Identity Service](../../../../identity-service/home.md):通過跨裝置和系統橋接身分，解決客戶體驗資料分散帶來的根本難題。
* [即時客戶個人檔案](../../../../profile/home.md):利用 [!DNL Identity Service] 即時從資料集建立詳細的客戶設定檔。 [!DNL Real-time Customer Profile] 從資料湖提取資料，並將客戶設定檔保存在其自己的個別資料存放區中。
* [Adobe Experience Platform Web SDK](../../../../edge/home.md):用戶端JavaScript程式庫，可讓您將各種平台服務整合至您面向客戶的網站。
   * [SDK同意命令](../../../../edge/consent/supporting-consent.md):本指南中所示同意相關SDK命令的使用案例概述。
* [Adobe Experience Platform區段服務](../../../../segmentation/home.md):可讓您將 [!DNL Real-time Customer Profile] 將資料分成具有類似特徵且會對行銷策略做出類似回應的個人群組。

除了上述的Platform服務外，您也應熟悉 [目的地](../../../../data-governance/home.md) 及其在平台生態系統中的角色。

## 客戶同意流程摘要 {#summary}

以下幾節說明在正確設定系統後，如何收集和執行同意資料。

### 同意資料收集

Platform可讓您透過下列程式收集客戶同意資料：

1. 客戶會透過您網站上的對話方塊，提供資料收集的同意偏好設定。
1. 您的CMP會偵測同意偏好設定變更，並據此產生TCF同意資料。
1. 使用Platform Web SDK時，產生的同意資料（由CMP傳回）會傳送至Adobe Experience Platform。
1. 收集的同意資料會擷取至 [!DNL Profile] — 啟用的資料集，其架構包含TCF同意欄位。

除了CMP同意變更鈎點所觸發的SDK命令外，同意資料也可透過任何客戶產生的XDM資料流入Experience Platform，這些資料會直接上傳至 [!DNL Profile] — 已啟用的資料集。

Adobe Audience Manager與Platform共用的任何區段(透過 [!DNL Audience Manager] 來源連接器或其他)也可能包含同意資料，但條件是已透過將適當欄位套用至這些區段 [!DNL Experience Cloud Identity Service]. 如需在 [!DNL Audience Manager]，請參閱 [適用於IAB TCF的Adobe Audience Manager外掛程式](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=zh-Hant).

### 下游同意強制執行

成功擷取TCF同意資料後，下列程式就會在下游Platform服務中進行：

1. [!DNL Real-time Customer Profile] 會更新該客戶設定檔所儲存的同意資料。
1. 只有在為叢集中的每個ID提供了平台(565)的廠商權限時，Platform才會處理客戶ID。
1. 將區段匯出至屬於TCF 2.0廠商清單成員的目的地時，只有在兩個平台的廠商權限皆為時，Platform才會包含設定檔(565) *和* 會針對叢集中的每個ID提供個別目的地。

本檔案的其餘章節提供如何設定Platform和您的資料作業，以符合上述收集和實作需求的指引。

## 決定如何在CMP中產生客戶同意資料 {#consent-data}

由於每個CMP系統都是獨一無二的，因此您必須決定讓客戶在與您的服務互動時提供同意的最佳方式。 達成此目的的常見方式是使用類似下列範例的Cookie同意對話方塊：

![](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

此對話方塊必須允許客戶選擇加入或退出下列項目：

| 同意選項 | 說明 |
| --- | --- |
| **用途** | 用途定義品牌可針對哪些廣告技術用途使用客戶資料。 若要讓Platform處理客戶ID，必須選擇加入下列用途： <ul><li>**目的1**:在設備上儲存和/或訪問資訊</li><li>**目的10**:開發和改進產品</li></ul> |
| **供應商權限** | 除了廣告技術用途以外，對話方塊也必須允許客戶選擇加入或退出讓特定廠商使用其資料，包括Adobe Experience Platform(565)。 |

### 同意字串 {#consent-strings}

無論您使用何種方法來收集資料，目標都是根據客戶選擇的同意選項（稱為同意字串）產生字串值。

在TCF規格中，同意字串可用來針對由政策和廠商所定義的特定行銷用途，編碼有關客戶同意設定的相關詳細資訊。 Platform會利用這些字串來儲存每個客戶的同意設定，因此每次這些設定變更時都必須產生新的同意字串。

同意字串只能由向IAB TCF註冊的CMP建立。 如需如何使用您的特定CMP產生同意字串的詳細資訊，請參閱 [同意字串格式設定指南](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) IAB TCF GitHub存放庫中。

## 使用TCF同意欄位建立資料集 {#datasets}

客戶同意資料必須傳送至其結構包含TCF同意欄位的資料集。 請參閱 [建立資料集以擷取TCF 2.0同意](./dataset.md) 了解如何在繼續使用本指南之前，先建立所需的設定檔資料集（以及選用的「體驗事件」資料集）。

## 更新 [!DNL Profile] 合併原則以包含同意資料 {#merge-policies}

建立 [!DNL Profile] — 啟用資料集以收集同意資料，您必須確定您的合併原則已設定為一律在客戶設定檔中包含TCF同意欄位。 這需要設定資料集優先順序，讓同意資料集優先順序高於其他可能發生衝突的資料集。

有關如何使用合併策略的詳細資訊，請參閱 [合併策略概述](../../../../profile/merge-policies/overview.md). 設定合併原則時，您必須確定區段包含 [XDM隱私權結構欄位群組](./dataset.md#privacy-field-group)，如資料集準備指南所述。

## 整合Experience PlatformWeb SDK以收集客戶同意資料 {#sdk}

>[!NOTE]
>
>若要直接在Adobe Experience Platform中處理同意資料，必須使用Experience PlatformWeb SDK。 [!DNL Experience Cloud Identity Service] 目前不支援。
>
>[!DNL Experience Cloud Identity Service] 不過，Adobe Audience Manager中的同意處理仍支援，且遵循TCF 2.0僅需要將程式庫更新為 [5.0版](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

將CMP設定為產生同意字串後，您必須整合Experience PlatformWeb SDK以收集這些字串，並將其傳送至Platform。 Platform SDK提供兩個命令，可用來將TCF同意資料傳送至Platform（相關說明請見下方子節），當客戶首次提供同意資訊時，以及隨後同意變更時，也應使用。

**SDK不會與任何現成可用的CMP介面**. 您可自行決定如何將SDK整合至您的網站、接聽CMP中的同意變更，並呼叫適當的命令。

### 建立新資料流

若要讓SDK將資料傳送至Experience Platform，您必須先為Platform建立新的資料流。 有關如何建立新資料流的特定步驟，請參閱 [SDK檔案](../../../../edge/datastreams/overview.md).

為資料流提供唯一名稱后，請選取旁邊的切換按鈕 **[!UICONTROL Adobe Experience Platform]**. 接下來，使用下列值來完成表單的其餘部分：

| 資料流欄位 | 值 |
| --- | --- |
| [!UICONTROL 沙箱] | 平台的名稱 [沙箱](../../../../sandboxes/home.md) 包含設定資料流所需的串流連線和資料集。 |
| [!UICONTROL 串流入口] | 有效的串流連線，用於Experience Platform。 請參閱 [建立串流連線](../../../../ingestion/tutorials/create-streaming-connection-ui.md) 如果您沒有現有的串流入口。 |
| [!UICONTROL 事件資料集] | 選取 [!DNL XDM ExperienceEvent] 在 [上一步](#datasets). 如果您包含 [[!UICONTROL IAB TCF 2.0同意] 欄位群組](../../../../xdm/field-groups/event/iab.md) 在此資料集的結構中，您可以使用 [`sendEvent`](#sendEvent) 命令，將資料儲存在此資料集中。 請記得，儲存在此資料集中的同意值是 **not** 用於自動執行工作流程。 |
| [!UICONTROL 設定檔資料集] | 選取 [!DNL XDM Individual Profile] 在 [上一步](#datasets). 回應CMP同意變更鈎點時，請使用 [`setConsent`](#setConsent) 命令，則收集的資料將儲存在此資料集中。 由於此資料集已啟用設定檔，因此儲存在此資料集中的同意值會在自動執行工作流程期間執行。 |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

完成後，請選取 **[!UICONTROL 儲存]** 在畫面底部，並繼續執行任何其他提示以完成設定。

### 執行同意更改命令

建立前一節所述的資料流後，您就可以開始使用SDK命令將同意資料傳送至Platform。 以下各節提供如何在不同案例中使用各個SDK命令的範例。

>[!NOTE]
>
>如需所有Platform SDK命令常見語法的簡介，請參閱 [執行命令](../../../../edge/fundamentals/executing-commands.md).

#### 使用CMP同意變更鈎點 {#setConsent}

許多CMP提供可接聽同意變更事件的現成可用鈎點。 當這些事件發生時，您可以使用 `setConsent` 命令來更新該客戶的同意資料。

此 `setConsent` command需要兩個參數：(1)指出命令類型的字串（在此例中為「setConsent」），以及(2)包含 `consent` 陣列，其中必須包含至少一個提供必要同意欄位的物件，如下所示：

```js
alloy("setConsent", {
  consent: [{
    standard: "IAB TCF",
    version: "2.0",
    value: "CLcVDxRMWfGmWAVAHCENAXCkAKDAADnAABRgA5mdfCKZuYJez-NQm0TBMYA4oCAAGQYIAAAAAAEAIAEgAA.argAC0gAAAAAAAAAAAA",
    gdprApplies: "true"
  }]
});
```

| 裝載屬性 | 說明 |
| --- | --- |
| `standard` | 使用的同意標準。 此值必須設為 `IAB` 以處理TCF 2.0同意。 |
| `version` | 同意標準的版本號碼，在 `standard`. 此值必須設為 `2.0` 以處理TCF 2.0同意。 |
| `value` | CMP產生的base-64編碼同意字串。 |
| `gdprApplies` | 指出GDPR是否適用於目前登入的客戶的布林值。 若要為此客戶強制執行TCF 2.0，值必須設為 `true`. 預設為 `true` 若未定義。 |

此 `setConsent` 命令應作為偵測同意設定變更的CMP連結的一部分。 以下JavaScript提供範例，說明 `setConsent` 命令可用於OneTrust的 `OnConsentChanged` 鈎點：

```js
OneTrust.OnConsentChanged(function () {
  // Retrieve the TCF 2.0 consent data generated by the CMP, and pass it to Alloy. 
  __tcfapi("getTCData", 2, function (data, success) {
    if (success) {
      var tcString = data.tcString;
      var gdpr = data.gdprApplies;

      alloy("setConsent", {
        consent: [{
          standard: "IAB TCF",
          version: "2.0",
          value: tcString,
          gdprApplies: gdpr
        }]
      });
    }
  });
});
```

#### 使用事件 {#sendEvent}

您也可以針對Platform中觸發的每個事件，使用 `sendEvent` 命令。

>[!NOTE]
>
>若要使用此方法，您必須已將體驗事件隱私權欄位群組新增至 [!DNL Profile]已啟用 [!DNL XDM ExperienceEvent] 綱要。 請參閱 [更新ExperienceEvent結構](./dataset.md#event-schema) 資料集準備指南中，提供設定此項目的相關步驟。

此 `sendEvent` 命令在網站的適當事件接聽程式中應作為回呼使用。 命令需要兩個參數：(1)指示命令類型的字串(在本例中， `sendEvent`)和(2)包含 `xdm` 以JSON形式提供必要同意欄位的物件：

```js
alloy("sendEvent", {
  xdm: {
    "consentStrings": [{
      "consentStandard": "IAB TCF",
      "consentStandardVersion": "2.0",
      "consentStringValue": "CLcVDxRMWfGmWAVAHCENAXCkAKDAADnAABRgA5mdfCKZuYJez-NQm0TBMYA4oCAAGQYIAAAAAAEAIAEgAA.argAC0gAAAAAAAAAAAA",
      "gdprApplies": true
    }]
  }
});
```

| 裝載屬性 | 說明 |
| --- | --- |
| `xdm.consentStrings` | 必須至少包含一個物件，且提供必要同意欄位的陣列。 |
| `consentStandard` | 使用的同意標準。 此值必須設為 `IAB` 以處理TCF 2.0同意。 |
| `consentStandardVersion` | 同意標準的版本號碼，在 `standard`. 此值必須設為 `2.0` 以處理TCF 2.0同意。 |
| `consentStringValue` | CMP產生的base-64編碼同意字串。 |
| `gdprApplies` | 指出GDPR是否適用於目前登入的客戶的布林值。 若要為此客戶強制執行TCF 2.0，值必須設為 `true`. 預設為 `true` 若未定義。 |

### 處理SDK回應

全部 [!DNL Platform SDK] 命令返回指示調用是成功還是失敗的承諾。 然後，您可以將這些回應用於其他邏輯，例如向客戶顯示確認訊息。 請參閱 [處理成功或失敗](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) ，請參閱執行特定範例的SDK命令指南。

## 匯出區段 {#export}

>[!NOTE]
>
>開始匯出區段之前，您必須確定區段包含所有必要的同意欄位。 請參閱 [配置合併策略](#merge-policies) 以取得更多資訊。

收集客戶同意資料並建立包含必要同意屬性的對象區段後，您就可以在將這些區段匯出至下游目的地時強制執行TCF 2.0法規遵循。

前提是同意設定 `gdprApplies` 設為 `true` 針對一組客戶設定檔，會根據每個設定檔的TCF同意偏好設定，篩選從這些設定檔匯出至下游目的地的任何資料。 在匯出程式期間，會略過任何不符合必要同意偏好設定的設定檔。

客戶必須同意下列用途(如 [TCF 2.0政策](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions))，以便將其設定檔納入匯出至目的地的區段中：

* **目的1**:在設備上儲存和/或訪問資訊
* **目的10**:開發和改進產品

TCF 2.0也要求資料來源必須先檢查目的地的廠商權限，才能將資料傳送至該目的地。 因此，Platform會先檢查目標的廠商權限是否已針對叢集中的所有ID選擇加入，再納入系結至該目標的資料。

>[!NOTE]
>
>任何與Adobe Audience Manager共用的區段，都會包含與Platform相同的TCF 2.0同意值。 自 [!DNL Audience Manager] 與Platform(565)共用相同的供應商ID，需要相同的用途和供應商權限。 請參閱 [適用於IAB TCF的Adobe Audience Manager外掛程式](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html) 以取得更多資訊。

## 測試您的實作 {#test-implementation}

設定TCF 2.0實作並將區段匯出至目的地後，任何不符合同意要求的資料都不會匯出。 不過，若要查看匯出期間是否篩選了正確的客戶設定檔，您必須手動檢查目的地上的資料存放區，以查看是否正確執行同意。

請務必注意，如果叢集中有多個ID，且TCF 2.0適用，則即使單一ID未包含正確用途和廠商權限，也會排除整個叢集。

## 後續步驟

本檔案說明如何設定您的Platform資料操作，以履行TCF 2.0所概述的業務義務。請參閱 [控管、隱私權和安全性](../../overview.md) 如需詳細資訊，請參閱Platform的隱私權相關功能。
