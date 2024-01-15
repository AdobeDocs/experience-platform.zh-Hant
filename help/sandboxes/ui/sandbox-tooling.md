---
title: 沙箱工具
description: 順暢地匯出和匯入沙箱之間的沙箱設定。
exl-id: f1199ab7-11bf-43d9-ab86-15974687d182
source-git-commit: 1f7b7f0486d0bb2774f16a766c4a5af6bbb8848a
workflow-type: tm+mt
source-wordcount: '1859'
ht-degree: 5%

---

# 沙箱工具

>[!NOTE]
>
>沙箱工具是支援兩者的基本功能 [!DNL Real-Time Customer Data Platform] 和 [!DNL Journey Optimizer] 以提升開發週期效率和設定準確性。<br><br>您必須具備下列兩個角色型存取控制許可權，才能使用沙箱工具功能：<br>- `manage-sandbox` 或 `view-sandbox`<br>- `manage-package`

提高沙箱之間的設定準確性，並利用沙箱工具功能順暢地匯出和匯入沙箱之間的沙箱設定。 使用沙箱工具來減少實作程式的價值實現時間，並跨沙箱移動成功的設定。

您可以使用沙箱工具功能來選取不同的物件，並將它們匯出到套件中。 套件可以包含單一物件或多個物件。 <!--or an entire sandbox.-->套件中包含的任何物件都必須來自相同沙箱。

## 沙箱工具支援的物件 {#supported-objects}

沙箱工具功能可讓您匯出 [!DNL Adobe Real-Time Customer Data Platform] 和 [!DNL Adobe Journey Optimizer] 物件放入封裝。

### Real-time Customer Data Platform物件 {#real-time-cdp-objects}

下表列出 [!DNL Adobe Real-Time Customer Data Platform] 目前支援沙箱工具的物件：

| 平台 | 物件 | 詳細資料 |
| --- | --- | --- |
| 客戶資料平台 | 來源 | 出於安全原因，不會將來源帳戶認證復寫到目標沙箱中，而是需要手動更新。 依照預設，來源資料流會以草稿狀態複製。 |
| 客戶資料平台 | 對象 | 僅限 **[!UICONTROL 客戶對象]** type **[!UICONTROL 分段服務]** 支援。 用於同意和管理的現有標籤將複製到相同的匯入工作中。 |
| 客戶資料平台 | 身分 | 在Adobe沙箱中建立時，系統會自動刪除重複的Target標準身分名稱空間。 對象規則中的所有屬性都已在聯合結構描述中啟用時，才能複製對象。 必須先移動並啟用統一設定檔的必要結構描述。 |
| 客戶資料平台 | 結構描述 | 用於同意和管理的現有標籤將複製到相同的匯入工作中。 將依原樣從來源沙箱複製結構描述統一設定檔狀態。 如果為來源沙箱中的統一設定檔啟用了結構描述，則所有屬性都會移至聯合結構描述。 封裝中不包含結構描述關聯邊緣案例。 |
| 客戶資料平台 | 資料集 | 資料集複製時會預設停用整合設定檔設定。 |

下列物件已匯入，但處於草稿或已停用的狀態：

| 功能 | 物件 | 狀態 |
| --- | --- | --- |
| 匯入狀態 | 來源資料流 | 草稿 |
| 匯入狀態 | 歷程 | 草稿 |
| 整合式設定檔 | 資料集 | 已停用整合式設定檔 |
| 原則 | 資料治理原則 | 停用 |

### Adobe Journey Optimizer物件 {#abobe-journey-optimizer-objects}

下表列出 [!DNL Adobe Journey Optimizer] 目前沙箱工具支援的物件和限制：

| 平台 | 物件 | 詳細資料 |
| --- | --- | --- |
| [!DNL Adobe Journey Optimizer] | 對象 | 對象可以復製為歷程物件的相依物件。 您可以選取建立新受眾或重複使用目標沙箱中的現有受眾。 |
| [!DNL Adobe Journey Optimizer] | 綱要 | 歷程中使用的結構描述可以復製為相依物件。 您可以選取建立新結構描述，或重複使用目標沙箱中的現有結構描述。 |
| [!DNL Adobe Journey Optimizer] | 歷程 — 畫布詳細資料 | 畫布上的歷程呈現方式包含歷程中的物件，例如條件、動作、事件、讀取對象等，這些物件均已複製。 跳轉活動會從複製中排除。 |
| [!DNL Adobe Journey Optimizer] | 活動 | 將會複製歷程中使用的事件和事件詳細資訊。 它一律會在目標沙箱中建立新版本。 |
| [!DNL Adobe Journey Optimizer] | 動作 | 歷程中使用的電子郵件和推播訊息可以復製為相依物件。 用於訊息個人化的歷程欄位中使用的管道動作活動不會檢查完整性。 不會複製內容區塊。<br><br>可以複製歷程中使用的更新設定檔動作。 也會複製歷程中使用的自訂動作和動作詳細資訊。 它一律會在目標沙箱中建立新版本。 |

不會複製曲面（例如預設集）。 系統會根據訊息型別和表面名稱，自動選取目標沙箱上最接近的相符專案。 如果在目標沙箱上找不到表面，則表面複製將失敗，導致訊息複製失敗，因為訊息需要表面才能用於設定。 在這種情況下，至少需要為訊息的正確通道建立一個表面，副本才能運作。

匯出歷程時，不支援將自訂身分型別當做相依物件使用。

## 將物件匯出到套件中 {#export-objects}

>[!NOTE]
>
>所有匯出動作都會記錄在稽核記錄中。

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_remove_object"
>title="移除一個物件"
>abstract="若要從封裝中移除物件，請選取要移除的列，然後使用在選取時可供使用的刪除選項。 請注意，您無法從已發佈的封裝中移除物件。"

>[!CONTEXTUALHELP]
>id="platform_sandbox_package_expiry"
>title="套件有效期設定"
>abstract="封裝會設定為在草稿狀態中閒置一段時間後到期。 預設日期是從今天起的90天。 該日期會持續變更，直到該套件發佈為止。如果您在明天造訪處於草稿狀態的套件，則日期會往前移動+1天，除非您手動進行此設定。"

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_package_status"
>title="套件狀態"
>abstract="依預設，狀態設定為草稿。一旦套件發佈後，狀態將變更為已發佈。套件發佈後，就不能進行任何變更。"

>[!NOTE]
>
>只有當您擁有存取物件的許可權時，才能匯入套件。

此範例會記錄匯出結構描述並將其新增到封裝的程式。 您可以使用相同的程式匯出其他物件，例如資料集、歷程等等。

### 將物件加入至新封裝 {#add-object-to-new-package}

選取 **[!UICONTROL 方案]** 從左側導覽列中，然後選取 **[!UICONTROL 瀏覽]** 標籤，其中列出可用的結構描述。 接著，選取省略符號(`...`)，而下拉式清單則會顯示控制項。 選取 **[!UICONTROL 新增到封裝]** 下拉式清單中的。

![結構描述清單，顯示醒目提示的下拉式選單 [!UICONTROL 新增到封裝] 控制。](../images/ui/sandbox-tooling/add-to-package.png)

從 **[!UICONTROL 新增到封裝]** 對話方塊中，選取 **[!UICONTROL 建立新封裝]** 選項。 提供 [!UICONTROL 名稱] 適用於您的套件，以及選購的 [!UICONTROL 說明]，然後選取 **[!UICONTROL 新增]**.

![此 [!UICONTROL 新增到封裝] 對話方塊 [!UICONTROL 建立新封裝] 已選取並醒目提示 [!UICONTROL 新增].](../images/ui/sandbox-tooling/create-new-package.png)

您將返回 **[!UICONTROL 方案]** 環境。 您現在可以依照下列的後續步驟，將其他物件加入您建立的封裝。

### 將物件新增至現有封裝並發佈 {#add-object-to-existing-package}

若要檢視可用綱要的清單，請選取 **[!UICONTROL 方案]** 從左側導覽列中，然後選取 **[!UICONTROL 瀏覽]** 標籤。 接著，選取省略符號(`...`)來檢視下拉式選單中的控制選項。 選取 **[!UICONTROL 新增到封裝]** 下拉式清單中的。

![結構描述清單，顯示醒目提示的下拉式選單 [!UICONTROL 新增到封裝] 控制。](../images/ui/sandbox-tooling/add-to-package.png)

此 **[!UICONTROL 新增到封裝]** 對話方塊隨即顯示。 選取 **[!UICONTROL 現有封裝]** 選項，然後選取 **[!UICONTROL 封裝名稱]** 下拉式清單，然後選取所需的套件。 最後，選取 **[!UICONTROL 新增]** 以確認您的選擇。

![[!UICONTROL 新增到封裝] 對話方塊，顯示下拉式清單中選取的套件。](../images/ui/sandbox-tooling/add-to-existing-package.png)

會列出加入封裝的物件清單。 若要發佈套件並使其可匯入沙箱，請選取 **[!UICONTROL 發佈]**.

![封裝中的物件清單，醒目提示 [!UICONTROL 發佈] 選項。](../images/ui/sandbox-tooling/publish-package.png)

選取 **[!UICONTROL 發佈]** 以確認發佈套件。

![發佈套件確認對話方塊，醒目提示 [!UICONTROL 發佈] 選項。](../images/ui/sandbox-tooling/publish-package-confirmation.png)

>[!NOTE]
>
>發佈後，無法變更套件的內容。 為避免相容性問題，請確保已選取所有必要的資產。 如果必須進行變更，您必須建立新封裝。

您將返回 **[!UICONTROL 封裝]** 索引標籤中的 [!UICONTROL 沙箱] 環境，您可在其中檢視新發佈的套件。

![強調新發佈套件的沙箱套件清單。](../images/ui/sandbox-tooling/published-packages.png)

## 將套件匯入目標沙箱 {#import-package-to-target-sandbox}

>[!NOTE]
>
>所有匯入動作都會記錄在稽核記錄中。

若要將套件匯入目標沙箱，請導覽至「沙箱」 **[!UICONTROL 瀏覽]** 索引標籤並選取沙箱名稱旁邊的加號(+)選項。

![沙箱 **[!UICONTROL 瀏覽]** 索引標籤中反白匯入封裝選取專案。](../images/ui/sandbox-tooling/browse-sandboxes.png)

使用下拉式功能表，選取 **[!UICONTROL 封裝名稱]** 您想要匯入至目標沙箱。 新增選用專案 **[!UICONTROL 工作名稱]**，將用於日後的監視，然後選取 **[!UICONTROL 下一個]**.

![匯入詳細資訊頁面顯示 [!UICONTROL 封裝名稱] 下拉式清單選取專案](../images/ui/sandbox-tooling/import-package-to-sandbox.png)

此 [!UICONTROL 套件物件與相依性] 頁面提供此封裝中包含的所有資產清單。 系統會自動偵測成功匯入所選父物件所需的相依物件。

![此 [!UICONTROL 套件物件與相依性] 頁面會顯示封裝中包含的資產清單。](../images/ui/sandbox-tooling/package-objects-and-dependencies.png)

>[!NOTE]
>
>相依物件可以用目標沙箱中的現有物件取代，這可讓您重複使用現有物件，而不是建立新版本。 例如，當您匯入包含方案的套件時，可以重複使用目標沙箱中現有的自訂欄位群組和身分名稱空間。 或者，當您匯入包含歷程的套件時，可以重複使用目標沙箱中的現有區段。

若要使用現有物件，請選取相依物件旁的鉛筆圖示。 隨即顯示建立新或使用現有專案的選項。 選取 **[!UICONTROL 使用現有]**.

![此 [!UICONTROL 套件物件與相依性] 顯示相依物件選項的頁面 [!UICONTROL 新建] 和 [!UICONTROL 使用現有].](../images/ui/sandbox-tooling/use-existing-object.png)

此 **[!UICONTROL 欄位群組]** 對話方塊會顯示物件可用的欄位群組清單。 選取所需的欄位群組，然後選取 **[!UICONTROL 儲存]**.

![顯示在「 」上的欄位清單 [!UICONTROL 欄位群組] 對話方塊，反白顯示 [!UICONTROL 儲存] 選取。 ](../images/ui/sandbox-tooling/field-group-list.png)

您將返回 [!UICONTROL 套件物件與相依性] 頁面。 從這裡，選擇 **[!UICONTROL 完成]** 以完成套件匯入。

![此 [!UICONTROL 套件物件與相依性] 頁面顯示套件中包含的資產清單，醒目提示 [!UICONTROL 完成].](../images/ui/sandbox-tooling/finish-object-dependencies.png)

<!--
## Export and import an entire sandbox 

>[!NOTE]
>
>All export and import actions are recorded in the audit logs.

### Export an entire sandbox {#export-entire-sandbox}

To export an entire sandbox, navigate to the [!UICONTROL Sandboxes] **[!UICONTROL Packages]** tab and select **[!UICONTROL Create package]**.

![The [!UICONTROL Sandboxes] **[!UICONTROL Packages]** tab highlighting [!UICONTROL Create package].](../images/ui/sandbox-tooling/create-sandbox-package.png)

Select **[!UICONTROL Entire sandbox]** for the Type of package in the [!UICONTROL Create package] dialog. Provide a [!UICONTROL Package name] for your package and select the **[!UICONTROL Sandbox]** from the dropdown. Finally, select **[!UICONTROL Create]** to confirm your entries.

![The [!UICONTROL Create package] dialog showing completed fields and highlighting [!UICONTROL Create].](../images/ui/sandbox-tooling/create-package-dialog.png)

The package is created successfully, select **[!UICONTROL Publish]** to publish the package.

![List of sandbox packages highlighting the new published package.](../images/ui/sandbox-tooling/publish-entire-sandbox-packages.png)

You are returned to the **[!UICONTROL Packages]** tab in the [!UICONTROL Sandboxes] environment, where you can see the new published package.

### Import the entire sandbox package {#import-entire-sandbox-package}

To import the package into a target sandbox, navigate to the [!UICONTROL Sandboxes] **[!UICONTROL Browse]** tab and select the plus (+) option beside the sandbox name.

![The sandboxes **[!UICONTROL Browse]** tab highlighting the import package selection.](../images/ui/sandbox-tooling/browse-entire-package-sandboxes.png)

Using the dropdown menu, select the full sandbox using the **[!UICONTROL Package name]** dropdown. Add an optional **[!UICONTROL Job name]**, which will be used for future monitoring, then select **[!UICONTROL Next]**.

![The import details page showing the [!UICONTROL Package name] dropdown selection](../images/ui/sandbox-tooling/import-full-sandbox-package.png)

>[!NOTE]
>
>All objects are created as new from the package when importing an entire sandbox. The objects are not listed in the [!UICONTROL Package object and dependencies] page, as there can be multiples. An inline message is displayed, advising of object types that are not supported.

You are taken to the [!UICONTROL Package object and dependencies] page where you can see the number of objects and dependencies that are imported and excluded objects. From here, select **[!UICONTROL Import]** to complete the package import.

 ![The [!UICONTROL Package object and dependencies] page shows the inline message of object types not supported, highlighting [!UICONTROL Import].](../images/ui/sandbox-tooling/finish-dependencies-entire-sandbox.png)
-->

## 監視匯入工作並檢視匯入物件詳細資訊

若要檢視匯入的物件和匯入的詳細資訊，請瀏覽至 [!UICONTROL 沙箱] **[!UICONTROL 匯入]** 標籤並從清單中選取封裝。 或者，使用搜尋列來搜尋套件。

![沙箱 [!UICONTROL 匯入] 索引標籤會醒目顯示匯入套件選項。](../images/ui/sandbox-tooling/imports-tab.png)

### 檢視匯入的物件 {#view-imported-objects}

在 **[!UICONTROL 匯入]** 索引標籤中的 [!UICONTROL 沙箱] 環境，選取 **[!UICONTROL 檢視匯入的物件]** 從右邊的詳細資料窗格。

選取 **[!UICONTROL 檢視匯入的物件]** 從右邊的詳細資料窗格 **[!UICONTROL 匯入]** 索引標籤中的 [!UICONTROL 沙箱] 環境。

![沙箱 [!UICONTROL 匯入] 索引標籤反白顯示 [!UICONTROL 檢視匯入的物件] 右窗格中的選取範圍。](../images/ui/sandbox-tooling/view-imported-objects.png)

使用箭頭來展開物件，以檢視已匯入封裝的欄位完整清單。

![沙箱 [!UICONTROL 匯入的物件] 顯示匯入封裝的物件清單。](../images/ui/sandbox-tooling/expand-imported-objects.png)

### 檢視匯入詳細資料 {#view-import-details}

選取 **[!UICONTROL 檢視匯入詳細資料]** 從右側詳細資料窗格 **[!UICONTROL 匯入]** tab鍵。

![沙箱 [!UICONTROL 匯入] 索引標籤反白顯示 [!UICONTROL 檢視匯入詳細資料] 右窗格中的選取範圍。](../images/ui/sandbox-tooling/view-import-details.png)

此 **[!UICONTROL 匯入詳細資料]** 對話方塊會顯示匯入的詳細劃分。

![此 [!UICONTROL 匯入詳細資料] 顯示匯入詳細劃分的對話方塊。](../images/ui/sandbox-tooling/import-details.png)

>[!NOTE]
>
>匯入完成後，您會在Platform UI中收到通知。 您可以從警示圖示存取這些通知。 如果工作失敗，您可以從這裡導覽至疑難排解。

## 教學課程影片

以下影片旨在協助您瞭解沙箱工具，並概述如何建立新套件、發佈套件和匯入套件。

>[!VIDEO](https://video.tv.adobe.com/v/3424763/?learn=on)

## 後續步驟

本檔案會示範如何在Experience PlatformUI中使用沙箱工具功能。 如需沙箱的詳細資訊，請參閱 [沙箱使用手冊](../ui/user-guide.md).

如需使用沙箱API執行不同操作的步驟，請參閱 [沙箱開發人員指南](../api/getting-started.md). 如需Experience Platform中沙箱的整體概觀，請參閱 [概述檔案](../home.md).
