---
title: IAB透明與同意框架2.0概觀
seo-title: 支援互動式廣告局透明度與同意框架2.0的Adobe Experience Platform Web SDK同意偏好設定
description: 瞭解如何使用Experience Platform Web SDK支援IAB TCF 2.0同意偏好設定
seo-description: 瞭解如何使用Experience Platform Web SDK支援IAB TCF 2.0同意偏好設定
keywords: consent;setConsent;Profile Privacy Mixin;Experience Event Privacy Mixin;Privacy Mixin;IAB TCF 2.0;Real-time CDP;Real-time Customer Data Profile
translation-type: tm+mt
source-git-commit: b82ee2508558f76e3ad56cbb8405abe9bfb235f6
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 0%

---


# IAB透明與同意框架2.0概觀

Adobe Experience Platform Web SDK(AEP Web SDK)支援Interactive Advertising Bureau透明度與同意框架2.0版(IAB TCF 2.0)。 本指南說明透過整合即時客戶資料平台、Audience Manager、Experience Events、Adobe Analytics和Experience Edge的AEP Web SDK，支援IAB TCF 2.0的需求。

此外，以下指南可協助您瞭解如何將IAB TCF 2.0與Adobe Experience Platform Launch整合，而不需使用Adobe Experience Platform Launch。

- [透過Adobe Experience Platform Launch](./with-launch.md)
- [不需Adobe Experience Platform Launch](./without-launch.md)

## 快速入門

若要使用IAB TCF 2.0來實作AEP Web SDK，您必須對「體驗資料模型」(XDM)和「體驗事件」有正確的認識。 開始之前，請先閱讀下列檔案：

- [體驗資料模型(XDM)系統概觀](../../../xdm/home.md):標準化和互操作性是Adobe Experience Platform的主要概念。 [!DNL Experience Data Model] (XDM)是由Adobe推動，旨在標準化客戶體驗資料並定義客戶體驗管理的架構。

## 即時客戶資料平台整合

Adobe即時客戶資料平台（即時CDP）以Adobe Experience Platform為基礎，可協助您整合來自多個企業來源的已知和匿名資料。 這可讓您建立客戶個人檔案，以便即時跨所有通道和裝置提供個人化的客戶體驗。 若要透過AEP Web SDK將同意資料傳送至即時CDP，請執行下列動作：

- 基於類的資料集， [!DNL XDM Individual Profile] 可在中使用， [!DNL Real-time Customer Profile]並帶有配置檔案隱私混合。
- 使用即時CDP和上述配置檔案資料集設定的邊緣配置。

請參閱有關建立資料集 [以取得TCF 2.0同意的教學課程](../../../rtcdp/privacy/iab/dataset-preparation.md) ，以瞭解如何建立必要的資料集。

有關建立 [邊配置的說明，請參閱IAB TCF 2.0合規性概述](../../../rtcdp/privacy/privacy-overview.md) 。

## Audience Manager整合

Adobe Audience Manager(AAM)包含對IAB TCF 2.0的支援，可讓您評估、尊重客戶隱私權選擇，並將之轉寄給下游合作夥伴。 <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>若要透過AEP Web SDK與Audience Manager整合，請確定您已設定好轉送至Adobe Audience Manager的Edge組態。

## 體驗事件與Adobe Analytics整合

雖然即時CDP和Audience Manager的受眾會追蹤客戶目前的同意偏好，但「體驗事件」可以保留在收集事件時有效的客戶同意偏好。

若要收集有關事件的同意資訊，請遵循下列規定：

- 基於類別的資料 [!DNL XDM Experience Event] 集，具有隱 [!DNL Experience Event] 私混合。
- 與上述資料集一起設定的 [!DNL XDM Experience Event] 邊緣設定。

如需如何將XDM體驗事件轉換為Analytics點擊的詳細資訊，請先閱讀 [Analytics總覽檔案](../../data-collection/adobe-analytics/analytics-overview.md) 。

## AEP Web SDK整合

以下各節說明IAB TCF 2.0與AEP Web SDK之間的主要整合點。

>[!NOTE]
>
>即使未設定即時CDP或Audience Manager，您仍可將IAB TCF 2.0與Web SDK整合。 同意偏好可用來控制「體驗事件」的收集和設定身分Cookie。

### 預設許可

如果客戶沒有為其保存的許可偏好，則使用預設許可。 這表示預設同意選項可控制AEP Web SDK的行為，並根據客戶所在地區進行變更。

例如，如果您的客戶不在通用資料保護規則(GDPR)的管轄範圍內，預設同意可設為 `in`，但在GDPR的管轄範圍內，預設同意可設為 `pending`。 您的雲端管理平台(CMP)可能會偵測客戶所在地區，並為IAB TCF 2.0 `gdprApplies` 提供旗標。此標誌可用於設定預設許可。

如需預設同意的詳細資訊，請參閱SDK [設定檔案中的](../../fundamentals/configuring-the-sdk.md#default-consent) 「預設同意」一節。

### 在許可更改時設定許可

AEP Web SDK有一個命令， `setConsent` 可讓您使用IAB TCF 2.0將客戶的同意偏好設定傳達給所有Adobe服務。如果您要與即時CDP整合，則此操作將更新客戶的概要檔案。 如果您要與Audience Manager整合，這會更新客戶的資訊。 呼叫此功能也會設定Cookie，其中包含全部或全部無的同意偏好設定，以控制是否允許傳送未來的「體驗事件」。 本動作是在同意變更時呼叫。 未來頁面載入時，將會讀取Experience Edge同意Cookie，以判斷是否可傳送「體驗事件」，以及是否可設定身分Cookie。

與Audience Manager的IAB TCF 2.0整合類似，當客戶明確同意下列目的時，Experience Edge會給予同意：

- **目的1:** 在裝置上儲存及／或存取資訊
- **目的十：** 開發和改進產品
- **特別目的1:** 確保安全性、防止詐欺和除錯。 （根據IAB TCF法規，一律同意）
- **Adobe廠商權限：** 同意Adobe（供應商565）

有關該命令的詳 `setConsent` 細資訊，請閱讀「支援 [同意」文檔](../../consent/supporting-consent.md)。

### 將同意加入體驗事件

AEP Web SDK有一個 `sendEvent` 收集體驗事件的命令。 如果您要與「體驗事件」或Adobe Analytics整合，並想要取得每個「體驗事件」的同意偏好設定，您應將同意資訊新增至每個 `sendEvent` 命令。

如需命令的詳細 `sendEvent` 資訊，請閱讀追蹤事件 [的檔案](../../fundamentals/tracking-events.md)。

## 後續步驟

既然您對IAB透明與同意框架2.0有基本的瞭解，請參閱IAB TCF 2.0與Adobe Experience Platform Launch [或](./with-launch.md) Adobe Experience Platform Launch的使用指南 [](./without-launch.md)。
