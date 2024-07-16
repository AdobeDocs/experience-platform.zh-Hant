---
solution: Experience Platform
title: 在UI中產生XDM結構描述的範例資料
description: 瞭解如何根據Adobe Experience Platform使用者介面中的現有結構描述產生範例JSON資料。
exl-id: e60eedb2-2245-42cd-b574-43caf9e3426c
source-git-commit: 19a9341a9f53559fe3f619b2f157015e53b25b64
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 14%

---

# 在 UI 中為 XDM 結構描述產生樣本資料 {#generate-sample-data-for-an-xdm-schema}

>[!CONTEXTUALHELP]
>id="platform_xdm_downloadsamplefile"
>title="下載範例檔案"
>abstract="產生符合您所選結構描述之結構的範例 JSON 物件。此物件可以充當範本，以確保您的資料格式正確，以便擷取到採用該結構描述的資料集中。您的瀏覽器將會下載範例 JSON 檔案。"

若要將資料內嵌至Adobe Experience Platform，資料的格式和結構必須符合現有的Experience Data Model (XDM)結構描述。 根據特定資料集的結構描述複雜性，可能很難判斷資料集在擷取時預期的資料確切形狀。

對於您在Experience PlatformUI中定義的任何結構描述，您可以產生符合結構描述結構的範例JSON物件。 此物件可當作任何資料之範本，這些資料會擷取到採用特定結構描述的資料集中。

在Platform UI中，選取左側導覽中的&#x200B;**[!UICONTROL 結構描述]**。 在&#x200B;**[!UICONTROL 瀏覽]**&#x200B;標籤下，找到您要產生範例資料的結構描述。 從清單中選取該架構，右邊欄會更新以顯示有關架構的詳細資訊。 從這裡，選取&#x200B;**[!UICONTROL 下載範例檔案]**。

![已選取結構描述的「結構描述」工作區的「瀏覽」索引標籤，並下載反白顯示的範例檔案。](../images/ui/sample/sample-data.png)

瀏覽器會下載範例JSON檔案。 您現在可以使用此檔案作為參考，瞭解在擷取至採用此結構的資料集時，如何建構您的資料。

## 後續步驟

本指南說明如何從Platform UI的XDM結構描述產生範例JSON檔案。 若要瞭解如何使用結構描述登入API產生範例資料，請參閱[範例資料端點指南](../api/sample-data.md)。

準備好開始內嵌資料後，請參閱有關[將CSV檔案對應至XDM](../../ingestion/tutorials/map-csv/overview.md)的教學課程，瞭解如何將一般資料檔案（例如CSV）對應至XDM結構描述並將其內嵌至Platform。 或者，您可以建立[來源連線](../../sources/home.md)，從外部來源匯入您的資料並將其對應至XDM。

如需UI中[!UICONTROL 結構描述]工作區的功能的詳細資訊，請參閱[[!UICONTROL 結構描述]工作區概觀](./overview.md)。
