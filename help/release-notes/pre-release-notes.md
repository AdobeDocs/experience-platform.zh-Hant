---
title: Experience Platform發行前說明
description: Adobe Experience Platform最新版本注意事項預覽。
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 9cf809f8fd6e424b4dcd800c3d554e4eb0e337dc
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 33%

---

# Adobe Experience Platform搶鮮版發行說明

>[!IMPORTANT]
>
>本檔案旨在當月發行說明的&#x200B;**預覽**。 發行專案可能會有所變更，且可能會在最終發行中新增或移除。

>[!TIP]
>
>如需其他 Adobe Experience Platform 應用程式的發行說明，請參閱以下文件：
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/releases/pre-release-notes)
>- [聯合客群構成](https://experienceleague.adobe.com/zh-hant/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/zh-hant/docs/real-time-cdp-collaboration/using/latest)

**發行日期： 2025年10月**

Adobe Experience Platform 的新功能及現有功能更新：

- [警報](#alerts)
- [目標](#destinations)
- [細分服務](#segmentation-service)
- [來源](#sources)

## 警報 {#alerts}

Experience Platform 可讓您訂閱各種 Experience Platform 活動的事件型警報。您可以透過 Experience Platform 使用者介面中的「[!UICONTROL 警報]」標籤訂閱不同的警報規則，而且可以選擇在使用者介面本身內或透過電子郵件通知接收警報訊息。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 目的地失敗率警報 | 已新增目的地的新警示： **目的地失敗率超過臨界值**。 此警報會在資料啟用期間的失敗記錄數超過允許的臨界值時通知您，讓您快速回應啟用問題。 |

{style="table-layout:auto"}

如需有關警報的詳細資訊，請閱讀[[!DNL Observability Insights] 概觀](../observability/home.md)。

## 目標 {#destinations}

[!DNL Destinations] 是預先建立的目標平台整合功能，能夠順暢啟用來自 Experience Platform 的資料。您可以使用目標來啟用已知和未知的資料，以供跨通道行銷活動、電子郵件行銷活動、定向廣告及其他許多使用案例使用。

**全新或已更新的目標**

| 目標 | 說明 |
| --- | --- |
| [!DNL AdForm] | 使用此目的地將Adobe Real-Time CDP對象傳送至[!DNL AdForm]，以根據Experience Cloud ID (ECID)和[!DNL AdForm]的ID Fusion來啟用。 [!DNL AdForm]的ID Fusion是一項ID解析服務，可讓您根據Experience Cloud ID (ECID)啟用第一方對象。 |
| `Amazon Ads` | 我們已新增其他個人識別碼支援，例如`firstName`、`lastName`、`street`、`city`、`state`、`zip`和`country`。 將這些欄位對應為目標身分可以提高對象符合率。 |

**全新或更新版功能**

| 功能 | 說明 |
| --- | --- |
| 支援[!DNL AES256]目的地中的[!DNL Amazon S3]伺服器端加密 | [!DNL Amazon S3]目的地現在支援[!DNL AES256]伺服器端加密，為您匯出的資料提供增強的安全性。 您可以在設定或更新您的[!DNL Amazon S3]目的地連線時設定此加密方法，確保您的資料已使用業界標準的[!DNL AES256]加密演演算法靜態加密。 如需詳細資訊，請閱讀 [[!DNL Amazon]  文件](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingEncryption.html)。 |
| [幾個支援對象層級監視的新目的地](../dataflows/ui/monitor-destinations.md#audience-level-view) | 下列目的地現在支援對象層級的監控： <ul><li>[!DNL Airship Tags]</li><li>(API) [!DNL Salesforce Marketing Cloud]</li><li>[!DNL Marketo Engage]</li><li>[!DNL Microsoft Bing]</li><li>(V1) [!DNL Pega CDH Realtime Audience]</li><li>(V2) [!DNL Pega CDH Realtime Audience]</li><li>[!DNL Salesforce Marketing Cloud]帳戶參與度</li><li>[!DNL The Trade Desk]</li></ul> |
| 資料集匯出護欄修正 | 已針對資料集匯出護欄實作修正。 以前，某些包含時間戳記欄但根據XDM體驗事件結構描述為&#x200B;_非_&#x200B;的資料集錯誤地被視為體驗事件資料集，將匯出限製為365天的回顧期間。 記錄的365天回顧護欄現在僅適用於體驗事件資料集。 使用XDM體驗事件結構描述以外的任何結構描述的資料集現在由100億筆記錄的護欄管理。 有些客戶可能會發現資料集的匯出數量增加，導致該資料集錯誤地落在365天的回顧期間下。 這可讓您匯出具有較長回顧視窗的預測性工作流程的資料集。 如需詳細資訊，請閱讀[資料集匯出護欄](../destinations/guardrails.md#dataset-exports)。 |
| 增強企業目的地的受眾層級報表 | 改善企業目標的對象層級報表邏輯。 在此版本之後，客戶會看到更準確的對象報表數字，其中只會包含與所選目的地相關的對象。 此監控調整可確保報表僅包含對應至資料流的對象，更清楚瞭解實際資料啟用的方式。 這不會影響啟用的資料量，純粹是為了改善報告準確性而提供的監視增強功能。 |

如需詳細資訊，請閱讀[目標概觀](../destinations/home.md)。

## 細分服務 {#segmentation-service}

[!DNL Segmentation Service] 會說明區分客戶群中可行銷人員群組的標準，進而定義設定檔的特定子集。客群的根據可以是記錄資料 (例如人口統計資訊) 或是代表客戶與您的品牌互動情形的時間序列事件。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 串流細分監視 | 串流區段的即時監視可在沙箱、資料集和受眾層級提供評估率、延遲和資料品品質度的透明度。 此功能支援主動警示和可操作的洞察，可協助資料工程師識別容量違規和攝取問題。監控量度包括評估率、P95擷取延遲，以及接收、評估、失敗和略過的記錄。 逐個資料集和逐個對象檢視功能可全面顯示符合資格和取消資格的淨新設定檔。 |

如需詳細資訊，請閱讀[[!DNL Segmentation Service] 概觀](../segmentation/home.md)。

## 來源 {#sources}

Experience Platform 提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證，並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間，並管理資料攝取輸送量。

**新的或更新來源**

| 來源 | 說明 |
| --- | --- |
| 熟客資料的[!BADGE Beta]{type=Informative} [!DNL Talon.one]來源 | 使用[!DNL Talon.One]來源將批次和串流忠誠度資料擷取到Experience Platform。 聯結器支援串流設定檔資料、交易資料，以及包括已賺取點數、已兌換點數、過期點數和層級資料的忠誠度資料。 |

**已更新來源**

| 來源 | 說明 |
| --- | --- |
| [!DNL Google Ads]來源的一般可用性（僅限API） | [!DNL Google Ads]來源的API版本現在為「一般可用性」。 已更新API檔案，以反映最新版本現在為`v21`，且Experience Platform支援所有版本v19及更高版本。 UI版本仍會保留為Beta版，且僅支援一次性內嵌。 若要使用增量資料擷取，請使用API路由。 |
| [!DNL Azure Event Hubs]虛擬網路支援 | Adobe現在明確支援虛擬網路連線至Azure事件中樞，可透過私人網路而非公用網路傳輸資料。 客戶可允許列出Experience Platform VNet，以透過Azure私人骨幹私下路由事件中樞流量，為資料擷取工作流程提供增強的安全性和合規性。 |

如需詳細資訊，請閱讀[來源概觀](../sources/home.md)。
