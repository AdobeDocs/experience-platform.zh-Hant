---
keywords: 啟用設定檔目的地；啟用目的地；啟用資料；啟用電子郵件行銷目的地；啟用雲端儲存目的地
title: 對串流設定檔匯出目的地啟用受眾資料
type: Tutorial
seo-title: 對串流設定檔匯出目的地啟用受眾資料
description: 了解如何將區段傳送至以設定檔為基礎的串流目的地，以啟動Adobe Experience Platform中您擁有的受眾資料。
seo-description: 了解如何將區段傳送至以設定檔為基礎的串流目的地，以啟動Adobe Experience Platform中您擁有的受眾資料。
source-git-commit: 02c22453470d55236d4235c479742997e8407ef3
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---


# 對串流設定檔匯出目的地啟用受眾資料

## 概覽 {#overview}

本文說明在Adobe Experience Platform串流設定檔型目的地(例如Amazon Kinesis)中啟用受眾資料所需的工作流程。

## 先決條件 {#prerequisites}

若要將資料激活到目的地，您必須已成功[連接到目標](./connect-destination.md)。 如果尚未這麼做，請前往[目標目錄](../catalog/overview.md)，瀏覽支援的目標，並設定您要使用的目標。

## 選取您的目的地 {#select-destination}

1. 前往&#x200B;**[!UICONTROL 連線>目的地]**，然後選取&#x200B;**[!UICONTROL 瀏覽]**&#x200B;標籤。

   ![目標瀏覽頁簽](../assets/ui/activate-streaming-profile-destinations/browse-tab.png)

1. 選取與您要啟用區段的目的地對應的&#x200B;**[!UICONTROL 新增區段]**&#x200B;按鈕，如下圖所示。

   ![激活按鈕](../assets/ui/activate-streaming-profile-destinations/activate-buttons-browse.png)

1. 移至下一個區段至[選取您的區段](#select-segments)。

## 選取您的區段 {#select-segments}

使用區段名稱左側的核取方塊，選取您要啟用至目的地的區段，然後選取&#x200B;**[!UICONTROL Next]**。

![選取區段](../assets/ui/activate-streaming-profile-destinations/select-segments.png)

## 選取設定檔屬性 {#select-attributes}

選取您要傳送至目標目的地的設定檔屬性。

>[!NOTE]
>
> Adobe Experience Platform會從您的架構中，使用四個建議且常用的屬性來填入您的選取項目：`person.name.firstName`、`person.name.lastName`、`personalEmail.address`、`segmentMembership.status`。

檔案導出將以下方式有所不同，具體取決於是否選擇了`segmentMembership.status`:
* 如果選擇了`segmentMembership.status`欄位，則導出的檔案包括初始完整快照中的&#x200B;**[!UICONTROL 活動]**&#x200B;成員，以及後續增量導出中的&#x200B;**[!UICONTROL 活動]**&#x200B;和&#x200B;**[!UICONTROL 過期]**&#x200B;成員。
* 如果未選擇`segmentMembership.status`欄位，則導出的檔案在初始完整快照和後續增量導出中僅包含&#x200B;**[!UICONTROL 活動]**&#x200B;成員。

![建議的屬性](../assets/ui/activate-streaming-profile-destinations/attributes-default.png)

1. 在&#x200B;**[!UICONTROL 選擇屬性]**&#x200B;頁中，選擇&#x200B;**[!UICONTROL 添加新欄位]**。

   ![新增對應](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. 選擇&#x200B;**[!UICONTROL 架構欄位]**&#x200B;條目右側的箭頭。

   ![選擇源欄位](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. 在&#x200B;**[!UICONTROL 選擇欄位]**&#x200B;頁中，選擇要發送到目標的XDM屬性，然後選擇&#x200B;**[!UICONTROL 選擇]**。

   ![「選擇源欄位」頁](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)


1. 要添加更多映射，請重複步驟1到3，然後選擇&#x200B;**[!UICONTROL Next]**。

## 檢閱 {#review}

在&#x200B;**[!UICONTROL 檢閱]**&#x200B;頁面上，您會看到您所選項目的摘要。 選擇&#x200B;**[!UICONTROL 取消]**&#x200B;以分解流，選擇&#x200B;**[!UICONTROL 返回]**&#x200B;以修改設定，或選擇&#x200B;**[!UICONTROL 完成]**&#x200B;以確認您的選擇並開始向目標發送資料。

>[!IMPORTANT]
>
>在此步驟中，Adobe Experience Platform會檢查資料使用政策是否違反。 以下顯示違反原則的範例。 除非您解決違規，否則無法完成區段啟用工作流程。 有關如何解決策略違規的資訊，請參閱資料控管文檔部分中的[策略實施](../../rtcdp/privacy/data-governance-overview.md#enforcement)。

![資料策略違規](../assets/common/data-policy-violation.png)

如果未檢測到任何違反策略的情況，請選擇&#x200B;**[!UICONTROL 完成]**&#x200B;以確認您的選擇並開始向目標發送資料。

![檢閱](../assets/ui/activate-streaming-profile-destinations/review.png)

## 驗證區段啟用 {#verify}


對於電子郵件行銷目的地和雲端儲存空間目的地，Adobe Experience Platform會在您提供的儲存位置中建立以定位點分隔的`.csv`檔案。 預期每天會在儲存位置中建立新檔案。 預設檔案格式為：
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

您連續三天收到的檔案可能如下所示：

```console
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

儲存位置中是否存在這些檔案是成功激活的確認。 若要了解匯出的檔案的結構，您可以[下載範例.csv檔案](../assets/common/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv)。 此範例檔案包含設定檔屬性`person.firstname`、`person.lastname`、`person.gender`、`person.birthyear`和`personalEmail.address`。
