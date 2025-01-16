---
title: 使用沙箱工具備份物件設定
description: 若要安全地重設沙箱並新增版本設定支援，請使用沙箱工具套件備份物件設定（或中繼資料）。 備份套件可防止關鍵組態（例如結構描述、資料集和對象）遺失，尤其是在開發反複專案期間。
source-git-commit: f0cbee2663682f0afae6d7e4b174f250fcb3df53
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 3%

---

# 使用沙箱工具備份物件設定

若要安全地重設沙箱並新增版本設定支援，請使用沙箱工具套件備份物件設定（或中繼資料）。 備份套件可防止關鍵組態（例如結構描述、資料集和對象）遺失，尤其是在開發反複專案期間。

![顯示沙箱工具優點的總覽](../images/use-cases/tooling-overview.png)

## 為何考慮此使用案例 {#why-this-use-case}

使用沙箱工具建立備份套件，可確保您的物件設定儲存和安全。 當您進行實驗及建置時，開發沙箱會快速填滿，而在重設後從頭開始建置沙箱可能很耗時，並留下犯錯的空間。 藉助沙箱工具的強大功能，您可以將備份套件匯入全新重設的沙箱中，以立即傳回您理想的設定，以便您能夠繼續開發。

備份套件也可讓您在整個開發程式中支援版本設定。 隨著您的沙箱變更，在先前的套件旁邊建立其他備份套件，以便您可以輕鬆將沙箱還原到任何設定。

## 必要條件和規劃 {#prerequisites-and-planning}

當您計畫在組織內建立自己的備份套件時，請在規劃程式中考慮下列必要條件：

- 評估組織內沙箱的目前使用情況。 是否有任何非生產沙箱接近或超過其授權權利？
- 您要備份的中繼資料範圍為何？ 您可以根據使用案例，考慮備份完整或部分沙箱。
- 根據您想要備份的範圍中繼資料，請確定您瞭解如何手動[新增物件至封裝](../ui/sandbox-tooling.md#add-object-to-a-new-package)，或如何[匯出整個沙箱](../ui/sandbox-tooling.md#export-an-entire-sandbox)。
- 確保您擁有存取組織中沙箱工具的許可權，且擁有正確的許可權。

### 您將使用的 UI 功能、平台元件和 Experience Cloud 產品 {#ui-functionality-and-elements}

若要成功實作此使用案例，您必須使用Adobe Experience Platform的多個區域。 請確定您擁有這些區域所需的[屬性型存取控制許可權](../../access-control/abac/overview.md)，或要求系統管理員授與您必要的許可權。

- [沙箱工具](../ui/sandbox-tooling.md)
- [沙箱管理](../ui/user-guide.md)
- [授權使用量儀表板](../../landing/license-usage-and-guardrails/license-usage-dashboard.md)
- [資料集](../../catalog/datasets/overview.md)
- [結構描述](../../xdm//home.md)
- [客群](../../segmentation/home.md)
- 來自Adobe Journey Optimizer的[歷程](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)

## 如何實現使用案例：高層級概觀 {#achieve-the-use-case-high-level}

1. 定義您要備份的中繼資料的範圍。
2. 使用沙箱工具使用者介面，將您所需的物件匯出至備份套件。
3. 定期建立新版本的備份套件，以確保沙箱與目前的設定一致。
4. 根據您對非生產沙箱的權利，檢查您目前在授權使用儀表板中的使用情況。
5. 重設非生產沙箱以符合權益，或釋放不必要的資源和資料儲存。
6. 在重裝置份套件以還原物件設定後，將其匯入您的沙箱。

## 如何實現使用案例：逐步說明 {#step-by-step-instructions}

請閱讀以下章節，包含進一步檔案的連結，以完成上述高階概觀中的每個步驟。

### 定義中繼資料範圍

開始建立備份套件之前，您應該考慮套件的使用案例。 視您的需求而定，您可能想要備份完整的沙箱，或選取要新增到封裝中的特定物件，如[必要條件](#prerequisites-and-planning)中所述。

>[!NOTE]
>
> 如果您考慮備份沙箱以重設沙箱，請注意重設沙箱的[限制](../ui/user-guide.md#reset-a-sandbox)。

### 將您選擇的中繼資料匯出至封裝

此時，您已準備好使用沙箱工具使用者介面來備份沙箱。 此步驟將涵蓋備份整個沙箱和備份特定物件。

>[!NOTE]
>
> 並非所有物件都支援沙箱工具。 請參閱沙箱工具支援的[物件](../ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling)指南，以取得允許物件的完整清單。

#### 匯出完整的沙箱

若要完整備份您的沙箱，請依照[沙箱工具指南](../ui/sandbox-tooling.md#export-an-entire-sandbox)來建立和發佈包含您整個沙箱組態的新套件。

#### 匯出個別物件

您可以透過下列任一方式將個別物件備份至封裝中。 雖然這些指南著重於將結構描述新增到封裝中，但相同的步驟適用於其他物件，例如資料集、對象或歷程。

- 依照沙箱工具的[加入物件指南](../ui/sandbox-tooling.md#add-object-to-a-new-package)，將個別物件加入至新封裝。
- 依照[沙箱工具指南](../ui/sandbox-tooling.md#add-an-object-to-an-existing-package-and-publish)，將個別物件新增至現有的備份封裝，確定您發佈變更。
- 按照以下指南建立空白的多物件封裝，以將物件加入其中。

##### 建立多物件套件

在Experience Platform中，選取左側導覽中的&#x200B;**[!UICONTROL 沙箱]**，然後選取&#x200B;**[!UICONTROL 封裝]**。 若要開始建立新封裝，請從右上角選取&#x200B;**[!UICONTROL 建立封裝]**。

![沙箱儀表板中的「套件」索引標籤中反白顯示「建立套件」。](../images/use-cases/create-package.png)

**[!UICONTROL 建立封裝]**&#x200B;對話方塊就會顯示。 選擇&#x200B;**[!UICONTROL 選取物件]**，然後選取&#x200B;**[!UICONTROL 選取]**。

![「建立封裝」對話方塊中的「選取物件」和「選取」選項會反白顯示。](../images/use-cases/create-package-select-objects.png)

選取&#x200B;**[!UICONTROL 多物件]**&#x200B;選項。 現在，您需要提供新套件的名稱。 在&#x200B;**[!UICONTROL 封裝名稱]**&#x200B;文字欄位中輸入您想要的名稱。 完成後，選取&#x200B;**[!UICONTROL 建立]**。

![已選取「多物件」且封裝名稱「備份」已填入的「建立封裝」對話方塊。](../images/use-cases/name-multi-object.png)

您的新多物件封裝已建立並可在[!UICONTROL 封裝]儀表板中使用。 從清單中選取封裝。

![包含名為Backup之封裝的封裝儀表板反白顯示。](../images/use-cases/package-created.png)

封裝的資訊和內容會出現。 目前新封裝中沒有物件。 若要開始新增物件，請遵循[將物件新增至現有封裝](../ui/sandbox-tooling.md#add-object-to-a-new-package)的指南。

### 視需要建立備份套件的新版本

現在您已為沙箱建立了第一個備份套件，隨著沙箱設定的變更，您將想要建立備份套件的新版本。

雖然可以將新物件新增至您現有的備份套件，但建議您建立新套件以支援沙箱中的版本設定。 這可確保您在繼續開發時可輕鬆重設和匯入任何舊版的沙箱。

### 根據您的授權權益檢查您目前的使用情形

備份套件現在已準備就緒，您可以重設沙箱以重設您的使用情形。 您應該定期監控使用情況，以便調整授權權益或視需要重設沙箱。 您可以參閱[授權使用指南](../../dashboards/guides/license-usage.md)，以進一步瞭解授權使用儀表板。

### 重設您的沙箱

此時，您可以安全地重設沙箱，假設沙箱符合必要的引數。 依照[重設沙箱指南](../ui/user-guide.md#reset-a-sandbox)開始重設您的沙箱，請務必閱讀可能會阻止您重設沙箱的警告清單案例。

### 將新建立的備份套件匯入您的重設沙箱

現在您已重設沙箱，您可以使用您建立的備份套件。 如需將套件匯入目標沙箱的逐步程式，請依照[沙箱工具指南](../ui/sandbox-tooling.md#import-a-package-to-a-target-sandbox)操作。

## 透過沙箱工具實現的其他使用案例： {#other-use-cases}

探索透過沙箱工具啟用的更多使用案例：

- [使用沙箱工具啟用卓越中心](./center-of-excellence.md)
