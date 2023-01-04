---
title: Adobe Experience Platform發行說明2021年8月
description: 2021年8月Adobe Experience Platform發行說明。
doc-type: release notes
last-update: August 25, 2021
author: ens28527
exl-id: 0513b9dc-b16c-43b3-8e17-4be4499308d4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 6%

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

**新目的地**

| 目的地 | 說明 |
| ----------- | ----------- |
| [[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md) | 先前為測試版的Airship屬性目的地現在已可供使用。 |
| [[!DNL Airship Tags]](../../destinations/catalog/mobile-engagement/airship-tags.md) | 先前為測試版的Airship標籤目的地現在已可供使用。 |
| [[!DNL Braze]](../../destinations/catalog/mobile-engagement/braze.md) | Braze目的地先前是測試版，現已正式推出。 |
| [[!DNL Pinterest Customer List]](../../destinations/catalog/advertising/pinterest.md) | pinterest客戶清單目的地可讓您從客戶清單、造訪過您網站的人員或已在Pinterest上與您的內容互動的人員建立對象。 |
| [[!DNL Twitter Custom Audiences]](../../destinations/catalog/social/twitter.md) | 鎖定Twitter中現有的追隨者和客戶，並啟用Adobe Experience Platform中建置的對象，以建立相關的再行銷活動。 |
| [[!DNL Verizon Media/Yahoo DataX]](../../destinations/catalog/advertising/datax.md) | DataX是Verizon Media/Yahoo的聚合基礎架構，它承載各種元件，使Verizon Media/Yahoo能夠以安全、自動化和可擴展的方式與其外部合作夥伴交換資料。 |

**新功能**

| 功能 | 說明 |
| --- | --- |
| [[!DNL Destination SDK]](../../destinations/destination-sdk/overview.md) | Adobe Experience Platform Destination SDK是一組設定API，可讓您根據所選的資料和驗證格式，設定目標整合模式，讓Experience Platform將對象和設定檔資料傳送至端點。 設定會儲存在Experience Platform中，並可透過API擷取以取得其他更新。 |
| [目的地的可用性改善](../../destinations/ui/activation-overview.md) | 目的地的可用性改善可讓行銷人員對現有目的地順暢地啟用區段。 |

如需目的地的詳細一般資訊，請參閱 [目的地概述](../../destinations/home.md).

## 可觀察性深入分析 {#observability}

可觀察性前瞻分析可讓您透過使用統計量度和事件通知來監控Platform活動。

**新特性**

| 功能 | 說明 |
| --- | --- |
| 警報 | 您現在可以訂閱與Platform上執行的工作流程相關的重要警報。 訂閱特定警報規則後，當重要的生命週期事件（例如成功的資料擷取），或有需要您注意的問題（例如擷取流程失敗或區段工作花費的時間超過預期）時，您將會收到UI內通知和電子郵件。 如需詳細資訊，請參閱 [警報概觀](../../observability/alerts/overview.md). |

請參閱 [可觀察性深入分析概述](../../observability/home.md) 以取得服務的詳細資訊。

## 即時客戶個人檔案 {#profile}

Adobe Experience Platform可讓您為客戶提供協調、一致且相關的體驗，無論客戶在何處或何時與您的品牌互動。 透過即時客戶個人檔案，您可以全面了解各個客戶，其中結合來自多個管道的資料，包括線上、離線、CRM和第三方資料。 設定檔可讓您將客戶資料併入統一檢視中，提供每個客戶互動的可操作、時間戳記帳戶。

| 功能 | 說明 |
| ------- | ----------- |
| 按合併策略或標識瀏覽配置檔案 | 在Experience Platform中瀏覽設定檔時，您現在可以依合併原則瀏覽，以根據選取的合併原則預覽20個範例設定檔。 您也可以依身分瀏覽，以使用身分命名空間和相關身分值來搜尋特定設定檔。 如需詳細資訊，請參閱 [即時客戶個人檔案UI指南](../../profile/ui/user-guide.md). |

若要進一步了解即時客戶個人檔案，包括使用個人檔案資料的教學課程和最佳實務，請先閱讀 [即時客戶個人檔案概觀](../../profile/home.md).

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

| 功能 | 說明 |
| ------- | ----------- |
| 本機檔案上傳來源連接器 | 檔案擷取類別已重新命名為本機系統，可讓您使用本機檔案上傳連接器，將本機檔案直接帶入Platform。 透過此連接器擷取的資料可透過「監控控制面板」進行監控。 請參閱 [本機檔案上傳來源概觀](../../sources/connectors/local-system/local-file-upload.md) 以取得更多資訊。 |

若要進一步了解來源，請參閱 [來源概觀](../../sources/home.md).
