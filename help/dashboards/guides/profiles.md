---
keywords: Experience Platform;profile;real-time customer profile;user interface;UI;customization;profile dashboard;dashboard
title: 描述檔儀表板
description: Adobe Experience Platform提供儀表板，您可以透過儀表板檢視組織即時客戶個人檔案資料的重要資訊。
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: 2f2459c1c88c97a3ab322b08ee178463fbb4a592
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 0%

---


# （測試版）[!UICONTROL 描述檔]控制面板

>[!IMPORTANT]
>
>本檔案中概述的控制面板功能目前為測試版，並非所有使用者都能使用。 文件和功能可能會有所變更。

Adobe Experience Platform使用者介面(UI)提供控制面板，您可透過此控制面板檢視有關[!DNL Real-time Customer Profile]資料的重要資訊，如每日快照中所擷取。 本指南概述如何存取和使用UI中的[!UICONTROL 描述檔]控制面板，並提供控制面板中顯示之量度的相關資訊。

如需Experience Platform使用者介面中所有描述檔功能的概述，請造訪[即時客戶描述檔UI指南](../../profile/ui/user-guide.md)。

## 描述檔控制面板資料

[!UICONTROL Profiles]控制面板會顯示您組織在Experience Platform的Profile Store中所擁有屬性（記錄）資料的快照。 快照不包含任何事件（時間系列）資料。

快照中的屬性資料與拍攝快照時在特定時間點顯示的資料完全相同。 換言之，快照不是資料的近似值或範例，而「描述檔」控制面板不會即時更新。

>[!NOTE]
>
>自快照建立以來對資料所做的任何變更或更新，在下一個快照建立之前，不會反映在控制面板中。

## 探索[!UICONTROL 描述檔]控制面板

若要導覽至平台UI中的[!UICONTROL Profiles]控制面板，請在左側導軌中選取&#x200B;**[!UICONTROL Profiles]**，然後選取&#x200B;**[!UICONTROL Overview]**&#x200B;標籤以顯示控制面板。

![](../images/profiles/dashboard-overview.png)

### 選擇合併策略

顯示在[!UICONTROL Profiles]控制面板中的量度是根據套用至即時客戶描述檔資料的合併原則。 當從多個來源匯整資料時，資料可能包含衝突值（例如，一個資料集可將客戶列為「單一」，而另一個資料集可將客戶列為「已結婚」），而合併原則的工作是判斷哪些資料要優先排序並顯示為描述檔的一部分。

控制面板將自動選擇要顯示的合併策略，但您可以更改使用下拉菜單選擇的合併策略。 要選擇不同的合併策略，請選擇合併策略名稱旁的下拉式清單，然後選擇要查看的合併策略。

>[!NOTE]
>
>下拉菜單僅顯示與XDM單個配置檔案類相關的合併策略，但是，如果您的組織已建立多個合併策略，則可能表示您需要滾動才能查看可用合併策略的完整清單。

有關合併策略的詳細資訊，包括如何為組織建立、編輯和聲明預設的合併策略，請訪問[合併策略UI指南](../../profile/ui/merge-policies.md)。

![](../images/profiles/select-merge-policy.png)

### Widget和量度

控制面板由widget組成，widget是唯讀量度，提供您描述檔資料的重要資訊。 介面工具集上的「上次更新」日期和時間會顯示資料的最後快照拍攝的時間。

![](../images/profiles/dashboard-timestamp.png)

## 可用的Widget

Experience Platform提供多個Widget，您可使用這些Widget來視覺化與您的描述檔資料相關的不同量度。 選取下方介面工具集的名稱，以瞭解更多：

* [[!UICONTROL 受眾規模]](#audience-size)
* [[!UICONTROL 新增的設定檔]](#profiles-added)
* [[!UICONTROL 隨著時間增加的設定檔]](#profiles-added-over-time)
* [[!UICONTROL 依命名空間劃分的描述檔]](#profiles-by-namespace)
* [[!UICONTROL 命名空間重疊]](#namespace-overlap)

### [!UICONTROL 受眾規模] {#audience-size}

**[!UICONTROL 觀眾大小]**&#x200B;介面工具集顯示拍攝快照時，描述檔資料儲存區內合併的描述檔總數。 此數字是選定合併策略應用於您的配置檔案資料的結果，以便將配置檔案碎片合併到一起，為每個個人形成單個配置檔案。

有關碎片和合併配置檔案的詳細資訊，請首先閱讀[即時客戶配置檔案概述](../../profile/home.md)的&#x200B;*配置檔案片段與合併配置檔案*&#x200B;部分。

>[!NOTE]
>
>用於計算此度量的合併原則與用於計算[!UICONTROL 授權使用]控制面板中[!UICONTROL 可定址對象]的系統產生的合併原則不同，因此[!UICONTROL 設定檔]和[!UICONTROL 授權使用]控制面板中的對象計數不太可能完全相同。

![](../images/profiles/audience-size.png)

### [!UICONTROL 新增的設定檔] {#profiles-added}

添加的&#x200B;**[!UICONTROL 配置檔案]**&#x200B;構件顯示自上次快照建立以來添加到配置檔案資料儲存的合併配置檔案總數。 此數字是選定合併策略應用於您的配置檔案資料的結果，以便將配置檔案碎片合併到一起，為每個個人形成單個配置檔案。

![](../images/profiles/profiles-added.png)

### [!UICONTROL 隨著時間增加的設定檔] {#profiles-added-over-time}

隨時間添加的&#x200B;**[!UICONTROL 配置檔案]**&#x200B;介面工具集顯示最近30天每天添加到配置檔案資料儲存的合併配置檔案總數。 快照建立時每天都會更新此數字，因此，如果要將配置檔案添加到平台中，則在建立下一個快照之前不會反映配置檔案的數量。

新增的描述檔計數是選取的合併原則套用至您的描述檔資料的結果，以便將描述檔片段合併為每個個人的單一描述檔。

![](../images/profiles/profiles-added-over-time.png)

### [!UICONTROL 依命名空間劃分的描述檔] {#profiles-by-namespace}

**[!UICONTROL 依名稱空間劃分的描述檔]**&#x200B;介面工具集會顯示描述檔商店中所有合併描述檔的識別名稱空間劃分。 按[!UICONTROL ID namespace]（換言之，將每個命名空間顯示的值加在一起）列出的配置檔案總數可能高於合併配置檔案總數，因為一個配置檔案可能有多個與其關聯的命名空間。 例如，如果客戶在多個通道上與您的品牌互動，則多個名稱空間將與該個別客戶關聯。

若要進一步瞭解身分名稱空間，請造訪[Adobe Experience Platform Identity Service檔案](../../identity-service/home.md)。

![](../images/profiles/profiles-by-namespace.png)

### [!UICONTROL 命名空間重疊] {#namespace-overlap}

**[!UICONTROL 名稱空間重疊]**&#x200B;介面工具集顯示一個Venn圖或設定圖，顯示包含多個身份名稱空間的配置檔案儲存中配置檔案的重疊。

使用介面工具集上的下拉式功能表來選取您要比較的身分名稱空間後，會顯示社交圈，顯示每個名稱空間的相對大小，其中包含兩個名稱空間的描述檔數目，由社交圈之間重疊的大小來表示。

如果客戶在多個通道上與您的品牌互動，則多個名稱空間將與該個別客戶相關聯，因此您的組織可能會有多個描述檔，其中包含來自多個身分名稱空間的片段。

若要進一步瞭解身分名稱空間，請造訪[Adobe Experience Platform Identity Service檔案](../../identity-service/home.md)。

![](../images/profiles/namespace-overlap.png)

## 後續步驟

遵循本檔案，您現在應該可以找到「描述檔」控制面板，並瞭解可用Widget中顯示的量度。 若要進一步瞭解如何在Experience Platform UI中使用[!DNL Profile]資料，請參閱[即時客戶個人檔案UI指南](../../profile/ui/user-guide.md)。