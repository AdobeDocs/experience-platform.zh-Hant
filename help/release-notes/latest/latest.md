---
title: Adobe Experience Platform 發行說明
description: Adobe Experience Platform的最新發行說明。
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: b1dca51264582788ccbde005b063c57e2f3edc8f
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 8%

---


# Adobe Experience Platform 發行說明

**發行日期：2021 年 25 月 8 日**

Adobe Experience Platform 現有功能更新：

- [目的地](#destinations)
- [可觀察性深入分析](#observability)
- [即時客戶個人檔案](#profile)
- [來源](#sources)

## 目的地 {#destinations}

目的地是預先建置與目的地平台的整合，可順暢地從Adobe Experience Platform啟動資料。 您可以使用目的地來針對跨通路行銷活動、電子郵件行銷活動、目標廣告和其他許多使用案例，啟用已知和未知的資料。

**新功能**

| 功能 | 說明 |
| --- | --- |
| [目的地的可用性改善](../../destinations/ui/activation-overview.md) | 目的地的可用性改善可讓行銷人員對現有目的地順暢地啟用區段。 |

如需目的地的詳細一般資訊，請參閱[目的地概述](../../destinations/home.md)。

## 可觀察性深入分析 {#observability}

可觀察性前瞻分析可讓您透過使用統計量度和事件通知來監控Platform活動。

**新特性**

| 功能 | 說明 |
| --- | --- |
| 警報 | 您現在可以訂閱與Platform上執行的工作流程相關的重要警報。 訂閱特定警報規則後，當重要的生命週期事件（例如成功的資料擷取），或有需要您注意的問題（例如擷取流程失敗或區段工作花費的時間超過預期）時，您將會收到UI內通知和電子郵件。 如需詳細資訊，請參閱[警報概述](../../observability/alerts/overview.md)。 |

如需服務的詳細資訊，請參閱[可觀察性前瞻分析概述](../../observability/home.md) 。

## 即時客戶個人檔案 {#profile}

Adobe Experience Platform可讓您為客戶提供協調、一致且相關的體驗，無論客戶在何處或何時與您的品牌互動。 透過即時客戶個人檔案，您可以全面了解各個客戶，其中結合來自多個管道的資料，包括線上、離線、CRM和第三方資料。 設定檔可讓您將客戶資料併入統一檢視中，提供每個客戶互動的可操作、時間戳記帳戶。

| 功能 | 說明 |
| ------- | ----------- |
| 按合併策略或標識瀏覽配置檔案 | 在Experience Platform中瀏覽設定檔時，您現在可以依合併原則瀏覽，以根據選取的合併原則預覽20個範例設定檔。 您也可以依身分瀏覽，以使用身分命名空間和相關身分值來搜尋特定設定檔。 如需詳細資訊，請參閱[即時客戶設定檔UI指南](../../profile/ui/user-guide.md)。 |

若要深入了解即時客戶設定檔，包括使用設定檔資料的教學課程和最佳實務，請先閱讀[即時客戶設定檔概述](../../profile/home.md)開始。

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

| 功能 | 說明 |
| ------- | ----------- |
| 本機檔案上傳來源連接器 | 檔案擷取類別已重新命名為本機系統，可讓您使用本機檔案上傳連接器，將本機檔案直接帶入Platform。 透過此連接器擷取的資料可透過「監控控制面板」進行監控。 如需詳細資訊，請參閱[本機檔案上傳來源概述](../../sources/connectors/local-system/local-file-upload.md) 。 |

若要進一步了解來源，請參閱[來源概述](../../sources/home.md)。
