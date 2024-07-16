---
title: 平台儀表板的Power BI報表範本
description: 使用報表範本探索使用Power BI的Experience Platform資料。
exl-id: fb98a79f-3d82-4e11-b08a-b7cb06414462
source-git-commit: 729d218f72a8caecc90a98810b973d0754f7757b
workflow-type: tm+mt
source-wordcount: '1465'
ht-degree: 0%

---

# 控制面板的Power BI報表範本

Power BI報表範本功能可讓您建立令人驚豔的報表，並填入來自Adobe Experience Platform的資料。 簡化的安裝程式會自動安裝適用於Real-time Customer Profile、細分和目標的標準Widget。 此安裝也會將Power BI連線至您的資料模型，以便您輕鬆自訂及擴充報表範本。 這些報告可在您的整個組織中共用，接收者不需要貴組織在Platform上的認證。

本檔案說明如何連結Adobe Experience Platform與Power BI應用程式，並使用報表範本與外部使用者共用重要的Platform資料深入分析。

## 快速入門

在繼續此教學課程之前，建議您先透過[聯合結構描述](../../xdm/schema/composition.md#union)深入瞭解Experience Platform中的[結構描述組合](../../xdm/schema/composition.md)，以及屬性如何包含在即時客戶設定檔中。

若要安裝Power BI應用程式整合，使用者必須先取得下列Platform許可權：

- 管理查詢
- 管理沙箱

若要瞭解如何指派這些許可權，請參閱[存取控制](../../access-control/home.md)檔案。

您也必須有Power BI帳戶才能參閱本教學課程。 若要建立帳戶，請瀏覽至[Power BI首頁](https://powerbi.microsoft.com/en-us/)，並依照註冊程式進行。 此Power BI帳戶的使用者也必須在其Power BI設定中啟用&#x200B;**建立工作區**&#x200B;設定。 此設定可在Power BI管理入口網站的租使用者設定中找到。 如果您的帳戶是由租使用者或僱主所提供，請連絡您各自的管理員以啟用此設定。

![Power BI管理入口網站建立工作區設定。](../images/power-bi/create-workspace-settings.png)

>[!NOTE]
>
>為了讓「儀表板」標籤顯示在Platform UI的左側導覽器中，並顯示「儀表板詳細目錄」檢視，您必須有權存取任一個「設定檔」、「區段」或「目的地」儀表板，這是您平台授權的一部分。

## 安裝Power BI應用程式整合

在Platform UI中，選取左側導覽中的&#x200B;**[!UICONTROL 儀表板]**&#x200B;以開啟[!UICONTROL 儀表板]工作區。 [!UICONTROL 瀏覽]索引標籤會顯示目前可用的儀表板檢視清單。 若要深入瞭解如何檢視可用的儀表板，請參閱[詳細目錄檔案](../inventory.md)。

接著，選取&#x200B;**[!UICONTROL 整合]**&#x200B;標籤。 便會顯示「Power BI應用程式整合」頁面。 從這裡，選取&#x200B;**[!UICONTROL 安裝]**&#x200B;以開始安裝。

>[!NOTE]
>
>[!UICONTROL 安裝]按鈕已停用，除非您同時擁有查詢服務管理及管理沙箱許可權。

![顯示[安裝]按鈕的Power BI詳細資訊畫面。](../images/power-bi/details-screen.png)

### 提供認證

安裝程式的第一個步驟是為Power BI應用程式整合提供不會到期的認證。 有兩個選項可供提供： [[!UICONTROL 建立新認證]](#create-new-credentials)或[[!UICONTROL 使用現有的認證]](#use-existing-credentials)。 選取適當的切換以繼續。

#### 建立新認證 {#create-new-credentials}

產生新認證時有兩個必要欄位： [!UICONTROL 名稱]和[!UICONTROL 指派給]。 [!UICONTROL 指派給]欄位與您的Power BI帳戶相關聯的電子郵件地址有關。

![Power BI產生新認證畫面。](../images/power-bi/generate-new-credentials.png)

>[!IMPORTANT]
>
>建立不會到期的認證需要您指派特定的許可權和角色。 必要的許可權是管理沙箱和管理查詢服務整合。 所需的角色為Adobe Experience Platform管理員和開發人員角色。 若要瞭解如何指派這些許可權，請參閱[存取控制](../../access-control/home.md)檔案。

若要進一步瞭解如何產生不會到期的查詢服務認證，請參閱[不會到期的認證指南](../../query-service/ui/credentials.md#non-expiring-credentials)。

在第一次產生不會到期的認證後，會將JSON檔案下載至該電腦。 然後可以將此JSON檔案作為憑證與其他使用者共用，以完成安裝過程。

#### 使用現有的認證 {#use-existing-credentials}

JSON認證檔案也可上傳以通過驗證。 建立不會到期的認證時，會將儲存不會到期的認證值的這些JSON檔案下載到正在使用的本機電腦。

>[!IMPORTANT]
>
>若要使用現有的不會到期的認證，使用者必須已被指派認證。 如果使用者未指派認證，且無法使用Adobe Admin Console建立新認證，則使用者無法繼續安裝程式。

選取&#x200B;**[!UICONTROL 上傳認證檔案]**，然後在出現的對話方塊中選取要上傳的適當JSON檔案。

![上傳認證檔案按鈕反白顯示的Power BI認證畫面。](../images/power-bi/upload-credential-file.png)

在您提供不會到期的認證後，平台會自動驗證這些認證。 一旦驗證成功，就會顯示確認訊息。 選取&#x200B;**[!UICONTROL 下一步]**&#x200B;以檢閱Power BI應用程式的同意合約。

![已成功驗證不會到期的認證畫面，並反白顯示[下一步]按鈕。](../images/power-bi/successfully-uploaded-credential-file.png)

### 提供同意

同意顯示隨即顯示。 選取&#x200B;**[!UICONTROL 檢閱同意]**&#x200B;以開啟新視窗，詳述Power BI根據其服務條款及隱私權宣告存取及使用您的資料所需的許可權。

![提供同意顯示並反白顯示[檢閱同意]按鈕。](../images/power-bi/provide-consent-display.png)

選取&#x200B;**[!UICONTROL 接受]**&#x200B;以授予Power BI存取及使用平台資料的許可權。

![Power BI應用程式的許可權要求。](../images/power-bi/permissions.png)

>[!NOTE]
>
>如果您在提供同意之前在任何時候退出安裝程式，Power BI應用程式整合將不會安裝到儀表板詳細目錄。

在提供同意後，報表範本會作為安裝流程的一部分，自動安裝在Power BI環境中。 接著，Power BI會使用不會到期的認證來存取Platform、依序執行所有SQL查詢，並將傳回的資料填入報表範本。

選取&#x200B;**[!UICONTROL 完成]**&#x200B;以返回儀表板詳細目錄。

![提供同意顯示並反白顯示[完成]按鈕。](../images/power-bi/finish-consent-review.png)

現在已安裝Power BI報告範本，它會顯示在[!UICONTROL 瀏覽]標籤下的可用控制面板清單中。 從清單中選取&#x200B;**[!UICONTROL Power BI]**&#x200B;以瀏覽至Power BI環境。

![Power BI列在儀表板詳細目錄中。](../images/power-bi/power-bi-dashboard-inventory.png)

>[!IMPORTANT]
>
>Power BI管理員需確定使用者擁有適當的存取許可權，才能在Power BI環境中檢視這些控制面板。

## Power BI工作區

登入[Power BI工作區](https://dxt.powerbi.com)後，報表範本可供您存取的每個服務使用。 報表範本包含設定檔、區段和目的地儀表板&#x200B;**僅限** （如果他們有對應的檢視許可權）。

預設情況下，Power BI範本報表中可提供來自設定檔、區段和目的地的標準Widget。

>[!NOTE]
>
>您必須啟用指定儀表板的編輯許可權，才能允許在Power BI環境中安裝該儀表板。

使用標準平台設定檔介面工具集的![Power BI設定檔範本報告。](../images/power-bi/profile-report-template.png)

在Power BI中安裝儀表板後，報表範本會依預設顯示給所有使用者。 如果您想要限制對任何報告範本的存取權，請務必在Power BI環境中停用相關使用者的存取權。

## 自訂您的Power BI報表範本

透過使用自訂Widget，您可以將自訂屬性新增至資料模型，以豐富Power BI提供的報表範本。

>[!NOTE]
>
>可用於自訂Widget的屬性取決於聯合結構描述中可用的屬性。 若要瞭解如何檢視和探索聯合結構描述以利您的自訂Widget，請參閱[聯合結構描述UI指南](../../profile/ui/union-schema.md)。

### 建立自訂Widget

自訂Widget是透過Widget資料庫建立。 請參閱[Widget程式庫概觀](../customize/widget-library.md)以瞭解功能的簡介，並參閱[建立自訂Widget](../customize/custom-widgets.md)的教學課程以瞭解具體指示。

>[!IMPORTANT]
>
>新建立的自訂Widget在Adobe Experience Platform儀表板和Power BI報表範本之間&#x200B;**不會**&#x200B;自動同步。 在Platform UI中建立的任何自訂Widget都必須在Power BI環境中手動重新建立。

### 在Power BI環境中重新建立自訂Widget

一旦您的儀表板擁有包含在自訂Widget中的適當量度和屬性，您就可以準備修改從Power BI環境中顯示的報表範本。 請參閱[Power BI檔案](https://docs.microsoft.com/en-us/power-bi/)，以瞭解如何透過使用者介面編輯報告。

## 刪除Power BI應用程式整合

若要刪除儀表板，請導覽至儀表板詳細目錄，並選取儀表板名稱旁的刪除圖示(![](../images/power-bi/delete-icon.png))。

>[!NOTE]
>
>只有安裝Power BI控制面板的使用者才能從Platform UI刪除整合。

![儀表板詳細目錄畫面瀏覽索引標籤顯示，瀏覽按鈕和刪除圖示反白顯示。](../images/power-bi/delete-power-bi-dashboard.png)

確認彈出視窗隨即顯示。 選取&#x200B;**[!UICONTROL 刪除]**&#x200B;以確認程式。

>[!IMPORTANT]
>
>從Platform UI刪除Power BI儀表板&#x200B;**不會**&#x200B;刪除您的Power BI環境中可用的報告範本。 如果您想要完全刪除Power BI報告範本中保留的資訊，您必須登入您的Power BI帳戶，並從該環境中刪除報告範本。 刪除後，使用者可以依照上述相同的安裝指示，重新安裝Power BI控制面板。

## 後續步驟

閱讀本檔案後，您就能更加瞭解Power BI報表範本如何整合至Platform，以分享您的設定檔、區段或目的地儀表板引人注目的資料深入分析。 請參閱[儀表板自訂總覽](../customize/overview.md)，深入瞭解如何自訂儀表板。
