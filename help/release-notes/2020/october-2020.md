---
title: Adobe Experience Platform 發行說明 (2020 年 10 月)
description: Adobe Experience Platform 2020 年 10 月版發行說明。
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
exl-id: 89f5e2bd-8892-4d3f-a3fe-5433bb5ece7a
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 17%

---

# Adobe Experience Platform 發行說明

**發行日期： 2020年10月14日**

- [資料準備](#data-prep)
- [即時客戶輪廓](#profile)
- [Segmentation Service](#segmentation)
- [來源](#sources)
- [價值逗留時間](#time-to-value)

## 資料準備 {#data-prep}

「資料準備」讓資料工程師可在體驗資料模式 (XDM) 之間對應、轉換和驗證資料。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| `is_set`函式 | `is_set`函式可讓您檢查來源資料中是否有屬性。 `is_set`可以與`is_empty`結合使用，以檢查屬性是否存在，以及屬性內是否存在值。 |
| `get_values`函式 | `get_values`函式可讓您從任何指定索引鍵的輸入對應取得值。 |

若要了解更多資訊，請詳閱[資料準備概觀](../../data-prep/home.md)。

## 即時客戶輪廓 {#profile}

Adobe Experience Platform 讓您能夠為客戶提供一致且相關的協調體驗，無論他們何時何地與您的品牌互動。透過[!DNL Real-Time Customer Profile]，您可以看到結合來自多個管道（包括線上、離線、CRM和第三方資料）之資料的每個個別客戶的整體檢視。 [!DNL Profile]可讓您將不同的客戶資料合併成統一的檢視表，針對每個客戶互動提供可採取行動且附有時間戳記的說明。

| 功能 | 說明 |
| ------- | ----------- |
| 設定檔預覽API新增 | 設定檔預覽API (`/previewsamplestatus`)現在包含檢視整個組織設定檔片段總計劃分的功能，以及檢視跨身分識別名稱空間設定檔片段分佈的功能。 |
| 聯合結構描述檢視更新 | 在Experience Platform UI中，使用者可以更輕鬆地找到有關貢獻聯合結構的所有結構描述和資料集的資訊，以及表面關鍵屬性，例如身分和關係欄位。 這些更新可改善疑難排解功能，並驗證設定檔是否已正確設定、身分是否已正確連結，以及資料是否已成功內嵌。 |

如需[!DNL Real-Time Customer Profile]的詳細資訊，包括使用[!DNL Profile]資料的教學課程和最佳實務，請閱讀[即時客戶個人檔案總覽](../../profile/home.md)。

## 分段服務 {#segmentation}

Adobe Experience Platform Segmentation Service提供使用者介面和RESTful API，可讓您建立區段，並從[!DNL Real-Time Customer Profile]資料產生對象。 這些區段是在[!DNL Experience Platform]上集中設定和維護，讓任何Adobe應用程式都能輕鬆存取。

[!DNL Segmentation Service] 會說明區分客戶群中可行銷的一群人的標準，從而定義輪廓的特定子集。區段的基礎可能是記錄資料 (例如人口統計資訊) 或表示客戶與您的品牌互動的時間序列事件。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 串流分段限制移除 | 已移除回顧期間的七天限制。 |

如需[!DNL Segmentation Service]的詳細資訊，請參閱[分段總覽](../../segmentation/home.md)

## 來源 {#sources}

Adobe Experience Platform可從外部來源擷取資料，同時允許您使用[!DNL Experience Platform]服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform]提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間並管理資料攝取輸送量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| SFTP的SSH驗證支援 | 您可以使用RSA/DSA Open SSH金鑰將您的SFTP帳戶連線至[!DNL Experience Platform]。 如需詳細資訊，請參閱[SFTP總覽](../../sources/connectors/cloud-storage/sftp.md)。 |
| UX改進 | 您可以在資料擷取程式期間啟用[!DNL Profile]的資料集。 如需詳細資訊，請參閱[雲端儲存體資料流工作流程](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md)教學課程。 |

若要深入瞭解來源，請參閱[來源概觀](../../sources/home.md)。

## 價值逗留時間 {#time-to-value}

Adobe Experience Platform可讓行銷營運團隊完全建立客戶的360度檢視，而不需要廣泛的資料工程專業知識。 目標是透過資料速度加速團隊和創造價值。

「實現價值的時間」會跨越角色。 資料工程師可利用資料活動透明度，以有效率且加速的方式完成工作，更早提供健全、可擴充的即時客戶設定檔。 行銷人員隨後可使用完整、強大的客戶設定檔進行細分和啟動。

### 功能重點

#### 結構描述

升級可用性和工作流程，並提供現成的深入分析、標準化，以及結構描述組合中關鍵欄位的透明度。 針對以「聯合結構描述」代表的個別資料模型組合公開資料譜系，在結構和組成部分中提供insight給即時客戶個人檔案。

- 結構描述工作流程升級
   - 針對最常見的XDM結構描述型別使用捷徑，在結構描述編輯器中使用自動化設定，並根據您的目標提供結構描述欄位群組建議
   - 使用多個欄位群組選擇和預覽功能提高工作流程效率
   - 提供結構描述組合關鍵屬性的透明度，包括身分、關係，以及必填和已棄用的欄位
- 聯合結構描述資料譜系和關鍵屬性透明度

#### 資料擷取與收集

自動對應、對應預覽和可用性升級會從任何平台或來源引入資料，以用於設定檔、下游細分和啟用。 系統具備效率與智慧，讓此程式更易於使用，即使是IT以外的人也能使用。

- 透過目錄頁面卡和資料表內嵌動作模式升級，更輕鬆地存取資料來源
- 資料擷取的計算欄位/運算式
- 資料對應建議可加速擷取程式
- 對應預覽和驗證

#### 設定檔組態

具有自訂功能的行銷人員友善設定檔檢視器可協助您瞭解用於細分、規劃和啟用案例的設定檔組成。 合併的工作流程會提供合併原則的逐步工作流程，以可控且有效率的方式對設定檔進行水合。

- 在增強的設定檔檢視器中檢視每個個別設定檔，該檢視器會顯示具有完整自訂功能的儀表板，以便根據行銷人員的業務目標啟用分組的跨管道資料。
- 根據業務需求，在基本資訊Widget中編輯標準和自訂屬性。
- 使用聯合結構描述選擇器，使用即時客戶設定檔中的屬性自訂Widget。 聯合結構描述是從設定檔資料擷取中使用的基礎資料模型衍生而來。


#### 監控

確保資料流程的透明度，並提供insight有關來源聯結器進入系統資料流量的健康狀況，提供更完善的自助服務，並加快疑難排解情境時的可操作性。

- 監視所有流程執行，並檢視每個執行的詳細檢視，包括完成狀態、執行持續時間、已處理的檔案清單、錯誤和可操作的診斷
