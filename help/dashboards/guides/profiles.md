---
keywords: Experience Platform；設定檔；即時客戶設定檔；使用者介面；UI；自訂；設定檔控制面板；控制面板
title: 設定檔控制面板
description: Adobe Experience Platform提供控制面板，讓您透過該控制面板檢視貴組織「即時客戶個人檔案」資料的重要資訊。
topic-legacy: guide
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: 11e8acc3da7f7540421b5c7f3d91658c571fdb6f
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 0%

---

# (Beta)[!UICONTROL 設定檔]控制面板

>[!IMPORTANT]
>
>本檔案中概述的控制面板功能目前為測試版，並非所有使用者都能使用。 文件和功能可能會有所變更。

Adobe Experience Platform使用者介面(UI)提供控制面板，您可透過該控制面板檢視[!DNL Real-time Customer Profile]資料的重要資訊，如每日快照期間所擷取。 本指南概述如何在UI中存取和使用[!UICONTROL Profiles]控制面板，並提供控制面板中所顯示量度的相關資訊。

如需Experience Platform使用者介面中所有設定檔功能的概觀，請造訪[即時客戶設定檔UI指南](../../profile/ui/user-guide.md)。

## 設定檔控制面板資料

[!UICONTROL Profiles]控制面板顯示您的組織在Profile儲存區中Experience Platform的屬性（記錄）資料的快照。 快照不包含任何事件（時間系列）資料。

快照中的屬性資料與建立快照時在特定時間點顯示的資料完全相同。 換句話說，快照不是資料的近似值或樣本，而且「配置檔案」儀表板不會即時更新。

>[!NOTE]
>
>自拍攝快照以來對資料所做的任何更改或更新都不會反映在儀表板中，直到拍攝下一個快照。

## 探索[!UICONTROL 設定檔]控制面板

若要導覽至Platform UI中的[!UICONTROL Profiles]控制面板，請在左側邊欄中選取&#x200B;**[!UICONTROL Profiles]**，然後選取&#x200B;**[!UICONTROL Overview]**&#x200B;標籤以顯示控制面板。

![](../images/profiles/dashboard-overview.png)

### 選擇合併策略

顯示在[!UICONTROL Profiles]控制面板中的量度是以套用至您即時客戶設定檔資料的合併原則為基礎。 從多個來源匯整資料時，資料可能會包含衝突值（例如，一個資料集可能將客戶列為「單一」，而另一個資料集可能將客戶列為「已婚」），而合併原則的工作是決定要排定優先順序並顯示為設定檔一部分的資料。

控制面板將自動選擇要顯示的合併策略，但您可以使用下拉菜單更改所選的合併策略。 要選擇不同的合併策略，請選擇合併策略名稱旁的下拉清單，然後選擇要查看的合併策略。

>[!NOTE]
>
>下拉式功能表只會顯示與XDM個別設定檔類別相關的合併原則，但是，如果貴組織已建立多個合併原則，可能表示您需要捲動才能檢視完整的可用合併原則清單。

有關合併策略的詳細資訊，包括如何為貴組織建立、編輯和聲明預設的合併策略，請從閱讀[合併策略概述](../../profile/merge-policies/overview.md)開始。

![](../images/profiles/select-merge-policy.png)

### Widget和量度

控制面板由Widget組成，Widget是唯讀量度，提供關於設定檔資料的重要資訊。 介面工具集上的「上次更新」日期和時間會顯示資料的最後快照拍攝時間。

![](../images/profiles/dashboard-timestamp.png)

## 可用介面工具集

Experience Platform提供多個小工具集，可用來視覺化與您的設定檔資料相關的不同量度。 選取下方介面工具集的名稱以深入了解：

* [[!UICONTROL 對象大小]](#audience-size)
* [[!UICONTROL 新增的設定檔]](#profiles-added)
* [[!UICONTROL 隨時間新增的設定檔]](#profiles-added-over-time)
* [[!UICONTROL 依命名空間的設定檔]](#profiles-by-namespace)
* [[!UICONTROL 命名空間重疊]](#namespace-overlap)

### [!UICONTROL 對象大小] {#audience-size}

**[!UICONTROL 對象大小]**&#x200B;介面工具集會顯示拍攝快照時，設定檔資料存放區中合併的設定檔總數。 此數字是您的設定檔資料所套用的所選合併原則的結果，以便將設定檔片段合併在一起，以便為每個個人建立單一設定檔。

如需片段和已合併設定檔的詳細資訊，請先閱讀[即時客戶設定檔概述](../../profile/home.md)的&#x200B;*設定檔片段與已合併設定檔*&#x200B;區段。

>[!NOTE]
>
>用於計算此度量的合併策略與用於在[!UICONTROL 許可證使用]控制面板中計算[!UICONTROL 可定址對象]的系統生成合併策略不同，因此[!UICONTROL 配置檔案]和[!UICONTROL 許可證使用]控制面板中的對象計數不太可能完全相同。

![](../images/profiles/audience-size.png)

### [!UICONTROL 新增的設定檔] {#profiles-added}

**[!UICONTROL 新增的設定檔]**&#x200B;介面工具集會顯示自上次快照建立以來，已新增至設定檔資料存放區的合併設定檔總數。 此數字是您的設定檔資料所套用的所選合併原則的結果，以便將設定檔片段合併在一起，以便為每個個人建立單一設定檔。

![](../images/profiles/profiles-added.png)

### [!UICONTROL 隨時間新增的設定檔] {#profiles-added-over-time}

一段時間內新增的&#x200B;**[!UICONTROL 設定檔]**&#x200B;介面工具集會顯示過去30天內每天新增至設定檔資料存放區的合併設定檔總數。 拍攝快照時每天都會更新此數字，因此，如果您要將設定檔內嵌至Platform，則在拍攝下一個快照前不會反映設定檔數。

新增的設定檔計數是將選取的合併原則套用至您的設定檔資料的結果，以便將設定檔片段合併在一起，以便為每個個人建立單一設定檔。

![](../images/profiles/profiles-added-over-time.png)

### [!UICONTROL 依命名空間的設定檔] {#profiles-by-namespace}

**[!UICONTROL 依命名空間的設定檔]**&#x200B;介面工具集會顯示「設定檔」存放區中所有合併設定檔的身分識別命名空間劃分。 按[!UICONTROL ID命名空間]顯示的設定檔總數（換句話說，將每個命名空間顯示的值加總）可能高於合併設定檔總數，因為一個設定檔可能有多個相關聯的命名空間。 例如，如果客戶在多個管道上與您的品牌互動，則多個命名空間將會與該個別客戶相關聯。

若要進一步了解身分識別命名空間，請造訪[Adobe Experience Platform Identity Service檔案](../../identity-service/home.md)。

![](../images/profiles/profiles-by-namespace.png)

### [!UICONTROL 命名空間重疊] {#namespace-overlap}

**[!UICONTROL 命名空間重疊]**&#x200B;介面工具集會顯示文氏圖表或設定圖，顯示包含多個身分命名空間之設定檔存放區中的設定檔重疊。

使用介面工具集上的下拉式功能表來選取您要比較的身分命名空間後，圓圈會顯示每個命名空間的相對大小，包含兩個命名空間的設定檔數目會以圓圈之間重疊的大小來表示。

如果客戶在多個管道上與您的品牌互動，則該個別客戶將擁有多個命名空間，因此您的組織可能會有多個設定檔，其中包含來自多個身分命名空間的片段。

若要進一步了解身分識別命名空間，請造訪[Adobe Experience Platform Identity Service檔案](../../identity-service/home.md)。

![](../images/profiles/namespace-overlap.png)

## 後續步驟

依照本檔案操作，您現在應該能夠找到「設定檔」控制面板，並了解可用介面工具集中顯示的量度。 若要進一步了解如何在Experience PlatformUI中使用[!DNL Profile]資料，請參閱[即時客戶設定檔UI指南](../../profile/ui/user-guide.md)。
