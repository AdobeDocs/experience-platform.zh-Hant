---
title: Adobe Experience Platform Web SDK中的IAB TCF 2.0支援
description: 瞭解如何使用Adobe Experience Platform Web SDK支援IAB TCF 2.0同意偏好設定
keywords: 同意；setConsent；設定檔隱私權欄位群組；體驗事件隱私權欄位群組；隱私權欄位群組；IAB TCF 2.0；Real-Time CDP；
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 0%

---

# Adobe Experience Platform Web SDK中的IAB TCF 2.0支援

Adobe Experience Platform Web SDK支援Interactive Advertising Bureau Transparency &amp; Consent Framework 2.0版(IAB TCF 2.0)。 本指南說明透過Adobe Experience Platform Web SDK與Adobe Real-Time Customer Data Platform、Audience Manager、Experience Events、Adobe Analytics和Edge Network整合來支援IAB TCF 2.0的需求。

此外，下列指南可協助您瞭解如何整合IAB TCF 2.0與標籤，以及不使用標籤。

- [含標籤](./with-tags.md)
- [不含標籤](./without-tags.md)

## 快速入門

若要使用IAB TCF 2.0實作Web SDK，您必須實際瞭解體驗資料模型(XDM)和體驗事件。 開始之前，請檢閱下列檔案：

- [Experience Data Model (XDM)系統概覽](../../../xdm/home.md)：標準化和互用性是Adobe Experience Platform背後的重要概念。 [!DNL Experience Data Model (XDM)]由Adobe驅動，致力於標準化客戶體驗資料並定義客戶體驗管理的結構描述。

## Experience Platform整合

若要使用SDK將同意資料傳送至Adobe Experience Platform，需具備下列條件：

- 資料集的結構描述是以[!DNL XDM Individual Profile]類別為基礎，並包含已啟用於[!DNL Real-Time Customer Profile]中使用的TCF 2.0同意欄位。
- 使用Experience Platform設定的資料流以及上述已啟用設定檔的資料集。

請參閱[TCF 2.0規範](../../../landing/governance-privacy-security/consent/iab/overview.md)的指南，瞭解建立必要資料集和資料流的說明。

## Audience Manager整合

Adobe Audience Manager (AAM)支援IAB TCF 2.0，可讓您評估、尊重客戶的隱私權選擇，並將其轉寄給下游合作夥伴。<!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>若要透過Adobe Experience Platform Web SDK與Audience Manager整合，請務必設定好資料流以轉送至Adobe Audience Manager。

## Experience Events與Adobe Analytics整合

Real-Time CDP和Audience Manager的受眾會追蹤客戶目前的同意偏好設定，而Experience Events則可保留客戶在收集事件時啟用的同意偏好設定。

若要收集事件的同意資訊，需具備下列條件：

- 以[!DNL XDM Experience Event]類別為基礎，具有[!DNL Experience Event]隱私權結構描述欄位群組的資料集。
- 使用上述[!DNL XDM Experience Event]資料集設定的資料流。

如需如何將XDM Experience事件轉換為Analytics點選的詳細資訊，請參閱[使用網頁SDK傳送資料至Adobe Analytics](/help/web-sdk/use-cases/adobe-analytics.md)。

## Adobe Experience Platform Web SDK整合

以下各節說明IAB TCF 2.0與Adobe Experience Platform Web SDK之間的主要整合點。

>[!NOTE]
>
>即使未設定Real-Time CDP或Audience Manager，您仍可將IAB TCF 2.0與Web SDK整合。 同意偏好設定可用於控制體驗事件的收集及設定身分Cookie。

### 預設同意

若尚未儲存客戶的同意偏好設定，則使用預設同意。 這表示預設同意選項可控制Adobe Experience Platform Web SDK的行為，並根據客戶地區變更。

例如，如果您的客戶不在一般資料保護規範(GDPR)的管轄範圍內，則預設同意可設為`in`，但在GDPR的管轄範圍內，預設同意可設為`pending`。 您的同意管理平台(CMP)可能會偵測客戶的區域，並為IAB TCF 2.0提供標幟`gdprApplies`。此旗標可用於設定預設同意。 如需詳細資訊，請參閱[`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md)。

### 變更時設定同意

Adobe Experience Platform Web SDK有`setConsent`命令，可使用IAB TCF 2.0將客戶的同意偏好設定傳達給所有Adobe服務。如果您正在與Real-Time CDP整合，這會更新客戶的設定檔。 如果您正在與Audience Manager整合，這會更新您的客戶資訊。 呼叫此專案也會設定具有完全或完全不同同意偏好設定的Cookie，該偏好設定會控制是否允許傳送未來的體驗事件。 其目的是每當同意變更時，就會呼叫此動作。 日後載入頁面時，系統會讀取Edge Network同意Cookie，決定是否可傳送Experience事件，以及是否可設定身分識別Cookie。

與Audience Manager的IAB TCF 2.0整合類似，當客戶針對下列用途提供明確同意時，Edge Network會提供同意：

- **用途1：**&#x200B;儲存和/或存取裝置上的資訊
- **用途10：**&#x200B;開發和改進產品
- **特殊用途1：**&#x200B;確保安全性、防止欺詐和偵錯。 （根據IAB TCF法規，一律同意）
- **Adobe廠商許可權：** Adobe的同意（廠商565）

如需`setConsent`命令的詳細資訊，請閱讀[setConsent](../../../web-sdk/commands/setconsent.md)上的專屬網頁SDK檔案。

### 新增同意至體驗事件

Adobe Experience Platform Web SDK有收集體驗事件的[`sendEvent`](/help/web-sdk/commands/sendevent/overview.md)命令。 如果您要與Experience Events或Adobe Analytics整合，並且想要每個體驗事件的同意偏好設定，請為每個`sendEvent`命令新增同意資訊。

## 後續步驟

現在您已基本瞭解IAB透明與同意架構2.0，請參閱其中一份使用含標籤[&#128279;](./with-tags.md)的IAB TCF 2.0 或不含標籤的[的指南](./without-tags.md)。
