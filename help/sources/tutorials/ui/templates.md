---
description: 瞭解如何在Adobe Experience PlatformUI中使用模板來加速B2B資料的資料接收過程。
title: 使用UI中的模板建立源資料流
badge1: "Beta"
exl-id: 48aa36ca-656d-4b9d-954c-48c8da9df1e9
source-git-commit: 91d6832231d75c9dd23e91a5f1152eac61558fc5
workflow-type: tm+mt
source-wordcount: '1554'
ht-degree: 9%

---

# 使用UI中的模板建立源資料流

>[!IMPORTANT]
>
>模板在Beta中，並受以下源支援：
>
>* [[!DNL Marketo Engage]](../../connectors/adobe-applications/marketo/marketo.md)
>* [[!DNL Microsoft Dynamics]](../../connectors/crm/ms-dynamics.md)
>* [[!DNL Salesforce]](../../connectors/crm/salesforce.md)
>
>文檔和功能可能會更改。

Adobe Experience Platform提供了預配置的模板，您可以使用這些模板加快資料接收過程。 模板包括自動生成的資產，如方案、資料集、標識、映射規則、標識命名空間和資料流，在將資料從源引入Experience Platform時可以使用這些資產。

使用模板，您可以：

* 通過加快模板化資產建立，縮短接收的時間到價值。
* 將手動資料接收過程中可能發生的錯誤降至最低。
* 隨時更新自動生成的資產以適合您的使用情形。

以下教程提供了如何在平台UI中使用模板的步驟。

## 快速入門

本教程需要對以下Experience Platform組成部分進行有效理解：

* [源](../../home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。
* [[!DNL Experience Data Model (XDM)] 系統](../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化框架。
* [沙箱](../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

## 在平台UI中使用模板 {#use-templates-in-the-platform-ui}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_accounttype"
>title="選取商業類型"
>abstract="為您的使用案例選取適合的商業類型。您的存取權限可能會依據您的即時客戶資料平台訂閱帳戶而不同。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html" text="Real-Time CDP 概觀"

在平台UI中，選擇 **[!UICONTROL 源]** 從左側導航 [!UICONTROL 源] 工作區，並查看Experience Platform中可用的源目錄。

使用 *[!UICONTROL 類別]* 按類別篩選源。 或者，在搜索欄中輸入源名稱以從目錄中查找特定源。

轉到 [!UICONTROL Adobe應用程式] 類別以查看 [!DNL Marketo Engage] 源卡，然後選擇 [!UICONTROL 添加資料] 開始。

![突出顯示Marketo Engage源的源工作區的目錄。](../../images/tutorials/templates/catalog.png)

此時將出現一個彈出窗口，為您提供瀏覽模板或使用現有架構和資料集的選項。

* **瀏覽模板**:源模板自動為您建立具有映射規則的架構、標識、資料集和資料流。 您可以根據需要自定義這些資產。
* **使用我的現有資產**:使用您建立的現有資料集和架構接收資料。 如果需要，還可以建立新資料集和架構。

要使用自動生成的資產，請選擇 **[!UICONTROL 瀏覽模板]** ，然後選擇 **[!UICONTROL 選擇]**。

![一個彈出窗口，其中包含瀏覽模板或使用現有資產的選項。](../../images/tutorials/templates/browse-templates.png)

### 驗證

此時將顯示驗證步驟，提示您建立新帳戶或使用現有帳戶。

>[!BEGINTABS]

>[!TAB 使用現有帳戶]

要使用現有帳戶，請選擇 [!UICONTROL 現有帳戶] 然後，從顯示的清單中選擇要使用的帳戶。

![現有帳戶的選擇頁面，其中包含您可以訪問的現有帳戶清單。](../../images/tutorials/templates/existing-account.png)

>[!TAB 建立新帳戶]

要建立新帳戶，請選擇 **[!UICONTROL 新帳戶]**，然後提供源連接詳細資訊和帳戶身份驗證憑據。 完成後，選擇 **[!UICONTROL 連接到源]** 讓新連接有時間建立。

![具有源連接詳細資訊和帳戶驗證憑據的新帳戶的驗證頁。](../../images/tutorials/templates/new-account.png)

>[!ENDTABS]

### 選擇模板

根據您選擇的業務類型，將顯示模板清單。 選擇預覽表徵圖 ![預覽表徵圖](../../images/tutorials/templates/preview-icon.png) 的子菜單。

![高亮顯示預覽表徵圖的模板清單。](../../images/tutorials/templates/templates.png)

此時將出現預覽窗口，允許您瀏覽和檢查模板中的示例資料。 完成後，選擇 **[!UICONTROL 明白了]**。

![預覽示例資料窗口。](../../images/tutorials/templates/preview-sample-data.png)

接下來，從清單中選擇要使用的模板。 您可以選擇多個模板並同時建立多個資料流。 但是，每個帳戶只能使用一個模板。 選擇模板後，選擇 **[!UICONTROL 完成]** 讓這些資產能產生一些時間。

如果從可用模板清單中選擇一個或部分項，則仍將生成所有B2B架構和標識命名空間，以確保正確配置架構間的B2B關係。

>[!NOTE]
>
>已使用的模板將從選擇中禁用。

![已選擇Opportunity Contact Role模板的模板清單。](../../images/tutorials/templates/select-template.png)

### 設定計畫

的 [!DNL Microsoft Dynamics] 和 [!DNL Salesforce] 源都支援調度資料流。

使用調度介面為資料流配置接收調度。 將攝取頻率設定為 **一次** 產生一次性攝取。

![Dynamics和Salesforce模板的計畫介面。](../../images/tutorials/templates/schedule.png)

或者，可以將攝取頻率設定為 **分鐘**。 **小時**。 **日**&#x200B;或 **周**。 如果為多個接收計畫資料流，則必須設定一個時間間隔以在每個接收之間建立一個時間幀。 例如，接收頻率設定為 **小時** 間隔設定為 **15** 意味著資料流計畫在每個 **15小時**。

在此步驟中，您還可以 **回填** 並為資料增量接收定義一列。 回填用於接收歷史資料，而您為增量接收定義的列允許將新資料與現有資料區分。

配置完接收計畫後，選擇 **[!UICONTROL 完成]**。

![啟用回填的Dynamics和Salesforce模板的計畫介面。](../../images/tutorials/templates/backfill.png)

### 審閱資產 {#review-assets}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_review"
>title="檢閱您自動產生的資產"
>abstract="產生所有資產最多可能需要五分鐘的時間。如果您選擇離開頁面，資產完成後您將收到傳回的通知。您可以在產生資產後檢閱資產，並可隨時對資料流進行其他設定。"

的 [!UICONTROL 審閱模板資產] 頁面顯示自動生成的資產作為模板的一部分。 在此頁中，可以查看與源連接關聯的自動生成的架構、資料集、標識命名空間和資料流。 產生所有資產最多可能需要五分鐘的時間。如果您選擇離開頁面，資產完成後您將收到傳回的通知。您可以在產生資產後檢閱資產，並可隨時對資料流進行其他設定。

預設情況下，自動生成的資料流設定為草稿狀態，以允許對配置進行進一步自定義，如映射規則或調度頻率。 選取橢圓(`...`)旁邊，然後選擇 **[!UICONTROL 預覽映射]** 查看為草稿資料流建立的映射集。

![選中預覽映射選項的下拉窗口。](../../images/tutorials/templates/preview.png)

此時將出現預覽頁，允許您檢查源資料欄位和目標架構欄位之間的映射關係。 查看資料流映射後。 選擇 **[!UICONTROL 明白。]**

![映射預覽窗口。](../../images/tutorials/templates/preview-mappings.png)

您可以在執行後隨時更新資料流。 選取橢圓(`...`)旁邊，然後選擇 **[!UICONTROL 更新資料流]**。 您將進入「源工作流」頁，在該頁中可以更新資料流詳細資訊，包括部分接收、錯誤診斷和警報通知的設定以及資料流的映射。

可以使用架構編輯器視圖更新自動生成的架構。 訪問指南 [使用架構編輯器](../../../xdm/tutorials/create-schema-ui.md) 的子菜單。

![選擇了更新資料流選項的下拉窗口。](../../images/tutorials/templates/update.png)

>[!TIP]
>
>您可以通過 [!UICONTROL 資料流] 目錄。 選擇 **[!UICONTROL 資料流]** 從頂部標題中選擇要更新的資料流。
>
>![源工作區的資料流目錄中現有資料流的清單。](../../images/tutorials/templates/dataflows.png)

### 發佈資料流

通過源工作流開始發佈過程。 選擇後 [!UICONTROL 更新資料流]，您將 *[!UICONTROL 添加資料]* 的子菜單。 選擇 **[!UICONTROL 下一個]** 繼續。

![草稿資料流的添加資料步驟](../../images/tutorials/templates/continue-draft.png)

接下來，確認資料流詳細資訊並配置錯誤診斷、部分接收和警報通知的設定。 完成後，選擇 **[!UICONTROL 下一個]**。

![草稿資料流的資料流詳細步驟。](../../images/tutorials/templates/dataflow-detail.png)

>[!NOTE]
>
>可以選擇 **[!UICONTROL 另存為草稿]** 隨時停止並保存對資料流所做的更改。

將出現映射步驟。 在此步驟中，可以重新配置資料流的映射配置。 有關用於映射的資料準備功能的全面指南，請訪問 [資料準備UI指南](../../../data-prep/ui/mapping.md)。

![草稿資料流的映射步驟。](../../images/tutorials/templates/mapping.png)

最後，查看資料流的詳細資訊，然後選擇 **[!UICONTROL 保存和攝取]** 發佈草稿。

![草稿資料流的審閱步驟。](../../images/tutorials/templates/review.png)

## 後續步驟

按照本教程，您現在已使用模板建立了資料流以及架構、資料集和標識命名空間等資產。 有關來源的一般資訊，請訪問 [源概述](../../home.md)。

## 警報和通知 {#alerts-and-notifications}

「Adobe Experience Platform警報」支援模板，您可以使用通知面板接收有關資產狀態的更新，也可以導航回審閱頁。

選擇平台UI頂部標題中的通知表徵圖，然後選擇狀態警報以查看要查看的資產。

![平台UI中的通知面板會突出顯示故障資料流的通知。](../../images/tutorials/templates/notifications.png)

您可以更新模板的警報設定，以接收有關資料流狀態的電子郵件通知和平台內通知。 有關配置警報的詳細資訊，請閱讀上的指南 [如何訂閱源資料流的警報](../ui/alerts.md)。