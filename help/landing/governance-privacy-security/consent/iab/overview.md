---
keywords: Experience Platform;home;IAB;IAB 2.0；同意；同意
solution: Experience Platform
title: IAB TCF 2.0Experience Platform支援
topic: privacy events
description: 瞭解如何設定您的資料作業和結構，以在將區段啟動至Adobe Experience Platform的目的地時傳達客戶同意選擇。
translation-type: tm+mt
source-git-commit: a845ade0fc1e6e18c36b5f837fe7673a976f01c7
workflow-type: tm+mt
source-wordcount: '2472'
ht-degree: 0%

---


# IAB TCF 2.0在Experience Platform方面的支援

[!DNL Transparency & Consent Framework](TCF)是[!DNL Interactive Advertising Bureau](IAB)概述的開放標準技術框架，旨在讓組織能夠根據歐盟的[!DNL General Data Protection Regulation](GDPR)，取得、記錄和更新消費者對個人資料處理的同意。 該框架的第二次迭代—— TCF 2.0 ——賦予消費者如何提供或拒絕同意的更大靈活性，包括供應商是否和如何使用資料處理的某些特徵，如精確地理位置。

>[!NOTE]
>
>有關TCF 2.0的更多資訊可在[IAB歐洲網站](https://iabeurope.eu/tcf-2-0/)上找到，包括支援材料和技術規格。

Adobe Experience Platform是註冊的[IAB TCF 2.0供應商清單](https://iabeurope.eu/vendor-list-tcf-v2-0/)的一部分，該清單位於ID **565**&#x200B;下。 根據TCF 2.0要求，Platform可讓您收集客戶同意資料，並將其整合到您儲存的客戶個人檔案中。 然後，視使用案例而定，可以將此同意資料納入匯出的受眾細分中。

>[!IMPORTANT]
>
>平台僅能符合TCF（或更新版本）的2.0版。 不支援舊版TCF。

本檔案概述如何設定您的資料作業和描述檔結構，以接受您的CMP產生的客戶同意資料，以及平台在匯出區段時如何傳達使用者同意選擇。

## 先決條件

為遵循本指南，您必須使用與IAB TCF整合且符合規範的「同意管理平台」(CMP)，不論是商業或您自己的平台。 有關詳細資訊，請參見[相容CMP的清單](https://iabeurope.eu/cmp-list/)。

>[!IMPORTANT]
>
>如果CMP的ID無效，平台將繼續按原樣處理您的資料。 為了強制實施TCF 2.0，您必須先確認您的CMP具有已向IAB TCF 2.0註冊的有效ID，然後再將資料傳送至平台。

本指南還需要對下列平台服務有良好的理解：

* [體驗資料模型(XDM)](../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
* [Adobe Experience Platform身分服務](../../../../identity-service/home.md):透過跨裝置和系統橋接身分，解決客戶體驗資料分散所帶來的根本挑戰。
* [即時客戶個人檔案](../../../../profile/home.md):利用 [!DNL Identity Service] 資料集即時建立詳細的客戶個人檔案。[!DNL Real-time Customer Profile] 從資料湖提取資料，並將客戶個人檔案保留在其個別的資料儲存中。
* [Adobe Experience Platform網頁SDK](../../../../edge/home.md):用戶端JavaScript程式庫，可讓您將各種平台服務整合至您的客戶導向網站。
   * [SDK同意命令](../../../../edge/consent/supporting-consent.md):本指南中所示同意相關SDK命令的使用案例概述。
* [Adobe Experience Platform區段服務](../../../../segmentation/home.md):可讓您將資料分 [!DNL Real-time Customer Profile] 為具有類似特徵且回應類似行銷策略的個人群組。

除了上述平台服務外，您還應熟悉[目標](../../../../data-governance/home.md)及其在平台生態系統中的角色。

## 客戶同意流程摘要{#summary}

以下各節說明在正確配置系統後如何收集和強制執行許可資料。

### 同意資料收集

平台可讓您透過下列程式收集客戶同意資料：

1. 客戶會透過您網站上的對話方塊提供其資料收集的同意偏好設定。
1. 您的CMP會偵測同意偏好變更，並據以產生TCF同意資料。
1. 使用平台網頁SDK，產生的同意資料（由CMP傳回）會傳送至Adobe Experience Platform。
1. 收集的許可資料被吸收到[!DNL Profile]啟用的資料集中，其模式包含TCF許可欄位。

除了由CMP同意變更勾點觸發的SDK命令外，同意資料也可以透過任何客戶產生的XDM資料流入Experience Platform，這些資料會直接上傳至啟用[!DNL Profile]的資料集。

任何由Adobe Audience Manager（透過[!DNL Audience Manager]來源連接器或其他方式）與平台共用的區段，也可能包含同意資料，但必須透過[!DNL Experience Cloud Identity Service]將這些區段套用適當欄位。 有關在[!DNL Audience Manager]中收集許可資料的詳細資訊，請參閱[Adobe Audience Manager插件中IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html)的文檔。

### 下游許可強制執行

一旦成功吸收了TCF許可資料，下游平台服務將進行以下流程：

1. [!DNL Real-time Customer Profile] 更新該客戶個人檔案的已儲存同意資料。
1. 僅當為群集中的每個ID提供了平台(565)的供應商權限時，平台才處理客戶ID。
1. 當將區段匯出至屬於TCF 2.0廠商清單成員的目的地時，如果為叢集中的每個ID提供平台(565)*和*&#x200B;的廠商權限，平台僅會包含描述檔。

本檔案的其餘章節提供如何設定平台及資料作業以符合上述收集與強制要求的指引。

## 確定如何在CMP中生成客戶許可資料{#consent-data}

由於每個CMP系統都是獨一無二的，因此您必須確定在客戶與您的服務互動時允許他們提供許可的最佳方式。 要達成此目的，常見方式是使用類似下列範例的Cookie同意對話方塊：

![](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

此對話方塊必須允許客戶選擇加入或退出下列項目：

| 同意選項 | 說明 |
| --- | --- |
| **用途** | 用途定義品牌可以使用客戶資料的廣告技術用途。 為了讓平台處理客戶ID，必須選擇下列用途： <ul><li>**目的1**:在裝置上儲存及／或存取資訊</li><li>**目的十**:開發和改進產品</li></ul> |
| **供應商權限** | 除了廣告技術用途外，對話方式還必須允許客戶選擇加入或退出其資料供特定廠商使用，包括Adobe Experience Platform(565)。 |

### 同意字串{#consent-strings}

無論您使用何種方法來收集資料，其目標是根據客戶選擇的同意選項產生字串值，稱為同意字串。

在TCF規格中，同意字串用於根據政策和廠商所定義的特定行銷目的，編碼客戶同意設定的相關詳細資訊。 平台利用這些字串來儲存每個客戶的同意設定，因此每次這些設定變更時都必須產生新的同意字串。

許可字串只能由在IAB TCF中註冊的CMP建立。 有關如何使用特定CMP生成許可字串的詳細資訊，請參閱IAB TCF GitHub repo中的[許可字串格式指南](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md)。

## 使用TCF許可欄位建立資料集{#datasets}

客戶同意資料必須發送到方案包含TCF同意欄位的資料集。 請參閱[建立資料集以擷取TCF 2.0同意](./dataset.md)的教學課程，瞭解如何在繼續本指南之前建立兩個必要的資料集。

## 更新[!DNL Profile]合併政策以包含同意資料{#merge-policies}

在您建立[!DNL Profile]啟用的資料集以收集同意資料後，您必須確保您的合併政策已設定為一律在客戶個人檔案中包含TCF同意欄位。 這包括設定資料集優先順序，讓您的同意資料集優先順序高於其他可能衝突的資料集。

有關如何使用合併策略的詳細資訊，請參閱[合併策略使用手冊](../../../../profile/ui/merge-policies.md)。 設定合併政策時，您必須確保區段包含[XDM隱私權mixin](./dataset.md#privacy-mixin)提供的所有必要同意屬性，如資料集準備指南所述。

## 整合Experience PlatformWeb SDK以收集客戶同意資料{#sdk}

>[!NOTE]
>
>必須使用Experience Platform網頁SDK，才能直接在Adobe Experience Platform處理同意資料。 [!DNL Experience Cloud Identity Service] 目前不支援。
>
>[!DNL Experience Cloud Identity Service] 但是，在Adobe Audience Manager仍支援同意處理，而且符合TCF 2.0隻需將程式庫更新為 [5.0版](https://github.com/Adobe-Marketing-Cloud/id-service/releases)。

在您將CMP設定為產生同意字串後，您必須整合Experience Platform網頁SDK來收集這些字串，並將它們傳送至平台。 Platform SDK提供兩種命令，可用來將TCF同意資料傳送至Platform（如下各節所述），且當客戶首次提供同意資訊時，以及在同意變更後的任何時候，均應使用。

**SDK不會與任何出廠時的CMP介接**。您需自行決定如何將SDK整合至您的網站、聽取CMP中的同意變更，並呼叫適當的命令。

### 建立新的邊緣設定

為了讓SDK傳送資料至Experience Platform，您必須先在[!DNL Adobe Experience Platform Launch]中為平台建立新的邊緣設定。 如何建立新組態的特定步驟，請參閱[SDK檔案](../../../../edge/fundamentals/edge-configuration.md)。

為配置提供唯一名稱后，選擇&#x200B;**[!UICONTROL Adobe Experience Platform]**&#x200B;旁邊的切換按鈕。 接下來，請使用下列值來完成表單的其餘部分：

| Edge configuration欄位 | 值 |
| --- | --- |
| [!UICONTROL 沙盒] | 平台[沙盒](../../../../sandboxes/home.md)的名稱，其中包含設定邊緣配置所需的串流連接和資料集。 |
| [!UICONTROL 串流入口] | 有效的串流連線，以供Experience Platform。 如果您沒有現有的串流入口，請參閱有關建立串流連線的[教學課程。](../../../../ingestion/tutorials/create-streaming-connection-ui.md) |
| [!UICONTROL 事件資料集] | 選擇在[上一步](#datasets)中建立的[!DNL XDM ExperienceEvent]資料集。 |
| [!UICONTROL 描述檔資料集] | 選擇在[上一步](#datasets)中建立的[!DNL XDM Individual Profile]資料集。 |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

完成後，選擇螢幕底部的&#x200B;**[!UICONTROL Save]** ，然後繼續執行任何其他提示以完成配置。

### 進行許可更改命令

在您建立上一節所述的邊緣設定後，您就可以開始使用SDK命令，將同意資料傳送至平台。 以下各節提供如何在不同案例中使用每個SDK命令的範例。

>[!NOTE]
>
>有關所有Platform SDK命令的常見語法的簡介，請參閱[執行命令](../../../../edge/fundamentals/executing-commands.md)上的檔案。

#### 使用CMP許可更改掛接

許多CMP提供立即可用的掛鈎，以監聽許可更改事件。 當發生這些事件時，您可以使用`setConsent`命令來更新該客戶的同意資料。

`setConsent`命令需要兩個參數：(1)指示命令類型的字串（在本例中為「setConmence」），以及(2)包含`consent`陣列的裝載，其中必須包含至少一個提供必要許可欄位的對象，如下所示：

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
| `standard` | 使用許可標準。 對於TCF 2.0許可處理，此值必須設定為`IAB`。 |
| `version` | `standard`下所示同意標準的版本號。 對於TCF 2.0許可處理，此值必須設定為`2.0`。 |
| `value` | 由CMP生成的基本-64編碼的許可字串。 |
| `gdprApplies` | 一個布爾值，它指示GDPR是否適用於當前登錄的客戶。 要為此客戶強制執行TCF 2.0，必須將值設定為`true`。 如果未定義，則預設為`true`。 |

`setConsent`命令應當用作檢測許可設定更改的CMP掛接的一部分。 以下JavaScript提供如何將`setConsent`命令用於OneTrust的`OnConsentChanged`掛接的示例：

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

#### 使用事件

您也可以使用`sendEvent`命令，針對平台中觸發的每個事件收集TCF 2.0同意資料。

>[!NOTE]
>
>若要使用此方法，您必須將[!DNL Experience Event Privacy mixin]新增至已啟用[!DNL Profile]的[!DNL XDM ExperienceEvent]架構。 請參閱資料集準備指南中有關[更新ExperienceEvent架構](./dataset.md#event-schema)的章節，以取得如何設定此架構的步驟。

`sendEvent`命令應當用作您網站上適當事件監聽器的回呼。 該命令需要兩個參數：(1)指出命令類型的字串（在本例中為`sendEvent`），以及(2)包含`xdm`物件的裝載，以JSON形式提供必要的同意欄位：

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
| `xdm.consentStrings` | 必須至少包含一個提供所需許可欄位的對象的陣列。 |
| `consentStandard` | 使用許可標準。 對於TCF 2.0許可處理，此值必須設定為`IAB`。 |
| `consentStandardVersion` | `standard`下所示同意標準的版本號。 對於TCF 2.0許可處理，此值必須設定為`2.0`。 |
| `consentStringValue` | 由CMP生成的基本-64編碼的許可字串。 |
| `gdprApplies` | 一個布爾值，它指示GDPR是否適用於當前登錄的客戶。 要為此客戶強制執行TCF 2.0，必須將值設定為`true`。 如果未定義，則預設為`true`。 |

### 處理SDK回應

所有[!DNL Platform SDK]命令都返回表示呼叫是成功還是失敗的承諾。 然後，您可以將這些回應用於其他邏輯，例如向客戶顯示確認訊息。 如需特定範例，請參閱執行SDK命令指南中有關[處理成功或失敗的章節。](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure)

## 匯出區段{#export}

>[!NOTE]
>
>在開始匯出區段之前，您必須確定區段包含所有必要的同意欄位。 有關詳細資訊，請參閱[配置合併策略](#merge-policies)一節。

在您收集客戶同意資料並建立包含必要同意屬性的受眾細分後，在將這些細分匯出至下游目的地時，您就可以強制執行TCF 2.0規範。

如果對一組客戶配置檔案將許可設定`gdprApplies`設定為`true`，則根據每個配置檔案的TCF許可優先選項過濾從那些導出到下游目的地的配置檔案中的任何資料。 在出口過程中，會跳過任何不符合必要同意偏好的設定檔。

客戶必須同意下列用途（如[TCF 2.0政策](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)所述），才能將其個人檔案納入匯出至目的地的區段：

* **目的1**:在裝置上儲存及／或存取資訊
* **目的十**:開發和改進產品

TCF 2.0還要求資料源必須在向目標發送資料之前檢查目標的供應商權限。 因此，平台會先檢查目標廠商權限是否被選入群集中的所有ID，再包含系結至該目標的資料。

>[!NOTE]
>
>與Adobe Audience Manager共用的任何區段，其TCF 2.0同意值都會與其平台對應項目相同。 由於[!DNL Audience Manager]與平台(565)共用相同的供應商ID，因此需要相同的用途和供應商權限。 如需詳細資訊，請參閱[Adobe Audience ManagerIAB TCF增效模組的檔案。](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html)

## 測試您的實作{#test-implementation}

一旦您設定了TCF 2.0實作並將區段匯出至目的地後，任何不符合同意要求的資料都不會匯出。 不過，為了查看在匯出期間是否篩選了正確的客戶個人檔案，您必須手動檢查目的地上的資料儲存區，以檢視是否正確執行了同意。

請務必注意，如果叢集中有多個ID且套用TCF 2.0，則即使單一ID未包含正確的用途和廠商權限，也會排除整個叢集。

## 後續步驟

本檔案涵蓋設定平台資料作業以符合TCF 2.0所述之業務義務的程式。如需平台隱私權相關功能的詳細資訊，請參閱[控管、隱私權與安全性概觀。](../../overview.md)