---
title: Adobe Experience Platform Web SDK中的IAB TCF 2.0支援
description: 了解如何使用Adobe Experience Platform Web SDK支援IAB TCF 2.0同意偏好設定
keywords: 同意；setConsent；設定檔隱私權欄位群組；體驗事件隱私權欄位群組；隱私權欄位群組；IAB TCF 2.0；即時CDP；即時客戶資料設定檔
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---

# Adobe Experience Platform Web SDK中的IAB TCF 2.0支援

Adobe Experience Platform Web SDK支援互動式廣告局透明與同意架構2.0版(IAB TCF 2.0)。 本指南說明透過Adobe Experience Platform Web SDK支援IAB TCF 2.0的需求，這些IAB TCF 2.0與即時客戶資料平台、Audience Manager、體驗事件、Adobe Analytics和Experience Edge整合。

此外，也提供下列指南，協助學習如何將IAB TCF 2.0與標籤整合，以及不使用標籤。

- [帶標籤](./with-launch.md)
- [無標籤](./without-launch.md)

## 快速入門

若要使用IAB TCF 2.0實作Web SDK，您必須切實了解體驗資料模型(XDM)和體驗事件。 開始之前，請查閱以下文檔：

- [Experience Data Model(XDM)系統概觀](../../../xdm/home.md):標準化和互操作性是Adobe Experience Platform背後的重要概念。[!DNL Experience Data Model (XDM)]受Adobe推動，目標是標準化客戶體驗資料，並定義客戶體驗管理的結構。

## Experience Platform整合

若要使用SDK將同意資料傳送至Adobe Experience Platform，須執行下列操作：

- 架構以[!DNL XDM Individual Profile]類別為基礎，且包含TCF 2.0同意欄位的資料集，已啟用於[!DNL Real-time Customer Profile]中。
- 以Platform和上述已啟用設定檔的資料集所設定的資料流。

請參閱[TCF 2.0法規遵循指南](../../../landing/governance-privacy-security/consent/iab/overview.md) ，以取得建立所需資料集和資料流的相關說明。

## Audience Manager整合

Adobe Audience Manager(AAM)支援IAB TCF 2.0，可讓您評估、榮譽客戶隱私權選擇，並轉送給下游合作夥伴。<!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>若要透過Adobe Experience Platform Web SDK與Audience Manager整合，請確定您有可轉送至Adobe Audience Manager的資料流設定。

## Experience Events與Adobe Analytics整合

雖然即時CDP和Audience Manager的對象會追蹤客戶的目前同意偏好設定，但體驗事件可以保留客戶在收集事件時有效的同意偏好設定。

若要收集事件的同意資訊，需要下列項目：

- 以[!DNL XDM Experience Event]類別為基礎的資料集，並具有[!DNL Experience Event]隱私權架構欄位群組。
- 以上[!DNL XDM Experience Event]資料集設定的資料流。

如需如何將XDM體驗事件轉換為Analytics點擊的詳細資訊，請先閱讀[Analytics概述](../../data-collection/adobe-analytics/analytics-overview.md)檔案。

## Adobe Experience Platform Web SDK整合

以下各節說明IAB TCF 2.0與Adobe Experience Platform Web SDK之間的主要整合點。

>[!NOTE]
>
>即使未設定即時CDP或Audience Manager，您仍可將IAB TCF 2.0與Web SDK整合。 同意偏好設定可用來控制體驗事件的收集和身分識別Cookie的設定。

### 預設同意

若未為客戶儲存同意偏好設定，則會使用預設同意。 這表示預設同意選項可控制Adobe Experience Platform Web SDK的行為，並根據客戶地區進行變更。

例如，若您的客戶不在一般資料保護規範(GDPR)的管轄範圍內，預設同意可設為`in`，但在GDPR的管轄範圍內，預設同意可設為`pending`。 您的同意管理平台(CMP)可能會偵測客戶的地區，並提供標幟`gdprApplies`給IAB TCF 2.0。此標幟可用來設定預設同意。

如需預設同意的詳細資訊，請參閱SDK設定檔案中的[預設同意區段](../../fundamentals/configuring-the-sdk.md#default-consent)。

### 在變更時設定同意

Adobe Experience Platform Web SDK有`setConsent`命令，會使用IAB TCF 2.0將客戶的同意偏好設定傳遞至所有Adobe服務。如果您要與即時CDP整合，這會更新客戶的設定檔。 如果您要與Audience Manager整合，這會更新客戶的資訊。 呼叫這也會設定一個Cookie，其中包含「全有」或「全無」的同意偏好設定，可控制是否允許傳送未來的體驗事件。 意在當同意變更時呼叫此動作。 未來頁面載入時，會讀取Experience Edge同意Cookie，以判斷是否可傳送體驗事件，以及是否可設定身分識別Cookie。

與Audience Manager的IAB TCF 2.0整合類似，當客戶明確同意下列目的時，Experience Edge會提供同意：

- **用途1:** 在裝置上儲存和/或存取資訊
- **目的10:** 開發和改進產品
- **特殊用途1:** 確保安全性、防止欺詐及除錯。（根據IAB TCF法規，一律同意）
- **Adobe供應商權限：** Adobe的同意（廠商565）

有關`setConsent`命令的詳細資訊，請閱讀[支援同意](../../consent/supporting-consent.md)上的文檔。

### 將同意新增至體驗事件

Adobe Experience Platform Web SDK有`sendEvent`命令，用於收集體驗事件。 如果您要與體驗事件或Adobe Analytics整合，且想要在每個體驗事件上使用同意偏好設定，則應將同意資訊新增至每個`sendEvent`命令。

有關`sendEvent`命令的詳細資訊，請閱讀[tracking events](../../fundamentals/tracking-events.md)上的文檔。

## 後續步驟

現在您已基本了解IAB透明與同意架構2.0，請參閱使用IAB TCF 2.0 [搭配標籤](./with-launch.md)或[搭配標籤](./without-launch.md)的相關指南。
