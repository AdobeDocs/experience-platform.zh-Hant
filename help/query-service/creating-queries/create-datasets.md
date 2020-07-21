---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 從查詢結果生成資料集
topic: queries
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---


# 從查詢結果生成資料集

當查詢用 [!DNL Query Service] 於在中生成資料集，以用於輸入更多查詢或在其他服務(如 [!DNL Data Lake] 、 [!DNL Data Science Workspace]或)中時，可顯示其真 [!DNL Real-time Customer Profile]正威力 [!DNL Analysis Workspace]。

[!DNL Query Service] 允許從UI建立資料集。 請遵循下列步驟：

1. 使用連接的客戶端編寫查詢並驗證輸出。
2. 登入 [!DNL Platform] UI並前往查詢。
3. 在清單中尋找查詢，並將滑鼠指標暫留在列上。
4. 按一下 **[!UICONTROL 建立資料集]**。 ![影像](../images/queries/create-datasets/click-create-dataset.png)
5. 輸入資料集名稱，並加上您的LDAP ID(不必是唯一或SQL-safe; 系統會根據此處提供的名稱生成「表名」)。
6. 輸入資料集說明，然後按一下「 **[!UICONTROL 執行查詢」]**。![影像](../images/queries/create-datasets/run-query.png)
7. 觀看查詢完成，然後前往資料集清單頁面，查看您剛建立的資料集。

建立資料集後，可像在中的任何其他資料集一樣加以存取， [!DNL Data Lake] 並用於多種使用案例。

>[!NOTE]
>
>在即時實作中，您必須在建立資 [!DNL Data Governance] 料集後套用標籤。

## 使用預定義的模式生成數 [!DNL Experience Data Model] 據集

為了生成具有預定義(XDM)模 [!DNL Experience Data Model] 式的資料集，您必須使用SQL語法。 有關您必須使用哪些語法的詳細資訊，請閱讀 [SQL語法指南](../sql/syntax.md#create-table-as-select)。

## 輸出資料集

通過此功能建立的資料集使用與SQL陳述式中定義的輸出資料結構匹配的臨機模式生成。 某些下游服務需要具有特定(XDM) [!DNL Experience Data Model] 模式的資料集。 在寫入查詢之前，驗證下游服務的資料格式要求。