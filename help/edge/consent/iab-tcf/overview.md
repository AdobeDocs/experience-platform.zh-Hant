---
title: Adobe Experience Platform Web SDK中的IAB TCF 2.0支援
description: 了解如何使用Adobe Experience Platform Web SDK支援IAB TCF 2.0同意偏好設定
keywords: 同意；setConsent；設定檔隱私權欄位群組；體驗事件隱私權欄位群組；隱私權欄位群組；IAB TCF 2.0;Real-Time CDP;
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# Adobe Experience Platform Web SDK中的IAB TCF 2.0支援

Adobe Experience Platform Web SDK支援互動式廣告局透明與同意架構2.0版(IAB TCF 2.0)。 本指南說明透過Adobe Experience Platform Web SDK支援IAB TCF 2.0的需求，這些IAB TCF 2.0已與Adobe Real-time Customer Data Platform、Audience Manager、Experience Events、Adobe Analytics和Experience Edge整合。

此外，也提供下列指南，協助學習如何將IAB TCF 2.0與標籤整合，以及不使用標籤。

- [帶標籤](./with-launch.md)
- [無標籤](./without-launch.md)

## 快速入門

若要使用IAB TCF 2.0實作Web SDK，您必須切實了解體驗資料模型(XDM)和體驗事件。 開始之前，請查閱以下文檔：

- [Experience Data Model(XDM)系統概觀](../../../xdm/home.md):標準化和互操作性是Adobe Experience Platform背後的重要概念。 [!DNL Experience Data Model (XDM)]受Adobe推動，目標是標準化客戶體驗資料，並定義客戶體驗管理的結構。

## Experience Platform整合

若要使用SDK將同意資料傳送至Adobe Experience Platform，須執行下列操作：

- 結構以 [!DNL XDM Individual Profile] 類別和包含TCF 2.0同意欄位，已啟用，可在 [!DNL Real-Time Customer Profile].
- 以Platform和上述已啟用設定檔的資料集所設定的資料流。

請參閱 [TCF 2.0法規遵循](../../../landing/governance-privacy-security/consent/iab/overview.md) 以取得建立必要資料集和資料流的相關說明。

## Audience Manager整合

Adobe Audience Manager(AAM)支援IAB TCF 2.0，可讓您評估、榮譽客戶隱私權選擇，並轉送給下游合作夥伴。 <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>若要透過Adobe Experience Platform Web SDK與Audience Manager整合，請確定您有可轉送至Adobe Audience Manager的資料流設定。

## Experience Events與Adobe Analytics整合

雖然Real-Time CDP和Audience Manager的對象會追蹤客戶的目前同意偏好設定，但「體驗事件」可以保留收集事件時處於作用中狀態的客戶同意偏好設定。

若要收集事件的同意資訊，需要下列項目：

- 以 [!DNL XDM Experience Event] 類別，與 [!DNL Experience Event] 隱私權架構欄位群組。
- 使用 [!DNL XDM Experience Event] 資料集。

如需如何將XDM體驗事件轉換為Analytics點擊的詳細資訊，請先閱讀 [Analytics概觀](../../data-collection/adobe-analytics/analytics-overview.md) 檔案。

## Adobe Experience Platform Web SDK整合

以下各節說明IAB TCF 2.0與Adobe Experience Platform Web SDK之間的主要整合點。

>[!NOTE]
>
>即使未設定Real-Time CDP或Audience Manager，您仍可以整合IAB TCF 2.0與Web SDK。 同意偏好設定可用來控制體驗事件的收集和身分識別Cookie的設定。

### 預設同意

若未為客戶儲存同意偏好設定，則會使用預設同意。 這表示預設同意選項可控制Adobe Experience Platform Web SDK的行為，並根據客戶地區進行變更。

例如，若您的客戶不在一般資料保護規範(GDPR)的管轄範圍內，則預設同意可設為 `in`，但在GDPR的管轄範圍內，預設同意可設為 `pending`. 您的同意管理平台(CMP)可能會偵測客戶的地區並提供標幟 `gdprApplies` 至IAB TCF 2.0。此標幟可用來設定預設同意。

如需預設同意的詳細資訊，請參閱 [預設同意區段](../../fundamentals/configuring-the-sdk.md#default-consent) 在SDK設定檔案中。

### 在變更時設定同意

Adobe Experience Platform Web SDK具有 `setConsent` 命令，此命令會使用IAB TCF 2.0將客戶的同意偏好設定與所有Adobe服務通訊。如果您要與Real-Time CDP整合，這會更新客戶的設定檔。 如果您要與Audience Manager整合，這會更新客戶的資訊。 呼叫這也會設定一個Cookie，其中包含「全有」或「全無」的同意偏好設定，可控制是否允許傳送未來的體驗事件。 意在當同意變更時呼叫此動作。 未來頁面載入時，會讀取Experience Edge同意Cookie，以判斷是否可傳送體驗事件，以及是否可設定身分識別Cookie。

與Audience Manager的IAB TCF 2.0整合類似，當客戶明確同意下列目的時，Experience Edge會提供同意：

- **目的一：** 在設備上儲存和/或訪問資訊
- **目的十：** 開發和改進產品
- **特殊目的1:** 確保安全性、防止欺詐和調試。 （根據IAB TCF法規，一律同意）
- **Adobe供應商權限：** Adobe同意（供應商565）

如需 `setConsent` 命令，請閱讀 [支援同意](../../consent/supporting-consent.md).

### 將同意新增至體驗事件

Adobe Experience Platform Web SDK具有 `sendEvent` 收集體驗事件的命令。 如果您要與體驗事件或Adobe Analytics整合，且想要在每個體驗事件上使用同意偏好設定，則應將同意資訊新增至每個 `sendEvent` 命令。

如需 `sendEvent` 命令，請閱讀 [追蹤事件](../../fundamentals/tracking-events.md).

## 後續步驟

現在您已基本了解IAB透明與同意架構2.0，請參閱使用IAB TCF 2.0的相關指南 [帶標籤](./with-launch.md) 或 [無標籤](./without-launch.md).
