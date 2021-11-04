---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；產生資料集；產生資料集；建立資料集；
solution: Experience Platform
title: 從查詢服務中的結果生成資料集
topic-legacy: queries
type: Tutorial
description: Adobe Experience Platform Query Service可從UI建立資料集。 建立資料集後，您就可以像「資料湖」中的其他資料集一樣存取該資料集，並用於各種使用案例。
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# 在Query Service中從結果產生資料集

真正的力量 [!DNL Query Service] 查詢用來產生資料集時會顯示 [!DNL Data Lake] 將用作輸入到更多查詢或其它服務(如 [!DNL Data Science Workspace], [!DNL Real-time Customer Profile]，或 [!DNL Analysis Workspace].

[!DNL Query Service] 可從UI建立資料集。 請依照下列步驟操作：

1. 使用連接的客戶端編寫查詢並驗證輸出。
2. 登入 [!DNL Platform] UI並前往「查詢」。
3. 在清單中尋找查詢，並將滑鼠指標暫留在該列上。
4. 選擇 **[!UICONTROL 建立資料集]**. ![影像](../images/ui/create-datasets/output-dataset.png)
5. 輸入資料集名稱，並在前面加上您的LDAP ID(不必唯一或SQL安全；系統會根據此處提供的名稱產生「表格名稱」)。
6. 輸入資料集說明並選取 **[!UICONTROL 運行查詢]**.![影像](../images/ui/create-datasets/run-query.png)
7. 觀看查詢完成，然後前往資料集清單頁面查看您剛建立的資料集。

建立資料集後，您就可以像 [!DNL Data Lake] 並用於各種使用案例。

>[!NOTE]
>
>在即時實作中，您必須在建立資料集後套用資料控管標籤。

## 使用預先定義的產生資料集 [!DNL Experience Data Model] 綱要

若要產生預先定義的資料集 [!DNL Experience Data Model] (XDM)架構，則必須使用SQL語法。 如需您必須使用哪種語法的詳細資訊，請參閱 [SQL語法指南](../sql/syntax.md#create-table-as-select).

## 輸出資料集

通過此功能建立的資料集使用與SQL陳述式中定義的輸出資料結構相匹配的臨時架構生成。 有些下游服務需要特定的資料集 [!DNL Experience Data Model] (XDM)結構。 在寫入查詢之前，驗證下游服務的資料格式要求。
