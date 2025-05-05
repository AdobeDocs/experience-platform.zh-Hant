---
title: 使用UI連線Bombora Intent至Experience Platform
description: 瞭解如何將Bombora Intent連結至Experience Platform
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="B2P版本" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: 76a4fed5-b2d5-46d5-9245-b52792a7d323
source-git-commit: a1af85c6b76cc7bded07ab4acaec9c3213a94397
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 4%

---

# 使用UI連線[!DNL Bombora Intent]至Experience Platform

閱讀本指南，瞭解如何使用使用者介面將您的[!DNL Bombora Intent]帳戶連結至Adobe Experience Platform。

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

* [Real-Time CDP B2B edition](../../../../../rtcdp/b2b-overview.md)： Real-Time CDP B2B edition是專為以B2B服務模式運作的行銷人員所打造。 它將來自多個來源的資料集中在一起，並將其合併成包含人員和帳戶輪廓的單一檢視。這種統一的資料讓行銷人員可以精確地以特定客群為目標，並在所有可用的管道中和這些客群互動。
* [來源](../../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

### 先決條件

請閱讀[[!DNL Bombora Intent] 總覽](../../../../connectors/data-partners/bombora.md)，瞭解如何擷取您的驗證認證的相關資訊。

## 瀏覽來源目錄

在Experience Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取&#x200B;*[!UICONTROL 來源]*&#x200B;工作區。 您可以在&#x200B;*[!UICONTROL 類別]*&#x200B;面板中選取適當的類別。 或者，您可以使用搜尋列導覽至您要使用的特定來源。

若要使用[!DNL Bombora]，請選取&#x200B;*[!UICONTROL 資料與識別合作夥伴]*&#x200B;下的&#x200B;**[!UICONTROL Bombora Intent]**&#x200B;來源卡，然後選取&#x200B;**[!UICONTROL 新增資料]**。

>[!TIP]
>
>當指定的來源尚未具有已驗證的帳戶時，來源目錄中的來源會顯示&#x200B;**[!UICONTROL 設定]**&#x200B;選項。 一旦驗證帳戶存在，此選項就會變更為&#x200B;**[!UICONTROL 新增資料]**。

![已選取[Bombra Intent]卡的來源目錄。](../../../../images/tutorials/create/bombora/catalog.png)

## Authentication {#authentication}

### 使用現有帳戶 {#existing}

若要使用現有帳戶，請選取&#x200B;**[!UICONTROL 現有帳戶]**，然後從介面的帳戶清單中選取您要使用的帳戶。

選取您的帳戶後，選取[下一步] **[!UICONTROL 以繼續執行下一步。]**

![來源工作流程中的現有帳戶介面。](../../../../images/tutorials/create/bombora/existing.png)

### 建立新帳戶 {#create}

如果您沒有現有的帳戶，則必須提供與您來源對應的必要驗證認證，以建立新的帳戶。

若要建立新帳戶，請選取&#x200B;**[!UICONTROL 新帳戶]**，然後提供帳戶名稱，並選擇性地提供帳戶詳細資訊的說明。 接下來，提供適當的驗證值，以針對Experience Platform驗證您的來源。 若要連線您的[!DNL Bombora]帳戶，您必須擁有下列認證：

* **存取金鑰識別碼**：您的[!DNL Bombora]存取金鑰識別碼。 這是61個字元的英數字串，需要它才能向Experience Platform驗證您的帳戶。
* **秘密存取金鑰**：您的[!DNL Bombora]秘密存取金鑰。 這是40個字元、以Base64編碼的字串，驗證您的帳戶給Experience Platform是必要的。
* **Bucket名稱**：將從其中提取資料的[!DNL Bombora]Bucket。

![來源工作流程中的新帳戶介面。](../../../../images/tutorials/create/bombora/new.png)

## 提供資料流詳細資訊 {#provide-dataflow-details}

帳戶通過驗證並連線後，您現在必須為資料流提供下列詳細資料：

* **資料流名稱**：您的資料流名稱。 建立並處理資料流後，您就可以使用此名稱在UI中搜尋資料流。
* **描述**： （選擇性）資料流的簡短說明或其他資訊。
* **網域來源**：符合來源帳戶記錄與Experience Platform帳戶的網域或網站欄位。 此值取決於您的設定。 如果未提供，網域會預設為accountOrganization.website。

![來源工作流程的資料流詳細資料介面。](../../../../images/tutorials/create/bombora/dataflow-detail.png)

## 排程資料流 {#schedule-dataflow}

接下來，使用排程介面來設定資料流的擷取排程。

* **頻率**：設定頻率以指出資料流應該執行的頻率。 您可以排程[!DNL Bombora]資料流每週擷取資料。
* **間隔**：間隔代表每個擷取週期之間的時間量。 [!DNL Bombora]資料流唯一支援的間隔為1。 這表示您的資料流每週會擷取一次資料。
* **開始時間**：開始時間會指定資料流首次執行反複專案的時間。 [!DNL Bombora]每週在UTC下午12:00將資料捨棄到Adobe一次。 因此，您必須在UTC下午12:00之後設定擷取開始時間。 此外，您必須向[!DNL Bombora]確認擷取時間，因為他們可能會變更排程，將檔案拖放至Adobe時。

設定資料流的擷取排程後，請選取&#x200B;**[!UICONTROL 下一步]**。

![來源工作流程的排程介面。](../../../../images/tutorials/create/bombora/scheduling.png)

## 檢閱資料流 {#review-dataflow}

資料流建立流程的最後一步是在執行資料流之前進行檢閱。 使用&#x200B;*[!UICONTROL 檢閱]*&#x200B;步驟，在執行新資料流之前先檢閱其詳細資料。 詳細資料會分組到以下類別中：

* **連線**：顯示來源型別、所選來源檔案的相關路徑，以及該來源檔案中的欄數。
* **排程**：顯示內嵌排程的有效期間、頻率和間隔。

檢閱資料流後，請選取&#x200B;**[!UICONTROL 完成]**。

![來源工作流程的稽核介面。](../../../../images/tutorials/create/bombora/review.png)

## 後續步驟

依照本教學課程中的指示，您已成功建立資料流，以將意圖資料從[!DNL Bombora]來源帶入Experience Platform。 如需其他資源，請瀏覽以下概述的檔案。

### 監視資料流

建立資料流後，您可以監視透過它擷取的資料，以檢視擷取率、成功和錯誤的資訊。 如需如何監視資料流的詳細資訊，請造訪有關UI[&#128279;](../../../../../dataflows/ui/monitor-sources.md)中監視帳戶和資料流的教學課程。

### 更新您的資料流

若要更新資料流排程、對應和一般資訊的設定，請瀏覽有關[在UI中更新來源資料流的教學課程](../../update-dataflows.md)。

### 刪除您的資料流

您可以刪除不再需要的資料流，或使用&#x200B;**[!UICONTROL 資料流]**&#x200B;工作區中可用的&#x200B;**[!UICONTROL 刪除]**&#x200B;功能建立錯誤的資料流。 如需有關如何刪除資料流的詳細資訊，請瀏覽教學課程，瞭解如何在UI[&#128279;](../../delete.md)中刪除資料流。
