---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；產生資料集；產生資料集；建立資料集；
solution: Experience Platform
title: 從查詢結果產生輸出資料集
type: Tutorial
description: Adobe Experience Platform查詢服務可讓您從UI建立資料集。 建立資料集後，即可像資料湖中的其他資料集一樣存取該資料集，並用於各種使用案例。
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
source-git-commit: 59d2d74b2d77f3bbaca381af908de5295af24e5b
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---

# 從查詢結果產生輸出資料集

[!DNL Query Service] 可讓您使用查詢來產生 [!DNL Data Lake]. 然後，這些資料集就可以用作更多查詢或其他服務(例如 [!DNL Data Science Workspace]、即時客戶個人檔案，或 [!DNL Analysis Workspace].

## 從Adobe Experience Platform使用者介面產生資料集

若要從Adobe Experience Platform使用者介面(UI)建立資料集，請執行下列步驟：

1. 使用連線的使用者端建立查詢並驗證輸出。 若要瞭解如何使用撰寫查詢 [!DNL Query Editor]，閱讀 [!DNL Query Editor] UI指南 [在寫入查詢時](./user-guide.md#writing-queries).

2. 在Platform UI中，瀏覽至 **[!UICONTROL 查詢]** 後面接著 **[!UICONTROL 範本]** 標籤並選取您已建立的查詢。 如需如何在Platform UI中檢視針對貴組織建立和儲存的查詢的詳細資訊，請參閱 [[!DNL Query Service] 概述](./overview.md#browse).

3. 在「查詢詳細資訊」面板中，選取 **[!UICONTROL 以CTAS身分執行]**.

   ![查詢工作區 [!UICONTROL 範本] 使用Select標籤 [!UICONTROL 以CTAS身分執行] 反白顯示。](../images/ui/create-datasets/run-as-ctas.png)

4. 在出現的對話方塊中，輸入資料集名稱，並在其前面加上LDAP ID。 資料集名稱不須為唯一或SQL安全。 請注意，將會根據您在此建立的資料集名稱產生資料集的表格名稱。

5. 接下來，在下列欄位中輸入資料集的說明： [!UICONTROL 說明] 欄位並選取 **[!UICONTROL 以CTAS身分執行]**.

   ![包含資料集詳細資訊和的「輸出資料集」對話方塊 [!UICONTROL 以CTAS身分執行] 反白顯示](../images/ui/create-datasets/run-query.png)

6. 查詢執行完成後，切換作業選項至 **[!UICONTROL 資料集]** 以檢視您建立的資料集。 若要進一步瞭解如何在Platform UI中使用資料集時執行常見動作，請參閱 [資料集UI指南](../../catalog/datasets/user-guide.md).

建立資料集後，即可像中的任何其他資料集一樣加以存取。 [!DNL Data Lake] 並用於各種使用案例。

>[!NOTE]
>
>在即時實作中，您必須在建立資料集後套用資料控管標籤。 要瞭解更多有關如何將資料使用標籤套用至資料集的資訊，請參閱 [資料使用標籤總覽](../../data-governance/labels/overview.md).

## 產生具有預先定義的資料集 [!DNL Experience Data Model] 綱要

使用SQL語法產生有預先定義的資料集 [!DNL Experience Data Model] (XDM)結構描述。 如需所支援語法的詳細資訊 [!DNL Query Service]，請閱讀 [SQL語法指南](../sql/syntax.md#create-table-as-select).

## 輸出資料集

透過此功能建立的資料集是以符合輸出資料結構的臨時結構描述所產生，如在SQL陳述式中所定義。 某些下游服務需要具有特定XDM結構描述的資料集。 在寫入查詢之前，請先驗證下游服務的資料格式需求。

## 後續步驟

閱讀本檔案後，您現在應會瞭解如何使用 [!DNL Query Service] 以從Platform UI產生資料集。 如需如何在Platform UI中存取、寫入及執行查詢的詳細資訊，請參閱 [[!DNL Query Service] UI總覽](./overview.md).
