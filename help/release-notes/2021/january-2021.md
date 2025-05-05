---
title: Adobe Experience Platform 發行說明 (2021 年 1 月)
description: Adobe Experience Platform 2021 年 1 月版發行說明。
doc-type: release notes
last-update: January 27, 2021
author: ens60013
exl-id: 6fb92e35-922c-47ba-8cf4-44edd92acfa1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 27%

---

# Adobe Experience Platform 發行說明

**發行日期： 2021年1月27日**

Adobe Experience Platform 現有功能的更新：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep]可讓資料工程師對應、轉換及驗證與Experience Data Model (XDM)之間的資料。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 規則運算式函式 | [!DNL Data Prep]對應程式現在支援根據規則運算式比對及擷取部分輸入欄位。 |

如需詳細資訊，請參閱[[!DNL Data Prep] 總覽](../../data-prep/home.md)。

## 目標 {#destinations}

[!DNL Destinations] 是與目標平台的預先建立整合，能夠順暢啟用來自 Adobe Experience Platform 的資料。您可以使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、定向廣告和其他諸多使用案例。

**新目的地**

| 目標 | 說明 |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob]是Microsoft的雲端物件儲存解決方案。 |

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 進階識別碼比對 | 透過新增對其他身分比對（例如外部ID、電話號碼和行動裝置ID）的支援，增強[!DNL Facebook Custom Audiences]和[!DNL Google Customer Match]中的對象符合率功能。 如需詳細資訊，請參閱下列檔案： <ul><li>[Facebook目的地](../../destinations/catalog/social/facebook.md)</li><li>[Google客戶相符目的地](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[啟用串流區段匯出目的地的受眾資料](../../destinations/ui/activate-segment-streaming-destinations.md)</li></ul> |

若要進一步瞭解，請造訪[目的地概觀](../../destinations/home.md)。

## 即時客戶輪廓 {#profile}

Adobe Experience Platform 讓您能夠為客戶提供一致且相關的協調體驗，無論他們何時何地與您的品牌互動。透過即時客戶輪廓，您可查看每個個別客戶合併了多個管道的資料 (包括線上、離線、CRM 和協力廠商資料) 的整體檢視。 [!DNL Profile]可讓您將客戶資料合併成統一的檢視畫面，針對每個客戶互動提供可採取行動且附有時間戳記的說明。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 從設定檔存放區中刪除資料集 | 當您從Experience Platform資料湖中刪除資料集時，該資料集也會自動從設定檔存放區中刪除。 您不再需要使用設定檔系統作業API端點來提出刪除請求，以明確從設定檔存放區中刪除資料集。 如需詳細資訊，請參閱[設定檔系統工作API端點指南](../../profile/api/profile-system-jobs.md)。 |
| 特定區段的估計ID名稱空間計數 | 對於預估的設定檔計數，預覽API現在會報告：<ul><li>指定名稱空間之區段中的預估設定檔總數。</li><li>在指定名稱空間的設定檔聯合結構描述中預估的設定檔總數。</li></ul>若要深入瞭解，請參閱[設定檔預覽API端點指南](../../profile/api/preview-sample-status.md)。 |

如需即時客戶個人檔案的詳細資訊，包括使用[!DNL Profile]資料的教學課程和最佳實務，請先閱讀[即時客戶個人檔案總覽](../../profile/home.md)。

## [!DNL Sources] {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Experience Platform服務來建構、加標籤及增強這些資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間並管理資料攝取輸送量。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| Adobe Audience Manager來源聯結器增強功能 | 您現在可以從Audience Manager篩選及選取個別第一方區段，以擷取至Experience Platform，並篩選掉第一方特徵。 如需詳細資訊，請參閱有關[建立Audience Manager來源聯結器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)的教學課程。 |
| [!DNL Google BigQuery]來源聯結器增強功能 | 您現在可以使用[!DNL BigQuery]來源聯結器在一次資料流執行中擷取大於10GB的檔案。 如需詳細資訊，請參閱[[!DNL BigQuery] 來源聯結器總覽](../../sources/connectors/databases/bigquery.md)。 |
| 支援雲端儲存的複雜資料型別 | 使用雲端儲存空間來源聯結器時，您現在可以內嵌複雜的資料型別，例如JSON檔案中的陣列。 如需詳細資訊，請參閱在UI[&#128279;](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md)中建立雲端儲存體資料流[或使用 [!DNL Flow Service] API](../../sources/tutorials/api/collect/cloud-storage.md)建立的教學課程。 |
| 支援[!DNL Microsoft Dynamics]來源的服務主體金鑰式驗證 | 您現在可以使用服務主要金鑰來驗證您的[!DNL Dynamics]帳戶，作為密碼式驗證的替代方案。 如需詳細資訊，請參閱[[!DNL Dynamics] 來源聯結器總覽](../../sources/connectors/crm/ms-dynamics.md)。 |
| 雲端儲存空間來源中的自訂分隔符號的UI支援 | 您現在可以設定自訂欄分隔符號，例如逗號(`,`)、定位字元(`\t`)或垂直號(`|`)，以收集使用者介面中的分隔檔案。 如需詳細資訊，請參閱有關[使用雲端儲存空間來源聯結器](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md)建立資料流的教學課程 |

若要深入瞭解來源，請參閱[來源概觀](../../sources/home.md)。
