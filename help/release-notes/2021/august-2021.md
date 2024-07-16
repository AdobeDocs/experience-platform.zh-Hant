---
title: Adobe Experience Platform發行說明2021年8月
description: Adobe Experience Platform 2021 年 8 月版發行說明。
doc-type: release notes
last-update: August 25, 2021
author: ens28527
exl-id: 0513b9dc-b16c-43b3-8e17-4be4499308d4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 35%

---

# Adobe Experience Platform 發行說明

**發行日期： 2021年8月25日**

Adobe Experience Platform 現有功能的更新：

- [目的地](#destinations)
- [可觀察性深入分析](#observability)
- [即時客戶設定檔](#profile)
- [來源](#sources)

## 目的地 {#destinations}

目的地是預先建立的與目的地平台的整合，可無縫地從Adobe Experience Platform啟用資料。 您可使用目的地啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。

**新目的地**

| 目的地 | 說明 |
| ----------- | ----------- |
| [[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md) | 「飛艇屬性」目的地（先前為測試版）現已正式推出。 |
| [[!DNL Airship Tags]](../../destinations/catalog/mobile-engagement/airship-tags.md) | 飛艇標籤目的地（先前為測試版）現已正式推出。 |
| [[!DNL Braze]](../../destinations/catalog/mobile-engagement/braze.md) | Braze目的地（先前為測試版）現已正式推出。 |
| [[!DNL Pinterest Customer List]](../../destinations/catalog/advertising/pinterest.md) | 透過Pinterest客戶清單目的地，您可以從客戶清單、造訪過您網站的人或已在Pinterest上與您的內容互動的人中建立對象。 |
| [[!DNL Twitter Custom Audiences]](../../destinations/catalog/social/twitter.md) | 在Twitter中鎖定您現有的追隨者和客戶，並透過啟用您在Adobe Experience Platform中建立的對象來建立相關的再次行銷活動。 |
| [[!DNL Verizon Media/Yahoo DataX]](../../destinations/catalog/advertising/datax.md) | DataX是彙總的Verizon Media/Yahoo基礎架構，其中託管各種元件，讓Verizon Media/Yahoo能夠以安全、自動化及可擴充的方式與外部合作夥伴交換資料。 |

**新功能**

| 功能 | 說明 |
| --- | --- |
| [[!DNL Destination SDK]](../../destinations/destination-sdk/overview.md) | Adobe Experience Platform Destination SDK是一套設定API，可讓您根據您選擇的資料和驗證格式，設定用於Experience Platform的目的地整合模式，以將對象和設定檔資料傳送至您的端點。 設定儲存在Experience Platform中，並可透過API擷取以取得其他更新。 |
| [目的地的可用性改善](../../destinations/ui/activation-overview.md) | 目的地的可用性改良可讓行銷人員順暢地啟用現有目的地的區段。 |

如需有關目的地的詳細一般資訊，請參閱[目的地概觀](../../destinations/home.md)。

## 可觀察性深入分析 {#observability}

可觀察性深入分析可讓您透過使用統計量度和事件通知來監控Platform活動。

**新特性**

| 功能 | 說明 |
| --- | --- |
| 警報 | 您現在可以訂閱與Platform上執行的工作流程相關的重要警示。 訂閱特定警報規則後，當重要生命週期事件發生時（例如成功的資料擷取），或當發生需要您注意的問題時（例如擷取流程失敗或區段作業所花時間超過預期），您將會收到UI內通知和電子郵件。 如需詳細資訊，請參閱[警示概述](../../observability/alerts/overview.md)。 |

如需服務的詳細資訊，請參閱[可觀察性深入分析概觀](../../observability/home.md)。

## 即時客戶設定檔 {#profile}

Adobe Experience Platform 讓您能夠為客戶提供一致且相關的協調體驗，無論他們何時何地與您的品牌互動。透過即時客戶設定檔，您可查看每個個別客戶合併了多個管道的資料 (包括線上、離線、CRM 和協力廠商資料) 的整體檢視。 設定檔可讓您將客戶資料合併成統一的檢視畫面，針對每個客戶互動提供可採取行動且附有時間戳記的說明。

| 功能 | 說明 |
| ------- | ----------- |
| 依合併原則或身分瀏覽設定檔 | 在Experience Platform中瀏覽設定檔時，您現在可以依據合併原則瀏覽，以根據所選的合併原則預覽20個範例設定檔。 您也可以依身分瀏覽，以使用身分名稱空間和相關身分值搜尋特定設定檔。 如需詳細資訊，請參閱[即時客戶設定檔UI指南](../../profile/ui/user-guide.md)。 |

若要了解有關即時客戶設定檔的詳細資訊，包括使用設定檔資料的教學課程和最佳做法，請從閱讀[即時客戶設定檔概觀](../../profile/home.md)開始。

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Platform服務來建構、加標籤及增強這些資料。 您可以從各種來源擷取資料，例如 Adob&#x200B;&#x200B;e 應用程式、雲端型儲存空間、協力廠商軟體和 CRM 系統。

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定擷取執行的時間並管理資料擷取輸送量。

| 功能 | 說明 |
| ------- | ----------- |
| 本機檔案上傳來源聯結器 | 檔案擷取類別已重新命名為本機系統，好讓您可以使用本機檔案上傳聯結器將本機檔案直接引進Platform。 透過此聯結器擷取的資料可透過監控儀表板進行監控。 如需詳細資訊，請參閱[本機檔案上傳來源概觀](../../sources/connectors/local-system/local-file-upload.md)。 |

若要深入瞭解來源，請參閱[來源概觀](../../sources/home.md)。
