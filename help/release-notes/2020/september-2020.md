---
title: Adobe Experience Platform 發行說明 (2020 年 9 月)
description: Adobe Experience Platform 2020 年 9 月版發行說明。
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
exl-id: bf401f3a-b088-4cbd-9a64-224294b797b9
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 36%

---

# Adobe Experience Platform 發行說明

**發行日期： 2020年9月9日**

Adobe Experience Platform 現有功能的更新：

- [資料治理](#governance)
- [[!DNL Destinations]](#destinations)
- [[!DNL Observability Insights]](#observability)
- [[!DNL Privacy Service]](#privacy)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## 資料治理 {#governance}

Adobe Experience Platform 資料治理是一系列的策略和技術，用於管理客戶資料並確保符合適用於資料使用方式的法規、限制和政策。它在 [!DNL Experience Platform] 的不同階層都扮演重要的角色，包括編目、資料譜系、資料使用標籤、資料存取政策，以及對行銷動作資料的存取控制。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 資料集標籤UI增強功能 | 已將數個新的排序和篩選控制項新增至資料集標籤UI，以便更輕鬆地使用大型結構描述： <ul><li>根據完整結構描述路徑，依字母順序排序欄位。</li><li>對欄位路徑名稱執行部分搜尋。</li><li>篩選沒有標籤、選定標籤或標籤類別的欄位。</li></ul> |

如需服務的詳細資訊，請參閱[資料控管概觀](../../data-governance/home.md)。

## 目標 {#destinations}

在[Real-Time Customer Data Platform](../../rtcdp/overview.md)中，目的地是預先建立的與目的地平台的整合，可透過順暢的方式為這些合作夥伴啟用資料。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| UX改進 | 使用者可以存取內嵌表格動作，以更輕鬆地存取主要動作，例如新增資料、編輯排程和新增區段。 如需詳細資訊，請參閱[目的地工作區](../../destinations/ui/destinations-workspace.md)檔案。 |

若要深入瞭解，請造訪[目的地概觀](../../destinations/home.md)

## [!DNL Observability Insights] {#observability}

[!DNL Observability Insights]可讓您透過使用統計量度和事件通知來監視Adobe Experience Platform上的活動。

**新特性**

| 功能 | 說明 |
| --- | --- |
| Adobe I/O事件通知 | [!DNL Observability Insights]利用Adobe I/O Events為多個Experience Platform服務建立事件通知。 通知裝載會傳送至已設定的webhook，然後您可以使用它來自動化後續的下游流程。 |

如需服務的詳細資訊，請參閱[[!DNL Observability Insights] 總覽](../../observability/home.md)。

## [!DNL Privacy Service] {#privacy}

有多項法律及組織法規授予使用者權利，讓使用者有權透過請求，從您的資料存放區存取或刪除其個人資料。Adobe Experience Platform [!DNL Privacy Service] 提供 RESTful API 和使用者介面，協助您管理這些來自客戶的資料請求。透過 [!DNL Privacy Service]，您可以提交請求來存取和刪除 Adobe Experience Cloud 應用程式中的私人或個人客戶資料，從而促進法律和組織隱私法規的自動化合規。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 支援 LGPD (巴西) | 隱私權作業現在可根據巴西的 [!DNL Lei Geral de Proteção de Dados] (LGPD) 法規來建立。這些作業會受到監管法規 `lgpd_bra` 的追蹤。 |

參閱 [Privacy Service 概觀](../../privacy-service/home.md)可了解更多有關該服務的資訊。

## 即時客戶輪廓 {#profile}

Adobe Experience Platform 讓您能夠為客戶提供一致且相關的協調體驗，無論他們何時何地與您的品牌互動。透過[!DNL Real-Time Customer Profile]，您可以看到結合來自多個管道（包括線上、離線、CRM和第三方資料）之資料的每個個別客戶的整體檢視。 [!DNL Profile]可讓您將不同的客戶資料合併成統一的檢視表，針對每個客戶互動提供可採取行動且附有時間戳記的說明。

| 功能 | 說明 |
| ------- | ----------- |
| 設定檔檢視器 | Experience Platform UI中的設定檔檢視器已更新，成為具有完整自訂功能的儀表板。 使用者現在可以選擇執行下列工作： <ul><li>更新基本資訊Widget中選取的標準與自訂屬性。</li><li>建立、編輯和移除自訂Widget</li><li>調整大小並重新排列Widget</li></ul> |

如需[!DNL Real-Time Customer Profile]的詳細資訊，包括使用[!DNL Profile]資料的教學課程和最佳實務，請閱讀[即時客戶個人檔案總覽](../../profile/home.md)。

## 分段服務 {#segmentation}

Adobe Experience Platform Segmentation Service提供使用者介面和RESTful API，可讓您建立區段，並從[!DNL Real-Time Customer Profile]資料產生對象。 這些區段是在[!DNL Experience Platform]上集中設定和維護，讓任何Adobe應用程式都能輕鬆存取。

[!DNL Segmentation Service] 會說明區分客戶群中可行銷的一群人的標準，從而定義輪廓的特定子集。區段的基礎可能是記錄資料 (例如人口統計資訊) 或表示客戶與您的品牌互動的時間序列事件。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 匯出工作 | 已新增標幟，以允許將區段評估為匯出作業的一部分。 因此，使用者可以在單一工作中執行細分和匯出。 |
| 合併原則 | 單一批次分段工作中可包含多個合併原則。 |

如需[!DNL Segmentation Service]的詳細資訊，請參閱[分段總覽](../../segmentation/home.md)

## 來源 {#sources}

Adobe Experience Platform可從外部來源擷取資料，同時允許您使用[!DNL Experience Platform]服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform]提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間並管理資料攝取輸送量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 自動對應 | [!DNL Experience Platform]會根據使用者選取的目標結構描述或資料集，在資料擷取工作流程期間提供自動對應的智慧型建議。 您可以手動調整彈性的自動對應規則，以符合您的使用案例。 |
| UX改進 | 使用者可以存取內嵌表格動作，以便更輕鬆地存取主要動作，例如新增資料、編輯排程和新增區段。 如需詳細資訊，請參閱[監視資料流](../../sources/tutorials/ui/monitor.md)檔案。 |

若要深入瞭解來源，請參閱[來源概觀](../../sources/home.md)。
