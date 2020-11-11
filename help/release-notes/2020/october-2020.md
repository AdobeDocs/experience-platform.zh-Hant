---
title: Adobe Experience Platform 發行說明
description: Experience Platform發行說明2020年10月
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: e2b0048703816dc481eb9486310d86a8f2483af2
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 4%

---


# Adobe Experience Platform 發行說明

**發行日期：2020 年 10 月 14 日**

- [資料準備](#data-prep)
- [即時客戶個人檔案](#profile)
- [劃分服務](#segmentation)
- [來源](#sources)
- [價值時間](#time-to-value)

## 資料準備 {#data-prep}

資料準備可讓資料工程師將資料對應、轉換及驗證至Experience Data Model(XDM)。

**主要功能**

| 功能 | 說明 |
| ------- | ----------- |
| `is_set` 函數 | 此函 `is_set` 數允許您檢查源資料中是否存在屬性。 `is_set` 可與組合使用， `is_empty` 以檢查屬性的存在和屬性中值的存在。 |
| `get_values` 函數 | 此函 `get_values` 數可讓您從輸入映射取得任何指定鍵的值。 |

如需詳細資訊，請閱讀資料準 [備概觀](../../data-prep/home.md)。

## 即時客戶個人檔案 {#profile}

Adobe Experience Platform可讓您為客戶推動協調、一致且相關的體驗，不論客戶在何處或何時與您的品牌互動。 透過 [!DNL Real-time Customer Profile]此功能，您可以全面瞭解每個客戶，並結合來自多個通道的資料，包括線上、離線、CRM和第三方資料。 [!DNL Profile] 可讓您將分散的客戶資料整合為統一的檢視，提供每個客戶互動的可操作、時間戳記帳戶。

| 功能 | 說明 |
| ------- | ----------- |
| 描述檔預覽API新增功能 | 描述檔預覽API(`/previewsamplestatus`)現在包含在IMS組織中檢視描述檔片段總數的劃分，以及在身分名稱空間中檢視描述檔片段的分佈。 |
| 聯合架構視圖更新 | 在Experience Platform UI中，使用者可以更輕鬆地找到有關所有結構描述和資料集的資訊，以及表面金鑰屬性，例如身分和關係欄位。 這些更新可改善疑難排解和驗證描述檔已正確設定、身分識別已正確銜接，以及資料已成功擷取的能力。 |

有關使用資 [!DNL Real-time Customer Profile]料的更多資訊，包括教學課程和最佳實務，請 [!DNL Profile] 閱讀即時客 [戶資料概觀](../../profile/home.md)。

## 劃分服務 {#segmentation}

Adobe Experience Platform Segmentation Service提供使用者介面和REST風格的API，可讓您建立細分並從資料中產生受 [!DNL Real-time Customer Profile] 眾。 這些區段是集中設定並維護的， [!DNL Platform]讓任何Adobe應用程式都可輕鬆存取。

[!DNL Segmentation Service] 定義個人檔案的特定子集，方法是描述區分客戶群中有價人群的標準。 區段可以根據記錄資料（例如人口統計資訊）或代表客戶與品牌互動的時間系列事件來劃分。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 移除串流區段限制 | 回顧時段的七天限制已移除。 |

如需詳細資訊， [!DNL Segmentation Service]請參閱區 [段概觀](../../segmentation/home.md)

## 來源 {#sources}

Adobe Experience Platform可以從外部來源擷取資料，同時讓您使用服務來建構、標示和增強該資 [!DNL Platform] 料。 您可以從多種來源收集資料，例如Adobe應用程式、雲端儲存空間、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供REST風格的API和互動式UI，讓您輕鬆地為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定接收運行的時間，以及管理資料接收吞吐量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 分層映射 | 您可以在資料擷取程式期間預覽階層式來源檔案，例如JSON或Parce。 |
| SFTP的SSH驗證支援 | 您可以使用RSA/DSA Open SSH密鑰將SFTP [!DNL Platform] 帳戶連接到。 See the [SFTP overview](../../sources/connectors/cloud-storage/ftp-sftp.md) for more information. |
| UX改進 | 您可以在資料擷取程式 [!DNL Profile] 期間啟用資料集。 如需詳細 [資訊，請參閱雲端儲存資料流工作流程](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) 教學課程。 |

若要進一步瞭解來源，請參閱 [來源概觀](../../sources/home.md)。

## 價值時間 {#time-to-value}

Adobe Experience Platform完全讓行銷營運團隊能夠全方位瞭解客戶，而不需具備廣泛的資料工程專業知識。 其目標是透過資料速度加速團隊並發揮價值。

「價值時間」可跨角色切換。 資料工程師可以透過資料活動透明度，以有效率且快速的方式完成工作，以便更快地提供強穩、可擴充的即時客戶個人檔案。 然後，行銷人員就可使用完整、強穩的客戶個人檔案進行細分和啟動。

### 功能摘要

#### 結構

升級可用性和工作流程，並提供架構構圖中關鍵欄位的現成見解、標準化和透明度。 針對以「聯合架構」表示的個別資料模型組合公開資料世系，提供即時客戶描述檔的結構和成分分析。

- 架構工作流程升級
   - 使用最常見XDM結構描述類型的捷徑，在結構描述編輯器中使用自動設定，並根據您的目標混合建議
   - 運用多種混合選擇和預覽功能，提高工作流程效率
   - 提供結構構成關鍵屬性的透明度，包括身分、關係，以及必填和已過時欄位
- 聯合模式資料世系和關鍵屬性透明性

#### 資料擷取與收集

自動對應、對應預覽和可用性升級可從任何平台或來源匯入資料，以用於描述檔、下游區段和啟動。 此系統具備效率和智慧，讓此程式更易於使用，即使是IT以外的人也能使用。

- 透過目錄頁面卡和資料表內嵌動作模式升級，更輕鬆地存取資料來源
- 資料擷取的計算欄位／運算式
- 資料對應建議可加速擷取程式
- 對應預覽和驗證

#### 描述檔設定

適用於行銷人員的自訂設定檔檢視器可協助您瞭解設定檔的構成，以便用於細分、規劃和啟動案例。 通過提供用於合併策略的逐步工作流，整合的工作流以受控和有效的方式為配置檔案補充。

- 在增強的描述檔檢視器中檢視每個個別描述檔，其中顯示具有完整自訂的控制面板，以根據行銷人員的業務目標啟用分組的跨通道資料。
- 根據業務需要，在基本資訊構件中編輯標準屬性和自定義屬性。
- 使用聯合結構選擇器，使用即時客戶描述檔中的屬性來自訂Widget。 聯合模式是從描述檔資料擷取中使用的基礎資料模型衍生而來。


#### 監控

確保資料流的透明性，並深入瞭解來源連接器進入系統的資料流量狀況，為疑難排解情況提供更多自助服務和更快的行動能力。

- 監視所有流運行並查看每個運行的詳細視圖，包括完成狀態、運行持續時間、已處理檔案的清單、錯誤和可操作的診斷