---
keywords: 雲儲存目標；雲儲存
title: 建立雲端儲存空間目標
type: Tutorial
description: 連線至雲端儲存空間的指示
seo-description: 連線至雲端儲存空間的指示
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# 建立雲端儲存空間目標

本頁說明如何連線至Adobe Experience Platform中的雲端儲存空間位置。

在&#x200B;**[!UICONTROL Connections]** > **[!UICONTROL Destinations]**&#x200B;中，選擇您偏好的雲端儲存目標，然後選擇&#x200B;**[!UICONTROL Configure]**。

![連線至雲端儲存空間目標](../../assets/catalog/cloud-storage/workflow/connect.png)

>[!NOTE]
>
>如果已存在與此目標的連接，您可以在目標卡上看到&#x200B;**[!UICONTROL 激活]**&#x200B;按鈕。 有關&#x200B;**[!UICONTROL Activate]**&#x200B;和&#x200B;**[!UICONTROL Configure]**&#x200B;之間差異的詳細資訊，請參閱目標工作區文檔的[Catalog](../../ui/destinations-workspace.md#catalog)部分。

在&#x200B;**[!UICONTROL Authentication]**&#x200B;步驟中，如果您先前已設定到雲儲存目標的連接，請選擇&#x200B;**[!UICONTROL Existing Account]**&#x200B;並選擇您的現有連接。 或者，您可以選擇&#x200B;**[!UICONTROL 新帳戶]**&#x200B;來設定雲端儲存目的地的新連線。 填寫您的帳戶驗證憑證，然後選擇&#x200B;**[!UICONTROL 連接到目標]**。 或者，您可以附加RSA格式的公鑰，以便將加密添加到導出的檔案。 請注意，此公共密鑰&#x200B;**必須**&#x200B;寫入為Base64編碼字串。

如需&#x200B;**Authentication**&#x200B;步驟中憑證輸入的詳細資訊，請參閱[Amazon S3](./amazon-s3.md)目標、[[!DNL Amazon Kinesis]](./amazon-kinesis.md)目標、[[!DNL Azure Event Hubs]](./azure-event-hubs.md)目標和[SFTP](./sftp.md)目標。

>[!NOTE]
>
>平台支援驗證程式中的認證驗證，如果您在雲端儲存位置輸入錯誤的認證，則會顯示錯誤訊息。 這可確保您不會以不正確的憑證完成工作流程。

![連線至雲端儲存空間目標——驗證步驟](../../assets/catalog/cloud-storage/workflow/destination-account.png)

在&#x200B;**[!UICONTROL Setup]**&#x200B;步驟中，為激活流程輸入&#x200B;**[!UICONTROL Name]**&#x200B;和&#x200B;**[!UICONTROL Description]**。

此外，在此步驟中，您也可以選取任何應套用至此目的地的&#x200B;**[!UICONTROL 行銷使用案例]**。 行銷使用案例會指出將資料匯出至目的地的方式。 您可以從Adobe定義的行銷使用案例中選擇，也可以建立自己的行銷使用案例。 如需行銷使用案例的詳細資訊，請參閱[資料使用政策概述](../../../data-governance/policies/overview.md)。

對於Amazon S3目標，請將&#x200B;**[!UICONTROL 儲存桶名稱]**&#x200B;和&#x200B;**[!UICONTROL 資料夾路徑]**&#x200B;插入雲儲存目標中要傳送檔案的位置。 在填寫上述欄位後，選擇「建立目標」。****

![連線至Amazon S3雲端儲存空間目標——驗證步驟](../../assets/catalog/cloud-storage/workflow/amazon-s3-setup.png)

對於SFTP目標，請插入&#x200B;**[!UICONTROL 資料夾路徑]** ，以便將檔案傳送到該路徑。 在填寫上述欄位後，選擇「建立目標」。****

![連線至SFTP雲端儲存空間目標——驗證步驟](../../assets/catalog/cloud-storage/workflow/sftp-setup.png)

對於[!DNL Amazon Kinesis]目標，請在[!DNL Amazon Kinesis]帳戶中提供您現有資料流的名稱。 平台會將資料匯出至此串流。 在填寫上述欄位後，選擇「建立目標」。****

![連接到Kinesis雲儲存目標——驗證步驟](../../assets/catalog/cloud-storage/workflow/kinesis-setup.png)

對於[!DNL Azure Event Hubs]目標，請在[!DNL Amazon Event Hubs]帳戶中提供您現有資料流的名稱。 平台會將資料匯出至此串流。 在填寫上述欄位後，選擇「建立目標」。****

![連接到事件集線器雲儲存目標——驗證步驟](../../assets/catalog/cloud-storage/workflow/event-hubs-setup.png)

您的目標現在已建立。 如果您想稍後啟動區段，可以選取&#x200B;**[!UICONTROL 儲存並退出]**，或選取&#x200B;**[!UICONTROL Next]**&#x200B;以繼續工作流程並選取要啟動的區段。 在這兩種情況下，請參閱下一節[啟用區段](#activate-segments)，以便在工作流程的其餘部分匯出資料。

## 啟用區段{#activate-segments}

如需區段啟動工作流程的相關資訊，請參閱[啟用設定檔和區段至目標](../../ui/activate-destinations.md)。