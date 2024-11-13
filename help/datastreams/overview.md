---
title: 資料流概觀
description: 瞭解資料串流如何協助您將使用者端Experience PlatformSDK整合與Adobe產品和第三方目的地連線起來。
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: e3768a3f695abeedc9a3ce2fef591c6ecae9a897
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 70%

---

# 資料流概觀

資料流代表Adobe Experience Platform Web和Mobile SDK的伺服器端設定。 SDK中的[`configure`](/help/web-sdk/commands/configure/overview.md)命令會處理使用者端設定（例如`edgeDomain`），而資料串流會管理所有其他設定。

當您傳送要求給Edge Network時，`datastreamId`會參考傳送資料的資料流。 這可讓您更新伺服器端設定，而不變更網站的程式碼。

在 Adob&#x200B;&#x200B;e Experience Platform UI 或資料集合 UI 的左側導覽中選取&#x200B;**[!UICONTROL 資料流]**，即可建立並管理資料流。

![UI 中的資料流索引標籤](assets/overview/datastreams-tab.png)

如需有關如何在 UI 中設定資料流的詳細資訊，請參閱[設定指南](./configure.md)。

## 處理資料流中的敏感資料 {#sensitive}

>[!IMPORTANT]
>
>本文件的內容並非法律建議，其用意並非取代專業的法律建議。請洽詢貴公司的法律部門，以取得處理敏感資料的相關建議。

企業資料盡責管理政策和監管要求對於能夠收集、處理和使用敏感客戶資料的方式施加了越來越多的限制。這包括對於受保護的健康資料 (PHI) 的收集、處理和使用，這類資料受到《健康保險可攜與責任法案》(HIPAA) 等法規的規範。

資料串流提供三種方法來協助您安全地處理敏感資料：

* [增強型加密](#encryption)
* [資料控管](#governance)
* [稽核記錄](#audit-logs)

### 增強型加密 {#encryption}

透過 Edge Network 進行的所有資料傳輸都會使用 [HTTPS TLS 1.2](https://datatracker.ietf.org/doc/html/rfc5246) 在安全、加密的連線上實施。如果資料流將資料帶入 Experience Platform，則接著會在 Experience Platform 資料湖中將待用的資料加密。如需詳細資訊，請至 [Experience Platform 中的資料加密](../landing/governance-privacy-security/encryption.md)參閱文件。

### 資料控管 {#governance}

資料串流使用Experience Platform內建的資料控管功能，以防止將敏感資料傳送至不符合HIPAA標準的服務。 在資料流綱要中標記包含敏感資料的特定欄位，即可對於哪些資料欄位可用於特定目的採取精細的控制。

以下影片會針對如何在 UI 中設定資料流的資料使用限制並執行提供簡要概觀：

>[!VIDEO](https://video.tv.adobe.com/v/3409588/?quality=12&learn=on&speedcontrol=on)

在 Experience Platform 中，您可以將[敏感資料使用標籤](../data-governance/labels/reference.md#sensitive)套用在包含了貴組織視為敏感的資料的綱要和欄位上。例如，`RHD` 標籤用於標示受保護的健康資訊 (PHI)，而 `S1` 標籤則代表地理位置資料。

>[!NOTE]
>
>如需有關如何在 Experience Platform UI 或資料集合 UI 中的[!UICONTROL 綱要]索引標籤內套用資料使用標籤，請參閱[綱要標示教學課程](../xdm/tutorials/labels.md)。

當您建立資料流時，如果選取的結構描述包含敏感資料使用標籤，您只能將資料流設定為將該資料傳送至符合HIPAA要求的目的地。 目前，資料流支援的唯一符合 HIPAA 標準的目的地為 Adob&#x200B;&#x200B;e Experience Platform。針對包含敏感資料使用標籤的資料流，停用其他目的地服務，包括 Adob&#x200B;&#x200B;e Target、Adobe Analytics、Adobe Audience Manager、事件轉送和邊緣目的地。

如果有綱要正用於具有不符合 HIPAA 標準的服務的現有資料流中，則嘗試向該綱要新增敏感資料使用標籤會導致出現政策違規訊息，且該動作會受到制止。此訊息會指定哪個資料流觸發違規，並建議從資料流中移除任何非HIPAA就緒的服務以解決問題。

### 稽核記錄

在 Experience Platform 中，可使用稽核記錄的形式監視資料流活動。稽核記錄會指出&#x200B;**誰**&#x200B;執行了&#x200B;**什麼**&#x200B;動作，以及&#x200B;**何時**，以及其他可協助您疑難排解資料串流相關問題的內容資料，以協助您的企業遵守公司資料管理原則和法規要求。

每當使用者建立、更新或刪除資料流時，都會建立稽核記錄以記錄動作。每當使用者透過[資料集合的資料準備](./data-prep.md)建立、更新或刪除對應時，同樣的情況就會發生。無論更新的是資料流或是對應，都會將產生的稽核記錄分類為[!UICONTROL 資料流]資源類型。

如需有關如何解讀資料流的記錄和其他支援服務的詳細資訊，請至[稽核記錄](../landing/governance-privacy-security/audit-logs/overview.md)參閱文件。

## 後續步驟

本指南提供了資料流及其在資料集合以及敏感資料處理中之使用的高層級概觀。如需有關如何設定新資料流的步驟，請參閱[資料流設定指南](./configure.md)。
