---
title: Adobe Experience Platform發行說明2021年8月
description: 2021年8月為Adobe Experience Platform發佈的說明。
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
- [即時客戶設定檔](#profile)
- [來源](#sources)

## 目的地 {#destinations}

目的地是預先構建的與目標平台的整合，這些平台允許從Adobe Experience Platform無縫激活資料。 您可以使用目標來激活跨渠道市場營銷活動、電子郵件活動、目標廣告和許多其他使用案例的已知和未知資料。

**新目標**

| 目的地 | 說明 |
| ----------- | ----------- |
| [[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md) | 飛艇屬性目標（以前是beta）現已正式提供。 |
| [[!DNL Airship Tags]](../../destinations/catalog/mobile-engagement/airship-tags.md) | 飛艇標籤目的地以前是beta，現在已普遍提供。 |
| [[!DNL Braze]](../../destinations/catalog/mobile-engagement/braze.md) | Braze目的地以前是beta，現在已正式提供。 |
| [[!DNL Pinterest Customer List]](../../destinations/catalog/advertising/pinterest.md) | 使用Pinterest客戶清單目標，您可以從您的客戶清單、訪問您站點的人員或已與您在Pinterest上的內容進行交互的人員中建立訪問者。 |
| [[!DNL Twitter Custom Audiences]](../../destinations/catalog/social/twitter.md) | 瞄準您在Twitter的現有追隨者和客戶，並通過激活您在Adobe Experience Platform內構建的受眾來建立相關的再營銷活動。 |
| [[!DNL Verizon Media/Yahoo DataX]](../../destinations/catalog/advertising/datax.md) | DataX是Verizon Media/Yahoo的聚合基礎架構，它承載著各種元件，使Verizon Media/Yahoo能夠以安全、自動和可擴展的方式與外部合作夥伴交換資料。 |

**新功能**

| 功能 | 說明 |
| --- | --- |
| [[!DNL Destination SDK]](../../destinations/destination-sdk/overview.md) | Adobe Experience Platform Destination SDK是一套配置API，允許您配置目標整合模式，以便根據您選擇的資料和身份驗證格式將受眾和配置檔案資料傳送到您的端點。 這些配置儲存在Experience Platform中，並可通過API檢索，以進行其他更新。 |
| [對目標的可用性改進](../../destinations/ui/activation-overview.md) | 對目標的可用性改進使營銷人員能夠無縫地激活到現有目標的段。 |

有關目標的更多一般資訊，請參閱 [目標概述](../../destinations/home.md)。

## 可觀察性深入分析 {#observability}

Oncebrity Insights允許您通過使用統計度量和事件通知來監視平台活動。

**新特性**

| 功能 | 說明 |
| --- | --- |
| 警報 | 您現在可以訂閱與平台上運行的工作流相關的重要警報。 訂閱特定警報規則後，當發生重要生命週期事件（如成功的資料接收）或存在需要您注意的問題（如接收流失敗或段作業花費的時間超過預期）時，您將收到UI內通知和電子郵件。 有關詳細資訊，請參見 [警報概述](../../observability/alerts/overview.md)。 |

查看 [可觀性透視概述](../../observability/home.md) 的子菜單。

## 即時客戶設定檔 {#profile}

Adobe Experience Platform使您能夠為您的客戶提供協調、一致和相關的體驗，無論客戶在何處或何時與您的品牌進行交互。 使用即時客戶配置檔案，您可以看到每個客戶的整體視圖，該視圖將來自多個渠道的資料組合在一起，包括線上、離線、CRM和第三方資料。 配置檔案允許您將客戶資料整合到一個統一視圖中，為每次客戶交互提供一個可操作且時間戳記的帳戶。

| 功能 | 說明 |
| ------- | ----------- |
| 按合併策略或標識瀏覽配置檔案 | 在Experience Platform中瀏覽配置式時，現在可以通過合併策略瀏覽，以基於所選合併策略預覽20個示例配置式。 您還可以按標識瀏覽，以便使用標識命名空間和相關標識值搜索特定的配置檔案。 有關詳細資訊，請參見 [即時客戶概要檔案UI指南](../../profile/ui/user-guide.md)。 |

要瞭解有關即時客戶概要資訊的更多資訊，包括有關使用概要資訊資料的教程和最佳做法，請首先閱讀 [即時客戶概要資訊概述](../../profile/home.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用平台服務來構建、標籤和增強資料。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

Experience Platform提供REST風格的API和互動式UI，讓您能夠輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

| 功能 | 說明 |
| ------- | ----------- |
| 本地檔案上載源連接器 | 檔案接收類別已更名為本地系統，允許您使用本地檔案上載連接器將本地檔案直接帶到平台。 通過此連接器接收的資料可以通過監視儀表板進行監視。 查看 [本地檔案上載源概述](../../sources/connectors/local-system/local-file-upload.md) 的子菜單。 |

要瞭解有關源的詳細資訊，請參閱 [源概述](../../sources/home.md)。
