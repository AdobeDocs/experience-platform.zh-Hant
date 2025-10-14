---
title: 沙箱工具
description: 順暢地匯出和匯入沙箱之間的沙箱設定。
exl-id: f1199ab7-11bf-43d9-ab86-15974687d182
source-git-commit: 76e1edf7ed78cffdb8f858d5685836c452dd6dd3
workflow-type: tm+mt
source-wordcount: '3728'
ht-degree: 5%

---

# 沙箱工具

>[!NOTE]
>
>沙箱工具是同時支援[!DNL Real-Time Customer Data Platform]和[!DNL Journey Optimizer]的基礎功能，可改善開發週期效率和設定準確性。<br><br>您必須擁有下列兩個角色型存取控制許可權，才能使用沙箱工具功能： <br>- `manage-sandbox`或`view-sandbox`<br>- `manage-package`

提高沙箱之間的設定準確性，並利用沙箱工具功能順暢地匯出和匯入沙箱之間的沙箱設定。 使用沙箱工具來減少實作程式的價值實現時間，並跨沙箱移動成功的設定。

您可以使用沙箱工具功能來選取不同的物件，並將它們匯出到套件中。 套件可以包含單一物件或多個物件。 <!--or an entire sandbox.-->封裝中包含的任何物件都必須來自相同的沙箱。

## 沙箱工具支援的物件 {#supported-objects}

沙箱工具功能可讓您將[!DNL Adobe Real-Time Customer Data Platform]和[!DNL Adobe Journey Optimizer]物件匯出至封裝。

### 即時客戶資料平台物件 {#real-time-cdp-objects}

>[!BEGINSHADEBOX]

### 多實體客群匯入的變更

透過[B2B架構升級](../../rtcdp/b2b-architecture-upgrade.md)，如果在升級前已發佈包含這些對象的套件，您將無法再匯入具有B2B屬性和體驗事件的多實體對象。 這些對象將無法匯入，且無法自動轉換為新架構。

若要解決此限制，您必須使用更新的對象建立新套件，然後使用沙箱工具將其匯入各自的目標沙箱。


>[!ENDSHADEBOX]

下表列出目前沙箱工具支援的[!DNL Adobe Real-Time Customer Data Platform]物件：

| 平台 | 物件 | 詳細資料 |
| --- | --- | --- |
| 客戶資料平台 | 來源 | <ul><li>出於安全原因，不會將來源帳戶認證復寫到目標沙箱中，而是需要手動更新。</li><li>依照預設，來源資料流會以草稿狀態複製。</li></ul> |
| 客戶資料平台 | 客群 | <ul><li>僅支援&#x200B;**[!UICONTROL 客戶對象]**&#x200B;型別&#x200B;**[!UICONTROL 細分服務]**。</li><li>用於同意和管理的現有標籤將複製到相同的匯入工作中。</li><li> 檢查合併原則相依性時，系統將在具有相同XDM類別的目標沙箱中自動選取預設合併原則。</li><li>如果在匯入對象時偵測到具有相同名稱的現有物件，沙箱工具將一律重複使用現有物件，以避免物件擴散。</li></ul> |
| 客戶資料平台 | 身分識別 | <ul><li>系統將在Target沙箱中建立時自動刪除重複的Adobe標準身分名稱空間。</li><li>對象規則中的所有屬性都已在聯合結構描述中啟用時，才能複製對象。 必須先移動並啟用統一設定檔的必要結構描述。</li></ul> |
| 客戶資料平台 | 結構描述/欄位群組/資料型別 | <ul><li>用於同意和管理的現有標籤將複製到相同的匯入工作中。</li><li>您可以靈活地匯入未啟用「統一設定檔」選項的結構描述。 封裝中不包含結構描述關聯邊緣案例。</li><li>如果在匯入結構描述/欄位群組時偵測到具有相同名稱的現有物件，沙箱工具將一律重複使用現有物件，以避免物件擴散。</li></ul> |
| 客戶資料平台 | 資料集 | 資料集複製時會預設停用整合設定檔設定。 |
| 客戶資料平台 | 同意和治理原則 | 將使用者建立的自訂原則新增至套件，並橫跨沙箱移動這些原則。 |

下列物件已匯入，但處於草稿或已停用的狀態：

| 功能 | 物件 | 狀態 |
| --- | --- | --- |
| 匯入狀態 | Source資料流 | 草稿 |
| 匯入狀態 | 歷程 | 草稿 |
| 整合式設定檔 | 資料集 | 已停用整合式設定檔 |
| 原則 | 資料治理原則 | 停用 |

### Adobe Journey Optimizer物件 {#abobe-journey-optimizer-objects}

下表列出目前沙箱工具支援的[!DNL Adobe Journey Optimizer]物件與限制：

| 平台 | 物件 | 支援的相依物件 | 詳細資料 |
| --- | --- | --- | --- |
| [!DNL Adobe Journey Optimizer] | 客群 | | 對象可以復製為歷程物件的相依物件。 您可以選取建立新受眾或重複使用目標沙箱中的現有受眾。 |
| [!DNL Adobe Journey Optimizer] | 結構描述 | | 歷程中使用的結構描述可以復製為相依物件。 您可以選取建立新結構描述，或重複使用目標沙箱中的現有結構描述。 |
| [!DNL Adobe Journey Optimizer] | 合併原則 | | 歷程中使用的合併原則可以復製為相依物件。 在目標沙箱中，您&#x200B;**無法**&#x200B;建立新的合併原則，您只能使用現有的合併原則。 |
| [!DNL Adobe Journey Optimizer] | 歷程 | 歷程中使用的下列物件會復製為相依物件。 在匯入工作流程期間，您可以選擇&#x200B;**[!UICONTROL 建立新的]**&#x200B;或&#x200B;**[!UICONTROL 使用現有的]**： <ul><li>客群</li><li>畫布詳細資訊</li><li>內容範本</li><li>自訂動作</li><li>資料來源</li><li>活動</li><li>欄位群組</li><li>片段</li><li>結構描述</li></ul> | 當您在匯入程式期間選取&#x200B;**[!UICONTROL 使用現有]**&#x200B;將歷程複製到另一個沙箱時，您選擇的現有自訂動作&#x200B;**必須**&#x200B;與來源自訂動作完全相符。 如果兩者不相符，新歷程將產生無法解決的錯誤。<br>系統複製歷程中使用的事件和事件詳細資訊，並在目標沙箱中建立新版本。 |
| [!DNL Adobe Journey Optimizer] | 動作 | | 歷程中使用的電子郵件和推播訊息可以復製為相依物件。 用於訊息個人化的歷程欄位中使用的管道動作活動不會檢查完整性。 不會複製內容區塊。<br><br>可以複製歷程中使用的更新設定檔動作。 自訂動作可獨立新增至套件。 歷程中使用的動作詳細資料也會複製。 它一律會在目標沙箱中建立新版本。 |
| [!DNL Adobe Journey Optimizer] | 自訂動作 |  | 自訂動作可獨立新增至套件。 將自訂動作指派給歷程後，就無法再編輯它。 若要更新自訂動作，您應： <ul><li>在移轉歷程之前移動自訂動作</li><li>更新移轉後自訂動作的設定（例如請求標頭、查詢引數和驗證）</li><li>使用您在第一個步驟中新增的自訂動作移轉歷程物件</li></ul> |
| [!DNL Adobe Journey Optimizer] | 內容範本 | | 內容範本可以復製為歷程物件的相依物件。 獨立範本可讓您輕鬆在Journey Optimizer行銷活動和歷程中重複使用自訂內容。 |
| [!DNL Adobe Journey Optimizer] | 片段 | 所有巢狀片段。 | 片段可以復製為歷程物件的相依物件。 片段是可重複使用的元件，可在各個Journey Optimizer促銷活動和歷程的一封或多封電子郵件中參考。 |
| [!DNL Adobe Journey Optimizer] | 行銷活動 | 促銷活動中使用的下列物件會復製為相依物件： <ul><li>行銷活動</li><li>客群</li><li>結構描述</li><li>內容範本</li><li>片段</li><li>訊息/內容</li><li>管道設定</li><li>統一的決定物件</li><li>實驗設定/變體</li></ul> | <ul><li>行銷活動可與所有與設定檔、對象、結構、內嵌訊息和相依物件相關的專案一起複製。 有些專案不會複製，例如資料使用標籤和語言設定。 如需無法複製的物件完整清單，請參閱[將物件匯出至另一個沙箱](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer/using/configuration/copy-objects-to-sandbox)指南。</li><li>如果存在相同的設定，系統將自動檢測並重新使用目標沙箱中的現有通道設定物件。 如果找不到相符的設定，則在匯入期間會跳過頻道設定，使用者必須手動更新此歷程的目標沙箱中的頻道設定。</li><li>使用者可重複使用目標沙箱中的現有實驗與對象，作為所選行銷活動的相依物件。</li></ul> |
| [!DNL Adobe Journey Optimizer] | 決策 | 複製決策物件之前，目標沙箱中必須存在下列物件： <ul><li>用於決策物件的設定檔屬性</li><li>自訂選件屬性的欄位群組</li><li>用於跨規則、排名或上限之內容屬性的資料串流結構。</li></ul> | <ul><li>目前不支援複製使用AI模型的排名公式。</li><li>決定專案（優惠專案）不會自動納入。 若要確保它們已傳輸，請使用&#x200B;**新增至封裝**&#x200B;選項手動新增。</li><li>使用選擇策略的原則需要在複製過程中手動新增關聯的決定專案。 使用手動或遞補決定專案的原則會自動將這些專案作為直接相依性納入。</li><li>必須先複製決定專案，然後再複製任何其他相關物件。</li></ul> |

用於決策物件的設定檔屬性，
自訂選件屬性的欄位群組，
用於跨規則、排名或上限之內容屬性的資料串流結構。

不會複製曲面（例如預設集）。 系統會根據訊息型別和表面名稱，自動選取目標沙箱上最接近的相符專案。 如果在目標沙箱上找不到表面，則表面複製將失敗，導致訊息複製失敗，因為訊息需要表面才能用於設定。 在這種情況下，至少需要為訊息的正確通道建立一個表面，副本才能運作。

匯出歷程時，不支援將自訂身分型別當做相依物件使用。

## 將物件匯出到套件中 {#export-objects}

>[!NOTE]
>
>所有匯出動作都會記錄在稽核記錄中。

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_remove_object"
>title="移除一個物件"
>abstract="若要從套件中刪除物件，請選取要刪除的行，然後使用刪除選項 (選取時可用)。請注意，您無法從已發佈的套件中刪除物件。"

>[!CONTEXTUALHELP]
>id="platform_sandbox_package_expiry"
>title="套件有效期設定"
>abstract="套件在草稿狀態一段時間不活動後將過期。預設日期設定為從今天起 90 天。該日期會持續變更，直到該套件發佈為止。如果您明天造訪草稿狀態的套件，則日期會移動 +1 天 (除非您以手動設定)。"

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_package_status"
>title="套件狀態"
>abstract="依預設，狀態設定為草稿。一旦套件發佈後，狀態將變更為已發佈。套件發佈後，就不能進行任何變更。"

>[!NOTE]
>
>只有當您擁有存取物件的許可權時，才能匯入套件。

此範例會記錄匯出結構描述並將其新增到封裝的程式。 您可以使用相同的程式匯出其他物件，例如資料集、歷程等等。

### 將物件加入至新封裝 {#add-object-to-new-package}

從左側導覽選取&#x200B;**[!UICONTROL 結構描述]**，然後選取&#x200B;**[!UICONTROL 瀏覽]**&#x200B;標籤，其中會列出可用的結構描述。 接著，選取所選結構描述旁邊的省略符號(`...`)，下拉式清單就會顯示控制項。 從下拉式清單中選取&#x200B;**[!UICONTROL 新增到封裝]**。

![結構描述清單，顯示反白顯示[!UICONTROL 新增至封裝]控制項的下拉式功能表。](../images/ui/sandbox-tooling/add-to-package.png)

從&#x200B;**[!UICONTROL 新增至封裝]**&#x200B;對話方塊中，選取&#x200B;**[!UICONTROL 建立新封裝]**&#x200B;選項。 提供封裝的[!UICONTROL Name]和選用的[!UICONTROL 描述]，然後選取&#x200B;**[!UICONTROL 新增]**。

![已選取[!UICONTROL 建立新封裝]並醒目提示[!UICONTROL 新增]的[!UICONTROL 新增至封裝]對話方塊。](../images/ui/sandbox-tooling/create-new-package.png)

您返回到&#x200B;**[!UICONTROL 結構描述]**&#x200B;環境。 您現在可以依照下列的後續步驟，將其他物件加入您建立的封裝。

### 將物件新增至現有封裝並發佈 {#add-object-to-existing-package}

若要檢視可用的結構描述清單，請從左側導覽選取&#x200B;**[!UICONTROL 結構描述]**，然後選取&#x200B;**[!UICONTROL 瀏覽]**&#x200B;索引標籤。 接著，選取選取的結構描述旁邊的省略符號(`...`)，在下拉式功能表中檢視控制選項。 從下拉式清單中選取&#x200B;**[!UICONTROL 新增到封裝]**。

![結構描述清單，顯示反白顯示[!UICONTROL 新增至封裝]控制項的下拉式功能表。](../images/ui/sandbox-tooling/add-to-package.png)

**[!UICONTROL 新增至封裝]**&#x200B;對話方塊就會顯示。 選取「**[!UICONTROL 現有封裝]**」選項，然後選取「**[!UICONTROL 封裝名稱]**」下拉式清單，並選取所需的封裝。 最後，選取&#x200B;**[!UICONTROL 新增]**&#x200B;以確認您的選擇。

![[!UICONTROL 新增到封裝]對話方塊，顯示下拉式清單中選取的封裝。](../images/ui/sandbox-tooling/add-to-existing-package.png)

會列出加入封裝的物件清單。 若要發佈封裝並使其可匯入沙箱，請選取&#x200B;**[!UICONTROL 發佈]**。

![封裝中的物件清單，醒目顯示[!UICONTROL 發佈]選項。](../images/ui/sandbox-tooling/publish-package.png)

選取&#x200B;**[!UICONTROL 發佈]**&#x200B;以確認發佈封裝。

![發佈封裝確認對話方塊，醒目提示[!UICONTROL 發佈]選項。](../images/ui/sandbox-tooling/publish-package-confirmation.png)

>[!NOTE]
>
>發佈後，無法變更套件的內容。 為避免相容性問題，請確保已選取所有必要的資產。 如果必須進行變更，您必須建立新封裝。

您會回到&#x200B;**[!UICONTROL 沙箱]**&#x200B;環境中的[!UICONTROL 套件]索引標籤，您可以在其中看到新發佈的套件。

![醒目提示新發佈封裝的沙箱封裝清單。](../images/ui/sandbox-tooling/published-packages.png)

## 將套件匯入目標沙箱 {#import-package-to-target-sandbox}

>[!NOTE]
>
>所有匯入動作都會記錄在稽核記錄中。

若要將套件匯入目標沙箱，請導覽至沙箱&#x200B;**[!UICONTROL 瀏覽]**&#x200B;標籤，並選取沙箱名稱旁邊的加號(+)選項。

![沙箱&#x200B;**[!UICONTROL 瀏覽]**&#x200B;索引標籤醒目提示匯入封裝選取專案。](../images/ui/sandbox-tooling/browse-sandboxes.png)

使用下拉式功能表，選取您要匯入目標沙箱的&#x200B;**[!UICONTROL 封裝名稱]**。 新增將用於未來監視的&#x200B;**[!UICONTROL 工作名稱]**。 依預設，在匯入套件的結構描述時，統一設定檔將會停用。 切換&#x200B;**為設定檔**&#x200B;啟用結構描述以啟用此設定，然後選取&#x200B;**[!UICONTROL 下一步]**。

![匯入詳細資訊頁面顯示[!UICONTROL 封裝名稱]下拉式清單選項](../images/ui/sandbox-tooling/import-package-to-sandbox.png)

[!UICONTROL 封裝物件與相依性]頁面提供此封裝中包含的所有資產清單。 系統會自動偵測成功匯入所選父物件所需的相依物件。 任何遺失的屬性都會顯示在頁面頂端。 選取「**[!UICONTROL 檢視詳細資料]**」以取得更詳細的劃分。

![[!UICONTROL 封裝物件和相依性]頁面顯示遺漏的屬性。](../images/ui/sandbox-tooling/missing-attributes.png)

>[!NOTE]
>
>相依物件可以用目標沙箱中的現有物件取代，這可讓您重複使用現有物件，而不是建立新版本。 例如，當您匯入包含方案的套件時，可以重複使用目標沙箱中現有的自訂欄位群組和身分名稱空間。 或者，當您匯入包含歷程的套件時，可以重複使用目標沙箱中的現有區段。
>
>沙箱工具目前不支援更新或覆寫現有物件。 您可以選擇建立新物件，或繼續使用現有物件而不進行修改。 如果偵測到具有相同名稱的現有物件，沙箱工具將一律重複使用現有物件，即使您選取[!UICONTROL 建立新的]選項以避免物件擴散。

若要使用現有物件，請選取相依物件旁的鉛筆圖示。

![封裝物件與相依性[!UICONTROL 頁面會顯示包含在封裝中的資產清單。]](../images/ui/sandbox-tooling/package-objects-and-dependencies.png)

隨即顯示建立新或使用現有專案的選項。 選取&#x200B;**[!UICONTROL 使用現有的]**。

![顯示相依物件選項[!UICONTROL 建立新的]和[!UICONTROL 使用現有的]的[!UICONTROL 封裝物件和相依性]頁面。](../images/ui/sandbox-tooling/use-existing-object.png)

**[!UICONTROL 欄位群組]**&#x200B;對話方塊會顯示物件可用的欄位群組清單。 選取所需的欄位群組，然後選取&#x200B;**[!UICONTROL 儲存]**。

![&#x200B; [!UICONTROL 欄位群組]對話方塊上顯示的欄位清單，醒目顯示[!UICONTROL 儲存]選取專案。](../images/ui/sandbox-tooling/field-group-list.png)

您返回到[!UICONTROL 封裝物件和相依性]頁面。 從這裡，選取&#x200B;**[!UICONTROL 完成]**&#x200B;以完成封裝匯入。

![封裝物件和相依性[!UICONTROL 頁面會顯示包含在封裝中的資產清單，並醒目提示]完成[!UICONTROL 。]](../images/ui/sandbox-tooling/finish-object-dependencies.png)

## 匯出和匯入整個沙箱

>[!NOTE]
>
>目前，匯出或匯入整個沙箱時僅支援Real-time Customer Data Platform物件。 目前不支援歷程之類的Adobe Journey Optimizer物件。

您可以將所有支援的物件型別匯出至完整的沙箱套件，然後跨各種沙箱匯入套件以複製物件設定。 例如，此功能可讓您：

- 如果您需要重設沙箱，請重新匯入沙箱以重新產生物件的所有設定
- 將套件匯入其他沙箱，並將其用作Blueprint沙箱以加快開發流程。

### 匯出整個沙箱 {#export-entire-sandbox}

若要匯出整個沙箱，請瀏覽至[!UICONTROL 沙箱] **[!UICONTROL 套件]**&#x200B;索引標籤，並選取&#x200B;**[!UICONTROL 建立套件]**。

![&#x200B; [!UICONTROL 沙箱] **[!UICONTROL 封裝]**&#x200B;索引標籤醒目提示[!UICONTROL 建立封裝]。](../images/ui/sandbox-tooling/create-sandbox-package.png)

在&#x200B;**[!UICONTROL 建立封裝]**&#x200B;對話方塊中，選取[!UICONTROL 封裝]的[!UICONTROL 整個沙箱]。 為您的新封裝提供[!UICONTROL 封裝名稱]，並從下拉式清單中選取&#x200B;**[!UICONTROL 沙箱]**。 最後，選取&#x200B;**[!UICONTROL 建立]**&#x200B;以確認您的專案。

![&#x200B; [!UICONTROL 建立封裝]對話方塊顯示已完成的欄位並醒目提示[!UICONTROL 建立]。](../images/ui/sandbox-tooling/create-package-dialog.png)

已成功建立封裝，請選取&#x200B;**[!UICONTROL 發佈]**&#x200B;以發佈封裝。

![醒目提示新發佈封裝的沙箱封裝清單。](../images/ui/sandbox-tooling/publish-entire-sandbox-packages.png)

您會回到&#x200B;**[!UICONTROL 沙箱]**&#x200B;環境中的[!UICONTROL 套件]索引標籤，您可以在其中看到新發佈的套件。

### 匯入整個沙箱套件 {#import-entire-sandbox-package}

>[!NOTE]
>
>所有物件都會當作新物件匯入目標沙箱中。 最佳實務是將完整的沙箱套件匯入空的沙箱。

若要將套件匯入目標沙箱，請瀏覽至[!UICONTROL 沙箱] **[!UICONTROL 瀏覽]**&#x200B;標籤，並選取沙箱名稱旁的加號(+)選項。

![沙箱&#x200B;**[!UICONTROL 瀏覽]**&#x200B;索引標籤醒目提示匯入封裝選取專案。](../images/ui/sandbox-tooling/browse-entire-package-sandboxes.png)

使用下拉式功能表，使用&#x200B;**[!UICONTROL 封裝名稱]**&#x200B;下拉式功能表選取完整沙箱。 新增將用於未來監視的&#x200B;**[!UICONTROL 工作名稱]**&#x200B;和選用的&#x200B;**[!UICONTROL 工作描述]**，然後選取&#x200B;**[!UICONTROL 下一步]**。

![匯入詳細資訊頁面顯示[!UICONTROL 封裝名稱]下拉式清單選項](../images/ui/sandbox-tooling/import-full-sandbox-package.png)

>[!NOTE]
>
>您必須擁有封裝中包含之所有物件的完整許可權。 如果您沒有許可權，匯入作業將會失敗並顯示錯誤訊息。

您會進入[!UICONTROL 封裝物件與相依性]頁面，您可以在此頁面檢視匯入和排除物件的物件與相依性數目。 從這裡，選取&#x200B;**[!UICONTROL 匯入]**&#x200B;以完成封裝匯入。

![[!UICONTROL 封裝物件與相依性]頁面顯示不支援之物件型別的內嵌訊息，並醒目提示[!UICONTROL 匯入]。](../images/ui/sandbox-tooling/finish-dependencies-entire-sandbox.png)

留出一些時間讓匯入完成。 完成時間會因封裝中的物件數目而異。 您可以從[!UICONTROL 沙箱] **[!UICONTROL 工作]**&#x200B;索引標籤監視匯入工作。

## 監視匯入詳細資料 {#view-import-details}

若要檢視匯入的詳細資料，請瀏覽至[!UICONTROL 沙箱] **[!UICONTROL 工作]**&#x200B;標籤，然後從清單中選取封裝。 或者，使用搜尋列來搜尋套件。

![沙箱[!UICONTROL 工作]索引標籤會醒目提示匯入套件選項。](../images/ui/sandbox-tooling/imports-tab.png)

<!--### View imported objects {#view-imported-objects}

On the **[!UICONTROL Jobs]** tab in the [!UICONTROL Sandboxes] environment, select **[!UICONTROL View imported objects]** from the right details pane.

Select **[!UICONTROL View imported objects]** from the right details pane on the **[!UICONTROL Jobs]** tab in the [!UICONTROL Sandboxes] environment.

![The sandboxes [!UICONTROL Imports] tab highlights the [!UICONTROL View imported objects] selection in the right pane.](../images/ui/sandbox-tooling/view-imported-objects.png)

Use the arrows to expand objects to view the full list of fields that have been imported into the package.

![The sandboxes [!UICONTROL Imported objects] showing a list of objects imported into the package.](../images/ui/sandbox-tooling/expand-imported-objects.png)-->

在沙箱環境的&#x200B;**[!UICONTROL 工作]**&#x200B;索引標籤中，從右邊的詳細資料窗格中選取&#x200B;**[!UICONTROL 檢視匯入摘要]**。

![沙箱[!UICONTROL 匯入]索引標籤會在右窗格中反白顯示[!UICONTROL 檢視匯入詳細資料]選項。](../images/ui/sandbox-tooling/view-import-details.png)

**[!UICONTROL 匯入摘要]**&#x200B;對話方塊會顯示匯入的劃分以及進度百分比。

>[!NOTE]
>
>您可以導覽至特定的詳細目錄頁面，以檢視物件清單。

![顯示匯入詳細資料的[!UICONTROL 匯入詳細資料]對話方塊。](../images/ui/sandbox-tooling/import-details.png)

匯入完成時，會在Experience Platform UI中收到通知。 您可以從警示圖示存取這些通知。 如果工作失敗，您可以從這裡導覽至疑難排解。

## 透過沙箱工具傳輸沙箱間的反複物件設定更新 {#move-configs}

您可以使用沙箱工具在不同沙箱之間傳輸物件設定。 先前，您必須手動重新建立或重新匯入物件（例如結構描述、欄位群組和資料型別）的設定更新，才能傳輸到其他沙箱。 透過此功能，您可以使用沙箱工具來加速工作流程，並透過在不同沙箱之間順暢傳輸您的設定更新來減少潛在的錯誤。

![顯示如何在沙箱之間移動更新的圖表。](../images/ui/sandbox-tooling/move-updates-diagram.png)

>[!TIP]
>
> 嘗試在不同沙箱之間傳輸物件設定之前，請確定您具備以下先決條件。
>
>- 存取沙箱工具的適當許可權。
>- 在您的來源沙箱中新建立或更新後的物件（例如結構描述）。

>[!BEGINSHADEBOX]

### 支援的更新作業物件型別

以下是支援更新的物件型別：

- 結構描述
- 欄位群組
- 資料類型

| 支援的更新 | 不支援的更新 |
| --- | --- |
| <ul><li>將新欄位/欄位群組新增至資源。</li><li>將必填欄位設為選用。</li><li>引入新的必填欄位。</li><li>引入新的關係欄位。</li><li>引入新的身分欄位。</li><li>變更資源的顯示名稱和說明。</li></ul> | <ul><li>移除先前定義的欄位。</li><li>在針對Real-time Customer Profile啟用結構描述時，重新定義現有欄位。</li><li>移除或限制先前支援的欄位值。</li><li>將現有欄位移動到結構樹中的不同位置 — 這將在目標沙箱中建立一個新欄位，但不會移除上一個欄位。</li><li>啟用或停用結構描述以參與設定檔 — 比較時將略過此操作。</li><li>存取控制標籤。</li></ul> |

>[!ENDSHADEBOX]

請依照下列步驟瞭解如何使用沙箱工具來將您的物件設定傳輸到不同的沙箱。

### 先前匯入的物件

如果您的使用案例涉及來源沙箱中需要設定更新的現有物件，請在已封裝並匯入其他沙箱後，按照以下步驟操作。

首先，更新來源沙箱中的物件。 例如，導覽至&#x200B;**[!UICONTROL 結構描述]**&#x200B;工作區，選取您的結構描述，然後新增欄位群組。

![具有更新結構描述的結構描述工作區。](../images/ui/sandbox-tooling/update-schema.png)

更新結構描述後，請導覽至&#x200B;**[!UICONTROL 沙箱]**，選取&#x200B;**[!UICONTROL 封裝]**，然後找出您現有的封裝。

![已選取套件的沙箱工具介面](../images/ui/sandbox-tooling/select-package.png)

使用套件介面來驗證您的變更。 選取&#x200B;**[!UICONTROL 檢查更新]**&#x200B;以檢視封裝中成品的任何變更。 接著，選取&#x200B;**[!UICONTROL 檢視diff]**&#x200B;以接收針對成品進行的所有變更的詳細摘要。

![已選取包含檢視差異按鈕的封裝介面。](../images/ui/sandbox-tooling/view-diff.png)

[!UICONTROL 檢視diff]介面出現。 如需來源和目標成品的相關資訊，以及套用至這些成品的變更，請參閱此收費專案。

![變更摘要。](../images/ui/sandbox-tooling/summary-of-changes.png)

在此步驟中，您也可以選取[!UICONTROL 使用AI摘要]，以取得所有變更的逐步摘要。

![已啟用AI的摘要。](../images/ui/sandbox-tooling/ai-summary.png)

準備就緒後，請選取&#x200B;**[!UICONTROL 更新封裝]**，然後在出現的快顯視窗中選取&#x200B;**[!UICONTROL 確認]**。 工作完成後，您可以重新整理頁面，並選取&#x200B;**[!UICONTROL 檢視歷程記錄]**&#x200B;以驗證封裝的版本。

![確認視窗。](../images/ui/sandbox-tooling/confirm-changes.png)

若要匯入您的變更，請導覽回[!UICONTROL 套件]目錄，並選取套件旁邊的省略符號(`...`)，然後選取&#x200B;**[!UICONTROL 匯入套件]**。 Experience Platform自動選取[!UICONTROL 更新現有物件]。 驗證變更，然後選取&#x200B;**[!UICONTROL 完成]**。

>[!NOTE]
>
>在此工作流程中，所有相依物件都會自動更新到目標沙箱中。

![匯入目標介面。](../images/ui/sandbox-tooling/import-objective.png)

若要進一步驗證匯入程式，請導覽至您的目標沙箱，並從該沙箱中手動檢視更新的物件。

### 在目標沙箱中手動建立的物件

如果您的使用案例涉及將設定變更套用至在不同沙箱中手動建立的物件，請按照以下步驟操作。

首先，使用更新後的物件建立並發佈新套件。

接下來，將您的套件匯入至目標沙箱，其中包含您也要更新的物件。 在匯入程式期間，選取&#x200B;**[!UICONTROL 更新現有物件]**，然後使用物件導覽器手動選取要套用更新的目標物件。

>[!NOTE]
>
>- 可選擇在不同的沙箱中為相依物件選取目標對應。 如果未選取任何專案，則會建立新的專案。
>- 對於身分名稱空間，如果需要在目標沙箱中重複使用現有身分，系統會自動偵測是否需要建立新身分。

![要更新的目標物件的匯入目標介面（含預留位置）。](../images/ui/sandbox-tooling/update-existing-objects.png)

識別要更新的目標物件之後，請選取&#x200B;**[!UICONTROL 完成]**。

![選取的目標物件。](../images/ui/sandbox-tooling/add-updated-objects.png)

## 教學課程影片

以下影片旨在協助您瞭解沙箱工具，並概述如何建立新套件、發佈套件和匯入套件。

>[!VIDEO](https://video.tv.adobe.com/v/3446101/?learn=on&captions=chi_hant)

## 後續步驟

本檔案會示範如何使用Experience Platform UI中的沙箱工具功能。 如需沙箱的相關資訊，請參閱[沙箱使用手冊](../ui/user-guide.md)。

如需使用沙箱API執行不同作業的步驟，請參閱[沙箱開發人員指南](../api/getting-started.md)。 如需Experience Platform中沙箱的整體概觀，請參閱[概觀檔案](../home.md)。
