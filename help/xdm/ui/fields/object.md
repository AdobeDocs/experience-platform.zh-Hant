---
keywords: Experience Platform；主題；熱門主題；api;API;XDM;XDM系統；經驗資料模型；資料模型；ui;workspace;object;field;
solution: Experience Platform
title: 在UI中定義對象欄位
description: 瞭解如何在Experience Platform用戶介面中定義對象類型欄位。
exl-id: 5b7b3cf0-7f11-4e15-af87-09127f4423a5
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 在UI中定義對象欄位

Adobe Experience Platform允許您完全自定義自定義體驗資料模型(XDM)類、架構欄位組和資料類型的結構。 為了在自定義XDM資源中組織和嵌套相關欄位，可以定義可包含附加子欄位的對象類型欄位。

當 [定義新欄位](./overview.md#define) 在Adobe Experience Platform用戶介面中，使用 **[!UICONTROL 類型]** 下拉清單，選擇&quot;[!UICONTROL 對象]清單中。

![](../../images/ui/fields/special/object.png)

選擇 **[!UICONTROL 應用]** 將對象添加到架構。 畫布將更新以使用 [!UICONTROL 對象] 應用的資料類型，包括用於編輯子欄位和將子欄位添加到對象的控制項。

![](../../images/ui/fields/special/object-applied.png)

要添加子欄位，請選擇 **加(+)** 表徵圖。 對象下方將出現一個新欄位，其中包含用於在右滑軌中配置子欄位的控制項。

![](../../images/ui/fields/special/object-add-field.png)

配置子欄位並選擇後 **[!UICONTROL 應用]**，可以使用同一進程繼續向對象添加欄位。 您還可以添加子欄位，這些子欄位本身是對象，從而允許您根據需要將欄位嵌套得盡可能深。

構建完對象後，您可能會發現要在不同的類和欄位組中重複使用其結構。 在這種情況下，您可以選擇將對象轉換為資料類型。 請參閱 [將對象轉換為資料類型](../resources/data-types.md#convert) 的子菜單。

## 後續步驟

本指南介紹如何在UI中定義對象欄位。 請參閱 [定義UI中的欄位](./overview.md#special) 瞭解如何在 [!DNL Schema Editor]。
