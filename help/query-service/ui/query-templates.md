---
title: 查詢範本
description: 查詢模板是可重複使用的保存的SQL查詢，可由其他用戶重複使用，以節省時間和精力。 可使用查詢編輯器或查詢服務API來建立這些資料集，並可用於所有Experience Platform資料集。
exl-id: e74d058f-bb89-45ed-83cc-2e3a33401270
source-git-commit: d5d69134627b1a162691bda95732d989bd6e3469
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---

# 查詢範本

Adobe Experience Platform Query Service可讓您以查詢範本的形式儲存及重複使用SQL程式碼。 範本可避免重複通常執行的工作，以節省人力。 您可以在組織內共用模板，並輕鬆更改查詢值，而無需訪問或了解基礎SQL。

本文檔提供在查詢服務中建立查詢模板所需的資訊。

## 先決條件

您必須擁有 [!UICONTROL 管理查詢] 已啟用存取查詢編輯器和在Platform UI中檢視查詢控制面板的權限。 權限會透過Adobe啟用 [Admin Console](https://adminconsole.adobe.com/). 如果您沒有啟用此權限的管理員權限，請與貴組織的管理員聯繫。 請參閱存取控制檔案，以取得 [透過Admin Console新增權限的完整指示](../../access-control/home.md).

## 建立查詢範本

您可以透過兩種方法建立查詢範本，方法是向查詢服務API提出POST要求 `query-templates` 端點，或透過查詢編輯器撰寫、命名和儲存查詢。

### 使用查詢編輯器來編寫查詢並將其另存為模板

如需如何使用查詢編輯器以 [寫入](./user-guide.md#query-authoring) 和 [保存查詢](./user-guide.md#saving-queries). 在您命名並保存查詢後，該查詢即可在 [!UICONTROL 範本] 標籤。

## 瀏覽查詢模板 {#browse}

從Platform UI的「查詢」工作區中，選取 **[!UICONTROL 範本]** 顯示可用的已保存查詢的清單。

![查詢工作區，「模板」(Templates)頁簽突出顯示。](../images/ui/query-templates/query-templates.png)

要查找相關模板資訊，請從可用清單中選擇任何查詢模板以開啟「詳細資訊」面板。

![查詢工作區中的「詳細資訊」面板會反白顯示查詢ID。](../images/ui/query-templates/details-panel.png)

從「詳細資訊」面板，您可以執行四個不同的動作：

* 選擇 **[!UICONTROL 輸出資料集]** 編輯所選模板的輸出資料集。
* 選擇 **[!UICONTROL 檢視排程]** 導覽至 [!UICONTROL 排程] 標籤。 此視圖包含與查詢關聯的任何計畫資訊。
* 選擇 **[!UICONTROL 刪除查詢]** 刪除範本。
* 選擇模板名稱以導航到查詢編輯器，在該編輯器中預先填充SQL進行編輯。

### 使用查詢服務API建立範本

如需相關指示，請參閱本檔案。 [如何建立查詢範本](../api/query-templates.md#create-a-query-template) 使用查詢服務API。 新建立的查詢範本的詳細資訊包含在回應內文中。

>[!NOTE]
>
>使用API建立的範本也會顯示在「平台UI查詢服務範本」標籤中。

## 後續步驟

閱讀本檔案後，您現在更了解如何在Query Service中建立查詢範本。 請參閱 [UI概述](./overview.md)，或 [查詢服務API指南](../api/getting-started.md) 以進一步了解Query Service功能。

請參閱 [排程查詢端點指南](../api/scheduled-queries.md) 了解如何使用API排程查詢，或 [查詢編輯器指南](./user-guide.md#scheduled-queries) （適用於UI）。
