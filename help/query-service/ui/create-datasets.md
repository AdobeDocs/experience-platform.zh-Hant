---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；產生資料集；產生資料集；建立資料集；
solution: Experience Platform
title: 從查詢結果生成輸出資料集
type: Tutorial
description: Adobe Experience Platform Query Service可從UI建立資料集。 建立資料集後，您就可以像「資料湖」中的其他資料集一樣存取該資料集，並用於各種使用案例。
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# 從查詢結果生成輸出資料集

[!DNL Query Service] 可讓您使用查詢來產生 [!DNL Data Lake]. 然後，這些資料集便可用作更多查詢或其他服務(例如 [!DNL Data Science Workspace]、即時客戶個人檔案，或 [!DNL Analysis Workspace].

## 從Adobe Experience Platform使用者介面產生資料集

若要從Adobe Experience Platform使用者介面(UI)建立資料集，請遵循下列步驟：

1. 使用連接的客戶端建立查詢並驗證輸出。 了解如何使用 [!DNL Query Editor]，請閱讀 [!DNL Query Editor] UI指南 [寫入查詢](./user-guide.md#writing-queries).

2. 在Platform UI中，導覽至 **[!UICONTROL 查詢]** 後面 **[!UICONTROL 範本]** 頁簽，然後選擇已建立的查詢。 如需如何在Platform UI中檢視針對貴組織建立和儲存的查詢的詳細資訊，請參閱 [[!DNL Query Service] 概述](./overview.md#browse).

3. 在「查詢詳細資訊」面板中，選擇 **[!UICONTROL 輸出資料集]**.

   ![突出顯示「選擇輸出」資料集的「查詢工作區模板」頁簽。](../images/ui/create-datasets/output-dataset.png)

4. 在顯示的對話方塊中，輸入以LDAP ID為前置詞的資料集名稱。 資料集名稱不必是唯一的或SQL安全的。 請注意，資料集的表格名稱會根據您在此建立的資料集名稱產生。

5. 接下來，在 [!UICONTROL 說明] 欄位和選取 **[!UICONTROL 運行查詢]**.

   ![「輸出資料集」對話方塊中會反白顯示資料集詳細資料和執行查詢](../images/ui/create-datasets/run-query.png)

6. 查詢執行完成後，請導覽至 **[!UICONTROL 資料集]** 檢視您建立的資料集。 若要進一步了解在Platform UI內使用資料集時，如何執行常見動作，請參閱 [資料集UI指南](../../catalog/datasets/user-guide.md).

建立資料集後，您就可以像 [!DNL Data Lake] 並用於各種使用案例。

>[!NOTE]
>
>在即時實作中，您必須在建立資料集後套用資料控管標籤。 若要進一步了解如何將資料使用量標籤套用至資料集，請參閱 [資料使用量標籤概觀](../../data-governance/labels/overview.md).

## 使用預先定義的產生資料集 [!DNL Experience Data Model] 綱要

使用SQL語法，以預先定義的方式產生資料集 [!DNL Experience Data Model] (XDM)結構。 如需支援語法的詳細資訊，請參閱 [!DNL Query Service]，請閱讀 [SQL語法指南](../sql/syntax.md#create-table-as-select).

## 輸出資料集

通過此功能建立的資料集使用與SQL陳述式中定義的輸出資料結構相匹配的臨時架構生成。 有些下游服務需要具有特定XDM結構的資料集。 在寫入查詢之前，驗證下游服務的資料格式要求。

## 後續步驟

閱讀本檔案後，您現在應了解如何使用 [!DNL Query Service] 從Platform UI產生資料集。 如需如何在Platform UI中存取、寫入及執行查詢的詳細資訊，請參閱 [[!DNL Query Service] UI概述](./overview.md).
