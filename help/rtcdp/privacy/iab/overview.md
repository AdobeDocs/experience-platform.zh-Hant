---
keywords: Experience Platform;home;IAB;IAB 2.0;
solution: Experience Platform
title: 即時客戶資料平台中的IAB TCF 2.0支援
topic: privacy events
translation-type: tm+mt
source-git-commit: 350526e172b4ec3cf3b8cbe4d96f7b771aa1d669
workflow-type: tm+mt
source-wordcount: '2373'
ht-degree: 1%

---


# IAB TCF 2.0支援 [!DNL Real-time Customer Data Platform]

如 [!DNL Transparency & Consent Framework] (IAB)所概述的(TCF)是開放標準的技術框架，旨在讓組織能夠根據歐盟的 [!DNL Interactive Advertising Bureau][!DNL General Data Protection Regulation] (GDPR)，獲得、記錄和更新消費者對處理其個人資料的同意。 該框架的第二次迭代—— TCF 2.0 ——賦予消費者如何提供或拒絕同意的更大靈活性，包括供應商是否和如何使用資料處理的某些特徵，如精確地理位置。

>[!NOTE]
>
>有關TCF 2.0的更多資訊可在 [IAB歐洲網站上找到](https://iabeurope.eu/tcf-2-0/)，包括支援資料和技術規格。

[!DNL Real-time Customer Data Platform (Real-time CDP)] 是已註冊 [IAB TCF 2.0廠商清單的一部分](https://iabeurope.eu/vendor-list-tcf-v2-0/)，位於ID **565下**。 符合TCF 2.0要求，可讓 [!DNL Real-time CDP] 您收集客戶同意資料，並將其整合到儲存的客戶個人檔案中。 然後，視使用案例而定，可以將此同意資料納入匯出的受眾細分中。

>[!IMPORTANT]
>
>[!DNL Real-time CDP] 僅能符合TCF（或更新版本）的2.0版。 不支援舊版TCF。

本文檔概述了如何配置您的資料操作和概要檔案結構以接受由CMP生成的客戶許可資料，以及在導出段時如 [!DNL Real-time CDP] 何傳達用戶許可選擇。

## 必要條件

為遵循本指南，您必須使用與IAB TCF整合且符合規範的「同意管理平台」(CMP)，不論是商業或您自己的平台。 有關詳細 [資訊，請參見](https://iabeurope.eu/cmp-list/) 「相容CMP」清單。

>[!IMPORTANT]
>
>如果CMP的ID無效， [!DNL Real-time CDP] 將繼續按原樣處理您的資料。 為了強制執行TCF 2.0，您必須先確認您的CMP具有已向IAB TCF 2.0註冊的有效ID，然後再將資料發送到 [!DNL Experience Platform]。

本指南也需要對下列Adobe Experience Platform服務有良好的認識：

* [體驗資料模型(XDM)](../../../xdm/home.md):組織客戶體驗資料 [!DNL Experience Platform] 的標準化架構。
* [Adobe Experience Platform Identity Service](../../../identity-service/home.md):透過跨裝置和系統橋接身分，解決客戶體驗資料分散所帶來的根本挑戰。
* [即時客戶個人檔案](../../../profile/home.md):利用 [!DNL Identity Service] 資料集即時建立詳細的客戶個人檔案。 [!DNL Real-time Customer Profile] 從資料湖提取資料，並將客戶個人檔案保留在其個別的資料儲存中。
* [Adobe Experience Platform Web SDK](../../../edge/home.md):用戶端JavaScript程式庫，可讓您將各種服務整 [!DNL Platform] 合至您的客戶導向網站。
* [Adobe Experience Platform細分服務](../../../segmentation/home.md):可讓您將資料分 [!DNL Real-time Customer Profile] 為具有類似特徵且回應類似行銷策略的個人群組。

除了上述 [!DNL Platform] 服務外，您也應熟悉目 [的地](../../destinations/destinations-overview.md) 及其用途 [!DNL Real-time CDP]。

## 客戶同意流程摘要 {#summary}

以下各節說明在正確配置系統後如何收集和強制執行許可資料。

### 同意資料收集

[!DNL Real-time CDP] 允許您通過以下流程收集客戶同意資料：

1. 客戶會透過您網站上的對話方塊提供其資料收集的同意偏好設定。
1. 您的CMP會偵測同意偏好變更，並據以產生IAB同意資料。
1. 使用 [!DNL Experience Platform Web SDK]時，產生的同意資料（由CMP傳回）會傳送至Adobe Experience Platform。
1. 所收集的許可資料被吸收到其模式 [!DNL Profile]包含IAB許可欄位的啟用資料集中。

除了由CMP同意變更勾點觸發的SDK指令外，同意資料也可透過任何客戶產生的 [!DNL Experience Platform] XDM資料流入，這些資料會直接上傳至啟用 [!DNL Profile]的資料集。

Adobe Audience Manager（透過來源連接器或其他方式）共用的任何區段也可能包含同意資料，但是適當的欄位已套用至這些區段 [!DNL Platform][!DNL Audience Manager][!DNL Experience Cloud Identity Service]。 如需有關在中收集同意資料的 [!DNL Audience Manager]詳細資訊，請參閱 [Adobe Audience Manager增效模組for IAB TCF中的檔案](https://docs.adobe.com/help/zh-Hant/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html)。

### 下游許可強制執行

一旦成功吸收了IAB許可資料，下游服務將進行以下流 [!DNL Real-time CDP] 程：

1. [!DNL Real-time Customer Profile] 更新該客戶個人檔案的已儲存同意資料。
1. [!DNL Real-time CDP] 僅當為群集中的每個ID提 [!DNL Real-time CDP] 供(565)的供應商權限時，才處理客戶ID。
1. 將段導出到屬於TCF 2.0供應商清單成員的目標時， [!DNL Real-time CDP] 僅包括如果為群集中的每個ID提供了 [!DNL Real-time CDP] (565) ** 和目標的供應商權限的配置檔案。

本檔案的其餘章節提供如何設定和資料作業，以 [!DNL Real-time CDP] 滿足上述收集和強制要求的指導。

## 確定如何在CMP中生成客戶同意資料 {#consent-data}

由於每個CMP系統都是獨一無二的，因此您必須確定在客戶與您的服務互動時允許他們提供許可的最佳方式。 要達成此目的，常見方式是使用類似下列範例的Cookie同意對話方塊：

![](../assets/iab/cmp-dialog.png)

此對話方塊必須允許客戶選擇加入或退出下列項目：

| 同意選項 | 說明 |
| --- | --- |
| **用途** | 用途定義品牌可以使用客戶資料的廣告技術用途。 要處理客戶ID，必須選擇 [!DNL Real-time CDP] 下列用途： <ul><li>**目的1**:在裝置上儲存及／或存取資訊</li><li>**目的十**:開發和改進產品</li></ul> |
| **供應商權限** | 除了廣告技術用途外，對話方塊還必須允許客戶選擇加入或退出特定廠商使用其資料，包括 [!DNL  Real-time CDP] (565)。 |

### 許可條件 {#consent-strings}

無論您使用何種方法來收集資料，其目標是根據客戶選擇的同意選項產生字串值，稱為同 **意字串**。

在TCF規格中，同意字串用於根據政策和廠商所定義的特定行銷目的編碼客戶同意設定的相關詳細資訊。 [!DNL Real-time CDP] 使用這些字串來儲存每個客戶的同意設定，因此每次這些設定變更時都必須產生新的同意字串。

許可字串只能由在IAB TCF中註冊的CMP建立。 有關如何使用特定CMP生成許可字串的詳細資訊，請參 [閱IAB TCF GitHub repo](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) 中的許可字串格式指南。

## 使用IAB許可欄位建立資料集 {#datasets}

客戶同意資料必須發送到模式包含IAB許可欄位的資料集。 請參閱有關建立資 [料集以取得TCF 2.0同意的教學課程](./dataset-preparation.md) ，瞭解如何在繼續本指南之前建立兩個必要的資料集。

## 更新 [!DNL Profile] 合併政策以包含同意資料 {#merge-policies}

在您建立啟用資 [!DNL Profile]料集以收集同意資料後，您必須確定您的合併政策已設定為一律在客戶個人檔案中包含IAB同意欄位。 這包括設定資料集優先順序，讓您的同意資料集優先順序高於其他可能衝突的資料集。

有關如何使用合併策略的詳細資訊，請參閱合 [並策略使用手冊](../../../profile/ui/merge-policies.md)。 設定合併政策時，您必須確保區段包含 [XDM隱私權混合所提供的所有必要同意屬性](./dataset-preparation.md#privacy-mixin)，如資料集準備指南所述。

## 整合 [!DNL Experience Platform] Web SDK以收集客戶同意資料 {#sdk}

>[!NOTE]
>
>必須使用 [!DNL Experience Platform] Web SDK，才能直接在Adobe Experience Platform中處理同意資料。 [!DNL Experience Cloud Identity Service] 目前不支援。
>
>[!DNL Experience Cloud Identity Service] 但是，Adobe Audience Manager仍支援同意處理，而且符合TCF 2.0隻需將程式庫更新為5.0 [版](https://github.com/Adobe-Marketing-Cloud/id-service/releases)。

在您將CMP設定為產生同意字串後，您必須整合 [!DNL Experience Platform] Web SDK來收集這些字串並傳送給 [!DNL Platform]。 SDK提 [!DNL Platform] 供兩種命令，可用來將IAB同意資料傳送至平台（如下各節所述），當客戶首次提供同意資訊以及同意變更後的任何時間，均應使用。

**SDK不會與任何出廠時的CMP介接**。 您需自行決定如何將SDK整合至您的網站、聽取CMP中的同意變更，並呼叫適當的命令。

### 建立新的邊緣設定

為了讓SDK傳送資料至，您必 [!DNL Experience Platform]須先在中建立新的邊緣 [!DNL Platform] 設定 [!DNL Adobe Experience Platform Launch]。 如何建立新設定的特定步驟，請參閱 [SDK檔案](../../../edge/fundamentals/edge-configuration.md)。

為設定提供唯一名稱后，請選取 *[!UICONTROL Adobe Experience Platform旁的切換按鈕]*。 接下來，請使用下列值來完成表單的其餘部分：

| Edge configuration欄位 | 值 |
| --- | --- |
| [!UICONTROL 沙盒] | 沙盒的名 [!DNL Platform] 稱 [](../../../sandboxes/home.md) ，其中包含設定邊緣組態所需的串流連線和資料集。 |
| [!UICONTROL 串流入口] | 有效的串流連接 [!DNL Experience Platform]。 如果您沒有現 [有的串流入口](../../../ingestion/tutorials/create-streaming-connection-ui.md) ，請參閱有關建立串流連線的教學課程。 |
| [!UICONTROL 事件資料集] | 選取在上 [!DNL XDM ExperienceEvent] 一步驟中建立的 [資料集](#datasets)。 |
| [!UICONTROL 描述檔資料集] | 選取在上 [!DNL XDM Individual Profile] 一步驟中建立的 [資料集](#datasets)。 |

![](../assets/iab/edge-config.png)

完成後，按一 **[!UICONTROL 下畫面底部的]** 「儲存」，然後繼續依照任何其他提示完成設定。

### 進行許可更改命令

當您建立上一節所述的邊緣設定後，就可以開始使用SDK命令傳送同意資料給 [!DNL Platform]。 以下各節提供如何在不同案例中使用每個SDK命令的範例。

>[!NOTE]
>
>有關所有 [!DNL Platform] SDK命令的常見語法的簡介，請參閱執行命令 [的文檔](../../../edge/fundamentals/executing-commands.md)。

#### 使用CMP許可更改掛接

許多CMP提供立即可用的掛鈎，以監聽許可更改事件。 當發生這些事件時，您可以使 `setConsent` 用命令更新該客戶的同意資料。

該命 `setConsent` 令需要兩個參數：(1)指示命令類型的字串（在本例中為「setConnence」），以及(2)包含陣列的裝載，該陣列必須包含至少一個提供所需許可欄位的對象，如下所示： `consent`

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
| `standard` | 使用許可標準。 對於TCF 2.0許可處理，此值必須設定為&quot;IAB&quot;。 |
| `version` | 下面所示同意標準的版本號 `standard`。 對於TCF 2.0許可處理，此值必須設定為&quot;2.0&quot;。 |
| `value` | 由CMP生成的基本-64編碼的許可字串。 |
| `gdprApplies` | 一個布爾值，它指示GDPR是否適用於當前登錄的客戶。 要為此客戶強制執行TCF 2.0，必須將值設定為&quot;true&quot;。 |

該 `setConsent` 命令應當用作檢測許可設定更改的CMP掛接的一部分。 以下JavaScript提供如何將命 `setConsent` 令用於OneTrust掛接的示 `OnConsentChanged` 例：

```js
OneTrust.OnConsentChanged(function () {
  // Retrieve the TCF 2.0 consent data generated by the CMP, and pass it to Alloy. 
  __tcfapi("getTCData", 2, (data, success) => {
    if (success) {
      const { tcString, gdprApplies } = data;

      alloy("setConsent", {
        consent: [{
          standard: "IAB TCF",
          version: "2.0",
          value: tcString,
          gdprApplies
        }]
      });
    }
  });
});
```

#### 使用事件

您也可以使用命令收集在中觸發的每個事件的TCF 2.0 [!DNL Platform] 同意資 `sendEvent` 料。

>[!NOTE]
>
>若要使用此方法，您必須已將新增 [!DNL Experience Event Privacy mixin] 至啟 [!DNL Profile]用的 [!DNL XDM ExperienceEvent] 架構。 請參閱資料集準 [備指南中有關更新ExperienceEvent架構的章節](./dataset-preparation.md#event-schema) ，以取得如何設定此架構的步驟。

在您 `sendEvent` 網站上的適當事件監聽器中，該命令應當用作回呼。 該命令需要兩個參數：(1)指出命令類型的字串（在本例中為「sendEvent」），以及(2)包含物件的裝載， `xdm` 其中將必要的同意欄位提供為JSON:

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
| `consentStandard` | 使用許可標準。 對於TCF 2.0許可處理，此值必須設定為&quot;IAB&quot;。 |
| `consentStandardVersion` | 下面所示同意標準的版本號 `standard`。 對於TCF 2.0許可處理，此值必須設定為&quot;2.0&quot;。 |
| `consentStringValue` | 由CMP生成的基本-64編碼的許可字串。 |
| `gdprApplies` | 一個布爾值，它指示GDPR是否適用於當前登錄的客戶。 要為此客戶強制執行TCF 2.0，必須將值設定為&quot;true&quot;。 |

### 處理SDK回應

所有 [!DNL Platform SDK] 命令都返回表明呼叫是成功還是失敗的承諾。 然後，您可以將這些回應用於其他邏輯，例如向客戶顯示確認訊息。 如需特定範例， [請參閱執行SDK指令之指南](../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) 中有關處理成功或失敗的章節。

## 匯出區段 {#export}

>[!NOTE]
>
>在開始匯出區段之前，您必須確定區段包含所有必要的同意欄位。 如需詳細資訊，請 [參閱設定合併原則](#merge-policies) 一節。

在您收集客戶同意資料並建立包含必要同意屬性的受眾細分後，在將這些細分匯出至下游目的地時，您就可以強制執行TCF 2.0規範。

如果許可設定被 `gdprApplies` 設定為 `true` 一組客戶配置檔案，則根據每個配置檔案的許可偏好來過濾從那些導出到下游目的地的配置檔案中的任何資料。 在出口過程中，會跳過任何不符合必要同意偏好的設定檔。

客戶必須同意下列用途(如 [TCF 2.0政策所述](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions))，才能將其個人檔案納入匯出至目的地的區段：

* **目的1**:在裝置上儲存及／或存取資訊
* **目的十**:開發和改進產品

TCF 2.0還要求資料源必須在向目標發送資料之前檢查目標的供應商權限。 因此， [!DNL Real-time CDP] 在包括綁定到該目標的資料之前，檢查目標的供應商權限是否被選擇用於集群中的所有ID。

>[!NOTE]
>
>任何與Adobe Audience Manager共用的區段都會包含與其對應者相同的TCF 2.0同意 [!DNL Platform] 值。 由於 [!DNL Audience Manager] 與(565)共用相同的 [!DNL Real-time CDP] 廠商ID，因此需要相同的目的和廠商權限。 如需詳細資訊，請參 [閱適用於IAB TCF的Adobe Audience Manager外掛程式](https://docs.adobe.com/help/zh-Hant/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html) 。

## Test your implementation {#test-implementation}

一旦您設定了TCF 2.0實作並將區段匯出至目的地後，任何不符合同意要求的資料都不會匯出。 不過，為了查看在匯出期間是否篩選了正確的客戶個人檔案，您必須手動檢查目的地上的資料儲存區，以檢視是否正確執行了同意。

請務必注意，如果叢集中有多個ID且套用TCF 2.0，則即使單一ID未包含正確的用途和廠商權限，也會排除整個叢集。

## 後續步驟

本檔案涵蓋設定資料作業以符 [!DNL Real-time CDP] 合TCF 2.0的程式。如需其他隱私權功能的詳細資 [!DNL Real-time CDP]訊，請參閱下列檔案：

* [即時CDP中的隱私權](../privacy-overview.md)
* [即時CDP中的資料治理](../data-governance-overview.md)