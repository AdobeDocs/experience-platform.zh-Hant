---
keywords: Experience Platform;home；熱門主題；身份圖查看器；Identity Graph viewer;Graph viewer;Graph viewer;Identity namespace;Identity;Identity Service;identity service
solution: Experience Platform
title: Identity Graph檢視器概觀
topic: tutorial
description: 身分圖是特定客戶不同身分之間關係的地圖，可讓您以視覺化方式呈現客戶如何透過不同通道與您的品牌互動。
translation-type: tm+mt
source-git-commit: f4326c7a8bb8af90c092d3790e51c133744d498f
workflow-type: tm+mt
source-wordcount: '1038'
ht-degree: 1%

---


# 身分圖表檢視器概觀

身分圖是特定客戶不同身分之間關係的地圖，可讓您以視覺化方式呈現客戶如何透過不同通道與您的品牌互動。 Adobe Experience Platform Identity Service會針對客戶活動，近乎即時地管理和更新所有客戶識別圖。

平台使用者介面中的身分圖表檢視器可讓您視覺化並深入瞭解哪些客戶身份是結合在一起的，以及以哪些方式連結在一起。 檢視器可讓您拖曳圖形的不同部分並與之互動，讓您檢查複雜的身分關係、更有效率地進行除錯，並透過提高透明度來運用資訊。

## 教學課程影片

以下影片旨在協助您瞭解身分圖表檢視器。

>[!VIDEO](https://video.tv.adobe.com/v/331030/?quality=12&learn=on)

## 快速入門

使用身分圖檢視器需要瞭解所涉及的各種Adobe Experience Platform服務。 在開始使用身分圖檢視器之前，請先閱讀下列服務的檔案：

- [[!DNL Identity Service]](../home.md):跨裝置和系統橋接身分，以更全面地瞭解個別客戶及其行為。

### 術語

- **身分（節點）:** 身分或節點是實體（通常是個人）專屬的資料。身份由命名空間和身份值組成。
- **連結（邊緣）:** 連結或邊緣代表身分之間的連結。
- **圖形（群集）:** 圖形或群集是一組代表人的身分和連結。

## 存取身分圖表檢視器

若要使用UI中的身分圖表檢視器，請在左側導覽中選取&#x200B;**[!UICONTROL Identity]**，然後選取&#x200B;**[!UICONTROL Identity圖表]**&#x200B;標籤。 在&#x200B;**[!UICONTROL Identity Namespace]**&#x200B;螢幕中，按一下&#x200B;**[!UICONTROL 選擇標識名稱空間]**&#x200B;表徵圖以搜索要使用的名稱空間。

![namespace-screen](../images/identity-graph-viewer/identity-namespace.png)

出現&#x200B;**[!UICONTROL 選擇身份名稱空間]**&#x200B;面板。 此螢幕包含可供組織使用的命名空間清單，包括有關命名空間的&#x200B;**[!UICONTROL 顯示名稱]**、**[!UICONTROL 標識符號]**、**[!UICONTROL 所有者]**、**[!UICONTROL 上次更新日期和**[!UICONTROL &#x200B;說明&#x200B;]**的資訊。]**&#x200B;只要您有有效的識別值連接到名稱空間，您就可以使用任何提供的名稱空間。

選擇要使用的命名空間，然後按一下&#x200B;**[!UICONTROL 選擇]**&#x200B;繼續。

![select-identity-namespace](../images/identity-graph-viewer/select-identity-namespace.png)

在您選擇了命名空間後，請在&#x200B;**[!UICONTROL Identity value]**&#x200B;文本框中輸入其對應的特定客戶值，然後選擇&#x200B;**[!UICONTROL View]**。

![add-identity-value](../images/identity-graph-viewer/identity-value-filled.png)

### 從資料集存取身分圖表檢視器

您也可以使用資料集介面來存取身分圖表檢視器。 從資料集[!UICONTROL Browse]頁中，選擇要與之交互的資料集，然後選擇&#x200B;**[!UICONTROL Preview dataset]**

![preview-dataset](../images/identity-graph-viewer/preview-dataset.png)

從預覽視窗中，選取指紋圖示，以檢視透過身分圖表檢視器呈現的身分識別。

>[!TIP]
>
>只有當資料集有兩個或兩個以上的身分時，才會出現指紋圖示。

![指紋](../images/identity-graph-viewer/fingerprint.png)

此時會出現識別圖形檢視器。 畫面的左側是識別圖，顯示連結至您選取之命名空間的所有身分識別以及您輸入的身分識別值。 每個身分節點都由命名空間及其對應的ID值組成。 您可以選取並保留任何身分，以拖曳圖形並與之互動。 或者，您可以將滑鼠指標暫留在身分上，以檢視其ID值的相關資訊。 圖形輸出也顯示為螢幕中央的表清單。

>[!IMPORTANT]
>
>身分圖需要至少兩個連結的身分才能產生，以及有效的命名空間和ID對。 圖形檢視器可顯示的最大身分數為150。 如需詳細資訊，請參閱下面的[附錄](#appendix)一節。

![身份圖](../images/identity-graph-viewer/graph-viewer.png)

選擇標識以更新&#x200B;**[!UICONTROL Identities]**&#x200B;表上突出顯示的行，並更新右邊欄上提供的資訊，該資訊包括標識的&#x200B;**[!UICONTROL 值]**、**[!UICONTROL 批ID]**&#x200B;及其&#x200B;**[!UICONTROL 上次更新]**&#x200B;日期。

![select-identity](../images/identity-graph-viewer/select-identity.png)

您可以使用&#x200B;**[!UICONTROL Identities]**&#x200B;表格上方的排序選項，篩選圖形並隔離特定的命名空間。 從下拉式選單中，選取您要反白顯示的命名空間。

![filter-by-namespace](../images/identity-graph-viewer/filter-namespace.png)

圖形檢視器會傳回，反白顯示您選取的命名空間。 篩選器選項也會更新&#x200B;**[!UICONTROL Identities]**&#x200B;表格，僅傳回您選取之命名空間的資訊。

![篩選](../images/identity-graph-viewer/filtered.png)

圖形檢視器方塊的右上角包含放大選項。 選擇&#x200B;**(+)**&#x200B;圖示以放大顯示圖形，或選擇&#x200B;**(-)**&#x200B;圖示以縮小顯示。

![縮放](../images/identity-graph-viewer/zoom.png)

通過從標題中選擇&#x200B;**[!UICONTROL 資料源]**，可以查看有關批的詳細資訊。 **[!UICONTROL 資料來源]**&#x200B;表格顯示與圖形相關的&#x200B;**[!UICONTROL 批次ID]**&#x200B;清單，以及其&#x200B;**[!UICONTROL 連結ID]**、來源架構和擷取日期。

![資料源](../images/identity-graph-viewer/data-source-table.png)

您可以選擇身份圖中的任何連結，以查看對連結有貢獻的所有源批。

![select-links](../images/identity-graph-viewer/select-edge.png)

或者，您可以選擇一個批，以查看此批貢獻的所有連結。

![select-links](../images/identity-graph-viewer/select-batch.png)

也可透過身分圖檢視器存取具有較大身分叢集的身分圖。

![大群集](../images/identity-graph-viewer/large-cluster.png)

## 附錄

下節提供使用身分圖表檢視器的其他資訊。

### 瞭解錯誤訊息

存取身分圖檢視器時可能會發生錯誤。 以下是使用身分圖表檢視器時要注意的先決條件和限制清單。

- 標識值必須存在於所選命名空間中。
- 身分圖表檢視器至少需要兩個連結的身分才能產生。 可能只有一個識別值且沒有連結的識別，在此情況下，該值只會存在於[!DNL Profile]檢視器中。
- 身分圖表檢視器不能超過150個身分。

![錯誤畫面](../images/identity-graph-viewer/error-screen.png)

## 後續步驟

閱讀本檔案後，您便瞭解如何在平台UI中探索客戶的身分圖。 有關平台中身份的詳細資訊，請參閱[Identity Service概述](../home.md)

## 更改日誌

| Date | 動作 |
| ---- | ------ |
| 2021-01 | <ul><li>新增對串流內嵌資料和非生產沙盒的支援。</li><li>微幅錯誤修正。</li></ul> |
| 2021-02 | <ul><li>身分圖表檢視器可透過資料集預覽存取。</li><li>微幅錯誤修正。</li><li>身分圖表檢視器已設為「一般可用」。</li></ul> |
