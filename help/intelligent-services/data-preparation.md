---
keywords: Experience Platform;home;intelligent services;popular topics
solution: Experience Platform
title: 準備資料以用於智慧型服務
topic: Intelligent Services
translation-type: tm+mt
source-git-commit: 03135f564bd72fb60e41b02557cb9ca9ec11e6e8

---


# 準備資料以用於智慧型服務

為了讓智慧型服務能夠從行銷事件資料中發掘見解，資料必須以標準結構進行語義豐富和維護。 智慧型服務運用Experience Data Model(XDM)架構來達成此目標。 具體而言，Intelligent Services中使用的所有資料集都必須符合 **Consumer ExperienceEvent(CEE)** XDM架構。

本檔案提供將行銷事件資料從多個管道對應至此架構的一般指引，概述有關架構中重要欄位的資訊，以協助您判斷如何有效地將資料對應至其架構。

## 瞭解CEE架構

消費者體驗事件結構描述個人的行為，因為它與數位行銷事件（網路或行動裝置）以及線上或離線商務活動有關。 智慧服務需要使用此模式，因為其語義上定義良好的欄位（列），以避免任何未知名稱，否則會使資料不那麼清晰。

與所有XDM模式一樣，CEE混合模式具有可擴充性。 換言之，CEE混音中可新增其他欄位，若有需要，可在多個結構中加入不同的變數。

在公用 [XDM儲存庫中可找到混合的完整示例](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md)，並應用作以下部分中概述的關鍵欄位的參考。

### 關鍵字欄位

下表重點說明CEE混合中應使用的關鍵欄位，讓智慧型服務產生有用的見解，包括說明和參考檔案的連結，以取得更多範例。

| XDM欄位 | 說明 | 參考 |
| --- | --- | --- |
| `xdm:channel` | 與ExperienceEvent相關的行銷渠道。 欄位包含頻道類型、媒體類型和位置類型的相關資訊。 **必須提&#x200B;_供此欄_,Attribution AI才能處理您的資料**。 請參閱 [下表](#example-channels) ，以取得一些範例對應。 | [體驗通道架構](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) |
| `xdm:productListItems` | 代表客戶選擇之產品的一系列項目，包括產品SKU、名稱、價格和數量。 | [商務詳細資料結構](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) |
| `xdm:commerce` | 包含ExperienceEvent的商務相關資訊，包括採購訂單編號和付款資訊。 | [商務詳細資料結構](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) |
| `xdm:web` | 代表與ExperienceEvent相關的網頁詳細資料，例如互動、頁面詳細資料和反向連結。 | [ExperienceEvent Web詳細資料結構](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) |

### 頻道範例 {#example-channels}

欄位 `xdm:channel` 代表與ExperienceEvent相關的行銷渠道。 下表提供映射至XDM的行銷渠道的一些範例：

| Player Name | `channel.mediaType` | `channel._type` | `channel.mediaAction` |
| --- | --- | --- | --- |
| 付費搜尋 | 付費 | 搜尋 | 按一下 |
| 社交——行銷 | 免費 | SOCIAL | 按一下 |
| 顯示 | 付費 | 顯示 | 按一下 |
| 電子郵件 | 付費 | 電子郵件 | 按一下 |
| 內部反向連結 | 擁有 | 直接 | 按一下 |
| 顯示檢視 | 付費 | 顯示 | 曝光 |
| QR Code重新導向 | 擁有 | 直接 | 按一下 |
| SMS文字訊息 | 擁有 | 簡訊 | 按一下 |
| 行動 | 擁有 | 行動 | 按一下 |

## 對應和收錄資料

一旦您確定行銷事件資料是否可映射至CEE架構後，就可以開始將資料帶入智慧型服務。 請連絡Adobe諮詢服務，協助您將資料對應至架構，並將其內嵌至服務。

如果您有Adobe Experience Platform訂閱，而且想要自行對應及收錄資料，請遵循下節所述的步驟。

### 使用Adobe Experience Platform

>[!NOTE] 下列步驟需要訂閱Experience Platform。 如果您沒有平台存取權，請跳至下 [一步](#next-steps) 。

本節概述將資料對應並收錄至Experience Platform以用於智慧型服務的工作流程，包括教學課程的連結以取得詳細步驟。

#### 建立CEE架構和資料集

當您準備開始準備擷取資料時，第一個步驟是建立採用CEE mixin的新XDM架構。 下列教學課程將逐步說明在UI或API中建立新架構的程式：

* [在UI中建立結構](../xdm/tutorials/create-schema-ui.md)
* [在API中建立結構](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT] 上述教學課程會遵循建立架構的一般工作流程。 為架構選擇類時，必須使用 **XDM ExperienceEvent類**。 選擇此類後，可以將CEE混合添加到模式。

將CEE混音新增至架構後，您就可以視資料中其他欄位的需要新增其他混音。

建立並儲存架構後，您就可以根據該架構建立新的資料集。 下列教學課程將逐步說明在UI或API中建立新資料集的程式：

* [在UI中建立資料集](../catalog/datasets/user-guide.md#create) （依照工作流程使用現有架構）
* [在API中建立資料集](../catalog/datasets/create.md)

#### 映射和收錄資料

建立CEE架構和資料集後，您可以開始將資料表對應至架構，並將該資料內嵌至平台。 請參閱將CSV檔 [案對應至XDM架構的教學課程](../ingestion/tutorials/map-a-csv-file.md) ，以取得如何在UI中執行此動作的步驟。 在填入資料集後，可使用相同的資料集來擷取其他資料檔案。

## 下一步 {#next-steps}

本檔案提供有關準備資料以用於智慧型服務的一般指引。 如果您需要根據使用案例提供其他諮詢服務，請聯絡Adobe諮詢支援。

在您成功將客戶體驗資料填入資料集後，您就可以使用智慧服務產生見解。 請參閱下列檔案以開始使用：

* [Attribution AI概觀](./attribution-ai/overview.md)
* [客戶人工智慧概觀](./customer-ai/overview.md)
