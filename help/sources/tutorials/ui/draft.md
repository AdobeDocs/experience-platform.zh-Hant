---
title: UI中的草稿資料流
description: 瞭解如何將資料流儲存為草稿，並在稍後使用來源工作區時發佈。
exl-id: ee00798e-152a-4618-acb3-db40f2f55fae
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---

# UI中的草稿資料流

將資料流設定為草稿狀態，以儲存未完成的資料擷取工作流程進度。 您稍後可以繼續並完成草擬的資料流。

本檔案提供在Adobe Experience Platform UI中使用來源工作區時，如何儲存資料流的步驟。

## 快速入門

參閱本檔案前，請先實際瞭解下列Adobe Experience Platform元件：

* [來源](../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。

## 將資料流儲存為草稿

選取要帶入Experience Platform的資料後，您可以隨時暫停資料流建立進度。

例如，如果您想在資料流詳細步驟期間儲存進度，請選取&#x200B;**[!UICONTROL 另存為草稿]**。

![已選取另存為草稿之來源工作流程的資料流詳細資料步驟。](../../images/tutorials/draft/save-as-draft.png)

儲存草稿後，您將會進入帳戶的頁面，您可以在其中檢視現有資料流的清單，包括草稿。

![指定帳戶的資料流清單。](../../images/tutorials/draft/draft-dataflow.png)

>[!TIP]
>
>草擬的資料流將不會啟用，而且其狀態將設定為`draft`。

若要繼續草稿，請選取資料流名稱旁邊的省略符號(`...`)，然後選取&#x200B;**[!UICONTROL 更新資料流]**。

>[!NOTE]
>
>如果您的草稿包含排程資訊，則下拉式視窗也會提供您&#x200B;**[!UICONTROL 編輯排程]**&#x200B;的選項。

![已選取更新資料流程的下拉式視窗。](../../images/tutorials/draft/update-dataflow.png)

### 從來源目錄存取您的草稿

您也可以透過資料流目錄存取草稿資料流。 從頂端標題選取&#x200B;**[!UICONTROL 資料流]**&#x200B;以存取資料流目錄。 從這裡，從貴組織的現有資料流清單中尋找草稿，選取其名稱旁邊的省略符號(`...`)，然後選取&#x200B;**[!UICONTROL 更新資料流]**。

![指定組織的資料流清單。](../../images/tutorials/draft/catalog-access.png)

## 發佈您的草稿資料流

您會回到來源工作流程的[!UICONTROL 新增資料]步驟，您可以在此重新確認資料的格式，並繼續處理資料流。

在您確認資料的格式、分隔符號和壓縮型別後，請選取&#x200B;**[!UICONTROL 下一步]**&#x200B;以繼續。

![來源工作流程的新增資料步驟。](../../images/tutorials/draft/select-data.png)

接下來，確認您的資料流詳細資料。 使用資料流詳細資料介面更新圍繞資料流名稱、說明、部分擷取、錯誤診斷設定和警報偏好設定的設定。

完成設定後，請選取[下一步] **[!UICONTROL 以繼續。]**

![來源工作流程的資料流詳細資料步驟。](../../images/tutorials/draft/dataflow-detail.png)

[!UICONTROL 對應]步驟出現。 在此步驟中，您可以重新設定資料流的對應設定。 如需用於對應的資料準備功能的完整指南，請造訪[資料準備UI指南](../../../data-prep/ui/mapping.md)。

完成對應重新設定之後，請選取&#x200B;**[!UICONTROL 下一步]**&#x200B;以繼續。

![來源工作流程的對應步驟。](../../images/tutorials/draft/mapping.png)

使用[!UICONTROL 排程]步驟建立資料流的擷取排程。 您可以將擷取頻率設為`once`、`minute`、`hour`、`day`或`week`。 完成後，選取&#x200B;**[!UICONTROL 下一步]**&#x200B;以繼續。

![來源工作流程的排程步驟。](../../images/tutorials/draft/scheduling.png)

最後，檢閱您的資料流詳細資料，然後選取&#x200B;**[!UICONTROL 完成]**&#x200B;以發佈您的草稿。

![來源工作流程的稽核步驟。](../../images/tutorials/draft/review.png)

儲存並發佈草稿後，將會啟用資料流，您將無法再將其重設為草稿。

## 後續步驟

依照本教學課程所述，您已瞭解如何儲存進度並將資料流設定為草稿。 如需來源的詳細資訊，請瀏覽[來源概觀](../../home.md)。
