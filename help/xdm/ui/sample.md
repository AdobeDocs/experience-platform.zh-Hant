---
solution: Experience Platform
title: 在使用者介面中產生 XDM 架構的範例資料
description: 學習如何在 Adobe Experience Platform 使用者介面中，根據現有結構產生範例 JSON 資料。
exl-id: e60eedb2-2245-42cd-b574-43caf9e3426c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 14%

---

# 在 UI 中為 XDM 結構描述產生樣本資料 {#generate-sample-data-for-an-xdm-schema}

>[!CONTEXTUALHELP]
>id="platform_xdm_downloadsamplefile"
>title="下載範例檔案"
>abstract="產生符合您所選結構描述之結構的範例 JSON 物件。此物件可以充當範本，以確保您的資料格式正確，以便擷取到採用該結構描述的資料集中。您的瀏覽器將會下載範例 JSON 檔案。"

為了將資料匯入 Adobe Experience Platform，資料的格式與結構必須符合現有的體驗資料模型（XDM）架構。 根據特定資料集結構的複雜度，很難判斷資料集在擷取時預期的資料形狀。

對於你在 Experience Platform UI 中定義的任何 schema，都可以產生一個符合結構的範例 JSON 物件。 此物件可作為任何資料匯入使用該結構資料集的資料範本。

在體驗平台介面中，選擇 **[!UICONTROL Schemas]** 左側導覽。 在分 **[!UICONTROL Browse]** 頁下方，找到你想產生範例資料的結構。 從清單中選擇它，並選擇正確的軌道更新以顯示該結構的詳細資訊。 從這裡，選擇 **[!UICONTROL Download sample file]**。

![在 Schemas 工作區的瀏覽分頁中，選取結構並標示下載範例檔案。](../images/ui/sample/sample-data.png)

瀏覽器會下載一個範本 JSON 檔案。 你現在可以用這個檔案作為參考，了解如何在導入使用此結構的資料集時，如何結構化你的資料。

## 後續步驟

本指南說明了如何在 Experience Platform 介面中從 XDM 架構產生範例 JSON 檔案。 欲了解如何使用 Schema Registry API 產生範例資料，請參閱 [範例資料端點指南](../api/sample-data.md)。

當你準備好開始匯入資料時，可以參考教學 [，了解如何將 CSV 檔案映射到 XDM](../../ingestion/tutorials/map-csv/overview.md) ，學習如何將平面資料檔（例如 CSV）映射到 XDM 架構，並匯入 Experience Platform。 或者，你也可以建立 [來源連線](../../sources/home.md) ，將外部來源的資料帶入並映射到 XDM。

欲了解更多 UI 中工作區的功能 [!UICONTROL Schemas] ，請參閱 [[!UICONTROL Schemas] 工作區總覽](./overview.md)。
