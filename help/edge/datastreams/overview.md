---
title: 資料流概述
description: 連接您的客戶端 Experience Platform SDK 與 Adobe 產品和協力廠商目標的整合。
keywords: 設定；資料流；datastreamId;edge；資料流ID；環境設定；edgeConfigId；身分；ID同步；啟用ID同步容器ID；沙箱；串流入口；事件資料集；目標；用戶端代碼；屬性Token；目標環境ID;Cookie目的地；URL目標；Analytics設定區塊報表套裝ID；資料收集的資料準備；資料準備；映射器；XDM；邊緣上的DM
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 2cec87d3f45b1b774925a9b669b53a958e65e57a
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 2%

---

# 資料流概觀

資料流代表實作Adobe Experience Platform Web和Mobile SDK時的伺服器端設定。 若 [configure命令](../fundamentals/configuring-the-sdk.md) 在SDK中會控制必須在用戶端上處理的項目(例如 `edgeDomain`)，資料流會處理SDK的所有其他設定。 當請求傳送至Adobe Experience Platform Edge Network時， `edgeConfigId` 用於參考資料流。 這可讓您更新伺服器端設定，而無須在網站上變更程式碼。

您可以透過選取 **[!UICONTROL 資料流]** 在Adobe Experience Platform UI或資料收集UI的左側導覽中。

![UI中的「資料流」索引標籤](../assets/datastreams/overview/datastreams-tab.png)

如需如何在UI中設定資料流的詳細資訊，請參閱 [配置指南](./configure.md).

## 處理資料流中的敏感資料 {#sensitive}

>[!IMPORTANT]
>
>本檔案的內容不是法律建議，且用意並非要取代法律建議。 請諮詢貴公司的法律部門，以取得處理敏感資料的相關建議。

企業資料管理政策和法規要求對收集、處理和使用敏感客戶資料的方式日益加大限制。 這包括受保護健康資料(PHI)的收集、處理和使用，這些資料受《健康保險可移植性和責任法》(HIPAA)等法規的約束。

資料流提供三種方法，幫助您安全地處理敏感資料：

* [增強加密](#encryption)
* [資料控管](#governance)
* [稽核記錄](#audit-logs)

### 增強加密 {#encryption}

通過邊緣網路傳輸的所有資料都是使用安全、加密的連線進行 [HTTPS TLS 1.2](https://datatracker.ietf.org/doc/html/rfc5246). 如果資料流將資料帶入Experience Platform，則在Experience Platform資料湖中靜置加密資料。 請參閱 [資料加密Experience Platform](../../landing/governance-privacy-security/encryption.md) 以取得更多資訊。

### 資料控管 {#governance}

資料流利用Experience Platform的內置資料控管功能，防止將敏感資料發送到非HIPAA就緒的服務。 借由在資料流結構中標示包含敏感資料的特定欄位，您可以精細控制哪些資料欄位可用於特定用途。

以下影片簡要概述如何在UI中針對資料流設定和執行資料使用限制：

>[!VIDEO](https://video.tv.adobe.com/v/3409588/?quality=12&learn=on&speedcontrol=on)

在Experience Platform中，您可以套用 [敏感資料使用量標籤](../../data-governance/labels/reference.md#sensitive) 結構和欄位，其中包含貴組織認為屬於敏感資料。 例如， `RHD` 標籤用於表示受保護的健康資訊(PHI)，並且 `S1` 標籤代表地理位置資料。

>[!NOTE]
>
>如需如何在 [!UICONTROL 結構] Experience PlatformUI或資料收集UI中的索引標籤，請參閱 [方案標籤教學課程](../../xdm/tutorials/labels.md).

建立新資料流時，如果所選架構包含敏感資料使用標籤，則只能將資料流配置為將該資料發送到HIPAA就緒的目標。 目前，資料流支援的唯一適用於HIPAA的目的地是Adobe Experience Platform。 其他目的地服務(包括Adobe Target、Adobe Analytics、Adobe Audience Manager、事件轉送和邊緣目的地)則會針對包含敏感資料使用標籤的資料流而停用。

如果現有資料流中使用了不支援HIPAA的服務，嘗試將敏感資料使用標籤添加到該架構會導致策略違規消息，並且阻止該操作。 該消息指定觸發違規的資料流，並建議從資料流中刪除任何非HIPAA就緒服務以解決此問題。

### 稽核記錄

在Experience Platform中，可以以稽核記錄的形式監控資料流活動。 稽核記錄會告訴 **誰** 執行 **what** 動作，和 **when**，以及其他可協助您疑難排解資料流相關問題的內容資料，以協助您的企業遵守公司資料管理政策和法規要求。

每當使用者建立、更新或刪除資料流時，就會建立稽核記錄來記錄動作。 每當使用者建立、更新或刪除對應時，就會發生相同的情況 [資料收集的資料準備](./data-prep.md). 無論是資料流還是已更新的對應，產生的稽核記錄都會分類在 [!UICONTROL 資料流] 資源類型。

請參閱 [稽核記錄](../../landing/governance-privacy-security/audit-logs/overview.md) 如需如何從資料流和其他支援服務解譯記錄檔的詳細資訊。

## 後續步驟

本指南提供資料流及其在資料收集和處理敏感資料中的用途的概觀。 如需設定新資料流的步驟，請參閱 [datastream組態指南](./configure.md).
