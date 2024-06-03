---
solution: Experience Platform
title: 在UI中產生XDM結構描述的範例資料
description: 瞭解如何根據Adobe Experience Platform使用者介面中的現有結構描述產生範例JSON資料。
exl-id: e60eedb2-2245-42cd-b574-43caf9e3426c
source-git-commit: 19a9341a9f53559fe3f619b2f157015e53b25b64
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 1%

---

# 在UI中產生XDM結構描述的範例資料 {#generate-sample-data-for-an-xdm-schema}

>[!CONTEXTUALHELP]
>id="platform_xdm_downloadsamplefile"
>title="下載範例檔案"
>abstract="產生符合您所選結構描述結構的範例JSON物件。 此物件可作為範本，確保您的資料格式正確，以便擷取至採用該結構的資料集。 您的瀏覽器將下載範例JSON檔案。"

若要將資料內嵌至Adobe Experience Platform，資料的格式和結構必須符合現有的Experience Data Model (XDM)結構描述。 根據特定資料集的結構描述複雜性，可能很難判斷資料集在擷取時預期的資料確切形狀。

對於您在Experience PlatformUI中定義的任何結構描述，您可以產生符合結構描述結構的範例JSON物件。 此物件可當作任何資料之範本，這些資料會擷取到採用特定結構描述的資料集中。

在Platform UI中選取 **[!UICONTROL 方案]** ，位於左側導覽器中。 在 **[!UICONTROL 瀏覽]** 索引標籤中，找到您要為其產生範例資料的結構描述。 從清單中選取該架構，右邊欄會更新以顯示有關架構的詳細資訊。 從這裡，選擇 **[!UICONTROL 下載範例檔案]**.

![在選取了結構描述的「結構描述」工作區的「瀏覽」索引標籤中，下載反白顯示的範例檔案。](../images/ui/sample/sample-data.png)

瀏覽器會下載範例JSON檔案。 您現在可以使用此檔案作為參考，瞭解在擷取至採用此結構的資料集時，如何建構您的資料。

## 後續步驟

本指南說明如何從Platform UI的XDM結構描述產生範例JSON檔案。 若要瞭解如何使用結構描述登入API產生範例資料，請參閱 [範例資料端點指南](../api/sample-data.md).

在您準備好開始內嵌資料後，請參閱上的教學課程 [將CSV檔案對應至XDM](../../ingestion/tutorials/map-csv/overview.md) 瞭解如何將純資料檔案（例如CSV）對應至XDM結構描述，並將其擷取至Platform。 或者，您可以建立 [來源連線](../../sources/home.md) 從外部來源匯入資料，並將其對應至XDM。

如需功能的詳細資訊， [!UICONTROL 方案] 工作區在UI中，請參閱 [[!UICONTROL 方案] 工作區概觀](./overview.md).
