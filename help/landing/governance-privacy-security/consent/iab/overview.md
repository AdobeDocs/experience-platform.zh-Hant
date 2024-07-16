---
keywords: Experience Platform；首頁；IAB；IAB 2.0；同意；同意
solution: Experience Platform
title: Experience Platform中的IAB TCF 2.0支援
description: 瞭解如何設定您的資料作業和結構描述，以在對Adobe Experience Platform中的目的地啟用區段時傳達客戶同意選擇。
exl-id: af787adf-b46e-43cf-84ac-dfb0bc274025
source-git-commit: b08c6cf12a38f79e019544dea91913a77bd6490a
workflow-type: tm+mt
source-wordcount: '2492'
ht-degree: 0%

---

# Experience Platform中的IAB TCF 2.0支援

[!DNL Transparency & Consent Framework] (TCF) (如[!DNL Interactive Advertising Bureau] (IAB)所概述)是開放標準的技術架構，旨在讓組織能夠遵循歐盟的[!DNL General Data Protection Regulation] (GDPR)，取得、記錄及更新消費者同意以處理其個人資料。 此架構的第二個反複專案TCF 2.0為消費者提供或拒絕同意的方式提供更大彈性，包括廠商是否及如何使用特定資料處理功能，例如精確地理位置。

>[!NOTE]
>
>如需有關TCF 2.0的詳細資訊，請參閱[IAB Europe網站](https://iabeurope.eu/)，包括支援資料和技術規格。

Adobe Experience Platform是已登入的[IAB TCF 2.0廠商清單](https://iabeurope.eu/vendor-list-tcf/)的一部分，ID為&#x200B;**565**。 為符合TCF 2.0要求，Platform可讓您收集客戶同意資料，並將其整合至您儲存的客戶設定檔中。 之後，可根據使用者檔案的使用案例，將此同意資料納入是否將使用者檔案納入匯出的受眾區段中。

>[!IMPORTANT]
>
>Platform只能遵守TCF 2.0版（或更新版本）。 不支援舊版TCF。

本檔案概述如何設定您的資料作業和設定檔結構描述，以接受同意管理平台(CMP)產生的客戶同意資料。 此外也說明Platform在匯出區段時，如何傳達使用者的同意選擇。

## 先決條件

若要遵循本指南，您必須使用與IAB TCF整合且相容的商業或您自己的CMP。 如需詳細資訊，請參閱相容CMP的[清單](https://iabeurope.eu/cmp-list/)。

>[!IMPORTANT]
>
>如果CMP的ID無效，Platform會繼續依原樣處理您的資料。 若要強制執行TCF 2.0，您必須先確認您的CMP具備已向IAB TCF 2.0註冊的有效ID，才能將資料傳送至Platform。

本指南也需要您實際瞭解下列Platform服務：

* [體驗資料模型(XDM)](/help/xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
* [Adobe Experience Platform Identity Service](/help/identity-service/home.md)：透過跨裝置和系統橋接身分，解決客戶體驗資料分散所造成的根本挑戰。
* [即時客戶設定檔](/help/profile/home.md)：使用[!DNL Identity Service]從資料集即時建立詳細的客戶設定檔。 [!DNL Real-Time Customer Profile]從資料湖提取資料，並將客戶設定檔儲存在其自己的獨立資料存放區中。
* [Adobe Experience Platform Web SDK](/help/web-sdk/home.md)：使用者端的JavaScript程式庫，可讓您將各種平台服務整合至您面向客戶的網站。
   * [SDK同意命令](../../../../web-sdk/commands/setconsent.md)：本指南中顯示的同意相關SDK命令的使用案例概觀。
* [Adobe Experience Platform區段服務](/help/segmentation/home.md)：可讓您將[!DNL Real-Time Customer Profile]資料分割成共用類似特徵且對行銷策略有類似回應的個人群組。

除了上述Platform服務之外，您也應該熟悉[目的地](/help/data-governance/home.md)及其在平台生態系統中的角色。

## 客戶同意流程摘要 {#summary}

以下幾節將說明在系統正確設定後，如何收集和執行同意資料。

### 同意資料收集

Platform可讓您透過下列程式收集客戶同意資料：

1. 客戶透過您網站上的對話方塊提供其資料收集的同意偏好設定。
1. 您的CMP會偵測同意偏好設定變更，並據此產生TCF同意資料。
1. 使用Platform Web SDK時，產生的同意資料（由CMP傳回）會傳送至Adobe Experience Platform。
1. 收集的同意資料會擷取到已啟用[!DNL Profile]的資料集，其結構描述包含TCF同意欄位。

除了CMP同意變更掛接所觸發的SDK命令外，同意資料也可以透過任何客戶產生的XDM資料流入Experience Platform，這些資料直接上傳至啟用[!DNL Profile]的資料集。

如果透過[!DNL Experience Cloud Identity Service]將適當的欄位套用至這些區段，Adobe Audience Manager與Platform共用的任何區段（透過[!DNL Audience Manager]來源聯結器或其他方式）也可能包含同意資料。 如需在[!DNL Audience Manager]中收集同意資料的詳細資訊，請參閱適用於IAB TCF的[Adobe Audience Manager外掛程式](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=zh-Hant)上的檔案。

### 下游同意實作

成功擷取TCF同意資料後，下游Platform服務中將進行下列程式：

1. [!DNL Real-Time Customer Profile]會更新該客戶設定檔的已儲存同意資料。
1. 只有在為叢集中的每個ID提供Platform (565)的廠商許可權時，Platform才會處理客戶ID。
1. 將區段匯出至屬於TCF 2.0廠商清單成員的目的地時，只有在為叢集中的每個ID提供平台(565) *和*&#x200B;的廠商許可權時，Platform才會包含設定檔。

本檔案的其餘章節提供如何設定Platform和您的資料作業，以符合上述收集和執行要求的指引。

## 決定如何在您的CMP中產生客戶同意資料 {#consent-data}

由於每個CMP系統都是獨一無二的，因此您必須決定讓客戶在與您的服務互動時提供同意的最佳方式。 Cookie同意對話方塊是取得客戶同意的常見方式。 CMP對話方塊的範例如下所示。

![同意管理平台對話方塊範例。](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

此對話方塊必須允許客戶選擇加入或退出下列專案：

| 同意選項 | 說明 |
| --- | --- |
| **目的** | 用途定義品牌可將客戶資料用於哪些廣告技術用途。 Platform必須選擇下列用途來處理客戶ID： <ul><li>**用途1**：儲存和/或存取裝置上的資訊</li><li>**用途10**：開發並改善產品</li></ul> |
| **廠商許可權** | 除了廣告技術用途外，對話方塊也必須允許客戶選擇加入或退出讓特定廠商使用其資料，包括Adobe Experience Platform (565)。 |

### 同意字串 {#consent-strings}

無論您使用何種方法收集資料，目標都是根據客戶選擇的同意選項產生字串值，稱為同意字串。

在TCF規格中，同意字串是用來根據政策和廠商定義的特定行銷目的，編碼有關客戶同意設定的相關細節。 Platform會使用這些字串來儲存每個客戶的同意設定，因此，每次這些設定變更時，都必須產生新的同意字串。

同意字串只能由在IAB TCF註冊的CMP建立。 如需有關如何使用您的特定CMP產生同意字串的詳細資訊，請參閱IAB TCF GitHub存放庫中的[同意字串格式設定指南](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md)。

## 使用TCF同意欄位建立資料集 {#datasets}

客戶同意資料必須傳送至其結構描述包含TCF同意欄位的資料集。 請參閱有關[建立資料集以擷取TCF 2.0同意](./dataset.md)的教學課程，以瞭解如何建立必要的設定檔資料集（和選用的體驗事件資料集），然後再繼續本指南。

## 更新[!DNL Profile]合併原則以包含同意資料 {#merge-policies}

建立啟用[!DNL Profile]的資料集以收集同意資料後，您必須確保合併原則已設定為在客戶設定檔中一律包含TCF同意欄位。 這涉及設定資料集優先順序，讓您的同意資料集能比其他潛在衝突的資料集優先處理。

有關如何使用合併原則的詳細資訊，請參閱[合併原則概觀](/help/profile/merge-policies/overview.md)。 在設定合併原則時，您必須確保區段包含[XDM隱私權結構描述欄位群組](./dataset.md#privacy-field-group)提供的所有必要同意屬性，如資料集準備指南中所述。

## 整合Experience PlatformWeb SDK以收集客戶同意資料 {#sdk}

>[!NOTE]
>
>若要直接在Adobe Experience Platform中處理同意資料，則必須使用Experience Platform Web SDK。 不支援[!DNL Experience Cloud Identity Service]。
>
>在Adobe Audience Manager中仍支援[!DNL Experience Cloud Identity Service]的同意處理，但只要將程式庫更新為[5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases)版，才能符合TCF 2.0規範。

將CMP設定為產生同意字串後，您必須整合Experience PlatformWeb SDK以收集這些字串並傳送至Platform。 Platform SDK提供兩個命令，可用來將TCF同意資料傳送至Platform （以下小節說明）。 當客戶首次提供同意資訊，且同意其後隨時變更時，應使用這些命令。

**SDK未與任何現成的CMP介面**。 您可以自行決定如何將SDK整合至您的網站、接聽CMP中的同意變更，以及呼叫適當的命令。

### 建立資料串流

為了讓SDK將資料傳送至Experience Platform，您必須先為Platform建立資料串流。 [SDK檔案](/help/datastreams/overview.md)提供了如何建立資料串流的特定步驟。

為資料流提供唯一名稱后，請選取&#x200B;**[!UICONTROL Adobe Experience Platform]**&#x200B;旁的切換按鈕。 接下來，使用下列值完成表單的其餘部分：

| 資料流欄位 | 值 |
| --- | --- |
| [!UICONTROL 沙箱] | 平台[沙箱](/help/sandboxes/home.md)的名稱，其中包含設定資料串流所需的串流連線和資料集。 |
| [!UICONTROL 串流入口] | 適用於Experience Platform的有效串流連線。 如果您沒有現有的串流入口，請參閱有關[建立串流連線](/help/ingestion/tutorials/create-streaming-connection-ui.md)的教學課程。 |
| [!UICONTROL 事件資料集] | 選取在[先前的步驟](#datasets)中建立的[!DNL XDM ExperienceEvent]資料集。 如果您在此資料集的結構描述中包含[[!UICONTROL IAB TCF 2.0同意]欄位群組](/help/xdm/field-groups/event/iab.md)，您可以使用[`sendEvent`](#sendEvent)命令追蹤一段時間的同意變更事件，並將該資料儲存在此資料集中。 請記住，儲存在此資料集中的同意值&#x200B;**並非**&#x200B;用於自動執行工作流程。 |
| [!UICONTROL 設定檔資料集] | 選取在[先前的步驟](#datasets)中建立的[!DNL XDM Individual Profile]資料集。 使用[`setConsent`](#setConsent)命令回應CMP同意變更掛接時，收集的資料會儲存在此資料集中。 由於此資料集已啟用設定檔功能，在自動執行工作流程期間，將會接受儲存在此資料集中的同意值。 |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

完成時，選取畫面底部的&#x200B;**[!UICONTROL 儲存]**，然後繼續依照其他提示完成設定。

### 發出同意變更命令

建立上節所述的資料流後，您就可以開始使用SDK命令將同意資料傳送至Platform。 以下各節提供如何在不同情境中使用每個SDK命令的範例。

#### 使用CMP同意變更掛接 {#setConsent}

許多CMP提供可監聽同意變更事件的現成鉤點。 發生這些事件時，您可以使用[`setConsent`](/help/web-sdk/commands/setconsent.md)命令來更新該客戶的同意資料。

`setConsent`命令需要兩個引數：

1. 指出命令型別的字串（在此例中為「setConsent」）。
1. 包含`consent`陣列的裝載。 陣列必須至少包含一個提供必要同意欄位的物件。

`setConsent`命令顯示如下：

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
| `standard` | 使用的同意標準。 此值必須設定為`IAB`，才可進行TCF 2.0同意處理。 |
| `version` | 在`standard`下表示的同意標準的版本號碼。 此值必須設定為`2.0`，才可進行TCF 2.0同意處理。 |
| `value` | CMP產生的base-64編碼同意字串。 |
| `gdprApplies` | 布林值，指出GDPR是否適用於目前登入的客戶。 若要針對此客戶強制執行TCF 2.0，值必須設為`true`。 如果未定義，則預設為`true`。 |

`setConsent`命令應該當做CMP連結的一部分使用，以偵測同意設定中的變更。 下列JavaScript提供如何將`setConsent`命令用於OneTrust的`OnConsentChanged`鉤點的範例：

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

您也可以使用`sendEvent`命令，在Platform中觸發的每個事件上收集TCF 2.0同意資料。

>[!NOTE]
>
>若要使用此方法，您必須已將「體驗事件隱私權」欄位群組新增至已啟用[!DNL Profile]的[!DNL XDM ExperienceEvent]結構描述。 請參閱資料集準備指南中有關[更新ExperienceEvent結構描述](./dataset.md#event-schema)的章節，以瞭解如何設定此內容的步驟。

`sendEvent`命令應在您網站上的適當事件接聽程式中作為回呼。 命令需要兩個引數：(1)指出命令型別的字串（在此例中為`sendEvent`），以及(2)包含`xdm`物件的裝載（提供必要的同意欄位做為JSON）：

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
| `xdm.consentStrings` | 一個陣列，其中必須至少包含一個提供必要同意欄位的物件。 |
| `consentStandard` | 使用的同意標準。 此值必須設定為`IAB`，才可進行TCF 2.0同意處理。 |
| `consentStandardVersion` | 在`standard`下表示的同意標準的版本號碼。 此值必須設定為`2.0`，才可進行TCF 2.0同意處理。 |
| `consentStringValue` | CMP產生的base-64編碼同意字串。 |
| `gdprApplies` | 布林值，指出GDPR是否適用於目前登入的客戶。 若要針對此客戶強制執行TCF 2.0，值必須設為`true`。 如果未定義，則預設為`true`。 |

### 處理SDK回應

許多Web SDK命令會傳回promise，指出呼叫成功或失敗。 然後，您可以將這些回應用於其他邏輯，例如向客戶顯示確認訊息。 如需詳細資訊，請參閱[命令回應](/help/web-sdk/commands/command-responses.md)。

## 匯出區段 {#export}

>[!NOTE]
>
>開始匯出區段之前，您必須確定區段包含所有必要的同意欄位。 如需詳細資訊，請參閱[設定合併原則](#merge-policies)的相關章節。

收集客戶同意資料並建立包含所需同意屬性的受眾區段後，您就可以在將這些區段匯出至下游目的地時強制執行TCF 2.0合規性。

如果一組客戶設定檔的同意設定`gdprApplies`設為`true`，則系統會根據每個設定檔的TCF同意偏好設定，篩選這些設定檔中匯出至下游目的地的任何資料。 匯出程式會略過不符合必要同意偏好設定的任何設定檔。

客戶必須同意以下目的（如[TCF 2.0原則](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)所概述），其設定檔才能包含在匯出至目的地的區段中：

* **用途1**：儲存和/或存取裝置上的資訊
* **用途10**：開發並改善產品

TCF 2.0也要求資料來源在將資料傳送至目的地之前，必須先檢查目的地的廠商許可權。 因此，在包含繫結至該目的地的資料之前，Platform會先檢查是否已針對叢集中的所有ID選擇加入目的地的廠商許可權。

>[!NOTE]
>
>與Adobe Audience Manager共用的任何區段都會包含與其Platform對應專案相同的TCF 2.0同意值。 由於[!DNL Audience Manager]與Platform (565)共用相同的廠商ID，因此需要相同的用途和廠商許可權。 如需詳細資訊，請參閱適用於IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=zh-Hant)的[Adobe Audience Manager外掛程式上的檔案。

## 測試您的實作 {#test-implementation}

一旦您設定好TCF 2.0實作並將區段匯出至目的地後，任何不符合約意要求的資料都不會匯出。 若要檢視在匯出期間是否篩選了正確的客戶設定檔，您必須手動檢查目的地上的資料存放區，以檢視是否正確強制執行同意。

>[!IMPORTANT]
>
>如果叢集是由多個ID組成，且套用TCF 2.0，則即使單一ID不包含正確的用途和廠商許可權，也會排除整個叢集。

## 後續步驟

本檔案說明如何依照TCF 2.0概述，設定Platform資料作業，以履行您的業務義務。如需有關Platform隱私權相關功能的詳細資訊，請參閱[治理、隱私權及安全性](../../overview.md)的概觀。
