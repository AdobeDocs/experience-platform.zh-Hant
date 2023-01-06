---
keywords: Experience Platform；首頁；熱門主題；對應csv；對應csv檔案；對應csv檔案至xdm；將csv對應至xdm;ui指南；對應程式；資料準備；資料準備；準備資料；
solution: Experience Platform
title: 資料準備概述
description: 本檔案介紹Adobe Experience Platform中的資料準備。
exl-id: 9bef5c3b-368d-4492-bdef-64e67fc25bfd
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 2%

---

# 計算欄位

計算欄位允許根據輸入架構中的屬性建立值。 然後，可將這些值指派給目標架構中的屬性，並提供名稱和說明，以便更輕鬆參考。

若要建立計算欄位，請選取 **[!UICONTROL 新增計算欄位]**.

![](./images/calculated-fields/add-calculated-field.png)

此 **[!UICONTROL 建立計算欄位]** 框。 左側對話方塊包含計算欄位中支援的欄位、函式和運算子。 選取其中一個索引標籤，以開始將函式、欄位或運算子新增至運算式編輯器。

![](./images/calculated-fields/create-calculated-field.png)

| 標記 | 說明 |
| --- | ----------- |
| 函數 | 函式索引標籤列出可用於轉換資料的函式。 若要進一步了解可在計算欄位中使用的函式，請參閱 [使用資料準備（映射器）函式](./functions.md). |
| 欄位 | 「欄位」頁簽列出源架構中可用的欄位和屬性。 |
| 運算子 | 運算子索引標籤會列出可用於轉換資料的運算子。 |

您可以使用中心的運算式編輯器手動新增欄位、函式和運算子。 選取要開始建立運算式的編輯器。

![](./images/calculated-fields/write-calculated-field.png)

選擇 **[!UICONTROL 儲存]** 繼續。

映射螢幕將隨新建立的源欄位重新顯示。 應用相應的目標欄位並選擇 **[!UICONTROL 完成]** 填寫對應。

![](./images/calculated-fields/new-calculated-field.png)
