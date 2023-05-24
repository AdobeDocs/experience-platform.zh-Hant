---
title: Power BI平台儀表板報表模板
description: 使用報表模板使用Experience Platform資料Power BI。
exl-id: fb98a79f-3d82-4e11-b08a-b7cb06414462
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 0%

---

# Power BI報表模板

Power BI報告模板功能允許您建立填有Adobe Experience Platform資料的引人注目的報告。 簡化的安裝過程會自動為即時客戶配置檔案、細分和目標安裝標準小部件。 此安裝還將Power BI連接到資料模型，以便您可以輕鬆自定義和擴展報告模板。 這些報告可以在整個組織中共用，而無需在平台上為您的組織提供憑據的收件人。

本文檔提供有關如何將Adobe Experience Platform與Power BI應用程式連接以及使用報告模板與外部用戶共用平台資料關鍵見解的說明。

## 快速入門

在繼續本教程之前，建議您充分瞭解 [架構組合](../../xdm/schema/composition.md) 在Experience Platform中，以及如何通過 [聯合架構](../../xdm/schema/composition.md#union)。

要安裝Power BI應用程式整合，用戶必須首先獲得以下平台權限：

- 管理查詢
- 管理沙箱

要瞭解如何分配這些權限，請閱讀 [訪問控制](../../access-control/home.md) 文檔。

您還必須擁有一個Power BI帳戶才能學習本教程。 要建立帳戶，請導航到 [Power BI首頁](https://powerbi.microsoft.com/en-us/) 並遵循註冊過程。 此Power BI帳戶的用戶還必須啟用 **建立工作區** 設定Power BI。 在Power BI管理門戶的租戶設定中找到此設定。 如果您的帳戶是由您的租戶或雇主提供的，請與您各自的管理員聯繫以啟用此設定。

![Power BI管理門戶建立工作區設定。](../images/power-bi/create-workspace-settings.png)

>[!NOTE]
>
>為了使「儀表板」頁籤顯示在平台UI的左導航中，並且「儀表板清單」視圖可見，您必須有權訪問作為平台許可證一部分的配置檔案、段或目標儀表板中的任何一個。

## 安裝Power BI應用程式整合

在平台UI中，選擇 **[!UICONTROL 儀表板]** 的下界 [!UICONTROL 儀表板] 工作區。 的 [!UICONTROL 瀏覽] 頁籤顯示當前可用儀表板視圖的清單。 要瞭解有關查看可用儀表板的詳細資訊，請參閱 [庫存文檔](../inventory.md)。

接下來，選擇 **[!UICONTROL 整合]** 頁籤。 此時將顯示Power BI應用程式整合頁。 從此處，選擇 **[!UICONTROL 安裝]** 開始安裝。

>[!NOTE]
>
>的 [!UICONTROL 安裝] 按鈕被禁用，除非您同時具有「查詢服務管理」和「管理沙箱」權限。

![Power BI詳細資訊螢幕，「安裝」按鈕突出顯示。](../images/power-bi/details-screen.png)

### 提供憑據

安裝過程的第一步是為Power BI應用程式整合提供非過期憑據。 提供以下兩種選項： [[!UICONTROL 建立新憑據]](#create-new-credentials) 或 [[!UICONTROL 使用現有憑據]](#use-existing-credentials)。 選擇適當的切換以繼續。

#### 建立新憑據 {#create-new-credentials}

生成新憑據時有兩個必填欄位： [!UICONTROL 名稱] 和 [!UICONTROL 分配給]。 的 [!UICONTROL 分配給] 欄位與與您的Power BI帳戶關聯的電子郵件地址相關。

![Power BI生成新憑據螢幕。](../images/power-bi/generate-new-credentials.png)

>[!IMPORTANT]
>
>建立未過期的憑據需要您分配某些權限和角色。 必需的權限是「管理沙箱」和「管理查詢服務整合」。 所需角色是Adobe Experience Platform管理員和開發人員角色。 要瞭解如何分配這些權限，請閱讀 [訪問控制](../../access-control/home.md) 文檔。

要瞭解有關生成未過期的查詢服務憑據的詳細資訊，請參閱 [非過期憑據指南](../../query-service/ui/credentials.md#non-expiring-credentials)。

首次生成未過期的憑據後，JSON檔案將下載到該電腦。 此JSON檔案隨後可以作為憑據與其他用戶共用以完成安裝過程。

#### 使用現有憑據 {#use-existing-credentials}

還可以上載JSON憑據檔案以通過驗證。 這些包含非過期憑據值的JSON檔案將下載到建立非過期憑據時使用的本地電腦。

>[!IMPORTANT]
>
>要使用現有的非過期憑據，用戶必須已經分配了憑據。 如果用戶未分配憑據，並且無法使用Adobe Admin Console建立新憑據，則用戶無法繼續安裝過程。

選擇 **[!UICONTROL 上載憑據檔案]**，然後在顯示的對話框中選擇要上載的相應JSON檔案。

![「Power BI憑據」螢幕，「上載憑據檔案」按鈕突出顯示。](../images/power-bi/upload-credential-file.png)

在您提供未過期的憑據後，平台會自動驗證這些憑據。 驗證成功後，將顯示確認消息。 選擇 **[!UICONTROL 下一個]** 審閱Power BI申請的同意協定。

![未過期的憑據已成功驗證螢幕，「下一步」按鈕突出顯示。](../images/power-bi/successfully-uploaded-credential-file.png)

### 提供同意

將顯示同意顯示。 選擇 **[!UICONTROL 審查同意]** 開啟一個新窗口，詳細列出Power BI根據服務條款和隱私聲明訪問和使用資料所需的權限。

![「Review consence（審查同意）」按鈕突出顯示「provide conness（提供同意）」。](../images/power-bi/provide-consent-display.png)

選擇 **[!UICONTROL 接受]** 授予Power BI訪問和使用平台資料的權限。

![對Power BI應用程式的權限請求。](../images/power-bi/permissions.png)

>[!NOTE]
>
>如果您在提供許可之前在任何時間退出安裝過程，則Power BI應用程式整合將不會安裝到儀表板清單中。

在提供同意後，報告模板將作為安裝過程的一部分自動安裝在Power BI環境中。 然後，Power BI使用非過期的憑據訪問平台，依次執行所有SQL查詢，並使用返回的資料填充報表模板。

選擇 **[!UICONTROL 完成]** 返回儀表板清單。

![「Finish（完成）」按鈕突出顯示「provile conness（提供同意）」。](../images/power-bi/finish-consent-review.png)

現在，Power BI報告模板已安裝，它將出現在可用儀表板清單中 [!UICONTROL 瀏覽] 頁籤。 選擇 **[!UICONTROL Power BI]** 的子菜單。

![Power BI列在儀表板清單中。](../images/power-bi/power-bi-dashboard-inventory.png)

>[!IMPORTANT]
>
>Power BI管理員需要確保用戶具有在Power BI環境中查看這些儀表板的適當訪問權限。

## Power BI工作區

登錄後 [Power BI工作區](https://dxt.powerbi.com)，報告模板可用於您有權訪問的每個服務。 報表模板包括配置檔案、段和目標儀表板 **僅** 是否具有相應的視圖權限。

預設情況下，配置檔案、段和目標的標準小部件在Power BI模板報告中可用。

>[!NOTE]
>
>必須為給定儀表板啟用編輯權限，才能在Power BI環境中安裝該儀表板。

![Power BI使用標準平台配置檔案小部件的配置檔案模板報告。](../images/power-bi/profile-report-template.png)

在Power BI中安裝儀表板後，預設情況下將向所有用戶顯示報表模板。 如果要限制對任何報表模板的訪問，請確保在Power BI環境中禁用有關用戶的訪問。

## 自定義Power BI報表模板

通過使用自定義小部件，您可以將自定義屬性添加到資料模型中，以豐富Power BI提供的報表模板。

>[!NOTE]
>
>可用於自定義小部件的屬性取決於聯合架構中的可用內容。 要瞭解如何查看和瀏覽聯合架構以使自定義小部件受益，請參見 [聯合架構UI指南](../../profile/ui/union-schema.md)。

### 建立自定義小部件

通過小部件庫建立自定義小部件。 查看 [小部件庫概述](../customize/widget-library.md) 介紹功能和 [建立自定義小部件的教程](../customize/custom-widgets.md) 的子菜單。

>[!IMPORTANT]
>
>新建立的自定義小部件 **不** 在Adobe Experience Platform儀表板和Power BI報告模板之間自動同步。 必須在平台UI中建立的任何自定義小部件必須在Power BI環境中手動重新建立。

### 在Power BI環境中重新建立自定義小部件

一旦儀表板在自定義小部件中包含了相應的度量和屬性，您就可以修改從Power BI環境中顯示的報告模板。 查看 [Power BI文檔](https://docs.microsoft.com/zh-tw/power-bi/) 的子菜單。

## 刪除Power BI應用程式整合

要刪除儀表板，請導航到儀表板清單並選擇刪除表徵圖(![](../images/power-bi/delete-icon.png))。

>[!NOTE]
>
>只有安裝了Power BI儀表板的用戶才能從平台UI中刪除整合。

![顯示「瀏覽」按鈕和「刪除」表徵圖的儀表板清單螢幕瀏覽頁籤突出顯示。](../images/power-bi/delete-power-bi-dashboard.png)

出現確認跨距。 選擇 **[!UICONTROL 刪除]** 確認進程。

>[!IMPORTANT]
>
>從平台UI中刪除Power BI儀表板 **不** 刪除您的Power BI環境中可用的報表模板。 如果要完全刪除Power BI報告模板中保存的資訊，則需要登錄到Power BI帳戶並從該環境中刪除報告模板。 刪除後，用戶可以按照上面概述的相同安裝說明重新安裝Power BI板。

## 後續步驟

通過閱讀此文檔，您可以更好地瞭解如何將Power BI報告模板整合到平台中，以便從您的配置檔案、段或目標控制板中共用令人信服的資料洞察力。 查看 [儀表板自定義概述](../customize/overview.md) 瞭解有關自定義儀表板的詳細資訊。
