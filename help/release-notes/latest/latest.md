---
title: Adobe Experience Platform 發行說明
description: Experience Platform的最新發行說明
doc-type: release notes
last-update: July 15, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: f881c1365684b1ca9e6bf9a8ce866d234dc54128
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 5%

---


# Adobe Experience Platform 發行說明

**發行日期：2020 年 7 月 15 日**

Adobe Experience Platform現有功能的更新：

- [資料控管](#governance)
- [即時客戶個人檔案](#profile)
- [區段服務](#segmentation)
- [來源](#sources)

## [!DNL Data Governance] {#governance}

Adobe Experience Platform資料治理是一系列策略和技術，用於管理客戶資料並確保符合適用於資料使用的法規、限制和政策。 它在各個層級中都扮演了關 [!DNL Experience Platform] 鍵角色，包括編目、資料傳承、資料使用標籤、資料存取政策，以及對行銷動作資料的存取控制。

**新功能**

| 功能 | 說明 |
| -----------| ---------- |
| 自動執行 [!DNL Real-time Customer Data Platform] | 現在，當發生違反動作(包括將區段啟 [!DNL Real-time CDP] 用至目標)時，會自動強制執行資料使用原則。 觸發原則違規時，使用者即時檢視啟動工作流程中的使用限制，指出他們無法使用哪些資料及原因。<br><br>如需詳細資訊，請參 [閱中的概述中](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance) ，關於強制資料使 [!DNL Data Governance] 用規範的 [!DNL Real-time CDP] 章節。 |
| Adobe Audience Manager整合 | 從中共用的任何區段 [!DNL Audience Manager] 會繼 [!DNL Platform] 承任何套用的資料使用標籤，反之亦然 [!DNL Data Export Controls]。 請參閱文 [!DNL Audience Manager] 件，瞭解使用 [標籤與資料匯出控制項之間的特定對應](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep)。 |
| 自訂資料使用標籤 | 您現在可以使用原則服務API或在UI中建立自訂資料使用標籤。 如需詳細 [資訊，請參閱](../../data-governance/labels/overview.md) 「標籤概觀」。 |

如需服務 [的詳細資訊](../../data-governance/home.md) ，請參閱資料管理概觀。

## [!DNL Real-time Customer Profile] {#profile}

Adobe Experience Platform可讓您為客戶推動協調、一致且相關的體驗，不論客戶在何處或何時與您的品牌互動。 透過 [!DNL Real-time Customer Profile]此功能，您可以全面瞭解每個客戶，並結合來自多個通道的資料，包括線上、離線、CRM和第三方資料。 [!DNL Profile] 可讓您將分散的客戶資料整合為統一的檢視，提供每個客戶互動的可操作、時間戳記帳戶。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 資料使用政策實施 | 在中 [!DNL Real-time Customer Data Platform]，當嘗試在「描述檔」工作區中執行違規動作時，會自動呈現資 [!UICONTROL 料使用] 原則違規。 如需自動 [執行原則的詳細資訊，請參閱資料管理](#governance) 的發行說明。 |

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform Segmentation Service提供使用者介面和REST風格的API，可讓您建立細分並從資料中產生受 [!DNL Real-time Customer Profile] 眾。 這些區段是集中設定並維護的， [!DNL Platform]讓任何Adobe應用程式都可輕鬆存取。

[!DNL Segmentation Service] 定義個人檔案的特定子集，方法是描述區分客戶群中有價人群的標準。 區段可以根據記錄資料（例如人口統計資訊）或代表客戶與品牌互動的時間系列事件來劃分。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 串流區段 | 串流區段現在可以在資料進入區段時符合使用者資格，因 [!DNL Platform]此可大幅縮短區段限定時間。 串流分段也可減輕手動執行分段工作的需求。 |
| 資料使用政策實施 | 在中 [!DNL Real-time Customer Data Platform]，當嘗試「區段」工作區中的違規動作時，資料使用原則違 [!UICONTROL 規會自動呈現] 。 如需自動 [執行原則的詳細資訊，請參閱資料管理](#governance) 的發行說明。 |

如需詳細資訊， [!DNL Segmentation Service]請參閱區 [段概觀](../../segmentation/home.md)

## 來源 {#sources}

Adobe Experience Platform可以從外部來源擷取資料，同時讓您使用服務來建構、標示和增強該資 [!DNL Platform] 料。 您可以從多種來源收集資料，例如Adobe應用程式、雲端儲存空間、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供REST風格的API和互動式UI，讓您輕鬆地為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定接收運行的時間，以及管理資料接收吞吐量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 刪除資料流的UI支援 | 現在，可以通過UI刪除錯誤或已不必要的資料流。 |
| 單次擷取的API和UI支援 | 現在，可以通過API或使用UI執行資料流的一次性提取，其中僅提供開始日期，而且未計畫將來的提取。 |

若要進一步瞭解來源，請參閱 [來源概觀](../../sources/home.md)。
