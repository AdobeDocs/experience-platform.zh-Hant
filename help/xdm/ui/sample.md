---
solution: Experience Platform
title: 在UI中為XDM架構生成示例資料
description: 瞭解如何根據Adobe Experience Platform使用者介面中現有的架構產生範例JSON資料。
topic-legacy: user guide
exl-id: e60eedb2-2245-42cd-b574-43caf9e3426c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# 在UI中為XDM架構產生範例資料

為了將資料收錄至Adobe Experience Platform，資料的格式和結構必須符合現有的體驗資料模型(XDM)架構。 根據特定資料集的架構複雜性，很難判斷資料集在擷取時所需的確切資料形狀。

對於您在Experience PlatformUI中定義的任何結構，您可以產生符合結構的範例JSON物件。 此物件可當成任何資料的範本，這些資料會收錄在採用相關架構的資料集中。

在平台UI中，選擇左側導覽中的&#x200B;**[!UICONTROL Schemas]**。 在&#x200B;**[!UICONTROL Browse]**&#x200B;標籤下，找到要為其生成示例資料的方案。 從清單中選取它，然後右側邊欄會更新，以顯示架構的詳細資訊。 從此處選擇&#x200B;**[!UICONTROL Download sample file]**。

![](../images/ui/sample/sample-data.png)

瀏覽器會下載範例JSON檔案。 現在，您可以使用此檔案作為參考，瞭解在將資料收錄至採用此架構的資料集時，如何建構資料。

## 後續步驟

本指南說明如何從平台UI中的XDM架構產生範例JSON檔案。 要瞭解如何使用方案註冊表API生成示例資料，請參閱[示例資料端點指南](../api/sample-data.md)。

當您準備開始接收資料後，請參閱[將CSV檔案對應至XDM](../../ingestion/tutorials/map-a-csv-file.md)的教學課程，以瞭解如何將平面資料檔案（例如CSV）對應至XDM架構，並將它內嵌至平台。 或者，您可以建立[源連接](../../sources/home.md)，以便從外部源導入資料並將其映射到XDM。

有關UI中[!UICONTROL Schemas]工作區功能的詳細資訊，請參閱[[!UICONTROL Schemas]工作區概述](./overview.md)。
