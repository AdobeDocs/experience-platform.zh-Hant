---
keywords: Experience Platform; home；熱門主題；查詢服務；查詢服務；生成資料集；生成資料集；建立資料集；
solution: Experience Platform
title: 從查詢服務中的結果生成資料集
topic-legacy: queries
type: Tutorial
description: Adobe Experience Platform查詢服務允許從UI建立資料集。 建立資料集後，可像Data Lake中的任何其他資料集一樣加以存取，並用於多種使用案例。
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
translation-type: tm+mt
source-git-commit: d2f19cc97082f75e66cf38e54b5bdb89482930ed
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# 在查詢服務中從結果生成資料集

當使用查詢在[!DNL Data Lake]中生成資料集以用於輸入更多查詢或其他服務（如[!DNL Data Science Workspace]、[!DNL Real-time Customer Profile]或[!DNL Analysis Workspace]）時，可揭示[!DNL Query Service]的真正威力。

[!DNL Query Service] 允許從UI建立資料集。請遵循下列步驟：

1. 使用連接的客戶端編寫查詢並驗證輸出。
2. 登入[!DNL Platform] UI並前往「查詢」。
3. 在清單中尋找查詢，並將滑鼠指標暫留在列上。
4. 選擇「**[!UICONTROL Create Dataset]**」。![影像](../images/ui/create-datasets/output-dataset.png)
5. 輸入資料集名稱，並加上您的LDAP ID(不必是唯一或SQL-safe;系統會根據此處提供的名稱生成「表名」)。
6. 輸入資料集說明並選擇&#x200B;**[!UICONTROL Run Query]**。![影像](../images/ui/create-datasets/run-query.png)
7. 觀看查詢完成，然後前往資料集清單頁面，查看您剛建立的資料集。

建立資料集後，可像[!DNL Data Lake]中的任何其他資料集一樣加以存取，並用於多種使用案例。

>[!NOTE]
>
>在即時實作中，您必須在建立資料集後套用[!DNL Data Governance]標籤。

## 使用預定義的[!DNL Experience Data Model]模式生成資料集

要生成具有預定義[!DNL Experience Data Model](XDM)模式的資料集，必須使用SQL語法。 有關您必須使用的語法的詳細資訊，請閱讀[SQL語法指南](../sql/syntax.md#create-table-as-select)。

## 輸出資料集

通過此功能建立的資料集使用與SQL陳述式中定義的輸出資料結構匹配的臨機模式生成。 某些下游服務需要具有特定[!DNL Experience Data Model](XDM)模式的資料集。 在寫入查詢之前，驗證下游服務的資料格式要求。
