---
title: IAB TCF 2.0在Adobe Experience PlatformWeb SDK中的支援
description: 瞭解如何使用Adobe Experience PlatformWeb SDK支援IAB TCF 2.0同意首選項
keywords: 同意；setConnence；配置檔案隱私欄位組；體驗事件隱私欄位組；隱私欄位組；IAB TCF 2.0;Real-Time CDP;
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# IAB TCF 2.0在Adobe Experience PlatformWeb SDK中的支援

Adobe Experience Platform網路軟體開發工具包支援互動式廣告局透明度和同意框架2.0版(IAB TCF 2.0)。 本指南顯示了通過Adobe Experience PlatformWeb SDK支援IAB TCF 2.0的要求，該SDK整合了Adobe Real-time Customer Data Platform、Audience Manager、體驗事件、Adobe Analytics和體驗邊緣。

此外，以下指南可幫助學習如何將IAB TCF 2.0與標籤整合和不使用標籤。

- [帶標籤](./with-launch.md)
- [無標籤](./without-launch.md)

## 快速入門

為了使用IAB TCF 2.0實施Web SDK，您需要對「體驗資料模型」(XDM)和「體驗事件」有一定的瞭解。 開始之前，請查看以下文檔：

- [體驗資料模型(XDM)系統概述](../../../xdm/home.md):標準化和互操作性是Adobe Experience Platform背後的關鍵概念。 [!DNL Experience Data Model (XDM)]在Adobe的推動下，這是一種努力，目的是標準化客戶體驗資料並定義客戶體驗管理模式。

## Experience Platform整合

要使用SDK向Adobe Experience Platform發送同意資料，需要執行以下操作：

- 其模式基於 [!DNL XDM Individual Profile] 類並包含TCF 2.0同意欄位，在中啟用 [!DNL Real-Time Customer Profile]。
- 使用上述平台和啟用配置檔案的資料集設定的資料流。

請參閱上的指南 [TCF 2.0合規性](../../../landing/governance-privacy-security/consent/iab/overview.md) 以獲取有關建立所需資料集和資料流的說明。

## Audience Manager整合

Adobe Audience Manager(AAM)支援IAB TCF 2.0 ，使您能夠評估、榮譽並將客戶隱私選擇轉發給下游合作夥伴。 <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>要通過Adobe Experience PlatformWeb SDK與Audience Manager整合，請確保設定了資料流以轉發到Adobe Audience Manager。

## 體驗活動與Adobe Analytics整合

儘管Real-Time CDP和Audience Manager的受眾會跟蹤客戶當前的同意偏好，但「體驗事件」可以保留在收集事件時處於活動狀態的客戶同意偏好。

要收集有關事件的同意資訊，需要執行以下操作：

- 基於 [!DNL XDM Experience Event] 類，與 [!DNL Experience Event] 隱私架構欄位組。
- 與 [!DNL XDM Experience Event] 資料集。

有關如何將XDM體驗事件轉換為分析命中的詳細資訊，請首先閱讀 [分析概述](../../data-collection/adobe-analytics/analytics-overview.md) 文檔。

## Adobe Experience PlatformWeb SDK整合

以下各節介紹IAB TCF 2.0與Adobe Experience PlatformWeb SDK之間的主要整合點。

>[!NOTE]
>
>即使沒有Real-Time CDP或Audience Manager設定，您仍然可以將IAB TCF 2.0與Web SDK整合。 同意首選項可用於控制體驗事件的收集和設定身份cookie。

### 預設同意

如果尚未為客戶保存同意首選項，則使用預設同意。 這意味著預設同意選項可以控制Adobe Experience PlatformWeb SDK的行為並根據客戶區域進行更改。

例如，如果您的客戶不在一般資料保護法規(GDPR)的管轄範圍內，則預設同意可設定為 `in`但是，在GDPR的管轄範圍內，預設同意可以設定為 `pending`。 您的同意管理平台(CMP)可能會檢測客戶的區域並提供標誌 `gdprApplies` TCF 2.0。此標誌可用於設定預設同意。

有關預設同意的詳細資訊，請參閱 [預設同意部分](../../fundamentals/configuring-the-sdk.md#default-consent) 在SDK配置文檔中。

### 設定更改時的同意

Adobe Experience PlatformWeb SDK `setConsent` 命令，該命令使用IAB TCF 2.0將客戶的同意首選項傳達給所有Adobe服務。如果您正在與Real-Time CDP整合，則此操作將更新客戶的個人資料。 如果您正在與Audience Manager整合，則此操作會更新客戶的資訊。 調用此功能還可設定一個包含「全部」或「無」同意首選項的cookie，該首選項控制是否允許發送將來的體驗事件。 本意是在同意更改時調用此操作。 在將來的頁面載入時，將讀取體驗邊緣同意cookie以確定是否可以發送體驗事件以及是否可以設定身份cookie。

與Audience Manager的IAB TCF 2.0整合類似，當客戶明確同意以下目的時， Experience Edge會同意：

- **目的一：** 在設備上儲存和/或訪問資訊
- **目的十：** 開發和改進產品
- **特殊目的1:** 確保安全性、防止欺詐和調試。 （根據IAB TCF法規，這一點始終獲得同意）
- **Adobe供應商權限：** 同意Adobe（供應商565）

有關 `setConsent` 命令，閱讀 [支援同意](../../consent/supporting-consent.md)。

### 將同意添加到體驗事件

Adobe Experience PlatformWeb SDK `sendEvent` 收集「體驗事件」的命令。 如果您要與「體驗事件」或「Adobe Analytics」整合，並希望每個「體驗事件」的同意首選項，則應將同意資訊添加到每個 `sendEvent` 的子菜單。

有關 `sendEvent` 命令，閱讀 [跟蹤事件](../../fundamentals/tracking-events.md)。

## 後續步驟

現在，您對IAB透明度和同意框架2.0有了基本的瞭解，請參閱有關使用IAB TCF 2.0的指南 [帶標籤](./with-launch.md) 或 [無標籤](./without-launch.md)。
