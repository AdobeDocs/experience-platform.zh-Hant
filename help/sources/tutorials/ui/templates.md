---
description: Adobe Experience Platform提供預先設定的範本，供您加速資料擷取程式。 範本包含自動產生的資產，例如結構、資料集、對應規則、身分、身分識別命名空間，以及資料流，您可在將資料從來源傳入Experience Platform時使用這些資產。
title: （測試版）使用UI中的範本建立來源資料流
badge1: "Beta"
hide: true
hidefromtoc: true
exl-id: 48aa36ca-656d-4b9d-954c-48c8da9df1e9
source-git-commit: c4cb3783cbbab6f9bf25ffaa5b27a200c555b181
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 10%

---

# （測試版）使用UI中的範本建立來源資料流

>[!IMPORTANT]
>
>範本為測試版，且受下列來源支援：
>
>* [[!DNL Marketo Engage]](../../connectors/adobe-applications/marketo/marketo.md)
>* [[!DNL Microsoft Dynamics]](../../connectors/crm/ms-dynamics.md)
>* [[!DNL Salesforce]](../../connectors/crm/salesforce.md)
>
>檔案和功能可能會有所變更。

Adobe Experience Platform提供預先設定的範本，供您加速資料擷取程式。 範本包含自動產生的資產，例如結構、資料集、身分、對應規則、身分命名空間，以及在從來源傳入資料時可使用的資料流。

使用範本，您可以：

* 加速建立範本化資產，縮短擷取的實際時間。
* 將手動資料擷取程式期間可能發生的錯誤降至最低。
* 隨時更新自動產生的資產以符合您的使用案例。

以下教學課程提供如何在Platform UI中使用範本的步驟。

## 快速入門

本教學課程需要妥善了解下列Experience Platform元件：

* [來源](../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [[!DNL Experience Data Model (XDM)] 系統](../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
* [沙箱](../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

## 在平台UI中使用範本 {#use-templates-in-the-platform-ui}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_accounttype"
>title="選取商業類型"
>abstract="為您的使用案例選取適合的商業類型。您的存取權限可能會依據您的即時客戶資料平台訂閱帳戶而不同。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html" text="Real-Time CDP 概觀"

在平台UI中，選取 **[!UICONTROL 來源]** 從左側導覽器存取 [!UICONTROL 來源] 工作區，並查看Experience Platform中可用的來源目錄。

使用 *[!UICONTROL 類別]* 功能表來依類別篩選來源。 或者，在搜索欄中輸入源名稱，從目錄中查找特定源。

前往 [!UICONTROL Adobe應用程式] 類別，以查看 [!DNL Marketo Engage] 源卡，然後選擇 [!UICONTROL 新增資料] 開始。

![源工作區的目錄，其中突出顯示Marketo Engage源。](../../images/tutorials/templates/catalog.png)

此時會出現一個快顯視窗，提供您瀏覽範本或使用現有結構和資料集的選項。

* **瀏覽範本**:來源範本會自動建立結構、身分、資料集和資料流，並搭配對應規則使用。 您可以視需要自訂這些資產。
* **使用我的現有資產**:使用您建立的現有資料集和結構擷取資料。 您也可以視需要建立新資料集和結構。

若要使用自動產生的資產，請選取 **[!UICONTROL 瀏覽範本]** 然後選取 **[!UICONTROL 選擇]**.

![彈出式視窗，提供瀏覽範本或使用現有資產的選項。](../../images/tutorials/templates/browse-templates.png)

### 驗證

此時會出現驗證步驟，提示您建立新帳戶或使用現有帳戶。

>[!BEGINTABS]

>[!TAB 使用現有帳戶]

若要使用現有帳戶，請選取 [!UICONTROL 現有帳戶] 然後，從顯示的清單中選取您要使用的帳戶。

![現有帳戶的選擇頁面，包含您可存取的現有帳戶清單。](../../images/tutorials/templates/existing-account.png)

>[!TAB 建立新帳戶]

要建立新帳戶，請選擇 **[!UICONTROL 新帳戶]**，然後提供您的來源連線詳細資料和帳戶驗證憑證。 完成後，請選取 **[!UICONTROL 連接到源]** 並讓新連線有時間建立。

![具有源連接詳細資訊和帳戶身份驗證憑據的新帳戶的身份驗證頁。](../../images/tutorials/templates/new-account.png)

>[!ENDTABS]

### 選取範本

視您選取的業務類型而定，範本清單隨即顯示。 選取預覽圖示 ![預覽圖示](../../images/tutorials/templates/preview-icon.png) 範本名稱旁邊，以從範本預覽範例資料。

![高亮顯示預覽表徵圖的模板清單。](../../images/tutorials/templates/templates.png)

此時會出現預覽視窗，讓您探索並檢查範本中的範例資料。 完成後，請選取 **[!UICONTROL 明白了]**.

![預覽範例資料視窗。](../../images/tutorials/templates/preview-sample-data.png)

接下來，從清單中選取您要使用的範本。 您可以選擇多個模板並一次建立多個資料流。 不過，每個帳戶只能使用範本一次。 選取範本後，請選取 **[!UICONTROL 完成]** 並讓資產產生幾分鐘。

如果您從可用範本清單中選取一或多個部分項目，仍會產生所有B2B結構描述和身分識別命名空間，以確保正確設定各結構描述的B2B關係。

>[!NOTE]
>
>已使用的範本將在選取項目中停用。

![已選擇Opportunity Contact角色模板的模板清單。](../../images/tutorials/templates/select-template.png)

### 設定排程

此 [!DNL Microsoft Dynamics] 和 [!DNL Salesforce] 源均支援調度資料流。

使用計畫介面為資料流配置獲取計畫。 將擷取頻率設為 **一次** 來建立一次性擷取。

![Dynamics和Salesforce範本的排程介面。](../../images/tutorials/templates/schedule.png)

或者，您也可以將擷取頻率設為 **分鐘**, **小時**, **日**，或 **周**. 如果為多個內嵌計畫資料流，則必須設定時間間隔以建立每個內嵌之間的時間範圍。 例如，擷取頻率設為 **小時** 和間隔設定為 **15** 表示您的資料流計畫將資料 **15小時**.

在此步驟中，您也可以啟用 **回填** 並定義資料增量擷取的欄。 回填可用來內嵌歷史資料，而您為增量內嵌定義的欄則可讓新資料與現有資料有所區別。

完成擷取排程的設定後，請選取 **[!UICONTROL 完成]**.

![已啟用回填的Dynamics和Salesforce範本的排程介面。](../../images/tutorials/templates/backfill.png)

### 檢閱資產 {#review-assets}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_review"
>title="檢閱您自動產生的資產"
>abstract="產生所有資產最多可能需要五分鐘的時間。如果您選擇離開頁面，資產完成後您將收到傳回的通知。您可以在產生資產後檢閱資產，並可隨時對資料流進行其他設定。"

此 [!UICONTROL 檢閱範本資產] 頁面會顯示範本中自動產生的資產。 在本頁面中，您可以檢視與來源連線相關聯的自動產生結構、資料集、身分識別命名空間及資料流。 產生所有資產最多可能需要五分鐘的時間。如果您選擇離開頁面，資產完成後您將收到傳回的通知。您可以在產生資產後檢閱資產，並可隨時對資料流進行其他設定。

預設情況下，將啟用自動生成的資料流。 選取點(`...`)，然後選取 **[!UICONTROL 預覽對應]** 查看為資料流建立的映射集。

![下拉式視窗中選取了預覽對應選項。](../../images/tutorials/templates/preview.png)

此時將出現預覽頁，允許您檢查源資料欄位和目標架構欄位之間的映射關係。 查看資料流映射後。 選擇 **[!UICONTROL 明白。]**

![映射預覽窗口。](../../images/tutorials/templates/preview-mappings.png)

您可以在執行後隨時更新資料流。 選取點(`...`)，然後選取 **[!UICONTROL 更新資料流]**. 將進入源工作流頁，您可以在其中更新資料流詳細資訊，包括部分內嵌、錯誤診斷和警報通知的設定，以及資料流的映射。

您可以使用結構編輯器檢視來更新自動產生的結構。 請前往 [使用架構編輯器](../../../xdm/tutorials/create-schema-ui.md) 以取得更多資訊。

![選擇了更新資料流選項的下拉式窗口。](../../images/tutorials/templates/update.png)

## 後續步驟

依照本教學課程，您現在已使用範本建立資料流，以及結構、資料集和身分識別命名空間等資產。 如需來源的一般資訊，請造訪 [來源概觀](../../home.md).

## 附錄

以下章節提供有關範本的其他資訊。

### 使用通知面板返回審核頁面

Adobe Experience Platform警報支援範本，您可以使用通知面板接收資產狀態的更新，並導覽回檢閱頁面。

選取Platform UI頂端標題的通知圖示，然後選取狀態警報以查看您要檢閱的資產。

![Platform UI中的通知面板會強調顯示通知，提醒失敗的資料流。](../../images/tutorials/templates/notifications.png)
