---
keywords: Experience Platform；首頁；熱門主題；映射csv；映射csv；映射csv；將csv檔案映射到xdm；將csv映射到xdm;ui指南；映射；資料準備；準備資料；
solution: Experience Platform
title: 資料準備概述
description: 本文檔介紹Adobe Experience Platform內的資料準備。
exl-id: 9bef5c3b-368d-4492-bdef-64e67fc25bfd
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 2%

---

# 計算欄位

計算欄位允許根據輸入方案中的屬性建立值。 然後，可以將這些值分配給目標架構中的屬性，並提供名稱和說明，以便更容易地引用。

要建立計算欄位，請選擇 **[!UICONTROL 添加計算欄位]**。

![](./images/calculated-fields/add-calculated-field.png)

的 **[!UICONTROL 建立計算欄位]** 的子菜單。 左對話框包含計算欄位中支援的欄位、函式和運算子。 選擇一個頁籤，開始向表達式編輯器添加函式、欄位或運算子。

![](./images/calculated-fields/create-calculated-field.png)

| 標記 | 說明 |
| --- | ----------- |
| 函數 | 「函式」頁籤列出了可用於轉換資料的函式。 要瞭解有關在計算欄位中可以使用的功能的詳細資訊，請閱讀上的指南 [使用資料準備（映射器）函式](./functions.md)。 |
| 欄位 | 「欄位」頁籤列出源架構中可用的欄位和屬性。 |
| 運算子 | 「運算子」(Operators)頁籤列出了可用於轉換資料的運算子。 |

可以使用中心的表達式編輯器手動添加欄位、函式和運算子。 選擇編輯器以開始建立表達式。

![](./images/calculated-fields/write-calculated-field.png)

選擇 **[!UICONTROL 保存]** 繼續。

映射螢幕將隨新建立的源欄位重新出現。 應用相應的目標欄位並選擇 **[!UICONTROL 完成]** 完成映射。

![](./images/calculated-fields/new-calculated-field.png)
