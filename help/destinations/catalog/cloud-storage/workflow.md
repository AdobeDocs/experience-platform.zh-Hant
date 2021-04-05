---
keywords: 雲儲存目標；雲儲存
title: 建立雲端儲存空間目標
type: 教學課程
description: 連線至雲端儲存空間的指示
seo-description: 連線至雲端儲存空間的指示
exl-id: 58003c1e-2f70-4e28-8a38-3be00da7cc3c
translation-type: tm+mt
source-git-commit: 7bb862c4c6c52c42e45d5e736fa6d239e812ac2c
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---

# 建立雲端儲存空間目標

## 概述 {#overview}

本頁說明如何連接到Adobe Experience Platform的雲儲存位置。

在&#x200B;**[!UICONTROL Connections]** > **[!UICONTROL Destinations]**&#x200B;中，選擇您偏好的雲端儲存空間目標，然後選擇&#x200B;**[!UICONTROL Configure]**。

![連線至雲端儲存空間目標](../../assets/catalog/cloud-storage/workflow/connect.png)

>[!NOTE]
>
>如果已存在與此目標的連接，則可以在目標卡上看到&#x200B;**[!UICONTROL Activate]**&#x200B;按鈕。 有關&#x200B;**[!UICONTROL Activate]**&#x200B;和&#x200B;**[!UICONTROL Configure]**&#x200B;之間差異的詳細資訊，請參閱目標工作區文檔的[目錄](../../ui/destinations-workspace.md#catalog)部分。

## 帳戶步驟{#account}

在&#x200B;**[!UICONTROL Account]**&#x200B;步驟中，如果您先前已設定到雲儲存目標的連接，請選擇&#x200B;**[!UICONTROL Existing Account]**&#x200B;並選擇現有連接。 或者，您可以選擇&#x200B;**[!UICONTROL New Account]**&#x200B;來設定到雲儲存目標的新連接。 填寫您的帳戶驗證憑證，然後選取&#x200B;**[!UICONTROL Connect to destination]**。 或者，您可以附加RSA格式的公鑰，以便將加密添加到導出的檔案。 您的公開金鑰必須寫入為[!DNL Base64]編碼字串。

有關&#x200B;**驗證**&#x200B;步驟中輸入憑據的詳細資訊，請參閱[AmazonS3](./amazon-s3.md)目標、[[!DNL Amazon Kinesis]](./amazon-kinesis.md)目標、[[!DNL Azure Event Hubs]](./azure-event-hubs.md)目標和[SFTP](./sftp.md)目標。

>[!NOTE]
>
>平台支援驗證程式中的認證驗證，如果您在雲端儲存位置輸入錯誤的認證，則會顯示錯誤訊息。 這可確保您不會以不正確的憑證完成工作流程。

![連線至雲端儲存空間目標——帳戶步驟](../../assets/catalog/cloud-storage/workflow/destination-account.png)

## 驗證步驟{#authentication}

在&#x200B;**[!UICONTROL Authentication]**&#x200B;步驟中，輸入&#x200B;**[!UICONTROL Name]**&#x200B;和&#x200B;**[!UICONTROL Description]**&#x200B;作為啟動流程。

在此步驟中，您也可以選取任何應套用至此目的地的&#x200B;**[!UICONTROL Marketing action]**。 行銷動作會指出將資料匯出至目的地的方式。 您可以從Adobe定義的行銷動作中選擇，也可以建立自己的行銷動作。 如需行銷動作的詳細資訊，請參閱[資料使用政策概述](../../../data-governance/policies/overview.md)。

對於AmazonS3目標，請將&#x200B;**[!UICONTROL Bucket name]**&#x200B;和&#x200B;**[!UICONTROL Folder path]**&#x200B;插入雲端儲存空間目標，以便傳送檔案。 在填入上述欄位後，請選取&#x200B;**[!UICONTROL Create Destination]**。

![連線至AmazonS3雲端儲存空間目標——驗證步驟](../../assets/catalog/cloud-storage/workflow/amazon-s3-setup.png)

對於SFTP目標，請插入要傳送檔案的&#x200B;**[!UICONTROL Folder path]**。 在填入上述欄位後，請選取&#x200B;**[!UICONTROL Create Destination]**。

![連線至SFTP雲端儲存空間目標——驗證步驟](../../assets/catalog/cloud-storage/workflow/sftp-setup.png)

對於[!DNL Amazon Kinesis]目標，請在[!DNL Amazon Kinesis]帳戶中提供您現有資料流的名稱。 平台會將資料匯出至此串流。 在填入上述欄位後，請選取&#x200B;**[!UICONTROL Create Destination]**。

![連接到Kinesis雲儲存目標——驗證步驟](../../assets/catalog/cloud-storage/workflow/kinesis-setup.png)

對於[!DNL Azure Event Hubs]目標，請在[!DNL Amazon Event Hubs]帳戶中提供您現有資料流的名稱。 平台會將資料匯出至此串流。 在填入上述欄位後，請選取&#x200B;**[!UICONTROL Create Destination]**。

![連接到事件集線器雲儲存目標——驗證步驟](../../assets/catalog/cloud-storage/workflow/event-hubs-setup.png)

您的目標現在已建立。 如果您想稍後啟動區段，可以選取&#x200B;**[!UICONTROL Save & Exit]**，或選取&#x200B;**[!UICONTROL Next]**&#x200B;以繼續工作流程，並選取要啟動的區段。 閱讀[啟用區段](#activate-segments)一節，以匯出工作流程的其餘部分。

## 使用宏在儲存位置中建立資料夾{#use-macros}

要在儲存位置中為每個段檔案建立自定義資料夾，可以在資料夾路徑輸入欄位中使用宏。 在輸入欄位的末尾插入宏，如下所示。

![如何使用宏在儲存中建立資料夾](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

以下範例參考範例區段`Luxury Audience`，其ID為`25768be6-ebd5-45cc-8913-12fb3f348615`。

**宏1:`%SEGMENT_NAME%`**

輸入：`acme/campaigns/2021/%SEGMENT_NAME%`
儲存位置中的資料夾路徑：`acme/campaigns/2021/Luxury Audience`

**宏2:`%SEGMENT_ID%`**

輸入：`acme/campaigns/2021/%SEGMENT_ID%`
儲存位置中的資料夾路徑：`acme/campaigns/2021/25768be6-ebd5-45cc-8913-12fb3f348615`

**宏3:`%SEGMENT_NAME%/%SEGMENT_ID%`**

輸入：`acme/campaigns/2021/%SEGMENT_NAME%/%SEGMENT_ID%`
儲存位置中的資料夾路徑：`acme/campaigns/2021/Luxury Audience/25768be6-ebd5-45cc-8913-12fb3f348615`



## 啟用區段{#activate-segments}

如需區段啟動工作流程的相關資訊，請參閱[啟用設定檔和區段至目標](../../ui/activate-destinations.md)。
