---
title: 沙箱工具
description: 順暢地匯出和匯入沙箱之間的沙箱設定。
source-git-commit: 900cb35f6cb758f145904666c709c60dc760eff2
workflow-type: tm+mt
source-wordcount: '1619'
ht-degree: 9%

---


# [!BADGE 測試版] 沙箱工具

>[!IMPORTANT]
>
>此 **沙箱工具** 以下所述功能僅適用於部分Beta版客戶。

>[!NOTE]
>
>沙箱工具是支援兩者的基本功能 [!DNL Real-Time Customer Data Platform] 和 [!DNL Journey Optimizer] 以提升開發週期效率和設定準確性。<br><br>您必須具備下列兩個角色型存取控制許可權，才能使用沙箱工具功能：<br>- `manage-sandbox` 或 `view-sandbox`<br>- `manage-package`

提高沙箱之間的設定準確性，並利用沙箱工具功能順暢地匯出和匯入沙箱之間的沙箱設定。 使用沙箱工具來減少實作程式的價值實現時間，並跨沙箱移動成功的設定。

您可以使用沙箱工具功能來選取不同的物件，並將它們匯出到套件中。 套件可以包含單一物件、多個物件或整個沙箱。 套件中包含的任何物件都必須來自相同沙箱。

## 沙箱工具支援的物件 {#supported-objects}

下表列出目前沙箱工具支援的物件：

| 平台 | 物件 |
| --- | --- |
| [!DNL Adobe Journey Optimizer] | 歷程 |
| 客戶資料平台 | 來源 |
| 客戶資料平台 | 區段 |
| 客戶資料平台 | 身分 |
| 客戶資料平台 | 原則 |
| 客戶資料平台 | 結構描述 |
| 客戶資料平台 | 資料集 |

已匯入下列物件，但處於草稿或已停用的狀態：

| 功能 | 物件 | 狀態 |
| --- | --- | --- |
| 匯入狀態 | 來源資料流 | 草稿 |
| 匯入狀態 | 歷程 | 草稿 |
| 整合式設定檔 | 綱要 | 停用 |
| 整合式設定檔 | 資料集 | 停用 |
| 原則 | 同意原則 | 停用 |
| 原則 | 資料治理原則 | 停用 |

下列邊緣案例不包含在套件中：

* 方案關係

## 將物件匯出至封裝 {#export-objects}

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_exit_package"
>title="儲存並退出套件"
>abstract="若要退出套件與儲存，使用者只需使用後退選項即可。"

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_remove_object"
>title="移除一個物件"
>abstract="使用者必須選取該行，然後使用刪除選項 (在選取後可用) 以移除該行。"

>[!CONTEXTUALHELP]
>id="platform_sandbox_package_expiry"
>title="套件有效期設定"
>abstract="該日期設定為從今天起 90 天。該日期會持續變更，直到該套件發佈為止。如果使用者明天造訪草稿狀態的套件，則日期會移動 +1 天 (除非使用者設定)。"

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

## 匯出和匯入整個沙箱

### 匯出整個沙箱 {#export-entire-sandbox}

若要匯出整個沙箱，請導覽至 [!UICONTROL 沙箱] **[!UICONTROL 封裝]** 標籤並選取 **[!UICONTROL 建立封裝]**.

![此 [!UICONTROL 沙箱] **[!UICONTROL 封裝]** 標籤反白顯示 [!UICONTROL 建立封裝].](../images/ui/sandbox-tooling/create-sandbox-package.png)

選取 **[!UICONTROL 整個沙箱]** 中的封裝型別 [!UICONTROL 建立封裝] 對話方塊。 提供 [!UICONTROL 封裝名稱] ，並選取 **[!UICONTROL Sandbox]** 下拉式清單中的。 最後，選取 **[!UICONTROL 建立]** 以確認您的輸入。

![此 [!UICONTROL 建立封裝] 顯示已完成欄位和醒目提示的對話方塊 [!UICONTROL 建立].](../images/ui/sandbox-tooling/create-package-dialog.png)

已成功建立封裝，請選取 **[!UICONTROL 發佈]** 以發佈套件。

![強調新發佈套件的沙箱套件清單。](../images/ui/sandbox-tooling/publish-entire-sandbox-packages.png)

您將返回 **[!UICONTROL 封裝]** 索引標籤中的 [!UICONTROL 沙箱] 環境，您可在其中檢視新發佈的套件。

### 匯入整個沙箱套件 {#import-entire-sandbox-package}

若要將套件匯入目標沙箱，請導覽至 [!UICONTROL 沙箱] **[!UICONTROL 瀏覽]** 索引標籤並選取沙箱名稱旁邊的加號(+)選項。

![沙箱 **[!UICONTROL 瀏覽]** 索引標籤中反白匯入封裝選取專案。](../images/ui/sandbox-tooling/browse-entire-package-sandboxes.png)

使用下拉式選單，使用 **[!UICONTROL 封裝名稱]** 下拉式清單。 新增選用專案 **[!UICONTROL 工作名稱]**，將用於日後的監視，然後選取 **[!UICONTROL 下一個]**.

![匯入詳細資訊頁面顯示 [!UICONTROL 封裝名稱] 下拉式清單選取專案](../images/ui/sandbox-tooling/import-full-sandbox-package.png)

>[!NOTE]
>
>匯入整個沙箱時，所有物件都會從套件建立為新物件。 物件並未列於 [!UICONTROL 套件物件與相依性] 頁面，因為可以有倍數。 此時會顯示內嵌訊息，告知不支援的物件型別。

您被帶到 [!UICONTROL 套件物件與相依性] 您可以在此頁面檢視匯入和排除物件的物件數目和相依性。 從這裡，選擇 **[!UICONTROL 匯入]** 以完成套件匯入。

![此 [!UICONTROL 套件物件與相依性] 頁面顯示不支援之物件型別的內嵌訊息，強調顯示 [!UICONTROL 匯入].](../images/ui/sandbox-tooling/finish-dependencies-entire-sandbox.png)

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

## 後續步驟

本檔案會示範如何在Experience PlatformUI中使用沙箱工具功能。 如需沙箱的詳細資訊，請參閱 [沙箱使用手冊](../ui/user-guide.md).

如需使用沙箱API執行不同操作的步驟，請參閱 [沙箱開發人員指南](../api/getting-started.md). 如需Experience Platform中沙箱的整體概觀，請參閱 [概述檔案](../home.md).
