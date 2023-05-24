---
keywords: Experience Platform；首頁；熱門主題；
title: (Beta)在UI中建立Adobe Workfront源連接
description: 本教程提供了建立Adobe Workfront源連接的步驟，以便使用用戶介面將Workfront資料帶到Adobe Experience Platform。
exl-id: f82e852a-c9d1-4ecc-bc54-2b39d3b4cc1e
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 1%

---

# (Beta)在UI中建立Adobe Workfront源連接

>[!NOTE]
>
>Adobe Workfront的線人是β 查看 [源概述](../../../../home.md#terms-and-conditions) 的子菜單。

本教程提供了建立Adobe Workfront源連接的步驟，以便使用用戶介面將Workfront資料帶到Adobe Experience Platform。

## 快速入門

>[!IMPORTANT]
>
>必須將您配置為Adobe Admin Console的管理員才能訪問Workfront源。

本教程需要對以下Experience Platform組成部分進行有效理解：

* [體驗資料模型(XDM)系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化框架。
* [即時客戶配置檔案](../../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

## 在UI中建立Workfront源連接

在平台UI中，選擇 **[!UICONTROL 源]** 從左側導航 [!UICONTROL 源] 工作區。 的 [!UICONTROL 目錄] 螢幕顯示可用於建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 還可以使用搜索欄縮小顯示的源。

在 **[!UICONTROL Adobe應用程式]** 類別，選擇 **[!UICONTROL Adobe Workfront]** ，然後選擇 **[!UICONTROL 添加資料]**。

![重點介紹了Adobe Workfront來源的來源目錄。](../../../../images/tutorials/create/workfront/catalog.png)

## 選擇資料

的 [!UICONTROL 選擇資料] 的上界。 在此，必須為您的Workfront子域和Datalane提供值。 您的Workfront子域與用於訪問Workfront實例的URL相同，例如 `https://acme.workfront.com/`，而您的datalane表示您要使用的工作環境。

添加子域和資料檔案後，選擇 **[!UICONTROL 下一個]**。

![包含子域和資料欄佔位符值的「選擇資料」頁。](../../../../images/tutorials/create/workfront/select-data.png)

## 提供資料流詳細資訊

資料流詳細資訊步驟允許您為資料流提供名稱和可選說明。 在此步驟中，您還可以訂閱警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請訪問上的教程 [訂閱源UI中的警報](../../alerts.md)。

提供資料流詳細資訊並配置所需警報設定後，選擇 **[!UICONTROL 下一個]**。

![「資料流詳細資料」頁，其中包含有關資料流名稱、說明和警報通知的資訊](../../../../images/tutorials/create/workfront/dataflow-detail.png)

## 請檢閱

的 **[!UICONTROL 審閱]** 步驟，允許您在建立新資料流之前查看它。 詳細資訊按以下類別分組：

* **[!UICONTROL 連接]**:顯示源類型、所選源檔案的相關路徑以及該源檔案中的列數。
* **[!UICONTROL 分配資料集和映射欄位]**:顯示源資料正被攝取到的資料集，包括該資料集所遵循的架構。

查看資料流後，選擇 **[!UICONTROL 完成]** 並為建立資料流留出一些時間。

![概述連接資訊的審閱頁。](../../../../images/tutorials/create/workfront/review.png)

## 附錄

以下各節提供了關於Workfront來源的補充資料。

### Workfront更改事件架構

平台中的Workfront資料被表示為時間序列記錄資料，其中資料中的每一行都有一個時間戳，顯示事件發生的時間以及與該事件相關的屬性。

在設定過程中，將建立名為「來自流的Workfront更改事件」的架構。

| 架構欄位 | 說明 |
| --- | --- |
| `timestamp` | 所選事件發生的時間。 時間戳以GTM時區表示。 |
| `_workfront.objectType` | 對象類型。 可用值可以包括 `project`。 `task`。 `portfolio`，以及其他，具體取決於已更改或建立的對象。 |
| `_workfront.objectID` | 與對象類型對應的ID。 |
| `_workfront.created` | 此值設定為 `1` 的子菜單。 |
| `_workfront.deleted` | 此值設定為 `1` 的子菜單。 |
| `_worfkront.updated` | 此值設定為 `1` 的子菜單。 |
| `_workfront.completed` | 此值設定為 `1` 的子菜單。 |
| `_workfront.parentObjectType` | （可選）與對象父級對應的對象類型。 |
| `_workfront.parentID` | 父對象的ID。 |
| `_workfront.customData` | 事件期間填充的所有自定義表單域和值的映射。 |

>[!IMPORTANT]
>
>只填充已更改或已建立為事件一部分的屬性。 例如，如果僅更改對象的名稱，則將填充的欄位僅為：<ul><li>`timestamp`</li><li>`_workfront.update (=1)`</li><li>`_workfront.objectType`</li><li>`_workfront.objectID`</li><li>`_workfront.objectName`</li></ul>

## 後續步驟

按照本教程，您現在建立了一個資料流，將資料從Workfront帶到Experience Platform。 您現在可以使用服務，如 [查詢服務](../../../../../query-service/home.md) 以對資料進行進一步分析。 有關Workfront的更多資訊，請閱讀 [Workfront概述](../../../../connectors/adobe-applications/workfront.md)。
