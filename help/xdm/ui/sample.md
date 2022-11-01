---
solution: Experience Platform
title: 在UI中產生XDM結構的範例資料
description: 了解如何根據Adobe Experience Platform使用者介面中的現有結構，產生範例JSON資料。
topic-legacy: user guide
exl-id: e60eedb2-2245-42cd-b574-43caf9e3426c
source-git-commit: d380b4d2a75efb1c34010a30c619649a7b99643c
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# 在UI中產生XDM結構的範例資料

若要將資料內嵌至Adobe Experience Platform，資料的格式和結構必須符合現有的Experience Data Model(XDM)結構。 根據特定資料集的結構複雜度，很難判斷資料集擷取時所需資料的確切形狀。

對於您在Experience PlatformUI中定義的任何結構，您可以產生符合結構的範例JSON物件。 此物件可做為範本，內嵌至採用相關結構的資料集中的任何資料。

在平台UI中，選取 **[!UICONTROL 結構]** 的下一頁。 在 **[!UICONTROL 瀏覽]** 頁簽，找到要為其生成示例資料的架構。 從清單中選取，右側邊欄會更新，顯示架構的詳細資訊。 從此處，選擇 **[!UICONTROL 下載範例檔案]**.

![](../images/ui/sample/sample-data.png)

瀏覽器會下載範例JSON檔案。 現在，您可以使用此檔案作為參考，以了解在採用此結構的資料集中擷取資料時，如何建構資料。

## 後續步驟

本指南說明如何從Platform UI的XDM結構產生範例JSON檔案。 若要了解如何使用Schema Registry API產生範例資料，請參閱 [範例data端點指南](../api/sample-data.md).

準備好開始擷取資料後，請參閱 [將CSV檔案對應至XDM](../../ingestion/tutorials/map-csv/overview.md) 了解如何將一般資料檔案（例如CSV）對應至XDM結構，並內嵌至Platform。 或者，您可以建立 [源連接](../../sources/home.md) 將資料從外部來源匯入，並對應至XDM。

如需功能的詳細資訊，請參閱 [!UICONTROL 結構] 工作區，請參閱 [[!UICONTROL 結構] 工作區概述](./overview.md).
