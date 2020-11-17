---
keywords: Experience Platform;home;popular topics;identity graph viewer;Identity graph viewer;graph viewer;Graph viewer;identity namespace;Identity namespace;identity;Identity;Identity service;identity service
solution: Experience Platform
title: Adobe Experience Platform Identity Service
topic: tutorial
description: 身分圖是特定客戶不同身分之間關係的地圖，可讓您以視覺化方式呈現客戶如何透過不同通道與您的品牌互動。
translation-type: tm+mt
source-git-commit: af7eab0599b17be55d5a4c129f7ebaeba91333bc
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 1%

---


# （測試版）身分圖表檢視器

>[!NOTE]
>
>身分圖表檢視器目前處於測試階段。 其功能可能會有所改變。

身分圖是特定客戶不同身分之間關係的地圖，可讓您以視覺化方式呈現客戶如何透過不同通道與您的品牌互動。 Adobe Experience Platform Identity Service會針對客戶活動，近乎即時地管理和更新所有客戶識別圖。

平台使用者介面中的身分圖表檢視器可讓您視覺化並深入瞭解哪些客戶身份是結合在一起的，以及以哪些方式連結在一起。 檢視器可讓您拖曳圖形的不同部分並與之互動，讓您檢查複雜的身分關係、更有效率地進行除錯，並透過提高透明度來運用資訊。

## 快速入門

使用身分圖檢視器需要瞭解所涉及的各種Adobe Experience Platform服務。 在開始使用身分圖檢視器之前，請先閱讀下列服務的檔案：

- [[!DNL Identity Service]](../home.md):跨裝置和系統橋接身分，以更全面地瞭解個別客戶及其行為。

### 術語

- **身份（節點）:** 身分或節點是實體（通常是個人）專屬的資料。 身份由命名空間和身份值組成。
- **連結（邊緣）:** 連結或邊代表身份之間的連接。
- **圖形（群集）:** 圖形或群集是一組代表個人的身份和連結。

## 存取身分圖表檢視器

若要在UI中使用身分圖表檢視器，請在左側導覽中選 **[!UICONTROL 取「身分]** 」，然後選取「身 **[!UICONTROL 分圖表」標籤]** 。 在「 **[!UICONTROL Identity Namespace]** 」畫面中，按一下「 **[!UICONTROL Select identity namespace]** 」圖示，以搜尋您要使用的命名空間。

![namespace-screen](../images/identity-graph-viewer/identity-namespace.png)

此時將 **[!UICONTROL 顯示「選擇身份]** 命名空間」面板。 此螢幕包含組織可用的名稱空間清單，包括有關名稱空間的 **[!UICONTROL Display name]**、 **[!UICONTROL Identity符號、]** Proper **[!UICONTROL 、]********** Last UpdatedDate、AdoberOdberAdober的資訊。 只要您有有效的識別值連接到名稱空間，您就可以使用任何提供的名稱空間。

選擇要使用的命名空間，然後按一下「 **[!UICONTROL 選擇]** 」繼續。

![select-identity-namespace](../images/identity-graph-viewer/select-identity-namespace.png)

在您選擇了命名空間後，在「 **[!UICONTROL Identity value]** 」文本框中輸入其對應的特定客戶值，並選擇「 **[!UICONTROL View」（查看）]**。

![add-identity-value](../images/identity-graph-viewer/identity-value-filled.png)

此時會出現識別圖形檢視器。 畫面的左側是識別圖，顯示連結至您選取之命名空間的所有身分識別以及您輸入的身分識別值。 每個身分節點都由命名空間及其對應的ID值組成。 您可以選取並保留任何身分，以拖曳圖形並與之互動。 或者，您可以將滑鼠指標暫留在身分上，以檢視其ID值的相關資訊。 圖形輸出也顯示為螢幕中央的表清單。

>[!IMPORTANT]
>
>身分圖需要至少兩個連結的身分才能產生，以及有效的命名空間和ID對。 圖形檢視器可顯示的最大身分數為400。 如需詳細資 [訊，請參閱](#appendix) 以下附錄一節。

![身份圖](../images/identity-graph-viewer/graph-viewer.png)

選擇身份以更新 **[!UICONTROL Identities]** （身份）表上突出顯示的行，並更新右邊欄上提供的資訊，該資訊包括身份的 **[!UICONTROL Value]**、 **[!UICONTROL Batch ID]**，及其上次更新的 **** Adate。

![select-identity](../images/identity-graph-viewer/select-identity.png)

您可以透過圖形進行篩選，並使用「身分識別」表格上方的排序選項來隔離特定 **[!UICONTROL 命名空間]** 。 從下拉式選單中，選取您要反白顯示的命名空間。

![filter-by-namespace](../images/identity-graph-viewer/filter-namespace.png)

圖形檢視器會傳回，反白顯示您選取的命名空間。 篩選選項也會更新 **[!UICONTROL Identities]** 表，以僅傳回您選取之命名空間的資訊。

![篩選](../images/identity-graph-viewer/filtered.png)

圖形檢視器方塊的右上角包含放大選項。 選取 **(+)** 圖示以放大圖形，或 **** (-)圖示以縮小。

![縮放](../images/identity-graph-viewer/zoom.png)

您可以從題頭中選擇資料源，以查看有關批 **[!UICONTROL 的詳細資訊]** 。 「資 **[!UICONTROL 料來源]** 」表格會顯示與圖形 **[!UICONTROL 關聯的批次ID]** ，以及其 **[!UICONTROL 連結ID]**、來源架構和擷取日期的清單。

![資料源](../images/identity-graph-viewer/data-source-table.png)

您可以選擇身份圖中的任何連結，以查看對連結有貢獻的所有源批。

![select-links](../images/identity-graph-viewer/select-edge.png)

或者，您可以選擇一個批，以查看此批貢獻的所有連結。

![select-links](../images/identity-graph-viewer/select-batch.png)

也可透過身分圖檢視器存取具有較大身分叢集的身分圖。

![大群集](../images/identity-graph-viewer/large-cluster.png)

## 附錄

如果未符合下列必要條件，圖形檢視器會傳回錯誤：

- 識別值不存在於選定的命名空間中。
- 該圖只有少於2個恆等式。
- 該圖超過400個恆等式的上限。

![大群集](../images/identity-graph-viewer/error-screen.png)

## 後續步驟

閱讀本檔案後，您便瞭解如何在平台UI中探索客戶的身分圖。 有關平台中身分的詳細資訊，請參閱身分服務 [總覽](../home.md)