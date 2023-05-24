---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；生成資料集；生成資料集；建立資料集；
solution: Experience Platform
title: 從查詢結果生成輸出資料集
type: Tutorial
description: Adobe Experience Platform查詢服務允許從UI建立資料集。 建立資料集後，可以像Data Lake中的任何其他資料集一樣訪問該資料集，並用於各種使用情形。
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# 從查詢結果生成輸出資料集

[!DNL Query Service] 允許您使用查詢在 [!DNL Data Lake]。 然後，這些資料集可以用作更多查詢或其他服務(如 [!DNL Data Science Workspace]、即時客戶概要資訊，或 [!DNL Analysis Workspace]。

## 從Adobe Experience Platform用戶介面生成資料集

要從Adobe Experience Platform用戶介面(UI)建立資料集，請執行以下步驟：

1. 使用連接的客戶端建立查詢並驗證輸出。 瞭解如何使用 [!DNL Query Editor]，閱讀 [!DNL Query Editor] UI指南 [編寫查詢](./user-guide.md#writing-queries)。

2. 在平台UI中，導航到 **[!UICONTROL 查詢]** 後跟 **[!UICONTROL 模板]** 頁籤，然後選擇已建立的查詢。 有關如何查看在平台UI中為您的組織建立和保存的查詢的詳細資訊，請閱讀 [[!DNL Query Service] 概述](./overview.md#browse)。

3. 在「查詢詳細資訊」面板中，選擇 **[!UICONTROL 輸出資料集]**。

   ![突出顯示了「選擇輸出」資料集的「查詢」工作區模板頁籤。](../images/ui/create-datasets/output-dataset.png)

4. 在顯示的對話框中，輸入以LDAP ID為前置詞的資料集名稱。 資料集名稱不必是唯一的或SQL安全的。 請注意，將根據您在此處建立的資料集名稱生成資料集的表名。

5. 接下來，在 [!UICONTROL 說明] 選擇 **[!UICONTROL 運行查詢]**。

   ![突出顯示了資料集詳細資訊和運行查詢的「輸出資料集」對話框](../images/ui/create-datasets/run-query.png)

6. 查詢運行完成後，導航到 **[!UICONTROL 資料集]** 查看已建立的資料集。 要瞭解有關在平台UI中處理資料集時如何執行常見操作的詳細資訊，請參見 [資料集UI指南](../../catalog/datasets/user-guide.md)。

建立資料集後，可以像中的任何其他資料集一樣訪問該資料集 [!DNL Data Lake] 並用於各種使用案例。

>[!NOTE]
>
>在即時實施中，必須在建立資料集後應用「資料治理」標籤。 要瞭解有關如何將資料使用標籤應用到資料集的詳細資訊，請參見 [資料使用標籤概述](../../data-governance/labels/overview.md)。

## 使用預定義的資料集生成 [!DNL Experience Data Model] 架構

使用SQL語法生成具有預定義的資料集 [!DNL Experience Data Model] (XDM)架構。 有關支援的語法的詳細資訊 [!DNL Query Service]，請閱讀 [SQL語法指南](../sql/syntax.md#create-table-as-select)。

## 輸出資料集

通過此功能建立的資料集使用與SQL陳述式中定義的輸出資料結構匹配的即席模式生成。 某些下游服務需要具有特定XDM架構的資料集。 在編寫查詢之前驗證下游服務的資料格式要求。

## 後續步驟

閱讀此文檔後，您應該瞭解如何使用 [!DNL Query Service] 從平台UI生成資料集。 有關如何訪問、寫入和執行平台UI中查詢的詳細資訊，請參見 [[!DNL Query Service] UI概述](./overview.md)。
