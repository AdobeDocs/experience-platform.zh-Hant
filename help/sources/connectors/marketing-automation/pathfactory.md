---
title: PathFactory Source概觀
description: 瞭解如何使用API或使用者介面將PathFactory連線至Adobe Experience Platform。
last-substantial-update: 2024-04-30T00:00:00Z
exl-id: befb73c4-fd6a-4512-9124-d23a1c27e0e0
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 3%

---

# [!DNL PathFactory]

[[!DNL PathFactory]](https://www.pathfactory.com/)提供雲端型平台，可協助企業管理內容歷程，並透過智慧型內容深入分析促進參與。 本指南詳細說明如何運用PathFactory的聯結器將資料從PathFactory整合到Experience Platform中，以最佳化資料擷取。

您可以使用三個主要來源從[[!DNL PathFactory]](https://www.pathfactory.com/)內嵌資料：

* **[!DNL Visitors]**：將客戶和連絡資料擷取為記錄，以便更清楚瞭解您的對象。
* **[!DNL Sessions]**：追蹤您平台上個別使用者工作階段活動的時間序列事件。
* **[!DNL Page Views]**：提供正在檢視哪些頁面之深入分析的時間序列事件，可協助您分析內容效能。

請閱讀以下檔案，瞭解如何設定[!DNL PathFactory]來源帳戶的資訊。

## IP位址允許清單 {#ip-allow-list}

將來源連線至Experience Platform之前，您必須先將區域特定的IP位址新增至允許清單。 如需詳細資訊，請參閱[允許清單IP位址以連線至Experience Platform](../../ip-address-allow-list.md)的指南以瞭解詳細資訊。

## 先決條件 {#prerequisites}

開始將[[!DNL PathFactory]](https://www.pathfactory.com/)聯結器與Experience Platform整合之前，請確定您符合下列必要條件：

* **一個[PathFactory帳戶]**。
   * 如果您還沒有有效的帳戶，請連絡[[!DNL PathFactory]](https://www.pathfactory.com/portal/company/contactus.shtml)。
* **任何**&#x200B;產品的使用中訂閱[!DNL PathFactory]。
* **使用者名稱、密碼和網域**。
   * 需要這些認證才能存取您的[!DNL PathFactory]帳戶及其資料。
* **存取Token**&#x200B;和&#x200B;**API端點**。
   * 這些是與[!DNL PathFactory] API連線所需。

### 如何取得憑證和存取權杖 {#gather-credentials}

若要將[!DNL PathFactory]連線至Experience Platform，您必須提供下列認證：

| 認證 | 說明 | 端點 |
| --- | --- | --- |
| 使用者名稱 | 您的[!DNL PathFactory]帳戶使用者名稱。 | 不適用 |
| 密碼 | 您的[!DNL PathFactory]帳戶密碼。 | 不適用 |
| 網域 | 與您的[!DNL PathFactory]帳戶關聯的網域。 | 不適用 |
| 存取權杖 | 用於API驗證的唯一Token。 | 不適用 |
| 訪客端點 | 訪客資料的API端點。 | `/api/public/v3/data_lake_apis/visitors.json` |
| 工作階段端點 | 工作階段資料的API端點。 | `/api/public/v3/data_lake_apis/sessions.json` |
| 頁面檢視端點 | 頁面檢視資料的API端點。 | `/api/public/v3/data_lake_apis/page_views.json` |

如需有關如何取得您的使用者名稱、密碼、網域和存取Token的詳細指示，請造訪[[!DNL PathFactory] 支援中心](https://support.pathfactory.com/categories/adobe/)。 此資源提供全面性的認證擷取與管理指南。

### 在Experience Platform上設定許可權

您必須同時為帳戶啟用&#x200B;**[!UICONTROL View Sources]**&#x200B;和&#x200B;**[!UICONTROL Manage Sources]**&#x200B;許可權，才能將您的[!DNL PathFactory]帳戶連線至Experience Platform。 請聯絡您的產品管理員以取得必要許可權。 如需詳細資訊，請閱讀[存取控制UI指南](../../../access-control/ui/overview.md)。

## 將[!DNL PathFactory]連線至Experience Platform {#pathfactory-connect}

以下檔案提供如何使用API或使用者介面將[!DNL PathFactory]連線至Experience Platform的資訊：

* [使用API建立來源連線和資料流，將 [!DNL PathFactory] 資料匯入Experience Platform](../../tutorials/api/create/marketing-automation/pathfactory.md)。
* [使用UI [!DNL PathFactory] 將您的](../../tutorials/ui/create/marketing-automation/pathfactory.md)帳戶連線至Experience Platform。
* [使用UI](../../tutorials/ui/dataflow/marketing-automation.md)為來源連線建立資料流。
