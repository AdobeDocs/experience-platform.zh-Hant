---
title: Adobe Experience Platform Web SDK中的IAB TCF 2.0支援
description: 瞭解如何使用Adobe Experience Platform Web SDK支援IAB TCF 2.0同意偏好設定
keywords: connence;setConnonce；描述檔隱私權Mixin；體驗事件隱私權Mixin；隱私權Mixin;IAB TCF 2.0；即時CDP；即時客戶資料概要檔案
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 0%

---


# Adobe Experience Platform Web SDK中的IAB TCF 2.0支援

Adobe Experience Platform Web SDK支援Interactive Advertising Bureau透明度與同意框架2.0版(IAB TCF 2.0)。 本指南說明透過整合即時客戶資料平台、Audience Manager、Experience Events、Adobe Analytics和Experience Edge的Adobe Experience Platform Web SDK支援IAB TCF 2.0的需求。

此外，以下指南可協助您瞭解如何將IAB TCF 2.0與Adobe Experience Platform Launch整合，而不需使用Adobe Experience Platform Launch。

- [透過Adobe Experience Platform Launch](./with-launch.md)
- [不需Adobe Experience Platform Launch](./without-launch.md)

## 快速入門

若要使用IAB TCF 2.0來建置Web SDK，您必須對「體驗資料模型」(XDM)和「體驗事件」有正確的認識。 開始之前，請先閱讀下列檔案：

- [體驗資料模型(XDM)系統概觀](../../../xdm/home.md):標準化和互操作性是Adobe Experience Platform的主要概念。[!DNL Experience Data Model (XDM)]在Adobe的推動下，我們致力於標準化客戶體驗資料並定義客戶體驗管理的架構。

## Experience Platform整合

若要使用SDK將同意資料傳送至Adobe Experience Platform，請執行下列動作：

- 一種資料集，其模式基於[!DNL XDM Individual Profile]類並包含TCF 2.0許可欄位，可用於[!DNL Real-time Customer Profile]。
- 使用平台和上述啟用描述檔的資料集設定的邊緣設定。

有關建立所需資料集和邊緣配置的說明，請參閱[TCF 2.0 compliance](../../../landing/governance-privacy-security/consent/iab/overview.md)上的指南。

## Audience Manager整合

Adobe Audience Manager(AAM)包含對IAB TCF 2.0的支援，可讓您評估、尊重客戶隱私權選擇，並將之轉寄給下游合作夥伴。<!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>若要透過Adobe Experience Platform Web SDK與Audience Manager整合，請確定您已設定好前往Adobe Audience Manager的邊緣組態。

## 體驗事件與Adobe Analytics整合

雖然即時CDP和Audience Manager的受眾會追蹤客戶目前的同意偏好，但「體驗事件」可以保留在收集事件時有效的客戶同意偏好。

若要收集有關事件的同意資訊，請遵循下列規定：

- 以[!DNL XDM Experience Event]類別為基礎、具有[!DNL Experience Event]隱私混音的資料集。
- 與上述[!DNL XDM Experience Event]資料集一起設定的邊緣設定。

如需如何將XDM體驗事件轉換為Analytics點擊的詳細資訊，請先閱讀[Analytics overview](../../data-collection/adobe-analytics/analytics-overview.md)檔案。

## Adobe Experience Platform Web SDK整合

以下各節說明IAB TCF 2.0與Adobe Experience Platform Web SDK之間的主要整合點。

>[!NOTE]
>
>即使未設定即時CDP或Audience Manager，您仍可將IAB TCF 2.0與Web SDK整合。 同意偏好可用來控制「體驗事件」的收集和設定身分Cookie。

### 預設許可

如果客戶沒有為其保存的許可偏好，則使用預設許可。 這表示預設同意選項可以控制Adobe Experience Platform Web SDK的行為，並根據客戶所在地區進行變更。

例如，如果您的客戶不在通用資料保護規則(GDPR)的管轄範圍內，預設同意可設為`in`，但在GDPR的管轄範圍內，預設同意可設為`pending`。 您的雲管理平台(CMP)可能會偵測客戶所在地區，並將`gdprApplies`標幟提供給IAB TCF 2.0。此標誌可用於設定預設許可。

如需預設同意的詳細資訊，請參閱SDK設定檔案中的[預設同意部分](../../fundamentals/configuring-the-sdk.md#default-consent)。

### 在許可更改時設定許可

Adobe Experience Platform Web SDK有`setConsent`命令，可使用IAB TCF 2.0將客戶的同意偏好與所有Adobe服務通訊。如果您要與即時CDP整合，則此操作將更新客戶的概要檔案。 如果您要與Audience Manager整合，這會更新客戶的資訊。 呼叫此功能也會設定Cookie，其中包含全部或全部無的同意偏好設定，以控制是否允許傳送未來的「體驗事件」。 本動作是在同意變更時呼叫。 未來頁面載入時，將會讀取Experience Edge同意Cookie，以判斷是否可傳送「體驗事件」，以及是否可設定身分Cookie。

與Audience Manager的IAB TCF 2.0整合類似，當客戶明確同意下列目的時，Experience Edge會給予同意：

- **用途1：在** 裝置上儲存和／或存取資訊
- **目的十：開** 發和改進產品
- **特殊目的1：確** 保安全性、防止詐欺和除錯。（根據IAB TCF法規，一律同意）
- **Adobe廠商權限：** Adobe的同意（廠商565）

有關`setConsent`命令的詳細資訊，請閱讀有關[支援許可](../../consent/supporting-consent.md)的文檔。

### 將同意加入體驗事件

Adobe Experience Platform Web SDK有`sendEvent`命令，可收集「Experience Event」。 如果您要與「體驗事件」或Adobe Analytics整合，並想要取得每個「體驗事件」的同意偏好設定，您應將同意資訊新增至每個`sendEvent`命令。

有關`sendEvent`命令的詳細資訊，請閱讀有關[跟蹤事件](../../fundamentals/tracking-events.md)的文檔。

## 後續步驟

既然您對IAB透明與同意框架2.0有基本的瞭解，請參閱IAB TCF 2.0 [搭配Adobe Experience Platform Launch](./with-launch.md)或[搭配使用指南（不包括Adobe Experience Platform Launch](./without-launch.md)）。
