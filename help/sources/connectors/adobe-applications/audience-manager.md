---
keywords: Experience Platform;home;popular topics;Audience Manager connector;Audience manager;audience manager
solution: Experience Platform
title: Audience Manager連接器
topic: overview
description: Adobe Audience Manager資料連接器可將在Adobe Audience Manager中收集的第一方資料串流至Adobe Experience Platform。 Audience Manager連接器可將三種資料類別擷取至平台。
translation-type: tm+mt
source-git-commit: 6934bfeee84f542558894bbd4ba5759891cd17f3
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 1%

---


# Audience Manager連接器

Adobe Audience Manager資料連接器可將在Adobe Audience Manager中收集的第一方資料串流至Adobe Experience Platform。 Audience Manager連接器將三種資料類別擷取至平台：

- **即時資料：** 在Audience Manager的資料收集伺服器上即時擷取的資料。 此資料用於Audience Manager中，以填入以規則為基礎的特性，並會在最短的延遲時間內在平台中呈現。
- **描述檔資料：** Audience Manager使用即時和已登入的資料來衍生客戶個人檔案。 這些描述檔可用來填入區段實現的身分圖表和特徵。

Audience Manager連接器會將這些資料類別對應至Experience Data Model(XDM)架構，並將它們傳送至平台。 即時資料會以XDM ExperienceEvent資料傳送，而設定檔資料則會以XDM個別設定檔傳送。

如需有關使用平台UI建立與Adobe Audience Manager連線的指示，請參閱 [Audience Manager連接器教學課程](../../tutorials/ui/create/adobe-applications/audience-manager.md)。

## 什麼是體驗資料模型(XDM)?

XDM是公開記載的規格，可提供標準化的架構，讓平台組織客戶體驗資料。

遵循XDM標準，客戶體驗資料可以統一整合，更輕鬆地傳遞資料和收集資訊。

如需如何在Experience Platform中使用XDM的詳細資訊，請參閱 [XDM系統概觀](../../../xdm/home.md)。 若要進一步瞭解XDM結構描述（例如Profile和ExperienceEvent）的結構，請參 [閱架構構成基礎](../../../xdm/schema/composition.md)。

## XDM架構示例

以下是映射至平台中XDM ExperienceEvent和XDM個人設定檔的Audience Manager結構範例。

### ExperienceEvent —— 用於即時資料和已登錄資料

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### XDM個別配置檔案——用於配置檔案資料

![](images/aam-profile-xdm-for-profile-data.png)

## 如何將欄位從Adobe Audience Manager對應至XDM?

如需詳細資訊，請參 [閱Audience Manager對應欄位的檔案](./mapping/audience-manager.md) 。

## 平台上的資料管理

### 資料集

資料集是資料集合的儲存和管理結構，通常是表，它包含模式（列）和欄位（行），並可通過資料連接使用。 Audience Manager資料包含即時資料、傳入資料和描述檔資料。 若要找到您的Audience Manager資料集，請使用UI中的搜尋函式，並針對每種資料類型使用提供的命名慣例。

Audience Manager資料集依預設會停用至「設定檔」，而且使用者可以根據使用案例啟用或停用資料集。 建議不要停用將用於「描述檔」中區段成員資格的資料集。

| 資料集名稱 | 說明 |
| ------------ | ----------- |
| Audience Manager Realtime | 此資料集包含Audience Manager DCS端點上的直接點擊所收集的資料，以及Audience Manager設定檔的身分對應。 讓此資料集保持啟用以擷取描述檔。 |
| Audience Manager Realtime Profile更新 | 此資料集可讓Audience Manager特徵和區段的即時定位。 其中包含Edge地區路由、特徵和區段成員資格的資訊。 讓此資料集保持啟用以擷取描述檔。 |
| Audience Manager裝置資料 | 在Audience Manager中匯總具有ECID和對應區段實現的裝置資料。 |
| Audience Manager裝置設定檔資料 | 用於Audience Manager連接器診斷。 |
| Audience Manager驗證的設定檔 | 此資料集包含Audience Manager驗證的設定檔。 |
| Audience Manager驗證的設定檔中繼資料 | 用於Audience Manager Connector診斷。 |

### 連線

Adobe Audience Manager在目錄中建立一個連線： **Audience Manager Connection**。 目錄是Adobe Experience Platform中資料位置和世系記錄的系統。 連線是Catalog物件，是Connectors的客戶專屬例項。 如需目錄、連 [線和連接器的詳細資訊](../../../catalog/home.md) ，請參閱目錄服務概觀。

## 平台上的Audience Manager資料預期延遲為何？

| Audience Manager資料 | 延遲性 | 附註 |
| --- | --- | --- |
| 即時資料 | &lt; 35 分鐘. | 從在Realtime節點捕獲到在Platform Data Lake上顯示的時間。 |
| 傳入資料 | &lt; 13 小時 | 從在S3儲存區擷取到出現在平台資料湖上的時間。 |
| 描述檔資料 | &lt; 2 天 | 從Realtime/Inbound（即時／入站）資料捕獲到添加到用戶配置檔案並最終顯示在平台資料湖上的時間。 |