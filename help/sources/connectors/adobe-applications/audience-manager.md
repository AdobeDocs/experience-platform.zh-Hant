---
keywords: Experience Platform;home；熱門主題；Audience Manager連接器；Audience Manager;Audience Manager
solution: Experience Platform
title: Audience Manager來源連接器概觀
topic: overview
description: Adobe Audience Manager來源連接器可將Audience Manager中收集的第一方資料串流至Adobe Experience Platform。
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 0%

---


# Audience Manager連接器

Adobe Audience Manager資料連接器可將在Adobe Audience Manager中收集的第一方資料串流至Adobe Experience Platform。 Audience Manager連接器將兩類資料收錄至平台：

- **即時資料：在Audience Manager** 的資料收集伺服器上即時擷取的資料。此資料用於Audience Manager中，以填入以規則為基礎的特性，並會在最短的延遲時間內在平台中呈現。
- **描述檔資料：** Audience Manager使用即時和已登入的資料來衍生客戶描述檔。這些描述檔可用來填入區段實現的身分圖表和特徵。

Audience Manager連接器會將這些資料類別對應至Experience Data Model(XDM)架構，並將它們傳送至平台。 即時資料會以XDM ExperienceEvent資料傳送，而設定檔資料則會以XDM個別設定檔傳送。

如需有關使用平台UI建立與Adobe Audience Manager連線的指示，請參閱[Audience Manager連接器教學課程](../../tutorials/ui/create/adobe-applications/audience-manager.md)。

## 什麼是體驗資料模型(XDM)?

XDM是公開記載的規格，可提供標準化的架構，讓平台組織客戶體驗資料。

遵循XDM標準，客戶體驗資料可以統一整合，更輕鬆地傳遞資料和收集資訊。

如需如何在Experience Platform中使用XDM的詳細資訊，請參閱[XDM系統概觀](../../../xdm/home.md)。 如需進一步瞭解如何建構XDM結構描述檔（如Profile和ExperienceEvent），請參閱架構構成的[基本說明](../../../xdm/schema/composition.md)。

## XDM架構示例

以下是映射至平台中XDM ExperienceEvent和XDM個人設定檔的Audience Manager結構範例。

### ExperienceEvent —— 適用於即時資料和已登入資料

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### XDM個別配置檔案——用於配置檔案資料

![](images/aam-profile-xdm-for-profile-data.png)

## 如何將欄位從Adobe Audience Manager對應至XDM?

如需詳細資訊，請參閱[Audience Manager對應欄位](./mapping/audience-manager.md)的檔案。

## 平台上的資料管理

### 資料集

資料集是資料集合的儲存和管理結構，通常是表，它包含模式（列）和欄位（行），並可通過資料連接使用。 Audience Manager資料由即時資料、傳入資料和描述檔資料組成。 若要找到您的Audience Manager資料集，請使用UI中的搜尋函式，並針對每種資料類型使用提供的命名慣例。

Audience Manager資料集依預設會停用至「設定檔」，而且使用者可以根據使用案例啟用或停用資料集。 建議不要停用將用於「描述檔」中區段成員資格的資料集。

| 資料集名稱 | 說明 |
| ------------ | ----------- |
| AAM即時 | 此資料集包含Audience Manager DCS端點上的直接點擊所收集的資料，以及Audience Manager設定檔的身分對應。 讓此資料集保持啟用以擷取描述檔。 |
| AAM即時描述檔更新 | 此資料集可讓Audience Manager特徵和區段的即時定位。 其中包含Edge地區路由、特徵和區段成員資格的資訊。 讓此資料集保持啟用以擷取描述檔。 資料集中的資料不會顯示為批次。 您可以啟用&#x200B;**[!UICONTROL Profile]**&#x200B;切換，將資料直接收錄至Profile。 |
| AAM裝置資料 | 在Audience Manager中匯總具有ECID和對應區段實現的裝置資料。 資料集中的資料不會顯示為批次。 您可以啟用&#x200B;**[!UICONTROL Profile]**&#x200B;切換，將資料直接收錄至Profile。 |
| AAM裝置設定檔資料 | 用於Audience Manager連接器診斷。 資料集中的資料不會顯示為批次。 您可以啟用&#x200B;**[!UICONTROL Profile]**&#x200B;切換，將資料直接收錄至Profile。 |
| AAM驗證的設定檔 | 此資料集包含Audience Manager驗證的設定檔。 資料集中的資料不會顯示為批次。 您可以啟用&#x200B;**[!UICONTROL Profile]**&#x200B;切換，將資料直接收錄至Profile。 |
| AAM驗證的設定檔中繼資料 | 用於Audience Manager Connector診斷。 資料集中的資料不會顯示為批次。 您可以啟用&#x200B;**[!UICONTROL Profile]**&#x200B;切換，將資料直接收錄至Profile。 |
| AAM裝置資料回填 | 資料集，以匯入過去的裝置資料。 這包含ECID和Audience Manager中匯總的對應區段實現。 資料集中的資料不會顯示為批次。 您可以啟用&#x200B;**[!UICONTROL Profile]**&#x200B;切換，將資料直接收錄至Profile。 |
| AAM驗證的設定檔回填 | 資料集，以匯入過去的驗證資料。 這包含Audience Manager驗證的個人檔案。 資料集中的資料不會顯示為批次。 您可以啟用&#x200B;**[!UICONTROL Profile]**&#x200B;切換，將資料直接收錄至Profile。 |

### 連線

Adobe Audience Manager在目錄中建立一個連線：Audience Manager連線。 目錄是Adobe Experience Platform中資料位置和世系記錄的系統。 連線是Catalog物件，是Connectors的客戶專屬例項。 有關目錄、連接和連接器的詳細資訊，請參閱[目錄服務概述](../../../catalog/home.md)。

## 平台上的Audience Manager資料預期延遲為何？

| Audience Manager資料 | 延遲性 | 附註 |
| --- | --- | --- |
| 即時資料 | &lt; 35 分鐘. | 從在Audience Manager Edge節點擷取到出現在平台資料湖上的時間。 |
| 描述檔資料 | &lt; 2 天 | 從透過DCS/PCS Edge資料和已登入資料擷取、處理至使用者描述檔，然後顯示在描述檔中的時間。 今天，此資料並未直接登陸Platform Data Lake。 可為Audience Manager Profile資料集啟用描述檔切換，以直接將此資料收錄至描述檔。 |