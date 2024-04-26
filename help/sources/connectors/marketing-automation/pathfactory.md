---
title: PathFactory來源概觀
description: 瞭解如何使用API或使用者介面將PathFactory連線至Adobe Experience Platform。
last-substantial-update: 2024-04-30T00:00:00Z
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 18f6c253aec6815cf84272cbce340a9aa7ed8ab9
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 2%

---

# [!DNL PathFactory]

>[!NOTE]
>
>此 [!DNL PathFactory] 來源為測試版。 請閱讀 [來源概觀](../../home.md#terms-and-conditions) 以取得有關使用測試版標籤來源的詳細資訊。

[[!DNL PathFactory]](https://www.pathfactory.com/) 提供雲端型平台，協助企業管理內容歷程，並透過智慧型內容見解推動參與。 本指南詳細說明如何運用PathFactory的聯結器將資料從PathFactory整合到Experience Platform中，以最佳化資料擷取。

您可以從以下位置擷取資料： [[!DNL PathFactory]](https://www.pathfactory.com/) 使用三個主要來源：

* **[!DNL Visitors]**：將客戶和聯絡資料擷取為記錄，以便更清楚瞭解您的對象。
* **[!DNL Sessions]**：追蹤您平台上個別使用者工作階段活動的時間序列事件。
* **[!DNL Page Views]**：提供正在檢視哪些頁面之深入分析的時間序列事件，協助您分析內容效能。

請閱讀以下檔案，瞭解如何設定 [!DNL PathFactory] 來源帳戶。

## IP位址允許清單 {#ip-allow-list}

使用來源聯結器之前，可能需要將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

## 先決條件 {#prerequisites}

開始整合之前 [[!DNL PathFactory]](https://www.pathfactory.com/) 具有Experience Platform的聯結器，請確定您符合下列先決條件：

* **A [PathFactory帳戶]**.
   * 連絡人 [[!DNL PathFactory]](https://www.pathfactory.com/portal/company/contactus.shtml) 如果您還沒有有效的帳戶。
* **有效的訂閱** 至任何 [!DNL PathFactory] 產品。
* **使用者名稱、密碼和網域**.
   * 需要這些認證才能存取您的 [!DNL PathFactory] 帳戶及其資料。
* **存取權杖** 和 **api端點**.
   * 這些是連線所必需的 [!DNL PathFactory] API。

### 如何取得憑證和存取權杖 {#gather-credentials}

若要連線 [!DNL PathFactory] 若要Experience Platform，您必須提供下列認證：

| 認證 | 說明 | 端點 |
| --- | --- | --- |
| 使用者名稱 | 您的 [!DNL PathFactory] 帳戶使用者名稱。 | 不適用 |
| 密碼 | 您的 [!DNL PathFactory] 帳戶密碼。 | 不適用 |
| 網域 | 與您的關聯的網域 [!DNL PathFactory] 帳戶。 | 不適用 |
| 存取權杖 | 用於API驗證的唯一Token。 | 不適用 |
| 訪客端點 | 訪客資料的API端點。 | `/api/public/v3/data_lake_apis/visitors.json` |
| 工作階段端點 | 工作階段資料的API端點。 | `/api/public/v3/data_lake_apis/sessions.json` |
| 頁面檢視端點 | 頁面檢視資料的API端點。 | `/api/public/v3/data_lake_apis/page_views.json` |

如需有關如何取得您的使用者名稱、密碼、網域和存取Token的詳細說明，請造訪 [[!DNL PathFactory] 支援中心](https://support.pathfactory.com/categories/adobe/). 此資源提供全面性的認證擷取與管理指南。

### 設定Experience Platform的許可權

您必須同時擁有兩者 **[!UICONTROL 檢視來源]** 和 **[!UICONTROL 管理來源]** 為您的帳戶啟用的許可權以連線您的 [!DNL PathFactory] 要Experience Platform的帳戶。 請聯絡您的產品管理員以取得必要許可權。 如需詳細資訊，請閱讀 [存取控制UI指南](../../../access-control/ui/overview.md).

## 連線 [!DNL PathFactory] 至平台 {#pathfactory-connect}

以下檔案提供有關如何連線的資訊 [!DNL PathFactory] 使用API或使用者介面至Platform：

* [建立來源連線和資料流以帶來 [!DNL PathFactory] 使用API將資料匯入Platform](../../tutorials/api/create/marketing-automation/pathfactory.md).
* [連線您的 [!DNL PathFactory] 要使用UIExperience Platform的帳戶](../../tutorials/ui/create/marketing-automation/pathfactory.md).
* [使用UI為來源連線建立資料流](../../tutorials/ui/dataflow/marketing-automation.md).
