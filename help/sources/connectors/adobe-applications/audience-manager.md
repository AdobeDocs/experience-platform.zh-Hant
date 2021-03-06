---
keywords: Experience Platform；首頁；熱門主題；Audience Manager連接器；Audience Manager;audience Manager
solution: Experience Platform
title: Audience Manager源連接器概述
topic-legacy: overview
description: Adobe Audience Manager來源連接器會將Audience Manager中收集的第一方資料串流至Adobe Experience Platform。
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
source-git-commit: d0b6885b6e8606692cfe1173b75c7d3537800a5f
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# Audience Manager連接器

Adobe Audience Manager Data Connector會將在Adobe Audience Manager中收集的第一方資料串流至Adobe Experience Platform。 Audience Manager連接器會將兩類資料內嵌至Platform:

- **即時資料：** 在Audience Manager的資料收集伺服器上即時擷取的資料。 此資料會用於Audience Manager中，以填入規則型特徵，並會在最短的延遲時間內在Platform中顯示。
- **設定檔資料：** Audience Manager使用即時和已上線的資料來衍生客戶設定檔。 這些設定檔可用來填入區段實現的身分圖表和特徵。

Audience Manager連接器會將這些資料類別對應至Experience Data Model(XDM)架構，並將其傳送至Platform。 即時資料會以XDM ExperienceEvent資料傳送，而設定檔資料會以XDM個別設定檔傳送。

如需使用Platform UI建立與Adobe Audience Manager連線的指示，請參閱 [Audience Manager連接器教學課程](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## 什麼是Experience Data Model(XDM)?

XDM是公開記錄的規格，提供標準化的架構，Platform可借此組織客戶體驗資料。

遵循XDM標準，即可統一整合客戶體驗資料，更輕鬆傳送資料和收集資訊。

如需如何在Experience Platform中使用XDM的詳細資訊，請參閱 [XDM系統概觀](../../../xdm/home.md). 若要進一步了解XDM結構（如設定檔和ExperienceEvent）的建構方式，請參閱 [綱要構成基本知識](../../../xdm/schema/composition.md).

## XDM結構範例

以下是在Platform中對應至XDM ExperienceEvent和XDM個別設定檔的Audience Manager結構範例。

### ExperienceEvent — 用於即時資料和已上線資料

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### XDM個別設定檔 — 用於設定檔資料

![](images/aam-profile-xdm-for-profile-data.png)

## 如何將欄位從Adobe Audience Manager對應至XDM?

請參閱 [Audience Manager對應欄位](./mapping/audience-manager.md) 以取得更多資訊。

## 平台上的資料管理

### 資料集

資料集是資料集合的儲存和管理結構，通常為表格，包含結構（欄）和欄位（列），並可由資料連線使用。 Audience Manager資料包含即時資料、入站資料和設定檔資料。 若要找出Audience Manager資料集，請使用UI中的搜尋函式，搭配所提供的每種資料類型命名慣例。

「設定檔」預設會停用Audience Manager資料集，使用者可根據其使用案例啟用或停用資料集。 不建議停用「設定檔」中用於區段成員資格的資料集。

>[!NOTE]
>
>AAM即時是唯一會傳送至 [!DNL Data Lake]. 所有其他Audience Manager資料集會前往 [!DNL Profile]，若為 [!DNL Profile]. 若未針對啟用 [!DNL Profile]，則不會收到任何資料，且會顯示為空白。

| 資料集名稱 | 說明 | 類別 |
| --- | --- | --- |
| AAM即時 | 此資料集包含由Audience ManagerDCS端點上的直接點擊所收集的資料，以及Audience Manager設定檔的身分對應。 將此資料集保持為「設定檔擷取」狀態。 | 體驗事件 |
| AAM即時設定檔更新 | 此資料集可即時鎖定Audience Manager特徵和區段。 其中包含邊緣區域路由、特徵和區段成員資格的資訊。 將此資料集保持為「設定檔擷取」狀態。 資料集中無法以批次形式顯示資料。 您可以啟用 **[!UICONTROL 設定檔]** 切換，將資料直接內嵌至設定檔。 | 記錄 |
| AAM裝置資料 | 以ECID匯總的裝置資料，以及Audience Manager中相應的區段實現。 資料集中無法以批次形式顯示資料。 您可以啟用 **[!UICONTROL 設定檔]** 切換，將資料直接內嵌至設定檔。 | 記錄 |
| AAM裝置設定檔資料 | 用於Audience Manager連接器診斷。 資料集中無法以批次形式顯示資料。 您可以啟用 **[!UICONTROL 設定檔]** 切換，將資料直接內嵌至設定檔。 | 記錄 |
| AAM已驗證的設定檔 | 此資料集包含Audience Manager驗證的設定檔。 資料集中無法以批次形式顯示資料。 您可以啟用 **[!UICONTROL 設定檔]** 切換，將資料直接內嵌至設定檔。 | 記錄 |
| AAM驗證的設定檔中繼資料 | 用於Audience Manager連接器診斷。 資料集中無法以批次形式顯示資料。 您可以啟用 **[!UICONTROL 設定檔]** 切換，將資料直接內嵌至設定檔。 | 記錄 |
| AAM裝置資料回填 | 資料集，匯入過去裝置的資料。 這包含ECID和Audience Manager中匯總的對應區段實現。 資料集中無法以批次形式顯示資料。 您可以啟用 **[!UICONTROL 設定檔]** 切換，將資料直接內嵌至設定檔。 | 記錄 |
| AAM驗證的設定檔回填 | 資料集，匯入過去驗證的資料。 這包含Audience Manager驗證的設定檔。 資料集中無法以批次形式顯示資料。 您可以啟用 **[!UICONTROL 設定檔]** 切換，將資料直接內嵌至設定檔。 | 記錄 |

### 連線

Adobe Audience Manager在目錄中建立一個連線：Audience Manager連線。 目錄是Adobe Experience Platform內用於資料位置和歷程的記錄系統。 連線是目錄物件，是連接器的客戶專屬例項。 請參閱 [目錄服務概述](../../../catalog/home.md) 以取得目錄、連線和連接器的詳細資訊。

## 平台上Audience Manager資料的預期延遲為何？

| Audience Manager資料 | 延遲性 | 附註 |
| --- | --- | --- |
| 即時資料 | &lt; 35 分鐘. | 從在Audience Manager邊緣節點擷取到出現在Platform Data Lake上的時間。 |
| 設定檔資料 | &lt; 2 天 | 從透過DCS/PCS Edge資料和已上線資料擷取、處理至使用者設定檔，然後顯示於設定檔的時間。 目前，此資料無法直接登陸Platform Data Lake。 可為「Audience Manager設定檔」資料集啟用設定檔切換，以直接將此資料內嵌至「設定檔」。 |
