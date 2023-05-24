---
solution: Experience Platform
title: 在UI中為XDM架構生成示例資料
description: 瞭解如何根據Adobe Experience Platform用戶介面中的現有架構生成示例JSON資料。
exl-id: e60eedb2-2245-42cd-b574-43caf9e3426c
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# 在UI中為XDM架構生成示例資料

為了將資料導入Adobe Experience Platform，資料的格式和結構必須符合現有的經驗資料模型(XDM)架構。 根據特定資料集的模式的複雜性，很難確定資料集在攝取時期望的資料的確切形狀。

對於在Experience PlatformUI中定義的任何架構，可以生成符合架構結構的示例JSON對象。 此對象可以作為任何資料的模板，這些資料被攝取到使用有關架構的資料集中。

在平台UI中，選擇 **[!UICONTROL 架構]** 的子菜單。 在 **[!UICONTROL 瀏覽]** 頁籤，找到要為其生成示例資料的方案。 從清單中選擇它，然後右側的軌道更新以顯示有關架構的詳細資訊。 從此處，選擇 **[!UICONTROL 下載示例檔案]**。

![](../images/ui/sample/sample-data.png)

瀏覽器下載了示例JSON檔案。 現在，您可以使用此檔案作為在插入使用此架構的資料集時如何構造資料的參考。

## 後續步驟

本指南介紹了如何從平台UI中的XDM架構生成示例JSON檔案。 要瞭解如何使用架構註冊表API生成示例資料，請參見 [示例資料端點指南](../api/sample-data.md)。

準備好開始接收資料後，請參見上的教程 [將CSV檔案映射到XDM](../../ingestion/tutorials/map-csv/overview.md) 瞭解如何將平面資料檔案（如CSV）映射到XDM架構並將其導入平台。 或者，可以建立 [源連接](../../sources/home.md) 將資料從外部源導入並映射到XDM。

有關功能的詳細資訊 [!UICONTROL 架構] 工作區，請參閱 [[!UICONTROL 架構] 工作區概述](./overview.md)。
