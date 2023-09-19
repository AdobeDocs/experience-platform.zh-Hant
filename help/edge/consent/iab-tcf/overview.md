---
title: Adobe Experience Platform Web SDK中的IAB TCF 2.0支援
description: 瞭解如何使用Adobe Experience Platform Web SDK支援IAB TCF 2.0同意偏好設定
keywords: 同意；setConsent；設定檔隱私權欄位群組；體驗事件隱私權欄位群組；隱私權欄位群組；IAB TCF 2.0；Real-Time CDP；
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 0%

---

# Adobe Experience Platform Web SDK中的IAB TCF 2.0支援

Adobe Experience Platform Web SDK支援Interactive Advertising Bureau Transparency &amp; Consent Framework 2.0版(IAB TCF 2.0)。 本指南說明透過Adobe Experience Platform Web SDK整合Adobe Real-time Customer Data Platform、Audience Manager、Experience Events、Adobe Analytics和Edge Network，支援IAB TCF 2.0的需求。

此外，下列指南可協助您瞭解如何整合IAB TCF 2.0與標籤，以及不使用標籤。

- [含標籤](./with-launch.md)
- [不含標籤](./without-launch.md)

## 快速入門

若要使用IAB TCF 2.0實作Web SDK，您必須實際瞭解Experience Data Model (XDM)和Experience事件。 開始之前，請檢閱下列檔案：

- [Experience Data Model (XDM)系統概覽](../../../xdm/home.md)：標準化和互通性是Adobe Experience Platform背後的重要概念。 [!DNL Experience Data Model (XDM)]由Adobe推動，致力於標準化客戶體驗資料並定義客戶體驗管理的結構。

## Experience Platform整合

若要使用SDK將同意資料傳送至Adobe Experience Platform，須符合下列條件：

- 其結構描述基礎的資料集 [!DNL XDM Individual Profile] 類別並包含TCF 2.0同意欄位，這些欄位已啟用以用於中 [!DNL Real-Time Customer Profile].
- 使用Platform設定的資料流以及上述已啟用設定檔的資料集。

請參考以下指南： [符合TCF 2.0](../../../landing/governance-privacy-security/consent/iab/overview.md) 以取得建立所需資料集和資料流的指示。

## Audience Manager整合

Adobe Audience Manager (AAM)支援IAB TCF 2.0，可讓您評估、尊重客戶的隱私權選擇，並將其轉寄給下游合作夥伴。 <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>若要透過Adobe Experience Platform Web SDK與Audience Manager整合，請務必設定好資料流以轉送至Adobe Audience Manager。

## Experience Events與Adobe Analytics整合

雖然Real-Time CDP和Audience Manager的對象會追蹤客戶目前的同意偏好設定，但體驗事件可以保留客戶在收集事件時處於作用中的同意偏好設定。

若要收集事件的同意資訊，需具備下列條件：

- 資料集根據 [!DNL XDM Experience Event] 類別，具有 [!DNL Experience Event] 隱私權結構欄位群組。
- 使用設定的資料流 [!DNL XDM Experience Event] 以上資料集。

如需如何將XDM體驗事件轉換為Analytics點選的詳細資訊，請從閱讀 [Analytics概觀](../../data-collection/adobe-analytics/analytics-overview.md) 檔案。

## Adobe Experience Platform Web SDK整合

以下各節說明IAB TCF 2.0與Adobe Experience Platform Web SDK之間的主要整合點。

>[!NOTE]
>
>即使未設定Real-Time CDP或Audience Manager，您仍可將IAB TCF 2.0與Web SDK整合。 同意偏好設定可用於控制體驗事件的收集及設定身分Cookie。

### 預設同意

若尚未儲存客戶的同意偏好設定，則使用預設同意。 這表示預設同意選項可控制Adobe Experience Platform Web SDK的行為，並根據客戶的地區變更。

例如，若您的客戶不在一般資料保護規範(GDPR)的管轄範圍內，則預設同意可設為 `in`，但在GDPR的司法權區內，預設同意可設為 `pending`. 您的同意管理平台(CMP)可能會偵測客戶的區域並提供標幟 `gdprApplies` 至IAB TCF 2.0。此旗標可用於設定預設同意。

如需預設同意的詳細資訊，請參閱 [預設同意區段](../../fundamentals/configuring-the-sdk.md#default-consent) （在SDK設定檔案中）。

### 變更時設定同意

Adobe Experience Platform Web SDK具有 `setConsent` 命令，使用IAB TCF 2.0將客戶的同意偏好設定傳達給所有Adobe服務。如果您正在與Real-Time CDP整合，這會更新客戶的設定檔。 如果您正在與Audience Manager整合，這會更新客戶的資訊。 呼叫此專案也會設定具有完全或完全不同同意偏好設定的Cookie，該偏好設定會控制是否允許傳送未來的體驗事件。 其目的是每當同意變更時，就會呼叫此動作。 日後載入頁面時，系統會讀取Edge Network同意Cookie，判斷是否可傳送Experience事件，以及是否可設定身分Cookie。

與Audience Manager的IAB TCF 2.0整合類似，Edge Network會在客戶針對下列用途提供明確同意後提供同意：

- **目的1：** 儲存和/或存取裝置上的資訊
- **目的10：** 開發和改善產品
- **特殊用途1：** 確保安全性、防止欺詐和除錯。 （根據IAB TCF法規，一律同意）
- **Adobe廠商許可權：** 同意進行Adobe（廠商565）

如需詳細資訊，請參閱 `setConsent` 命令，請閱讀以下檔案： [支援同意](../../consent/supporting-consent.md).

### 新增同意至體驗事件

Adobe Experience Platform Web SDK具有 `sendEvent` 收集體驗事件的命令。 如果您正在與Experience Event或Adobe Analytics整合，並且想要瞭解每個體驗事件的同意偏好設定，您應將同意資訊新增至每個 `sendEvent` 命令。

如需詳細資訊，請參閱 `sendEvent` 命令，請閱讀以下檔案： [追蹤事件](../../fundamentals/tracking-events.md).

## 後續步驟

您已基本瞭解IAB透明與同意架構2.0，請參閱其中一份使用IAB TCF 2.0的指南 [含標籤](./with-launch.md) 或 [沒有標籤](./without-launch.md).
